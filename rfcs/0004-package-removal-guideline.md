# 标题

- 提案发起时间：2023-06-14
- 提案拉取请求：https://github.com/deepin-community/rfcs/pull/4

## 概要

完善软件源中包退出的流程

## 动机

在维护 deepin 软件源的过程中，我们发现了一些软件包已经不再维护，但是仍然存在于软件源中，这些软件包可能会造成一些问题，例如：

  1. 可能会造成用户的误用，导致用户的系统出现问题
  2. 出现 CVE 漏洞，但是由于软件包已经不再维护，无法及时修复
  3. 有新的软件包可以替代，但是由于软件包已经不再维护，无法及时替换

我们需要完善软件源中包退出的流程，以便及时发现软件包的退出，并及时通知用户。现有流程：https://wiki.deepin.org/zh/%E8%BD%AF%E4%BB%B6%E5%BC%80%E5%8F%91%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F%E7%AE%A1%E7%90%86

## 详细设计/制度正文

在 deepin-community/Repository-Manager 仓库下新建一个新的配置文件 removed-packages.yaml，用于记录软件包退出的信息，格式如下：

```yaml
- name: package_name  # 软件包名称
  version: package_version # 软件包版本
  reason: package_remove_reason # 软件包退出原因（例如：不再维护、存在安全漏洞等）
  replacement: package_replacement # 软件包的替代方案（可选）
  remove_time: package_remove_time # 软件包退出时间（指的是节点时间，例如：2023-06-14）
  remove_type: package_remove_type # 软件包退出类型（指的是软件包的类型，例如：main、dde、community 等）
  remove_by: package_remove_by # 软件包退出人（指的是软件包退出的发起人，例如：SIG 组成员、社区成员等）
  remove_repo: package_remove_repo # 软件包退出仓库（指的是软件包退出的仓库，例如：ci、testing、stable 等） 
```

并配置 CI，当软件包移除 pr 被提出时，CI 会检查软件包是否被依赖，列出依赖软件包的列表。

当一个软件出现打包问题，无法正常运行，或出现严重漏洞等一些情况时，由 sysdev 组提出并投票表决，如果投票通过（>=3/4),
则将软件包退出流程 PR 以邮件列表的形式通知社区，社区成员可以在一个月内提出异议，如果没有异议，则将软件包退出。

如果存在争议且无法达成一致，则由 TC 进行投票表决。

## 提案弊端

暂无

## 遗留问题

### 如果遇到例如 python2，Qt4 等软件包退出的情况，需要考虑如何处理。

新建一个页面追踪一个影响较大的包进行退出流程，比如 qt4 python2，因为大多数此类包低版本的停止维护后，依赖其开发的软件都会切换至高版本进行开发，
少数无人维护的包就走无人维护的包退出流程。当我们/（TC）认为退出对于生态的影响可控（投票表决）的时候，则退出此类包，并可以使用类似 DCM 的方式作为兜底

## 替代方案

暂无。
