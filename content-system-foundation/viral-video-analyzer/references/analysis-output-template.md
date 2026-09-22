# Video Summary 模板（viral-video-analyzer → 总控标准输出）

本文件是 viral-video-analyzer 交给「短视频内容总控 OS」的结构化 schema。
总控读取后，继续交给 content-and-copy → short-form-video-script → brand-voice → content-repurposing。

字段与说明：

```
## Video Summary
Video Summary:      <一句话：这条视频是什么、核心传播动作>
Hook:               <前3秒原句/画面 + 类型>
Hook Type:          <冲突|反常识|悬念|结果|故事|提问|数据|权威|人物|情绪|直接观点|其他>
Structure:          <文字结构概述>
Timecode Structure: <Timecode→内容→功能 表（见 SKILL.md §4）>
Core Insight:       <核心洞察/观点>
Conflict:           <冲突是什么>
Emotion:            <好奇/愤怒/恐惧/惊讶/共鸣/兴奋/希望/争议 中哪些>
Information Gap:    <观众原本不知道的信息>
Story Mechanism:    <故事如何推进>
CTA:                <CTA 类型与原文>
Viral Mechanism:    <主要传播机制 + 次要传播机制>
Transferable Elements:   <可迁移项：角度/Hook结构/节奏/逻辑/CTA机制/镜头逻辑>
Non-transferable Elements:<不可复制项：原句/经历/身份/案例/金句/表达>
Abstract Template:  <去内容化结构模板>
User Fit:           <与我的定位匹配度（0–10）+ 理由>
Originality:        <内容原创度（0–10）>
Similarity Risk:    <同质化风险（0–10，低好）>
AI Risk:            <AI 味风险（0–10，低好）>
Adaptation Angles:  <我的切口 A–E 方向列表 + 推荐方向>
Suggested Topics:   <结合我的主题建议>
Suggested Hooks:    <3–5 个我的 Hook 方向>
Suggested Script Direction: <脚本方向（交 short-form 细化）>
```

使用约定：
- `Transferable Elements` 与 `Non-transferable Elements` 必须成对出现，缺一项判不合格。
- `Abstract Template` 必须能套到不同主题仍成立（去内容化）。
- 一键仿写时，本 Summary 作为【内容包】前半段交给总控走 FULL MODE。
- 仿写产出须过 `brand-voice` 终审（反 AI 机制），本模板不替代人格化检查。
