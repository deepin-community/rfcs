# 标题

* 提案发起时间：2023-7-27
* 提案拉取请求：[https://github.com/deepin-community/rfcs/pull/0006](https://github.com/deepin-community/rfcs/pull/0006)

## 概要

对 deepin-community 下的仓库进行权限控制，防范不可信的维护者对仓库的恶意破坏。

## 动机

* 问题：现有社区并不存在一个完善的权限控制机制，此时仓库权限授予采用的是“信任”机制，即社区的维护者得到 sysdev 组的信任后，便可以对社区的所有仓库进行任意操作。
* 之前的讨论方案：@revy 曾经提出即使是公司新入职的员工，也不会立即获得对所有仓库的权限，而是需要经过一段时间的观察，以便 sysdev 组和社区其他成员对新员工的工作能力进行评估，从而决定是否授予新员工对仓库的权限。
* 先例：<https://www.debian.org/devel/join/newmaint>

## 详细设计/制度正文

### 社区成员身份

社区成员分为以下几种身份：

|**社区身份**|**对应权限**|论坛身份|
|:----|:----|:----|
|TC（技术标准委员会）|deepin-community owner 权限|TC/技术标准委员会|
|核心维护者|deepin-community 下除部分 TC 管辖的仓库的 maintain 权限|deepin 核心社区开发者|
|维护者 | 对应 SIG 管辖的仓库的 maintain 权限|deepin 社区开发者|
|见习维护者 | 可以加入 deepin-community 组织，但无权限 | 无|

### 社区成员身份的获取

#### 见习维护者

见习维护者是社区的新成员，他们需要经过一段时间的观察，以便社区其他成员对其工作能力进行评估，从而决定是否授予其维护者身份。所以见习维护者身份在社区不存在任何门槛，只要你愿意参与社区的工作，签署了 CLA，那么你就是社区的一员。

#### 维护者

维护者是社区的成员，当见习维护者加入或创建了一个 SIG 时，便可以获得对应 SIG 管辖的仓库的 maintain 权限（sysdev 组除外）。

#### 核心维护者

核心维护者是社区的核心成员，他们对社区的发展有着重要的影响力。当维护者在社区中的工作得到了社区其他成员的认可（在 TC 例会上由 TC 组表决通过），便可以获得 deepin-community 下除部分 TC 管辖的仓库的权限。

#### TC

技术标准委员会拥有 deepin-community 的 owner 权限，TC 接纳新成员的流程遵循 TC 流程文档

### 社区成员身份的变更

#### TC

TC 成员的身份变更遵循 TC 相关流程

#### 核心维护者

当一个核心维护者在半年内未做出有效贡献，或者其他情况被 sysdev 组清退的。失去核心维护者身份

#### 维护者

当维护者退出 SIG 后，失去维护者身份。

#### 见习维护者

见习维护者自愿退出 deepin-community 组织，失去见习维护者身份

### 关联 GITHUB 维护者权限管理方案

#### 方案概述

各角色成员通过 github team 方式管理，并结合[OWNERS 文件模板](https://github.com/deepin-community/template-repository/blob/master/debian/deepin/OWNERS)下发到 deepin-community 的各个代码仓库中，用于控制代码变更新的审核与合入权限。

#### GITHUB TEAM 变更方案

github team 的更新根据上述对应角色商定的变更流程进行变更，变更流程可根据实际情况结合 github action+webhook 的技术手动实现自动化，主要用于 deepin-commnity 组织范围内的权限变更，影响较大。

#### OWNERS 文件变更方案

OWNERS 文件变更方式为提交 GitHub PullRequest，主要用于 deepin-community 下单个代码仓库的审核与合入选项的变更，影响较小。

## 提案弊端

## 遗留问题

### SIG 关联代码仓库维护者权限管理

待确定，应当在维护者权限管理方案试试后的基础上根据 SIG 的责任范围细化 deepin-community 的代码仓库权限管控。

## 替代方案
