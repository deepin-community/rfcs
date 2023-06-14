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
  replacement: package_replacement # 软件包的替代方案
  remove_time: package_remove_time # 软件包退出时间（指的是节点时间，例如：2023-06-14）
  remove_type: package_remove_type # 软件包退出类型（指的是软件包的类型，例如：main、dde、community 等）
  remove_by: package_remove_by # 软件包退出人（指的是软件包退出的发起人，例如：SIG 组成员、社区成员等）
  remove_repo: package_remove_repo # 软件包退出仓库（指的是软件包退出的仓库，例如：ci、testing、stable 等） 
```

并配置 CI，当软件包移除 pr 被提出时，CI 会检查软件包是否被依赖，列出依赖软件包的列表。

情况 1：如果仅仅移除软件包，在通知软件包维护人员后，相关 pr 需要保留至少 7 天（从维护人员确认收到相关反馈开始计算，如果维护人员未响应，则 pr 保留 14 天），以便社区成员进行讨论。如果没有反对意见，则可以合并 pr，将软件包退出的信息添加到 removed-packages.yaml 中，在节点时间后将软件包移除，关闭 pr。

情况 2：如果软件包存在同名替换方案，在 pr 被提出且在 7 天内无反对意见后，将软件包替换为同名替换方案（CI 源），并交由测试人员进行测试。(将测试流程 pr 关联至此 pr)
在节点时间后将软件包更换为同名替换方案（软件源）并将软件包退出的信息添加到 removed-packages.yaml 中，关闭 pr。

情况 3：如果软件包存在非同名替换方案，原软件包停止维护，此情况无需立即移除软件包，可使两种软件包共存一段时间，以便用户进行迁移。在原方案出现漏洞或问题时，参照情况 1 进行处理。

情况 4：如果软件包出现严重后门等有必要停止提供软件包的安全风险，需要立即移除软件包，需要在 pr 标题中指出，由 deepin-sysdev 组和 deepin-security 组成员进行投票处理（超过 2/3 的人同意视为通过），投票通过后，将软件包移除，并将软件包退出的信息添加到 removed-packages.yaml 中。

## 提案弊端

暂无

## 遗留问题

## 替代方案

暂无。
