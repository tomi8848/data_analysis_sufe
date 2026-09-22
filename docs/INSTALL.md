# 安装与迁移

## 支持 Agent Skills 的工具

1. 找到 `skills/analyze-data-with-evidence/`。
2. 导入整个目录，或放入目标工具支持的技能目录。
3. 保留 `SKILL.md`、`references/`、`agents/` 和 `assets/` 的相对位置。
4. 用一项小任务确认工具能够读取主指令及参考文档。

各工具的导入入口和技能目录不同。`agents/openai.yaml` 是可选平台元数据；其他工具未必使用它。核心行为由 `SKILL.md` 和参考文档定义。

## 本地 Codex：项目内使用

将目录复制成项目下的 `.agents/skills/analyze-data-with-evidence/`。在当前项目根目录操作；下面假定你已下载仓库文件。

Windows PowerShell：

```powershell
New-Item -ItemType Directory -Force .agents\skills | Out-Null
Copy-Item -Recurse -Force .\skills\analyze-data-with-evidence .\.agents\skills\
```

macOS / Linux：

```bash
mkdir -p .agents/skills
cp -R skills/analyze-data-with-evidence .agents/skills/
```

之后用 `$analyze-data-with-evidence` 调用，或在技能选择器中选择它。官方文档列出的用户级目录为 `~/.agents/skills`，适合希望多个项目共用的情况。

## 另一个支持个人 Skill 导入的账号

使用发布套件中的 `analyze-data-with-evidence.zip`，上传并明确要求“安装这个数据分析 Skill”。是否可安装取决于目标账号和界面的技能能力。`skill-repository.zip` 用于 GitHub 仓库导入，不能与单技能包混用。

## 不支持 Skill 的聊天工具

上传以下四个 Markdown 文件，或把主指令放入项目指令、把参考文件放入项目知识文件：

- `SKILL.md`
- `references/course-principles.md`
- `references/execution-checks.md`
- `references/work-templates.md`

可发送：“请阅读主指令与参考文件，后续的数据分析按这些规则执行。无法读取文件或运行代码时明确说明，不编造运行结果。”

普通聊天附件只作为可用上下文，不能保证跨新会话自动生效。若工具不能运行代码，先让它输出分析方案和可运行代码，再在有运行环境的地方核对结果。

## 使用检查

使用 `examples/customer_mix.csv` 和案例问题，检查能否识别客群权重变化、正确复算销售额，并区分结构解释与促销因果效果。不要只测试模型能否复述六项原则。

## 官方参考

- [Codex / ChatGPT Skill 文档](https://learn.chatgpt.com/docs/build-skills)
- [Agent Skills 格式](https://agentskills.io/specification)
