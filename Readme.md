---
uuid: af859250-d65a-11ec-b1fa-cb183f0fbcca
title: Bentley二次开发MVVM框架构想
tags:
  - Bentley
updated: 2022-05-18
---

## 前言

在进行 Microstation Addin 插件的开发中，我们通常将窗体、Tool、生成逻辑耦合在一起开发，每写一个工具，都要实现上述三个模块。

除了耦合严重以外，还要处理窗体与 Tool 之间的关闭逻辑，处理 Tool 的返回，重置逻辑。

深度的耦合，带来的结果就是维护的困难。

因此，本框架从这个痛点出发，希望开发一个 MVVM 框架，方便快速创建工具。

<!--more-->

## 功能需求

1. 窗体上的 Combobox 可以切换 Tool
2. 窗体上的 Button 可以响应 Tool，Tool 退出后又返回到原来的 Tool
3. Tool 选择的数据的时候可以更新到窗体上

## 大致思路

### Tool

封装一层 Tool 参数，不直接使用 Tool。每个参数可以设置调用链，使用职责链模式。

### Window

1. 窗体与 Tool 采用事件进行中转
2. 窗体和 Tool 采用数据来控制实例化