# Research Summary 模板（content-research → 总控标准输出）

本文件是 content-research 交给「短视频内容总控 OS」的结构化 schema。
总控读取后，把 Research Summary 作为【内容包】前半段，继续交给
content-and-copy → short-form-video-script → brand-voice。

字段含义与示例：

```
## Research Summary
Research Summary: <一句话：基于什么研究、得出什么核心结论>
Trend:          <实时趋势信号，附来源+事实分级>
Topic:          <推荐选题（主标题级）>
Topic Type:     <实时热点|行业热点|用户痛点|反常识观点|故事型|常青>
Target Audience:<目标人群>
Core Pain Point:<核心痛点>
Core Insight:   <核心洞察/观点（我的立场）>
Recommended Angle:<推荐内容切口（6 切口之一或组合）>
Why Now:        <为什么现在值得拍（时效性理由）>
Why This Fits User:<为什么匹配我的定位（匹配度理由）>
Competition:    <竞争内容分析：大家怎么讲、哪些讲烂>
Opportunity Gap:<别人没讲烂的缺口在哪>
Hook Directions:<3–5 个 Hook 方向，含类型与首帧/第一句>
Evidence:       <证据清单，每条标 已确认事实/推测/观点/网络讨论/未经证实>
Risk / Fact Check:<事实核查结论与风险，敏感领域标来源等级>
Score:          <总分 0–100 + 10 维分项与一句理由>
Recommendation: <推荐等级 S/A/B/C/D + 只选一个时的建议>
Content Tree:   <选题树：主选题→3–5子观点→可延展视频>
```

使用约定：
- `Evidence` 与 `Risk / Fact Check` 必须存在；涉及健康/金融/政策等敏感领域，无权威来源不得写「已确认事实」。
- `Score` 的 10 维定义见 `topic-scoring-rubric.md`；「匹配度」「真实经历支撑」低分时不得因高热度评 S。
- 一次研究可产出多个 Topic，每个 Topic 一套 Research Summary；推荐等级最高者排第一。
