# 关于I/O Planning部分源码阅读

## I/O Planning 数据模型基类

`IOPModel : QAbstractItemModel` 关于数据来源关系的分析（主要提取核心的成员变量）：

```cpp
IOPModel {
private:
  IOPTreeNode* root_;	//--->其指向内容为模型核心
  Place::IO* ioPlace_;	//
}
```

每个`IOPModel`包含一个`IOPTreeNode*`指针，模型数据类型为树的节点：

```cpp
IOPTreeNode {
  IOPModelEntry data_;				// 核心数据
  QList<IOPTreeNode*> children_;	// 存储所有子节点的指针
  IOPTreeNode* parent_;				// 存储父节点的指针
}
```

其核心数据类型为`IOPModelEntry`，包含两个核心的成员变量pin和port：

1. pin - 类型为`PackagePin`
2. port - 类型为`IOPort`

这两个类型均继承自基类`IOPObject`，而`IOProject`类的核心是一个行索引和IOP基础属性的映射集合，如下。因此pin和port本质上都是**存储了一定数量基础属性的映射集合**。

```cpp
std::map<columId, shared_ptr<IOPBaseProperty>>
```

其中，`enum columId`提供了每个IOP基础属性的id，`IOPBaseProperty`类对基础属性的基本特征进行了一定的描述，如：

- value
- editable
- name
- associated properties

并提供了设置相应属性的基本方法。

以上为`IOPModel`类的数据包含结构，大致上的层级包含关系如下：

```cpp
IOPModel // 基础结构
	IOPTreeNode // 树状节点
		IOPModelEntry // 节点中包含的主要数据
			IOPObject(pin/port) // 主要数据有两种
  				IOPBaseProperty // 每种都存储了一定数量基础属性的映射集合
```



---

## I/O Planning 的代理模型类 proxy model

几种代理模型类继承关系如下：

```cpp
class IOPProxyModel : public QSortFilterProxyModel {...}
----class IOPPackagePinModel 	: public IOPProxyModel {...}
--------class IOPPackagePinSelectionModel 	: public QItemSelectionModel {...}
----class IOPIOPortModel 		: public IOPProxyModel {...}
--------class IOPIOPortSelectionModel 		: public QItemSelectionModel {...}

class IOPBankAttributeModel : public QSortFilterProxyModel {...}

class PackageLayoutModel : public IOPPackagePinModel {...}
```

代理模型和数据模型的代理关系：（`proxyModel->setSourceModel(sourceModel)`）

| **代理模型** （Proxy）        | **数据模型**（Source Model）                   |
| ----------------------- | ---------------------------------------- |
| `IOPIOPortModel`        | `IOPModel::instance()`                   |
| `IOPPackagePinModel`    | `IOPMOdel::instance()`                   |
| `IOPBankAttributeModel` | `IOPPackagePinModel` / `IOPIOPortModel`均可以 |
| `PackageLayoutModel`    | `IOPModel::instance()`                   |



---

## I/O Planning的视图类 view

在I/O Planning命名空间中：

```cpp
namespace ioplanning {
  class IOPPortView;
  class IOPPackagePinView;
  class AttributeEditor;
  class PackageLayoutWidget;
}
```

均直接继承自`QWidget`控件类。其中：

- `IOPPortView` 和 `IOPPackagePinView` 各自包含 `port_tree_` 和 `pin_tree_`的 `QTreeView` 成员变量；
- `AttributeEditor` （属性编辑器）包含一个 `PropertyPage` 成员，暂时没有发现View相关的成员变量；
- `PackageLayoutWidget` 包含一个 `class PackageView : public QAbstractItemView` 成员变量。

即视图存在与控件之中。



---

## I/O Planning的模型-视图对应关系 model-view

通过以上的分析已经很清楚了：（模型 <---> 视图）

- `IOPIOPortModel` <---> `IOPPortView`
- `IOPPackagePinModel` <---> `IOPPackagePinView`
- `PackageLayoutModel` <---> `PackageView(PackageLayoutWidget成员)`

