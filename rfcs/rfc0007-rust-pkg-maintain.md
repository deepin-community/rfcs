# 标题

- 提案发起时间：2023-07-27
- 提案拉取请求：https://github.com/deepin-community/rfcs/pull/7

## 概要

为rust系列软件包添加新的维护方式

## 动机

rust系列软件包数量预计有1700+ ，新增这些包会导致github组织下仓库增长过快有滥用github repo风险，参照当前的维护方式不利与rust系列软件包的维护。

## **详细设计**

在deepin-community下新建rust-pkg项目，这个项目存放存放所有rust相关软件包的debian目录等文件，从crates.io 拉取源码，CI/CD流程自动生成dsc orig等打包必须的文件自动化上传到OBS中进行构建，检查构建是否通过，PR合并后自动submit到对应的组件中去(main or  community)

## 提案弊端

弊端：区别于现有的包维护形式，需对CI/CD流程进行调整

## 遗留问题

这种维护方式后续是否扩展到其他类型的软件包维护工作中，例如golang相关的软件包

## 替代方案

暂无
