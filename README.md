# jobsfindCN — 中国求职能力提升助手 🎯

一个基于 Claude Code 的 AI Skill 系统，聚焦于**提高中国求职者的就职能力**。

现有的就职助手大多并不匹配中国就业环境，因此该项目完全聚焦于中国特色的求职场景

## 特点

- 专精 **算法** + **八股文** + **面试拷打** ,更适合中国宝宝的求职助手
- Java 后端、AI 算法、Agent 开发、Go 后端、C++、前端等更具有中国特色的岗位定位
- letcode + 小红书/牛客/脉脉/知乎,更具中国特色的题库和面经来源
- 角色驱动的能力画像,持续更新,越用越懂你


## 这是什么？

jobsfindCN 把你常用的 AI Coding CLI（Claude Code / Codex / Gemini / OpenCode）变成一个**私人求职教练**：

- **算法刷题** — 不是随机刷题，而是基于你的能力和目标公司生成个性化刷题计划
- **八股文准备** — 不是通用题库，而是根据你的岗位角色（Java 后端 / AI 算法 / Agent 开发...）针对性出题
- **简历优化** — 不是套模板，而是用 STAR-R 原则逐条诊断和改写
- **模拟面试** — 不是固定脚本，AI 扮演面试官，根据你的回答灵活追问，然后切换教练模式复盘
- **用户画像** — 不只是简历，系统持续追踪你的算法和八股文掌握水平，越用越精准

## 快速开始

```bash
# 1. 克隆仓库
git clone <repo-url> jobsfindCN
cd jobsfindCN

# 2. 用 Claude Code 打开
claude

# 3. 系统会自动检测你缺少哪些文件，引导你完成初始化

# 4. 开始使用
# 在 Claude Code 中输入 /jobsfind-cn 查看功能菜单
```

也可以直接说"帮我优化简历"、"我要刷题"、"帮我准备八股文"，系统会自动识别并进入对应模式。

## 核心功能

| 功能             | 说明                                                   |
| ---------------- | ------------------------------------------------------ |
| 📄 **简历解析**   | 支持 PDF 文本/Markdown/口述，提取结构化数据            |
| 👤 **用户画像**   | 角色驱动的能力画像（算法 15 主题 + 八股文角色分类）    |
| ✏️ **简历优化**   | STAR-R 原则逐条诊断改写，中文简历特性适配              |
| 🧮 **算法计划**   | 基于画像 + 目标公司，WebSearch LeetCode 生成 4 周计划  |
| 💻 **算法练习**   | 交互式出题 → 5 维评分 → 解法点评 → 更新 mastery        |
| 📚 **八股文计划** | 角色驱动 + 面经搜索（小红书/牛客/脉脉/知乎）→ 2 周计划 |
| 📝 **八股文练习** | 交互式出题 → 4 维评分 → 参考答案 → 追问预判            |
| 🎭 **模拟面试**   | AI 扮演面试官 → 算法+八股文+行为 → 教练复盘            |

## 支持的岗位角色

八股文分类体系根据你的目标岗位角色动态切换：

- **Java 后端开发** — 网络/数据库/编程语言/框架/OS/设计模式/分布式
- **AI 算法工程师** — 大模型/预训练/SFT/RLHF/推理优化/Prompt/评估
- **Agent 开发** — Agent架构/Vibe Coding/Skills/多Agent/RAG/LLM集成/Workflow
- **Go 后端开发** — Go基础/并发/框架/数据库/分布式/容器化
- **C++ 开发** — C++基础/OS/网络/编译链接/性能优化
- **前端开发** — HTML/CSS/JS/框架/工程化/浏览器原理/TS
- **数据开发** — SQL/数仓/大数据引擎/数据治理

## 项目结构

```
jobsfindCN/
  .agents/skills/jobsfindCN/SKILL.md    # 顶层 Skill 定义
  AGENTS.md                             # 主代理指令 + Onboarding
  CLAUDE.md                             # Claude Code 包装器
  DATA_CONTRACT.md                      # 数据契约
  README.md                             # 本文件
  
  config/
    profile.example.yml                 # 用户画像模板
  
  modes/
    _shared.md                          # 系统规则 + 评分逻辑
    _profile.template.md                # 用户个性化模板
    route.md                            # 模式路由
    parse-resume.md                     # Mode 1: 简历解析
    build-profile.md                    # Mode 2: 用户画像构建
    optimize-resume.md                  # Mode 3: 简历优化
    algorithm-plan.md                   # Mode 4: 算法刷题计划
    algorithm-practice.md               # Mode 5: 算法练习
    baguwen-plan.md                     # Mode 6: 八股文背诵建议
    baguwen-practice.md                 # Mode 7: 八股文练习
    mock-interview.md                   # Mode 8: 模拟面试
  
  references/
    algorithm-topics.md                 # 算法主题分类
    baguwen-role-taxonomy.md            # 角色驱动的八股文分类
    star-r-principle.md                 # STAR-R 原则 + 中文示例
    company-priority-map.md             # 公司-考点映射
    interview-question-bank.md          # 面经题目库
  
  data/                                 # 用户数据（gitignore）
    profile.yml                         # 完整用户画像
    cv.md                               # 用户简历
    algorithm-progress.md               # 算法练习历史
    baguwen-progress.md                 # 八股文学习历史
    practice-journal.md                 # 综合练习日志
```

## 设计理念

1. **角色驱动** — 不同的岗位有不同的准备重点，不做一刀切
2. **持续更新** — 每次练习都在更新你的能力画像，系统越用越了解你
3. **真实数据源** — 面经来自小红书/牛客/脉脉/知乎，算法题来自 leetcode.cn
4. **教练式互动** — 不给你答案，而是帮你找到答案
5. **中国优先** — 针对中国互联网公司的面试流程

## 灵感来源和鸣谢

- [career-ops](https://github.com/santifer/career-ops) — 多代理求职管道系统（投递管理）
- [interview-master-skill](https://github.com/santifer/interview-master-skill) — 全流程面试准备系统（面试准备）

## License

MIT License
