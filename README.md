# Research Paper Reader

版本：0.1.0 · [MIT License](LICENSE) · 适用于 Codex 的独立技能

面向 UTD 商科期刊论文的精读技能。输入论文标题、citation、DOI、链接、Zotero 条目或 PDF，即可获得研究问题、已有研究、核心直觉与方法讲解，并按指定路径整理成 Markdown 笔记。

默认使用中文，保留必要的英文术语。理论论文重点解释模型与求解，实证论文重点解释研究设计、识别与估计，结构模型论文同时讲解行为模型和参数估计。

## 主要功能

- **四个核心问题**：围绕 Research Problem、Prior Work、Core Intuition 和 Method 建立对论文的完整理解。
- **直觉与数学结合**：解释行为机制、关键公式和全部符号；后续追问可以展开完整推导。
- **审稿人视角**：分析增量贡献、关键假设、识别与证据，将判断融入对应问题。
- **后续 Critical Review**：使用 5C 和虚拟重建思路，系统检查隐含假设、方法问题、相关研究与可复现性。
- **全文获取**：直接阅读已提供的 PDF；仅有文献信息时优先检索 Zotero，缺少全文时通过 Edge 尝试 EBSCO 或 SSRN。
- **Obsidian 阅读笔记**：将讲解保存为 Markdown，包含文献属性、PDF 链接与来源索引。
- **持续积累**：把追问整理为同一份笔记中的专题附录，保留中间步骤和个人批注。

## 安装到 Codex

### 1. 下载技能

在 GitHub 仓库页面选择 **Code → Download ZIP** 并解压，也可以使用仓库克隆地址下载。找到包含 `SKILL.md` 的文件夹，将其命名为 `research-paper-reader`。

### 2. 选择安装位置

复制整个 `research-paper-reader` 文件夹，保留 `agents/`、`references/` 和 `LICENSE`：

| 使用范围 | 安装后的入口文件 |
|---|---|
| 当前用户的所有项目 | `~/.agents/skills/research-paper-reader/SKILL.md` |
| 单个项目 | `<项目根目录>/.agents/skills/research-paper-reader/SKILL.md` |

`~` 表示用户主目录；不存在的目录可以自行创建。两个位置选择一个即可。更新已有版本时替换技能文件，保留自行修改内容的备份。

安装后的目录结构应为：

```text
research-paper-reader/
├── SKILL.md
├── README.md
├── LICENSE
├── .gitignore
├── agents/
│   └── openai.yaml
└── references/
    ├── paper-access.md
    ├── note-style.md
    ├── markdown-notes.md
    ├── reviewer-reading.md
    ├── critical-review.md
    ├── empirical-methods.md
    └── detailed-derivation.md
```

### 3. 确认可以调用

在 Codex CLI 或 IDE 扩展中输入 `/skills`，或输入 `$` 查找 `research-paper-reader`；桌面端可在技能列表中查找。未出现时，检查是否多嵌套了一层解压文件夹，并重启 Codex。

可以先发送以下请求验证加载，不需要准备论文：

```text
使用 $research-paper-reader，确认技能已加载，
说明首次阅读的四个核心问题，以及何时启用 Critical Review。
这次不读取论文，不保存文件。
```

