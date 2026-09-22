# 问题驱动的数据分析 Skill

用明确的问题约束分析，用可核查的证据支持结论。

本项目把《分析思维与数据素养》《AI驱动的知识构建》课件中的原则整理为可供 AI 使用的工作流程，适合业务分析、研究分析、指标诊断、预测方案和分析报告审查。核心规则使用中文。

## 快速使用

把 [`skills/analyze-data-with-evidence`](skills/analyze-data-with-evidence) 整个目录导入支持 Agent Skills 的工具，然后调用 `analyze-data-with-evidence`。主指令位于 [SKILL.md](skills/analyze-data-with-evidence/SKILL.md)，完整安装方法见 [安装与迁移](docs/INSTALL.md)。

在本地 Codex 中可输入：

```text
使用 $analyze-data-with-evidence 分析这份数据。
先明确问题与指标口径，核验数据后选择方法，最后给出有证据边界的结论和下一步。
```

没有 Skill 功能的聊天工具也可以读取 `SKILL.md` 和三个参考文档，按其规则分析；这种使用不等于安装了会自动触发的技能。

## 它会怎样工作

| 原则 | 具体行为 |
| --- | --- |
| 问题导向 | 先确定对象、指标、时间、比较基准和需要支持的判断 |
| 可复现 | 保留数据来源、处理步骤、参数与运行环境 |
| 数据诚实 | 标明未知与模拟，报告反例、处理影响和不确定性 |
| 受众适配 | 每张图回答问题，标题与证据强度一致 |
| 从简单开始 | 先建基线，再判断复杂模型是否有新增价值 |
| 可行动 | 给出可评估的下一步，证据不足时先补数或验证 |

七步流程：定义问题、获取数据、清洗、探索、建模分析、解释沟通、反馈迭代。按任务裁剪，不要求每次都完成四类分析、训练模型或生成长报告。

特别检查加权均值、百分点与相对变化、样本选择、相关与因果、多重检验、时间泄漏、预测区间及图形误导。AI 写出的代码必须实际执行并核验，才会被表述为已运行结果。

## 使用示例

- **指标下降**：“客单价下降是否说明经营变差？请同时核对销售规模、客户构成和利润数据需求。”
- **预测方案**：“每天晚上预测次日销售额，哪些字段在预测时可获得？请设计基线和时间回测。”
- **报告审查**：“检查这份报告的指标口径、因果措辞、图表和行动建议是否有依据。”

可复算的教学数据和参考结果见 [案例说明](examples/README.md)。原始课件中的示例及本仓库的例子不代表真实市场观测。

## 文件导航

| 路径 | 用途 |
| --- | --- |
| `skills/analyze-data-with-evidence/SKILL.md` | AI 执行的主流程 |
| `skills/analyze-data-with-evidence/references/` | 原则来源、执行检查、工作模板 |
| `skills/analyze-data-with-evidence/agents/` | 兼容工具的显示与调用信息 |
| `docs/INSTALL.md` | 安装和迁移 |
| `docs/WEB_UPLOAD.md` | GitHub 纯网页上传 ZIP 与自动导入 |
| `docs/MAINTENANCE.md` | 更新包、覆盖范围和版本维护 |
| `examples/` | 教学数据、示例问题与核对结果 |
| `PACKAGE.json` | 包名称、版本和打包范围 |

## 网页上传 ZIP

GitHub 的普通 Upload files 会保存 ZIP 文件，不会自动展开。本发布套件提供一个独立的 `import-skill-zip.yml`，首次将它保存为仓库中的 `.github/workflows/import-skill-zip.yml`，随后上传 `skill-repository.zip` 即可由 GitHub Actions 校验、展开并提交文件。详见 [网页上传指南](docs/WEB_UPLOAD.md)。

该方式需要仓库允许 GitHub Actions 和所需写入权限。也可以解压后，把文件和目录拖入网页上传，不使用工作流。

## 来源与边界

原则来源见 [课件依据与映射](skills/analyze-data-with-evidence/references/course-principles.md)，其中保留文件名、授课者署名与页码。仓库包含原则转述及操作化整理，未附原始课件。它不代表课程作者或任何 AI 平台的官方发布。

这是工作流程与参考资料，不包含训练后的预测模型、私人业务数据、账号凭证或自动取得数据源权限的功能。具体执行能力取决于宿主 AI 的文件读取、代码运行和网络工具。此包未代替维护者选定开源许可证；发布者可按自己的授权安排补充。
