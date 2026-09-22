# Skill 注册表（short-video-content-orchestrator 可扩展架构）

总控 OS 不硬编码调用逻辑之外的事。未来新增 Skill，只需在此注册，总控即可自动路由。
不要为加 Skill 重设计 `../SKILL.md`。

## 已注册 Skill

### brand-voice（人格层）
- 功能：个人表达风格、AI 味检测、禁用表达
- 输入：文本 / 素材 / 我的修改稿
- 输出：检测报告、人格化修正版、voice-profile 更新
- 适用场景：任何内容的终检、改稿、风格学习
- 调用优先级：所有对外内容的最终一道

### content-and-copy（内容层）
- 功能：内容/文案产生与优化、结构、标题、金句、仿写分析、资产沉淀
- 输入：主题/观点/粗稿/参考内容
- 输出：内容包（核心观点/角度/冲突/故事/金句/传播点）
- 适用场景：选题、观点成文、改稿、仿写重创作、跨平台文字
- 调用优先级：内容策略阶段，视频脚本之前

### short-form-video-script（写法层）
- 功能：Hook、视频结构、留存、口播稿、拍摄提示
- 输入：内容包
- 输出：脚本包（标题/Hook/前3秒/正文/转折/金句/结尾/CTA/拍摄提示）
- 适用场景：任何要变成短视频的内容
- 调用优先级：内容包之后、人格化之前

### content-repurposing（裂变层）
- 功能：母体裂变、多平台改编、内容矩阵
- 输入：母体内容（视频/文章/观点/故事/案例）
- 输出：裂变方案 + 各平台独立作品骨架
- 适用场景：一稿多用、多平台、不同长度/目的版本
- 调用优先级：内容/写法之后，按需

### content-research（研究层 / 上游）
- 功能：实时研究（WebSearch/WebFetch）、选题发现、6 类分类、100 分评分、A/B/C/D「我能不能讲」、机会矩阵、内容切口、Hook 方向、竞争分析、评论痛点挖掘、选题树、事实核查、长期选题库
- 输入：主题/方向/空（泛雷达）
- 输出：Research Summary（标准 schema，见 `references/research-summary-template.md`）+ 选题机会矩阵
- 适用场景：类型 A 实时/热点类、一键研究→创作、任何「现在该拍什么」的决策
- 调用优先级：选题阶段最前，产出 Research Summary 后交给 content-and-copy
- 绝对路径：`~/.workbuddy/content-system-foundation/content-research/SKILL.md`（与 4 基础 Skill 同处隐藏目录，不在用户列表显示）
- 落盘：`~/.workbuddy/content-assets/topic-db.md`

### viral-video-analyzer（拆解 / 研究下游模块）
- 功能：爆款视频逐帧+字幕拆解（Hook/结构/节奏/画面/爆点机制）、可复制vs不可复制、抽象结构模板、自动找我的切口、差异化评分、批量横向分析、爆款结构库、反 AI 仿写交 brand-voice、一键拆解+仿写
- 输入：视频链接 / 文件路径 / 文字稿 / 截图 / 用户描述
- 输出：Video Summary（标准 schema，见 `references/analysis-output-template.md`）+ 我的版本仿写方向
- 适用场景：类型 E 视频拆解 / 爆款仿写 / 内容反推 / 结构库沉淀
- 调用优先级：拆解阶段最前，产出 Video Summary 后交给 content-and-copy
- 绝对路径：`~/.workbuddy/content-system-foundation/viral-video-analyzer/SKILL.md`（与基础 Skill 同处隐藏目录，不在用户列表显示）
- 落盘：`~/.workbuddy/content-assets/breakdown-library.md`（爆款结构库）

## 待注册（接口预留，暂不安装）

| 拟增 Skill | 功能 | 接入位置 |
|---|---|---|
| Trend Research | 实时热点研究（与 Research 互补或合并） | 类型 A 前置 |
| Content Analytics | 发布数据复盘 | 生命周期 Analyze |
| Thumbnail/Title | 封面标题 | Publish 前后 |
| Shooting Coach | 拍摄指导 | Record |
| Comment/Community | 评论区运营 | Publish 后 |

注册格式（新增时照抄）：
```
### <skill-name>（<层>）
- 功能：
- 输入：
- 输出：
- 适用场景：
- 调用优先级：
```
