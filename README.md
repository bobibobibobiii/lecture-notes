# lecture-notes — 交互式讲义生成器

一个 opencode skill：在包含课程材料（课件 PDF / PPT / Word / 笔记）的文件夹里运行，自动完成——

1. **读取材料**，通读全文；
2. **列出知识要点**，交用户确认；
3. **互动式询问掌握程度**（未学/一般/熟练），据以调节详略；
4. **按"控制原理讲义"风格**生成可编译的中文 LaTeX 讲义（默认排除背景与发展史、聚焦考点）；
5. 编译并核验（无缺字、无溢出、无未定义引用）。

产出与参考实现 `control-notes`（《控制原理完整自学讲义》）同款：`ctexart` + XeLaTeX + 脚注页码回查 + 分节文件 + 原图提取嵌入。

## 目录结构

```
lecture-notes/
├── SKILL.md                  # 技能主说明（工作流程 + 规则摘要）
├── README.md                 # 本文件
├── agents/
│   └── openai.yaml           # 各 Agent 的界面元数据与默认 prompt
├── assets/
│   └── main.tex              # LaTeX 讲义编译入口模板
└── references/
    └── style-guide.md        # 详细写作规则（段落/术语/详略分级/排版/核验）
```

## 安装

**方式一：opencode 本地技能目录**

把整个 `lecture-notes` 文件夹放入：

- 用户级：`~/.config/opencode/skills/`
- 项目级：`<项目>/.opencode/skills/`

**方式二：`@byted-supabase`/其他 Agent**

按目标 Agent 的 skill 安装规范挂载（本仓库同时提供 `agents/openai.yaml` 便于接入）。

## 使用

在放有课程材料的文件夹里，对 opencode 说：

```
用 lecture-notes 把这里的课件做成讲义
```

技能会按五步流程执行，其中"列知识要点"和"问掌握程度"是互动环节，会等你确认后再继续。

## 依赖（运行期）

- 文本提取：`pdftotext`（Popper/MiKTeX 自带），或 Python + PyMuPDF（`fitz`）。
- PPT/Word 抽取（可选）：Python `python-pptx` / `python-docx`。
- 编译：含 `ctex` 的 XeLaTeX（TeX Live / MiKTeX），或 `tectonic`。

## 说明

- 掌握程度只调节"解释详略"，不改变"内容取舍"——考点/可用知识都保留。
- 默认不纳入发展史与背景；如要保留，在对话中说明即可。
