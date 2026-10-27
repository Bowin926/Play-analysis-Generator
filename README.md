# 剧本分析 Skill

供 Codex 使用的剧本分析工作流。提供剧本附件或剧本名称，即可按统一结构生成剧本分析 Word、场景画面提示词和角色形象提示词。

## 直接下载

[下载完整 Skill 压缩包](https://github.com/Bowin926/Play-analysis-Generator/raw/refs/heads/main/downloads/play-analysis-generator.zip)

解压后得到 `play-analysis-generator` 文件夹，按下面的路径复制即可安装。

## 安装方法与路径

下载本仓库后，将包含 `SKILL.md` 和 `scripts/` 的完整文件夹命名为 `play-analysis-generator`，复制到以下任一位置：

| 安装范围 | 路径 |
| --- | --- |
| 个人安装（当前官方文档） | `~/.agents/skills/play-analysis-generator/` |
| Windows 个人安装 | `%USERPROFILE%\.agents\skills\play-analysis-generator\` |
| 当前项目使用 | `<项目目录>/.agents/skills/play-analysis-generator/` |

若使用本技能最初配置的 Codex 环境，其技能目录为 `~/.codex/skills/play-analysis-generator/`，Windows 对应 `%USERPROFILE%\.codex\skills\play-analysis-generator\`；也可按该环境实际提供的技能目录安装。不要在多个加载目录重复安装同名技能。

安装完成后的目录结构：

```text
play-analysis-generator/
├── SKILL.md
├── README.md
├── requirements.txt
└── scripts/
    └── generate_docs.py
```

生成 Word 需要 Python 和 `python-docx`，在该文件夹中执行：

```sh
python -m pip install -r requirements.txt
```

新安装的技能若未出现在技能列表中，请重启 Codex。也可以让 Codex 的 `$skill-installer` 从本仓库链接安装；安装器采用的具体目录以当前环境为准。

## 使用方法

在 Codex 对话中提供剧本附件或剧本名称，并明确指定技能，例如：

```text
请使用 $play-analysis-generator 分析《哈姆雷特》，生成剧本分析 Word、
场景画面提示词和角色形象提示词，保存到当前工作区。
```

也可以指定偏好：

```text
请使用 play-analysis-generator 分析我上传的剧本。
场景采用 16:9 镜框式舞台，角色只生成手绘风格提示词。
```

只有剧本名时，基于通常通行版本分析并说明依据；提供附件可让分析更贴合指定版本。场景比例、演出场地和角色画面风格均可在对话中调整。

## 生成内容

| 文件 | 内容 |
| --- | --- |
| `{剧本名}剧本分析.docx` | 形象种子及解释、整体与分幕故事梗概、分幕场景描述、全剧核心矛盾及每幕主要/次要矛盾、主要角色分析 |
| `{剧本名}场景画面提示词.txt` | 每幕一条，包含机位、比例、演出场地、场景内容、色调与舞台结构；默认正面平视、居中、16:9、镜框式舞台 |
| `{剧本名}角色形象提示词.txt` | 主要角色的外形与时代服装描述；默认白底、全身、独立居中、3:4，并提供手绘和写实两版；指定风格时仅输出该版 |

角色分析包括形象种子、形象描述、性格、内在与外在矛盾、结局和角色关系。三个文件默认保存到当前工作区。提示词文件用于后续图像创作，本技能交付的是文档与文字提示词。

`scripts/generate_docs.py` 是文档排版辅助脚本，需要由 Codex 先生成并填入实际分析内容；直接执行当前空数据模板只会输出空白内容框架。

安装目录和调用方式参考 [OpenAI 官方技能文档](https://learn.chatgpt.com/docs/build-skills)。
