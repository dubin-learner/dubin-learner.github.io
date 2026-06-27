# Density概念与计算
Density又称Utilization，计算公式如下：
```bash
Density = leaf cell 面积 / 可用总面积 
```
leaf cell面积、可用总面积的计算，受多种因素的影响：
- 通常leaf cell包括std cell跟hard macro；
- 在计算Density的时候，如果hard macro的placement status是FIXED或COVER，则hard macro的面积不算在leaf cell面积、可用总面积之内。Hard macro的面积包含Block halos；
- 如果hard macro的placement status是PLACED，则hard macro的面积会算在leaf cell面积、可用总面积内；
- leaf cell的面积可以从lib直接读出，也可从lef中读出`SIZE X BY Y`计算得到；通常std cell和hard macro是矩形，从lib中读出的面积和从lef中读出`SIZE X BY Y`计算得到的面积是相等的。但有些macro是多边形，此时从lib中读出的面积跟从lef中读出的`SIZE X BY Y`计算得到的面积是不同的，对于多边形hard macro，在lef中会有`LAYER OVERLAP`的定义；不同工具的不同命令在lef报hard macro的面积时对多边形的处理会不同，有的命令直接用`SIZE X BY Y`，有的命令会将OVERLAP部分减去。

