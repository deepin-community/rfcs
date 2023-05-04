# deepin 社区提案（RFC）备忘录

提案（[RFC](https://zh.wikipedia.org/wiki/RFC)，征求意见稿）是 deepin 社区贡献者在一个集中的环境中提出、设计和讨论项目方向的新特性和变化的一种方式。

提案的发起应当通过在此处创建 Pull Request 的方式进行：<https://github.com/deepin-community/rfcs/pulls>

当提案被接纳并通过后，提案将被收入备忘录，可在此处查阅：<https://github.com/deepin-community/rfcs/tree/master/rfcs>

## 提案的作用是什么？

提案的流程旨在为 deepin 社区发展过程中的重要变更带来关注焦点并引入公开且有组织性的讨论，并最终达成决定上的一致。提案流程的公开透明性也至关重要，使得无论是技术委员会（TC）、兴趣小组（SIG）还是个人贡献者在内的所有人都可以参与到相关提案的讨论中来。

另外，提案仅作为设计文档。若提案所涉及的内容包括了某方面功能的实现或设计规划，提案本身无需等待相关的功能的代码实现完成即可予以通过，且提案本身不代表对所设计相关功能的实现日程规划。

## 谁可以发起提案？

任何人都可以发起提案，但若一个提案的发起人并非 TC 成员，那么则应当至少有一位 TC 成员愿意承接对应提案的相关事项、与发起人共同协力进行提案的推进，才可以继续提案的后续讨论流程。

## 什么情况下应当发起提案？

当你不清楚你的想法是否应当发起提案时，最好的做法是在实施交流群组、讨论板、邮件列表等位置发起讨论。我们鼓励在发起提案之前优先寻找相关的项目成员展开讨论，以便在发起前评估相关的议题内容并获取相关人员的支持，并在提案发起前预先发现并解决可能存在的潜在问题。一个提案若在发起前就已经经过了初步讨论，那么提案被接纳的可能性会更大。

提案旨在对“重大”的变化拟定相关的规划、设计与策略。例如某个设计或决策可能会很大程度地改善现状以使相关项目与人员受益，或是某个变更可能造成尚不明确的破坏性影响需要评估。举例而言，包括但不限于这些类别的内容便适合进行提案的起草与发起：

- 以系统与桌面环境整体的角度，对特定方向技术的决策草案
- 可能对基础设施、软件仓库与项目带来不兼容或破坏性的变化的决策
- 对 deepin 社区体制与流程本身的制度拟定或补充
- 对已批准提案的实质内容的修订

而这些内容则不适合以新提案的形式进行：

- 为 deepin 软件仓库独立的增、删、调整、更新软件包
- 为系统或桌面环境增加非关键性的新特性
- 为系统或桌面环境提供安全更新或无影响的基础设施调整
- 对已批准提案的无实质性变更的微调（例如调整措辞以消除歧义、对错字与排版的调整等）
- 为已批准提案提供新的第一方译文

值得注意的是，RFC 提案备忘录通常只收录适宜以提案形式进行记录并存档的内容，一般包括制度规范与设计/规划文档类的内容。部分 deepin 社区活动展开过程中所涉及的事项可能存在一定影响因而需要 TC 决议，但如果相关事项本身不适合以 RFC 提案文档的形式体现，则也不需要以提案的形式来发起。对于这类事项，可根据实际情况，采取在邮件列表进行常规讨论的形式或在常规 TC 例会中进行讨论与决议的形式完成。

## 提案的发起

### 第〇步：决定是否要发起提案

正如上文所述，在提案发起前，我们建议您先寻求与您所计划拟定的提案相关的组织或团队，并与它们展开讨论，在得到较为确定的讨论结果后，再正式发起提案。另外，作为提案作者，最好保持当前时刻最多存在一个由你所发起的提案。

尽管这并非强制要求，如此做法可以使提案的质量在发起时就得以初步的保障，并节省其它贡献者有限的精力，使之可以聚焦于提案本身的讨论之中。

当然，在发起提案之前，也建议您监视现有的提案是否有与您要发起的提案所相关或相近的提案。如果有，则应当考虑参与到现有提案的讨论之中。

### 第一步：复刻（Fork）本仓库

将此仓库 Fork 到你的名下，以便进行后续操作。

### 第二步：编写提案

将 `rfc/0000-template.md` 复制并命名为 `rfc/0000-提案标题.md`，然后根据模板内容进行提案的起草和完善。

在提案的编写过程中请深思熟虑。一个好的提案应当能清晰地解释其动机，并仔细地考虑可能存在的弊端与备选方案。提案应当能展示出问题本身，并通过提案内容恰当且具体地描述出提案本身为何能以及怎样地解决了相关的问题。

### 第三步：发送拉取请求

提交（Commit）并推送你所拟定的提案到你的复刻仓库，然后在 <链接> 发起 Pull Request（拉取请求），你所创建的拉取请求本身即为征求意见稿。对于提案的讨论过程发生在你所创建的拉取请求之中，以 Comment 评论与 Review 评注的形式对提案的内容进行讨论并发起修订建议。

当拉取请求创建后，你就会得到一个拉取请求对应的编号（比如 114），这个编号即为提案的代号。此后，你需要：

1. 更新提案文件名中的编号为这个代号，例如 `rfc/0114-first-party-support-for-Mir.md`。这将便于在提案接纳并归入备忘录时，提案可根据编号顺序升序显示。
2. 更新提案文件内所描述的对应编号。

已经发起的提案即便有内容或格式错误也不必担心，你可以在提案被接纳归档前修改提案并更新合并请求。

### 第四步：宣布提案以征求意见

当你的提案就绪后，即可在 deepin-devel 邮件列表中宣布提案以征求社区与 TC 成员的意见。若您因故不便向邮件列表中宣布提案，也可联系 TC 并由 TC 人员代发。

一个示例的提案宣告模板邮件如下：

```
邮件标题：RFC: <提案标题>
----------------------
一个新的提案已发起，现征求广大贡献者的建议与意见：

<Pull Request 链接>

请访问此链接以参与讨论。

提案概要：<在这里简要的描述提案内容>
```

## 提案讨论的展开

提案的讨论过程发生在提案所对应的拉取请求之中，以 Comment 评论与 Review 评注的形式对提案的内容进行讨论并发起修订建议。如果在提案发起之前，相关议题已经在其它位置展开过讨论，那么也建议同时在拉取请求的描述中总结相关讨论的结论，并给出对应的链接以便后续检索与参考。

提案发起后，我们仍然允许存在发生在拉取请求的讨论区域之外的讨论，对于这些讨论，我们同样建议在得到阶段性的结果后，将讨论结果进行总结并回复至拉取请求的讨论之中，并附带相关的链接以供后续的检索与参考。

在提案的讨论过程中，请以 **推进获得结论** 为方向进行讨论的展开。对提案本身的讨论主题，也请将讨论的重点聚焦在提案的内容之上。

## 提案的定稿

当提案即将定稿后，任何 TC 成员都可以发起表决将此提案进入最终评论周期（FCP，Final Comment Period）。若要发起最终评论周期的表决，您需要先在提案对应的拉取请求中通过 Review 的形式以 Approve 表决提案，然后在 deepin-devel 邮件列表中宣布提案进入最终评论周期。

一个示例的宣布提案进入最终评论周期的模板邮件如下：

```
邮件标题：RFC FCP: <提案标题>
--------------------------
一个提案已经进入了最终评论阶段，在此后的 7 天内，讨论将结束，对应的提案将根据各位的表决情况最终被接纳、拒绝或撤销：

<Pull Request 链接>

请访问上述链接以参与讨论。

提案摘要：<在这里简要地描述提案内容>
```

最终评论周期最短为七天，其中应当包含至少五个工作日（以法定节假日为准）。若不足五个工作日则应当延长最终评论周期的长度以使其至少能够覆盖五个工作日。

最终评论周期的进入可以由任意 TC 成员发起，且发起时并不需要所有人均达成共识。最终评论周期结束后，若无反对与较大的修改意见，则提案通过，相应拉取请求将被合入，提案即进入备忘录仓库。若最终评论周期结束时，仍存在反对或较大的修改意见，则提案会被拒绝。

被拒绝的提案可由提案作者或推进人重新修改并再次发起最终评论阶段。若提案在此阶段被拒累计两次而提案发起人/推进人仍有意愿推进此提案，则对应的提案后续只能经过 TC 例会表决的形式进行决议通过，而无法再以一般的最终评论周期的形式通过。

## 关于提案流程

此文档是针对提案自发起到最终归入备忘录的整个流程的概要说明，可能并未覆盖到所有提案发起的场景。由于提案所涵盖的范围可能很广，也无法通过单一文档做到面面俱到的覆盖。故对于此文档无法直接对应的场景，我们建议具体情况具体分析来采取恰当的措施。对于有争议或有问题的提案，我们鼓励通过邮件列表、讨论板、Issue 面板、实时聊天等各种渠道与我们取得联系。

此文档并非法律文档，请勿耗费时间分析此文档的措辞。如果您认为此文档本身存在歧义或可改进的地方，也可通过发起 Pull Request 的形式来更新此文档。