预期结果是说明四问题初读结构、后续 Critical Review 和按请求保存的规则。安装位置、发现与调用方式依据 [OpenAI 官方技能文档](https://developers.openai.com/codex/skills/)。

## 运行环境与使用准备

本仓库提供阅读流程和写作规范，不附带 Zotero 连接器、PDF 解析工具或浏览器控制工具。安装技能后，按所需功能准备对应能力：

| 使用方式 | 需要准备什么 |
|---|---|
| 直接阅读 PDF | 提供可访问的本地 PDF 路径或上传文件；运行环境能够提取文本并查看公式、图表所在页面 |
| 从 Zotero 获取 | 当前环境可使用 Zotero 插件，Zotero Desktop 已打开，相关附件已下载到本地 |
| 缺少全文时在线获取 | 当前环境提供 Microsoft Edge 浏览器控制能力；需要机构访问时完成 EBSCO 登录 |
| 调研背景和相关工作 | 当前环境提供网页检索及原始文献读取能力 |
| 保存到 Obsidian | 提供本地 vault 中笔记文件夹的完整路径，并允许写入 |

可以先使用本地 PDF 体验讲解，再接入文献库和笔记库。技能通过写入 Markdown 文件生成 Obsidian 笔记，这一流程无需专用 Obsidian 插件。

使用 Zotero 前，在当前环境中安装或启用支持 Zotero Desktop 的连接器，按该连接器说明完成配置。仅打开 Zotero 或 Edge 不会自动赋予模型操作权限。工具不可用时，技能会说明缺少的能力；提供可读 PDF 后仍可直接阅读。

## 快速开始

明确指定技能和论文：

```text
使用 $research-paper-reader 阅读这篇论文：
Alptekinoğlu, Aydın, and Adem Örsdemir. 2022.
“Is Adopting Mass Customization a Path to Environmentally Sustainable Fashion?”
Manufacturing & Service Operations Management 24 (6): 2982–3000.
https://doi.org/10.1287/msom.2022.1088
```

也可以只提供标题或 DOI：

```text
使用 $research-paper-reader 阅读这篇论文：
https://doi.org/10.1287/msom.2022.1088
```

如果当前环境尚未列出这个技能，可以明确提供技能文件，将示例中的 `/path/to` 替换为实际位置：

```text
请读取并使用 /path/to/research-paper-reader/SKILL.md，
讲解这篇论文：论文标题或 DOI。
```

此技能仅在明确指定时启用。普通的“帮我读这篇论文”不会自动调用。同一阅读任务的后续追问无须重复写技能名称。

## 搭配 Zotero 与 Obsidian

可以让 Zotero 管理论文，让 Obsidian 保存逐步积累的理解：

| 工具 | 在阅读流程中的作用 |
|---|---|
| Zotero | 管理 citation 与 PDF，为精读提供论文全文 |
| Research Paper Reader | 获取论文、解释问题与方法、回答追问、整理笔记 |
| Obsidian | 浏览 Markdown 笔记、关联 PDF、添加个人批注 |

推荐按以下步骤使用。

### 1. 在 Zotero 中准备论文

保存论文条目和 PDF，打开 Zotero，并确认附件能够正常读取。已有标题或 DOI 时，可以直接让技能检索，不必手动查找附件路径。

### 2. 在 Obsidian 中准备笔记位置

确定 vault 内的阅读笔记文件夹，例如 `Papers/Notes`。可按以下方式组织：

```text
你的 Obsidian vault/
├── Papers/
│   └── Notes/
│       └── Paper Short Title (2022).md
└── PDFs/                             可选，已有的库内 PDF
```

PDF 可以继续保存在 Zotero 中。若你也在 vault 中保存了 PDF，技能会使用已核实的库内双链；否则使用实际附件路径。该流程不会自动复制 PDF 或同步两个库。

### 3. 读取论文并生成笔记

下面是完整调用示例。请将 `/path/to/your-vault/Papers/Notes` 替换为自己的笔记文件夹路径。

```text
使用 $research-paper-reader 阅读：
https://doi.org/10.1287/msom.2022.1088

优先从 Zotero 获取全文，从审稿人视角围绕四个核心问题讲解。
将笔记保存到：
/path/to/your-vault/Papers/Notes

这篇论文的后续追问也同步整理到同一份笔记，按主题追加或更新 Appendix。
```

### 4. 追问后回到 Obsidian 阅读

初读后，可以继续询问核心设定、公式、证明或识别策略。技能将追加内容整理为专题附录，你可以在 Obsidian 中打开对应文件继续阅读和批注。

```text
进一步解释 Proposition 2 的完整推导，沿用原文符号，
补充每一步计算及其经济含义，并更新这份笔记的 Appendix。
```

## 文献获取

已提供可读 PDF、上传全文或同一任务已有匹配全文时，技能核对身份和版本后直接阅读。只有标题、citation、DOI 或文献落地页时，优先检索 Zotero，并核对作者、标题、年份和 DOI。缺失附录或页面不可读时，仅补充获取相关材料。

如果库中没有论文，或条目缺少全文，技能会告知具体情况，再通过 Microsoft Edge 尝试从 EBSCO 或 SSRN 获取。使用前可打开 Zotero；需要机构访问时，在 Edge 中登录相应账户。遇到登录或验证码，会提示你完成该步骤。

Zotero 连接不可用时，会说明无法检索文献库，并在 Edge 控制能力可用时继续在线获取。Edge 控制能力也不可用时，可以手动下载 PDF 后提供给技能。

也可以直接提供本地 PDF：

```text
使用 $research-paper-reader 阅读以下 PDF：
/完整路径/论文.pdf
```

下载全文与导入 Zotero 分开处理。需要新增文献条目或附件时，请另外明确提出。

## 首次阅读会得到什么

首次讲解以简洁的研究概览开始，正文围绕四个问题展开：

| 部分 | 回答的问题 |
|---|---|
| Research Problem | 研究什么问题？背景是什么？为什么重要？解决后带来什么具体价值？ |
| Prior Work | 已有研究解决到了哪一步？采用了什么方法？仍有什么不足？ |
| Core Intuition | 核心机制是什么？哪个条件改变了谁的行为，又怎样影响结果？ |
| Method | 模型或研究设计如何建立？主体、信息、时序、目标与约束是什么？如何求解或估计？ |

Method 包含理解论文所需的关键公式、符号解释、求解逻辑和主要结果。首次阅读不自动添加独立的核心设定、完整证明或 Appendix。原文位置和背景文献集中放在末尾的来源索引。

如果希望从审稿人视角阅读，可以这样指定：

```text
使用 $research-paper-reader，从审稿人视角阅读这篇论文：论文标题。
重点分析贡献是否成立，以及模型假设如何影响结论。
```

审稿判断会融入四个核心问题，贡献评价放在 Prior Work，机制与假设分析放在 Core Intuition 和 Method。

## 保存 Markdown 笔记

在阅读请求中提供文件夹或完整文件路径：

```text
使用 $research-paper-reader 阅读这篇论文：论文标题或 DOI。
将讲解保存到：
/path/to/your-vault/Papers/Notes
```

只指定文件夹时，自动采用 `论文短标题 (年份).md` 的文件名。指定完整路径时，使用你给出的名称：

```text
将这篇论文的讲解整理为笔记，保存到：
/完整路径/Mass Customization and Sustainable Fashion (2022).md
```

未要求保存时，默认只在对话中回答。上面的路径是调用示例，不会自动成为每次的保存位置。

笔记采用适合 Obsidian 的结构：

```text
文献属性：PDF、Citation、journal、paper_type、topic

研究概览

1. Research Problem
2. Prior Work
3. Core Intuition
4. Method

来源索引
```

PDF 已存在于目标 Obsidian 库时，使用实际库内文件的双链；只有 Zotero 附件时，使用实际可访问路径。笔记保存后会返回文件链接。

## 通过追问补充附录

完成首次阅读后，可以继续提出具体问题。

**理解核心设定**

```text
进一步解释这篇论文的核心设定。
每个设定为什么需要？改变它会影响哪个机制或结论？
将回答整理到刚才笔记的 Appendix 中。
```

**完整推导模型**

```text
请逐步推导基准模型的求解过程。
沿用原文符号，解释每一步求导、代入和化简，检查边界解与成立条件。
将完整推导补充到同一份笔记的 Appendix 中。
```

**解释一个命题**

```text
请详细解释 Proposition 2，说明结论如何从模型中得到。
补充必要的中间步骤和经济直觉，并更新笔记中的对应附录。
```

**深入分析实证方法**

```text
进一步解释本文的识别策略。
说明估计目标、识别所依赖的变异，以及主要稳健性检验分别针对什么问题。
整理为同一份笔记的专题附录。
```

新专题依次整理为 Appendix A、Appendix B 等；同一专题继续更新已有附录。初读正文和个人批注保留，推导中的公式、符号解释和中间步骤完整保存。后续发现错误时，同步修正受影响的正文。

如果希望后续追问持续更新笔记，可以一次说明：

```text
这篇论文的后续追问都同步整理到这份笔记中，按主题追加或更新 Appendix。
```

另开对话继续阅读时，请重新指定技能、论文和已有笔记的完整路径。

## Critical Review

完成首次阅读后，可以进一步要求完整批判性评估：

```text
请对这篇论文做 critical review。
按 5C 框架评估，并尝试在作者设定下重建主要结果，
检查隐含假设、方法问题、遗漏的比较与可复现性。
```

技能按需加载 `references/critical-review.md`，完成相应检查后，以固定结构输出，中文通常 400–800 字：

```markdown
## 5C overview
- Category / Context / Correctness / Contributions / Clarity

## Implicit assumptions
## Method / experiment issues
## Missing comparisons or related work
## Reproducibility
```

5C 分别评价研究类型、文献定位、论证正确性、贡献和表达。Virtual re-implementation 要求沿着作者的设定重建研究链条：理论论文检查模型到均衡的推理，实证论文检查样本到估计结果的过程，数值研究检查参数、算法和结果之间的关系。

方法参考 [S. Keshav 的 How to Read a Paper](https://web.stanford.edu/class/ee384m/Handouts/HowtoReadPaper.pdf)，并借鉴 [CUTEPKQ / paper-reading 的评估组织方式](https://github.com/CUTEPKQ/paper-reading/blob/main/references/critical-review.md)。

需要深入或保存时，可以继续说明：

```text
详细展开最重要的方法问题，并给出可行的检验方案。
将 critical review 整理为同一份笔记的 Appendix。
```

初读仍然围绕四个核心问题；Critical Review 由后续请求启用。保存时采用独立附录，已有评估则更新同一部分。只问某个公式或假设时，回答限定在该问题。

## 调整阅读方式

| 需求 | 可以怎样提出 |
|---|---|
| 只解释一部分 | “只解释公式 5 及其所依赖的设定。” |
| 从基础开始 | “假设我刚开始学习贝叶斯博弈，补充理解本文所需的基础概念。” |
| 互动共读 | “逐节阅读，每节讲解后等待我继续。” |
| 保留聊天结果 | “这次只在对话中回答，不更新笔记。” |
| 延续已有笔记 | “继续使用此技能，读取以下笔记并补充本次讨论：完整路径。” |

默认连续完成当前请求；指定互动共读后才逐节等待。

## 常见问题

**必须同时使用 Zotero 和 Obsidian 吗？**

可以直接提供 PDF 并在对话中阅读，也可以将笔记保存到普通文件夹。Zotero 与 Obsidian 适合已有文献管理和长期阅读笔记需求的使用方式。

**首次阅读会生成详细推导附录吗？**

首次 Method 讲清模型和关键求解逻辑。只有后续追问时，才增加完整推导、核心设定等专题附录。

**会自动把笔记写回 Zotero 吗？**

笔记保存为指定位置的 Markdown 文件。新增 Zotero 条目、附件或子笔记需要另外明确提出。

**会覆盖原有笔记吗？**

明确要求更新既有笔记时，先读取文件，再更新对应内容并保留个人批注。首次保存遇到无法确认的同名文件时，采用带版本后缀的新文件名。

## 技能文件

- [README.md](README.md)：安装、环境准备与使用示例。
- [LICENSE](LICENSE)：MIT 许可证。
- [SKILL.md](SKILL.md)：调用范围和共同阅读流程。
- [笔记风格](references/note-style.md)：研究讲解风格与初读、追问的区分。
- [Markdown 笔记](references/markdown-notes.md)：保存、属性和附录更新规则。
- [文献获取](references/paper-access.md)：Zotero、Edge、EBSCO 与 SSRN 获取流程。
- [审稿人分析](references/reviewer-reading.md)：贡献、假设与证据分析。
- [Critical Review](references/critical-review.md)：后续 5C 评估、虚拟重建与固定输出模板。
- [实证方法](references/empirical-methods.md)：识别、估计与结果解释。
- [详细推导](references/detailed-derivation.md)：逐步求解和验证要求。

## 验证范围

已在 Codex 环境中使用一篇 M&SOM 理论论文测试 Zotero 全文读取和后续 Critical Review。发布前检查覆盖技能元数据、显式调用配置、文件结构、内部链接及个人路径残留。不同连接器下的 EBSCO/SSRN 下载与实证论文阅读仍需在相应环境中验证。

## 许可证

本项目采用 [MIT License](LICENSE)，版权署名为 `Research Paper Reader contributors`。引用的论文、外部项目和服务保留各自的许可证及使用条款。

## README 参考

本指南的功能概览、准备步骤、搭配工具和调用示例组织方式参考了以下项目，并按本技能的显式调用、四问题初读和附录更新流程重新编写：

- [CUTEPKQ / paper-reading](https://github.com/CUTEPKQ/paper-reading/blob/main/README.md)：功能概览、快速使用、搭配工具与模式示例的组织方式。
- [Renaaa1a / Zotero-Paper-Notes](https://github.com/Renaaa1a/Zotero-Paper-Notes/blob/main/README.md)：Zotero 使用准备和技能文件说明的组织方式。
- [RayChen200318 / stats-econometrics-paper-reader](https://github.com/RayChen200318/stats-econometrics-paper-reader/blob/main/README.md)：按阅读需求介绍场景，并提供具体公式、证明与实证分析提示词的方式。
