# Health Personal-Brand Short-Video Orchestrator

> 别名：**健康个人IP短视频文案生成总控台**

**An opinionated WorkBuddy skill that turns one line of natural language into a finished short-video script — by routing your request to the right downstream skill and chaining them in the right order.**

把一句话需求，自动路由到正确的下游 Skill，按顺序串成流水线，最后只给你「拿起来就能拍」的短视频文案。

---

## Why I built this / 为什么做这个

我做健康个人 IP，每天要产出短视频文案。但选题、仿写、观点成文、改稿、拆解爆款、多平台裂变——每一环本来都要我手动挑工具、手动组织顺序。

我的理念很朴素，也是从 Zara Zhang（张咋啦）那里学到的：**把你的工作流做成开源工具，就是最强的 Learn in Public。** 代码（和提示词）是一种自我表达的媒介。所以我没藏起这套流程，而是把它开源，欢迎任何人 Fork、改、提 Issue。

> Follow builders, not influencers. 看创造者，不看网红。

---

## Who is this for / 给谁用

- 想做**健康个人 IP** 短视频，但不想每次都从零想结构的人
- 已经有一堆基础 Skill，但懒得记名字、懒得手动拼调用链的人
- 非技术背景、用自然语言指挥 AI 的人

你只说人话，剩下的调度交给这个 Skill。

---

## What it does / 核心功能

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

不同 Skill 之间用两个结构化包传递上下文，下游不用重新理解：

```markdown
## 内容包 (Content Package)
主题:  目标人群:  视频目的:  核心观点:  内容角度:  冲突:  故事:  案例:
金句:  情绪:  传播点:  依据/来源:

## 脚本包 (Script Package)
<内容包 完整带入>
标题:  Hook:  前3秒:  正文:  转折:  金句:  结尾:  CTA:  拍摄提示:
```

---

## Install / 安装

1. 安装 [WorkBuddy](https://www.workbuddy.cn)。
2. 把本仓库放进 Skill 扫描目录：

```bash
mkdir -p ~/.workbuddy/skills
cp -r health-personal-ip-short-video-copy-orchestrator ~/.workbuddy/skills/
```

3. 完全退出并重开 WorkBuddy，让 Skill 列表刷新。

---

## Configure / 配置

本 Skill 依赖 4 个基础 Skill 作为执行层：

| Skill | 功能 | 默认路径 |
|---|---|---|
| `brand-voice` | 人格化 / AI 味检测 | `~/.workbuddy/content-system-foundation/brand-voice/SKILL.md` |
| `content-and-copy` | 文案生成与改写 | `~/.workbuddy/content-system-foundation/content-and-copy/SKILL.md` |
| `short-form-video-script` | 短视频脚本结构 | `~/.workbuddy/content-system-foundation/short-form-video-script/SKILL.md` |
| `content-repurposing` | 多平台裂变 | `~/.workbuddy/content-system-foundation/content-repurposing/SKILL.md` |

可选增强：`content-research`（实时选题研究）、`viral-video-analyzer`（爆款拆解）。

> 基础 Skill 默认放在隐藏目录 `content-system-foundation/` 下，不出现在用户 Skill 列表。想让它们显示，移到 `~/.workbuddy/skills/` 即可。

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

**Example / 示例**

> 用户：「完整做一条关于熬夜和代谢的 1 分钟短视频」

Skill 流水线：
1. `content-and-copy` 产出【内容包】
2. `short-form-video-script` 产出【脚本包】
3. `brand-voice` 做人格化检查并修正
4. 最终输出：选题、标题、Hook、完整口播、拍摄方式、CTA、设计说明

---

## Design philosophy / 设计哲学

- **只调度，不替代**：本 Skill 不做选题、不写文案、不改稿，只判断意图、串联调用链。
- **最小调用链**：按意图走最短路径，不每次调全部 Skill，省 token。
- **不暴露内部流程**：对用户只给结果和必要的设计说明。
- **不虚构事实**：研究类任务必须真搜；没信号就明说。
- **待确认信息不当事实**：写进资产库的内容必须标注 `状态: 已确认 / 待确认`。

---

## Skill structure / 目录结构

```text
health-personal-brand-short-video-orchestrator/
├── SKILL.md                    # 主文件：路由与调度逻辑
├── references/
│   └── skill-registry.md       # 可扩展架构注册表
├── .env.example                # 环境变量模板
├── README.md                   # 本文件
└── LICENSE                     # MIT License
```

---

## Contributing / 贡献

欢迎 Fork、提 Issue、二次改造。

有优化想法直接来——这个 Skill 的核心逻辑不藏私。新增下游 Skill 只需在 `references/skill-registry.md` 注册，总控即可自动路由，无需重写 `SKILL.md`。

---

## License

[MIT](LICENSE)

---

Built by chengangrun with WorkBuddy.
