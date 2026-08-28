# Agent Skills

[English](README.md) | 简体中文

一组小而可审计的 Agent Skills：在理解偏差演变成实现偏差之前，先把它找出来并对齐。

本仓库收录目标明确、可独立安装的 skills。核心指令遵循开放的 [Agent Skills](https://agentskills.io/) 格式，`agents/` 目录下的可选元数据则用于改善 Codex 中的使用体验。

## 为什么做这个项目

Agent 失败不只是因为它不会写代码。很多时候，真正的问题是意图、术语、假设或解释在未被察觉时逐渐偏离。

这个集合从两个方向缩小理解差距：

- `common-ground` 帮助用户与 agent 在行动前发现足以影响结果的认知差距。
- `eli5` 把复杂主题转化成容易检查、理解和分享的视觉解释。

本项目不追求尽可能多地收集 skills，而是维护一组规模克制、用途清晰、边界明确的工作流。

## Skills

| Skill | 适用场景 | 产出 |
| --- | --- | --- |
| [`common-ground`](skills/common-ground/) | 双方对意图、术语、验收标准或关键假设的理解可能不一致 | 一份共享工作地图，明确区分事实、决定、假设、未知项与偏离规则 |
| [`eli5`](skills/eli5/) | 复杂主题更适合通过图示和少量文字来理解 | 一份可移植、可独立运行的 HTML 视觉解说页面 |

## 安装

安装前先查看仓库中可用的 skills：

```bash
npx skills add HughLee824/skills --list
```

为 Codex 全局安装单个 skill：

```bash
npx skills add HughLee824/skills --skill common-ground -g -a codex
npx skills add HughLee824/skills --skill eli5 -g -a codex
```

移除 `-g` 即可改为项目级安装。也可以把 `codex` 替换为 [`skills`](https://skills.sh/) CLI 支持的其他 agent。

Skill 会以当前 agent 已拥有的权限运行。安装或调用前，请先阅读对应的 `SKILL.md` 以及其中包含的脚本。

### 为 Codex 手动安装

克隆仓库，然后把所需 skill 复制到用户级 skills 目录：

```bash
git clone https://github.com/HughLee824/skills.git agent-skills
mkdir -p "$HOME/.agents/skills"
cp -R agent-skills/skills/common-ground "$HOME/.agents/skills/common-ground"
```

如果新 skill 没有自动出现，请重启 Codex。

## 使用

需要明确启用某个工作流时，可以直接调用对应 skill：

```text
$common-ground 在开始实现结账流程改版前，先帮我们对齐理解。

$eli5 用图解释 DNS 如何把域名转换成服务器地址。
```

当请求与 `description` 明确匹配时，这两个 skills 也可能被自动选择。

## 兼容性

- 每个 skill 都是独立目录，并包含 Agent Skills 格式要求的 `SKILL.md`。
- 已使用 Codex 和 `skills` CLI 完成验证。
- 在实际可行的前提下，核心指令不依赖特定 agent。
- `agents/openai.yaml` 提供可选的 Codex 展示元数据与调用策略。

其他 agent 能否使用，取决于其对 Agent Skills 格式以及对应 skill 所需能力的支持程度。

## 项目结构

```text
.
├── .github/
│   └── PULL_REQUEST_TEMPLATE.md
├── skills/
│   ├── common-ground/
│   │   ├── SKILL.md
│   │   ├── agents/
│   │   └── references/
│   └── eli5/
│       ├── SKILL.md
│       ├── agents/
│       ├── LICENSE
│       └── NOTICE
├── CONTRIBUTING.md
├── LICENSE
├── NOTICE
├── README.md
├── README.zh-CN.md
└── SECURITY.md
```

## 设计原则

- **专注：** 每个 skill 只解决一个完整而明确的问题。
- **边界清晰：** description 说明什么时候应该触发，也说明什么时候不应该触发。
- **可审计：** 重要决定与约束使用可直接阅读的 Markdown 表达。
- **可移植：** 可选参考资料、资源、元数据与归属声明跟随其所属的 skill。
- **基于证据演进：** 根据真实使用或已观察到的失败改进，而不是为假想场景堆积复杂度。

## 参与贡献

欢迎提交缺陷报告、文档修正以及范围明确的 skill 改进。发起 Pull Request 前，请先阅读 [CONTRIBUTING.md](CONTRIBUTING.md)。

涉及安全问题时，请遵循 [SECURITY.md](SECURITY.md) 中的报告方式。

## 致谢

- `common-ground` 受到 known knowns、known unknowns、unknown knowns 与 unknown unknowns 框架、[Matt Pocock 的 Grilling skill](https://github.com/mattpocock/skills/blob/main/skills/productivity/grilling/SKILL.md)，以及 Anthropic 的[未知项探索指南](https://claude.com/blog/a-field-guide-to-claude-fable-finding-your-unknowns)启发。
- `eli5` 是面向 Codex 的重写版本，其灵感来自 Anthropic [`claude-plugins-community`](https://github.com/anthropics/claude-plugins-community/tree/main/eli5) 中由 Thariq Shihipar 最初编写的 `eli5` skill。详情请参阅 [`skills/eli5/NOTICE`](skills/eli5/NOTICE)。

以上内容仅作为来源致谢，不构成运行时依赖。

## 许可证

本项目采用 [Apache License 2.0](LICENSE)。第三方归属和改编说明保留在 [NOTICE](NOTICE) 以及对应 skill 自己的目录中。
