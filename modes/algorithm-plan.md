# Mode 4: 算法刷题计划 (algorithm-plan)

## 目标

基于用户画像中的算法 mastery 和目标公司，生成个性化 LeetCode 刷题计划。

## 前置条件

- `data/profile.yml` 应已存在，且 `algorithm_mastery` 已评估
- `references/company-priority-map.md` 和 `references/algorithm-topics.md` 提供映射

## 执行流程

### Step 1: 加载画像

读取 `data/profile.yml`：
- `algorithm_mastery.topics`（各主题当前 level）
- `target_roles.companies`（目标公司）
- `preferences.programming_language`（刷题语言）
- `preferences.practice_frequency`（练习频率）

### Step 2: 公司-主题优先级计算

根据目标公司的 tier 分布，从 `references/company-priority-map.md` 查表：

```
对每个算法主题：
  priority_score = Σ(每家公司对该主题的频率权重)
  频率权重: 🔴必考=5, 🟡高频=3, 🟢常见=2, ⚪偶见=1
```

如果用户目标公司跨 tier（如同时在字节和微软），取并集。

### Step 3: Gap 分析

```
对每个主题：
  gap = priority_score × (6 - current_level)
  
gap 越大 = 越优先
```

**优先规则：**
- P0（最高优先）：gap ≥ 15 → 本周重点
- P1（高优先）：gap 10-14 → 两周内
- P2（中优先）：gap 5-9 → 四周内
- P3（低优先）：gap < 5 → 有余力再做

### Step 4: WebSearch 获取题目

对 P0 和 P1 主题，使用 WebSearch 从 leetcode.cn 获取真实题目：

如果 WebSearch 功能不可用, 则使用 devtool-chrome-tool 通过浏览器获取题目。

搜索策略（每个高频主题搜 2-3 次）：
```
site:leetcode.cn "[主题关键词]" "[难度]"
site:leetcode.cn "[公司名]" 面试算法题
```

从搜索结果中提取：
- 题号、题名、难度
- 是否是公司真题（标注来源）
- 题目涉及的核心算法

### Step 5: 生成 4 周计划

```
## 🧮 算法刷题计划

**目标公司层：** [Tier 1: XX, XX / Tier 2: XX]
**当前算法水平：** [X]/5 | 已做 [N] 题
**练习频率：** [频率设定]
**薄弱的 P0 主题：** [主题1 (level X), 主题2 (level X)]

---

### 第 1 周：[重点主题]

| 优先级 | 题目 | 难度 | 主题 | 预计用时 | 公司标签 |
|--------|------|------|------|---------|---------|
| P0 | [题号]. [题名] | 简单 | [主题] | 20min | [公司]真题 |
| P0 | [题号]. [题名] | 中等 | [主题] | 30min | - |
| P1 | [题号]. [题名] | 中等 | [主题] | 30min | [公司]真题 |
| P2 | [题号]. [题名] | 困难 | [主题] | 45min | - |

**本周目标：** 完成 [N] 题，重点攻克 [主题]

### 第 2 周：[重点主题]
...

### 第 3 周：[主题]
...

### 第 4 周：复习 + 综合练习
**本周目标：** 复习前 3 周错题 + 2 道困难题 + 模拟面试

---

### 刷题建议

1. **每道题先自己想 15 分钟**，想不出来再看题解
2. **做过的题 3 天后复习一次**，确认真正掌握
3. **同一主题至少做 3-5 题**，形成肌肉记忆
4. **困难题不必追求数量**，每周 1-2 道足矣
5. **用 `/jobsfind-cn 算法练习`** 开始交互式刷题
```

### Step 6: 保存并引导

将计划写入 `data/algorithm-progress.md`。

> "刷题计划已生成。想开始练习吗？运行 `/jobsfind-cn 算法练习`，我会根据计划给你出第一道题。"

## 计划更新

如果用户已有计划但想更新：
- "算法水平更新了" → 重新计算 Gap → 调整计划
- "目标公司变了" → 重算公司优先级 → 调整计划
- "时间不够" → 减少每周题目数，保留 P0

## 注意事项

- 题目来源标注清楚（"LeetCode 真题" / "预测重点题"）
- 不要一次搜索所有主题——优先搜索 P0 主题即可
- 如果 WebSearch 未返回有效结果，使用已知的经典题号补充
- 计划存储在 `data/algorithm-progress.md`，不要覆盖用户已有的完成记录
