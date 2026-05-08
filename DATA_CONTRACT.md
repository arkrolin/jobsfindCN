# Data Contract — jobsfindCN

本文档定义哪些文件属于**系统层**（可自动更新），哪些属于**用户层**（永不自动更新）。

## User Layer（永不自动更新）

这些文件包含用户的个人数据、个性化设置和工作成果。更新过程绝不会修改它们。

| File | Purpose |
|------|---------|
| `data/profile.yml` | 完整用户画像 |
| `data/cv.md` | 用户简历 |
| `data/algorithm-progress.md` | 算法练习历史 |
| `data/baguwen-progress.md` | 八股文学习历史 |
| `data/practice-journal.md` | 综合练习日志 |

## System Layer（可安全自动更新）

这些文件包含系统逻辑、指令和模板，随每次 release 改进。

| File | Purpose |
|------|---------|
| `AGENTS.md` | 主代理指令 |
| `CLAUDE.md` | Claude Code 包装器 |
| `DATA_CONTRACT.md` | 本文件 |
| `README.md` | 项目说明 |
| `modes/_shared.md` | 系统规则、评分逻辑 |
| `modes/_profile.template.md` | 用户自定义模板 |
| `modes/route.md` | 模式路由 |
| `modes/parse-resume.md` | 简历解析模式 |
| `modes/build-profile.md` | 画像构建模式 |
| `modes/optimize-resume.md` | 简历优化模式 |
| `modes/algorithm-plan.md` | 算法计划模式 |
| `modes/algorithm-practice.md` | 算法练习模式 |
| `modes/baguwen-plan.md` | 八股文计划模式 |
| `modes/baguwen-practice.md` | 八股文练习模式 |
| `modes/mock-interview.md` | 模拟面试模式 |
| `config/profile.example.yml` | 画像模板 |
| `references/*` | 所有参考文件 |
| `.agents/skills/jobsfindCN/SKILL.md` | Skill 定义 |
| `.claude/skills/jobsfindCN/SKILL.md` | 符号链接 |

## The Rule

**如果文件在 User Layer，任何更新过程不得读取、修改或删除它。**

**如果文件在 System Layer，它可以被上游最新版本安全替换。**
