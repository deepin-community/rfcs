# 标题

- 提案发起时间：2023-07-27
- 提案拉取请求：https://github.com/deepin-community/rfcs/pull/7

## 概要

为 rust 系列软件包添加新的维护方式

## 动机

rust 系列软件包数量预计有 1700+ ，新增这些包会导致 github 组织下仓库增长过快有滥用 github repo 风险，参照当前的维护方式不利与 rust 系列软件包的维护。

## **详细设计**

在 deepin-community 下新建 rust-pkg 项目，这个项目存放存放所有 rust 相关软件包的 debian 目录等文件，从 crates.io 拉取源码，CI/CD 流程自动生成 dsc orig 等打包必须的文件自动化上传到 OBS 中进行构建，检查构建是否通过，PR 合并后自动 submit 到对应的组件中去(main or  community)

## 提案弊端

弊端：区别于现有的包维护形式，需对 CI/CD 流程进行调整

## 遗留问题

这种维护方式后续是否扩展到其他类型的软件包维护工作中，例如 golang 相关的软件包

## 替代方案

暂无
