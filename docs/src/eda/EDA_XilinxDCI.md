# Xilinx DCI technology

Xilinx公司的digitally controlled impedance (DCI) 技术相关笔记。

数字控制阻抗（数控电阻）？

> ug471_7Series_SelectIO.pdf Page 19 Introduction

## 1. Introduction

在PCB设计中涉及到IO通常需要考虑阻抗匹配（输入端和输出端）。FPGA规模变大增多了IO端口，此时通过在IO端口附近增加电阻的方式会导致板上元件过多，某些区域还会出现物理不可实现的问题。为解决以上问题，Xilinx公司提出了digitally controlled impedance (DCI) 技术。

> However, due to increased device I/Os, adding resistors close to the device pins increases the board area and component count, and can in some cases be physically impossible. To address these issues and to achieve better signal integrity, Xilinx developed the digitally controlled impedance (DCI) technology.

