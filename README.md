# Skills

集中维护跨项目复用的个人 Agent Skills 和项目 Agent 指令。具体任务、输出要求和平台依赖由各技能或指令文件说明。

## 技能目录

| Skill | 用途 | 目录 |
| --- | --- | --- |
| draft-software-design | 围绕目标、约束、方案和未决问题编写或修订设计手稿，供讨论或关联施工参考，保存在设计区的 drafts/。 | [draft-software-design/](draft-software-design/) |
| document-confirmed-design | 编写或维护已确认设计的正式说明，记录概念、数据关系、职责、契约和后续方向，不新增设计决定。 | [document-confirmed-design/](document-confirmed-design/) |

## 项目 Agent 指令

根目录的 [AGENTS.md](AGENTS.md) 用于维护本仓库；`agents/` 下的指令文件供实际项目通过软链或复制使用。当前提供 [Swift 项目指令](agents/swift/AGENTS.md)。

在目标项目根目录选择一种方式，先将示例中的 `/path/to/skills` 替换为本仓库的实际路径：

```bash
# 软链：共享本仓库中的源文件
ln -s /path/to/skills/agents/swift/AGENTS.md AGENTS.md

# 复制：在目标项目中独立维护
cp -i /path/to/skills/agents/swift/AGENTS.md AGENTS.md
```

通过软链编辑目标项目的 `AGENTS.md` 会修改这里的源文件；复制后的文件独立于源文件，后续更新由目标项目维护。

指令中的设计索引、项目结构和应用架构引用面向目标项目，用于按需定位和理解相关内容，无需在本仓库中提供对应文档。项目业务约定由目标项目维护。

## 公共编写约定

根目录的 [AGENTS.md](AGENTS.md) 定义维护本仓库时的 Agent 规则；本 README 解释这些约定并提供使用入口。各技能的执行规则由其 `SKILL.md` 和引用的资源定义。

- 每个技能使用独立目录，目录名与 `SKILL.md` 中的 `name` 一致，采用小写字母、数字和连字符。
- `SKILL.md` 是必需文件；参考资料、脚本、模板和评测案例按实际需要添加。
- Agent 指令、参考规范和评测说明使用英文；供维护者阅读的 README 使用中文。示例材料、模板和生成内容的语言遵循具体技能及用户要求。
- 单个技能应能独立使用，所需规则保存在技能内部，避免依赖仓库根目录的说明文件。
- 各技能的 README 按维护需要提供，用于说明和示例；执行规则的修改应同步检查相关说明。

## 使用与维护

在 Codex 中，可以通过 `$技能名` 显式调用，例如：

```text
用 $draft-software-design 为当前模块起草设计手稿，先在对话中给出方案和待讨论的问题。
```

手稿与正式说明按用途分工，不按篇幅区分。手稿默认保存在项目设计区的 `drafts/`，只在明确关联的讨论、首次实现或施工任务中参考；正式文档用于查阅有效约定。实现时先理解相关代码，再核对涉及的正式约定；需求与已确认设计决定改动目标。目录描述用途，不意味着文件会自动删除。

已有结论需要形成正式说明时，使用：

```text
用 $document-confirmed-design 把已确认的职责和数据关系整理成正式说明，不继续补设计。
```

普通工程问答和局部措辞修改不自动进入上述工作流。

正式文档编写中，冲突影响有效约定应如何表述时，先提出具体问题，暂停受影响内容，澄清后再继续；材料已明确区分尚未实现的目标与当前行为时直接记录。具体边界见 [正式文档技能的澄清规则](document-confirmed-design/SKILL.md#clarify-conflicts-before-continuing)。

创建或修改技能时，可以使用当前环境提供的 `$skill-creator`，说明任务、典型输入、期望输出和触发边界，并指定在本仓库中创建：

```text
用 $skill-creator 在本仓库创建 <技能名>。
处理的任务：……
典型输入和期望输出：……
应该触发和不应该触发的场景：……
遵循本仓库的命名、语言和资源组织约定。
```

修改已有技能时，说明要解决的问题和需要保留的约定。新增、重命名、移除技能或调整其用途时，同步更新上面的目录表。

修改后检查元数据、文件引用及相关说明的一致性。根据改动需要和已有授权进行行为评测，分别报告结构检查与实际行为验证；结构检查通过不代表行为评测通过。具体技能的案例和验证方法见其目录。

Codex 的接入和发现方式参见 [官方技能文档](https://learn.chatgpt.com/docs/build-skills)；仓库维护指令的加载方式参见 [AGENTS.md 文档](https://learn.chatgpt.com/docs/agent-configuration/agents-md)。
