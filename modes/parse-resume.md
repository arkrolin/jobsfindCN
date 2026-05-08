# Mode 1: 简历解析 (parse-resume)

## 目标

从用户提供的简历文件中提取结构化信息，写入 `data/cv.md`，并初始化 `data/profile.yml` 骨架。

## 输入形式

用户可能通过以下方式提供简历：
- 提供 PDF 文件路径（Claude Code Read 工具直接读取）
- 粘贴简历文本（纯文本 / Markdown）
- 口头描述经历（"我是 XX 大学计算机专业..."）

## 执行流程

### Step 1: 获取简历内容

**如果用户粘贴文本：**
直接进入 Step 2。

**如果用户提供 PDF 路径：**

PDF 解析使用两层策略——优先在线 API，被拒后用本地库：

```
Step 1a — 询问 Doc2X API
  Doc2X 是专业的 PDF 解析 API，解析效果最好（支持表格/扫描件/复杂排版）。
  → "要解析这份 PDF，我推荐使用 Doc2X API（解析效果好，支持表格和扫描件）。
     你有 Doc2X 的 API Key 吗？如果有，我可以通过 API 调用帮你解析。"
  
  如果用户同意并提供 API Key：
  → 使用 Bash 调用 Doc2X API：
    curl -X POST "https://api.doc2x.com/v1/parse" \
      -H "Authorization: Bearer $DOC2X_API_KEY" \
      -F "file=@[PDF路径]" \
      -F "output_format=md"
  → 获取返回的 Markdown 文本 → 进入 Step 2 结构化提取

Step 1b — 用户拒绝 / 无 API Key → 使用 PyMuPDF
  PyMuPDF 是本地 PDF 解析库，无需 API Key，效果优于 Read 工具。
  → 先检查 PyMuPDF 是否已安装：
    python -c "import fitz; print('ok')" 2>&1
  → 如果未安装（ImportError）：
    告知用户并安装：pip install PyMuPDF
  
  → 使用 Bash 执行 PyMuPDF 提取文本：
    python -c "
  import fitz
  doc = fitz.open('[PDF绝对路径]')
  for page in doc:
      print(page.get_text())
    "
  → 获取文本 → 进入 Step 2 结构化提取

Step 1c — PyMuPDF 也失败 → 最终回退
  如果 PyMuPDF 也报错（文件损坏/加密/纯扫描件等）：
  → "PDF 自动解析失败。你可以：
    1. 把 PDF 中的文字内容复制粘贴给我
    2. 简单描述你的经历，我帮你整理成简历格式
    哪个方便？"

  特殊情况处理：
  - PyMuPDF 返回空文本但无报错（图片型 PDF）：
    → "这个 PDF 似乎是扫描图片格式，文字内容无法直接提取。
       如果你有 Doc2X 的 API Key，它可以处理扫描件。
       或者你可以直接把关键经历告诉我，我帮你整理。"
  - 文件需要密码（fitz.open 报 "password" 相关错误）：
    → "PDF 有密码保护。请提供无密码版本或直接粘贴简历文本。"
```

### Step 2: 结构化提取

从简历文本中提取以下信息：

```markdown
# [姓名] 的简历

## 基本信息
- 姓名：
- 邮箱：
- 电话：
- 地点：
- LinkedIn / GitHub / 个人网站：

## 教育背景
- **学校名称** — 专业（学位）| YYYY.MM - YYYY.MM
  - GPA（如适用）
  - 相关课程

## 工作经历
- **公司名称** — 岗位 | YYYY.MM - YYYY.MM
  - 关键成果 1（尽量量化）
  - 关键成果 2
  - 关键成果 3

## 项目经验
- **项目名称** — 角色 | YYYY.MM - YYYY.MM
  - 项目简介（一句话）
  - 你的贡献（量化为佳）
  - 技术栈

## 技能
- 编程语言：
- 框架/工具：
- 数据库：
- 其他：

## 其他（可选）
- 证书/奖项
- 开源贡献
- 语言能力
```

### Step 3: 确认和补充

展示提取结果，询问：
> "我从你的简历中提取了以上信息。有几个地方想确认：
> - 你的目标岗位是什么？（Java后端 / AI算法 / Agent开发 / 前端 / 其他）
> - 有没有遗漏的重要经历或项目？
> - 有需要补充的技能吗？"

### Step 4: 写入文件

确认后：
1. 将结构化 Markdown 写入 `data/cv.md`
2. 将提取的基本信息写入 `data/profile.yml` 的 `candidate` 部分
3. 如果 profile.yml 不存在，创建骨架文件（所有 mastery 默认为 level=1）

### Step 5: 下一步引导

> "简历已解析并保存到 `data/cv.md`。接下来建议：
> - **构建用户画像** → 帮你建立完整的算法和八股文能力画像
> - **简历优化** → 用 STAR-R 原则帮你改写优化
>
> 需要我帮你构建画像吗？"

## 注意事项

- 永远不要编造用户没有提到的数据或经历
- 量化数据缺失时，主动询问（"这个项目提升了多少性能？"）
- 不确定的信息标注 `[待确认]`
- 不要修改已有的 `data/cv.md` 除非用户明确要求
