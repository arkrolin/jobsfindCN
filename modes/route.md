# Mode Router — jobsfindCN

<!-- 路由逻辑：根据用户输入选择对应模式 -->

## Mode Detection

根据用户意图选择模式：

| 触发器 | 模式文件 |
|--------|---------|
| 用户粘贴 PDF/简历文本 / "解析简历" / "parse" | `modes/parse-resume.md` |
| "构建画像" / "更新画像" / "我的画像" / "profile" | `modes/build-profile.md` |
| "简历优化" / "优化简历" / "改写简历" / "resume" | `modes/optimize-resume.md` |
| "算法计划" / "刷题计划" / "algorithm plan" | `modes/algorithm-plan.md` |
| "算法练习" / "刷题" / "来一题" / "practice" / "做题" | `modes/algorithm-practice.md` |
| "八股文计划" / "八股文建议" / "baguwen plan" / "背诵" | `modes/baguwen-plan.md` |
| "八股文练习" / "来一道八股文" / "baguwen practice" / "面经练习" | `modes/baguwen-practice.md` |
| "模拟面试" / "mock" / "面试模拟" / "来面试" | `modes/mock-interview.md` |
| 无参数 / "帮助" / "help" / "菜单" | 显示功能菜单 |

## Route Execution

1. 匹配用户意图到对应 mode 文件
2. 按顺序加载上下文：
   - `modes/_shared.md`（系统规则）
   - `modes/_profile.md`（如果存在）
   - 目标 mode 文件
3. 执行 mode 中的流程

## Auto-Detection

如果用户输入不匹配任何已知触发器，尝试自动检测：
- 包含"简历"或大段文本 → 可能是简历解析或优化
- 包含"LeetCode" / "算法" / "题" → 可能是算法相关
- 包含"面试" / "八股文" / "面经" → 可能是面试/八股文
- 无法判断 → 显示功能菜单，询问用户意图
