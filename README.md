# Health Personal-Brand Short-Video Content System

> 别名：**健康个人IP短视频文案生成总控台（完整系统版）**

**A complete, opinionated short-video content system for WorkBuddy — one natural-language request in, a finished short-video script out. It routes your intent to the right downstream skill and chains them in the right order.**

把一句话需求，自动路由到正确的下游 Skill，按顺序串成流水线，最后只给你「拿起来就能拍」的短视频文案。

本仓库 = **1 个总控 + 6 个基础 Skill** 的完整系统，朋友克隆一次即可全部安装。

---

## Why I built this / 为什么做这个

我做健康个人 IP，每天要产出短视频文案。但选题、仿写、观点成文、改稿、拆解爆款、多平台裂变——每一环本来都要我手动挑工具、手动组织顺序。

我的理念很朴素，也是从 Zara Zhang（张咋啦）那里学到的：**把你的工作流做成开源工具，就是最强的 Learn in Public。** 代码（和提示词）是一种自我表达的媒介。所以我没藏起这套流程，而是把它开源，欢迎任何人 Fork、改、提 Issue。

> Follow builders, not influencers. 看创造者，不看网红。

---

## What's inside / 包含什么

| Skill | 层 | 功能 |
|---|---|---|
| `short-video-content-orchestrator` | 总控 | 听懂自然语言、判断意图、调度下面所有 Skill |
| `brand-voice` | 人格层 | 像不像我、AI 味检测、禁用表达 |
| `content-and-copy` | 内容层 | 写/改文字、结构、标题、金句、仿写分析 |
| `short-form-video-script` | 写法层 | Hook、视频结构、留存、口播、拍摄提示 |
| `content-repurposing` | 裂变层 | 母体裂变、多平台改编、内容矩阵 |
| `content-research` | 研究层 | 实时选题研究（热点/评分/机会矩阵） |
| `viral-video-analyzer` | 拆解层 | 爆款视频逐帧+字幕拆解、可迁移结构 |

### 任务路由 / Task routing

| 类型 | 触发示例 | 调用链 |
|---|---|---|
| A. 选题 | 「今天拍什么」「最近什么热点适合我」 | content-research → content-and-copy |
| B. 仿写 | 「这个视频不错帮我仿一个」 | 分析参考 → content-and-copy → short-form-video-script → brand-voice |
| C. 观点成片 | 「我有个观点帮我写成视频」 | content-and-copy → short-form-video-script → brand-voice |
| D. 改稿 | 「帮我把这段改得像我说话」 | content-and-copy → brand-voice |
| E. 视频拆解 | 「拆一下这条视频」 | viral-video-analyzer → 按需下游 |
| F. 多平台裂变 | 「把这条裂变到抖音小红书朋友圈」 | content-repurposing → brand-voice |
| FULL. 完整生产 | 「完整做一条短视频」 | content-and-copy → short-form-video-script → brand-voice → 质检 |

### 上下文传递机制 / Context handoff

```markdown
## 内容包 (Content Package)
主题:  目标人群:  视频目的:  核心观点:  内容角度:  冲突:  故事:  案例:
金句:  情绪:  传播点:  依据/来源:

## 脚本包 (Script Package)
<内容包 完整带入>
标题:  Hook:  前3秒:  正文:  转折:  金句:  结尾:  CTA:  拍摄提示:
```

---

## Install / 安装（朋友只需这一步）

1. 安装 [WorkBuddy](https://www.workbuddy.cn)。
2. 把本仓库下载/克隆下来，把 **4 个目录** 分别复制到 WorkBuddy 对应位置：

```bash
# 总控 Skill
cp -r skills/short-video-content-orchestrator ~/.workbuddy/skills/

# 6 个基础 Skill（隐藏目录，总控用绝对路径读取）
cp -r content-system-foundation ~/.workbuddy/

# 内容资产库（⚠️ 当前是示例，请替换成你自己的）
cp -r content-assets ~/.workbuddy/

# 个人表达风格（⚠️ 当前是示例，请替换成你自己的）
cp -r voice-profile ~/.workbuddy/
```

3. 完全退出并重开 WorkBuddy，让 Skill 列表刷新。

---

## ⚠️ 替换你的数据 / Replace the example data

仓库里的 `content-assets/` 和 `voice-profile/` 是**示例占位**（已标注 `[示例]`），不含任何真实业务或个人信息。要让系统真正像**你**，请替换成你自己的：

- `content-assets/content-assets.md` → 你的观点库/故事库/案例库/金句库/选题库
- `content-assets/content-map.md`、`hook-library.md`、`breakdown-library.md`、`topic-db.md` → 你的多平台映射、Hook、拆解结构、选题
- `voice-profile/voice-profile.md` → 你的真实表达习惯、禁用词、AI 味高危词
- `voice-profile/corpus/我的说话方式和内容.md` → 你的真实语料
- `voice-profile/feedback-log.md` → 留空，运行后自动积累

> 不替换也能跑（系统不会因缺文件报错），但产出的文案会是通用示例风格，不像你。

---

## Configure / 配置

如果你的路径不同，复制 `.env.example` 为 `.env` 自定义：

```bash
cp .env.example .env
```

```ini
WORKBUDDY_HOME="~/.workbuddy"
CONTENT_SYSTEM_FOUNDATION="~/.workbuddy/content-system-foundation"
CONTENT_ASSETS_DIR="~/.workbuddy/content-assets"
VOICE_PROFILE_DIR="~/.workbuddy/voice-profile"
```

---

## How to use / 使用

在 WorkBuddy 里用自然语言触发即可，不用记 Skill 名。

**Trigger phrases / 常用触发语**
- 「给我做个关于代谢健康的短视频」
- 「帮我想几个选题」
- 「这个视频不错帮我仿一个」
- 「帮我把这段改得像我说话」
- 「拆一下这条视频」
- 「把这条裂变到抖音小红书朋友圈」
- 「完整做一条短视频」

---

## Design philosophy / 设计哲学

- **只调度，不替代**：总控不做选题、不写文案、不改稿，只判断意图、串联调用链。
- **最小调用链**：按意图走最短路径，不每次调全部 Skill，省 token。
- **不暴露内部流程**：对用户只给结果和必要的设计说明。
- **不虚构事实**：研究类任务必须真搜；没信号就明说。
- **待确认信息不当事实**：写进资产库的内容必须标注 `状态: 已确认 / 待确认`。

---

## Skill structure / 目录结构

```text
health-personal-brand-short-video-orchestrator/
├── skills/
│   └── short-video-content-orchestrator/   # 总控
│       ├── SKILL.md
│       └── references/skill-registry.md
├── content-system-foundation/              # 6 个基础 Skill
│   ├── brand-voice/
│   ├── content-and-copy/
│   ├── short-form-video-script/
│   ├── content-repurposing/
│   ├── content-research/
│   └── viral-video-analyzer/
├── content-assets/                         # 示例数据（请替换）
├── voice-profile/                          # 示例人设（请替换）
├── .env.example
├── .gitignore
├── README.md
└── LICENSE
```

---

## Contributing / 贡献

欢迎 Fork、提 Issue、二次改造。

有优化想法直接来——核心逻辑不藏私。新增下游 Skill 只需在 `references/skill-registry.md` 注册，总控即可自动路由，无需重写 `SKILL.md`。

---

## License

[MIT](LICENSE)

---

Built by chengangrun with WorkBuddy.
