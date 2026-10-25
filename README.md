# zh-natural-editor

中文自然改写与审稿 Skill。它清理翻译腔、模板腔、空泛包装和机械结构，同时保护事实、数字、引文、限定条件、责任主体、作者立场与技术精度。

适用于 Claude Code、Codex、OpenClaw、WorkBuddy，以及其他支持 `SKILL.md` / Agent Skills 的 Agent。

## 特点

- 中文优先，也支持中英混合文本。
- 改写前建立受保护事实清单，防止数字、归属、条件和判断强度漂移。
- 支持轻改、标准、结构重写，以及只审不改和对照版。
- 支持干净专业、自然商务、作者型长文、自然口语、克制营销和社媒精简等配置。
- 不判断“AI 率”，不承诺绕过检测器，不通过错别字、乱码或虚构经历制造所谓真人感。
- 纯指令包，无脚本、网络、模型下载、API key 或第三方运行时依赖。

## 快速安装

### 通用安装器

适合 Claude Code、Codex、Cursor 等支持 skills.sh 的客户端：

```bash
npx skills add bolvarfordragon-dev/zh-natural-editor
```

全局安装：

```bash
npx skills add bolvarfordragon-dev/zh-natural-editor -g
```

### Claude Code

```bash
npx skills add bolvarfordragon-dev/zh-natural-editor -a claude-code
```

也可以手动克隆到项目或个人 Skill 目录：

```bash
git clone https://github.com/bolvarfordragon-dev/zh-natural-editor.git .claude/skills/zh-natural-editor
```

安装后直接描述改写任务；如果客户端支持显式 Skill 调用，也可以选择或调用 `zh-natural-editor`。

### Codex

```bash
npx skills add bolvarfordragon-dev/zh-natural-editor -a codex
```

或让 Codex 的 `$skill-installer` 从以下仓库安装：

```text
https://github.com/bolvarfordragon-dev/zh-natural-editor
```

手动安装到个人目录：

```bash
git clone https://github.com/bolvarfordragon-dev/zh-natural-editor.git ~/.agents/skills/zh-natural-editor
```

调用：

```text
$zh-natural-editor 把下面这段改得更像中文母语者写的，保留所有事实和限定词。
```

### OpenClaw

OpenClaw v2026.6.6 及兼容版本：

```bash
openclaw skills install git:bolvarfordragon-dev/zh-natural-editor@main
```

全局安装：

```bash
openclaw skills install git:bolvarfordragon-dev/zh-natural-editor@main --global
```

### WorkBuddy

WorkBuddy 对市场发布包要求额外的中英文展示元数据，因此仓库提供单独包：

```text
dist/zh-natural-editor-workbuddy.zip
```

在 WorkBuddy Open Platform 或技能创建入口上传该 ZIP。压缩包根目录是 `zh-natural-editor/`，其中直接包含 `SKILL.md`、`references/` 和 `LICENSE`。

### 其他 Agent

把本仓库克隆或复制到该 Agent 的 skills 目录即可。最低要求是宿主能读取目录根部的 `SKILL.md`，并支持相对路径加载 `references/`。

## 使用示例

### 默认改写

```text
把下面这段去掉 AI 味，保留原意、全部数字、产品名和“可能”“预计”等限定词。只给改稿。

原稿：……
```

### 只审不改

```text
只标问题，不改写全文。重点检查翻译腔、机械结构、空泛包装和结论强度。每条给出片段、问题和修改方向。
```

### 带风格和边界

```text
用自然商务风格、轻改力度处理这封客户邮件。保留 10 月 28 日、财务团队和“预计最晚”；不要新增补偿承诺。
```

### 参考样本

```text
参考样稿的短句、克制语气和数据优先结构改写原稿。不要复用样稿的案例、标题、数字、比喻或标志性表达。
```

## 目录

```text
.
├── SKILL.md
├── agents/openai.yaml
├── references/
│   ├── style-profiles.md
│   └── test-cases.md
├── packages/workbuddy/zh-natural-editor/
└── dist/zh-natural-editor-workbuddy.zip
```

## 兼容性说明

| Agent | 安装方式 | 调用方式 |
|---|---|---|
| Claude Code | `npx skills add` 或复制到 `.claude/skills/` | 自然语言或客户端 Skill 选择器 |
| Codex | `npx skills add`、`$skill-installer` 或复制到 `~/.agents/skills/` | `$zh-natural-editor` 或自然语言 |
| OpenClaw | `openclaw skills install git:...` | 自然语言或 Skill 名称 |
| WorkBuddy | 上传专用 ZIP | 安装后在会话中自然语言调用 |
| 其他 Agent Skills 客户端 | 克隆到其 skills 目录 | 取决于宿主的显式／隐式触发机制 |

## 验证

- 标准版 `SKILL.md` 通过 Agent Skills 基础结构校验。
- Codex 展示元数据 `agents/openai.yaml` 通过 YAML 解析。
- WorkBuddy 专用版包含其官方文档要求的展示名、双语简介、版本、作者与调用示例字段。
- `references/test-cases.md` 提供 6 组人工验收样例与失败条件。

这些结果证明包结构和规则完整，不等同于所有模型上的效果保证。正式内容生产建议用自己的脱敏样本做盲评，重点记录事实丢失、语义强度漂移、过度改写和风格不符。

## License

MIT
