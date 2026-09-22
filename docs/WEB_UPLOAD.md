# GitHub 网页上传 ZIP

## 先分清两个压缩包

| 文件 | 用途 |
| --- | --- |
| `github-upload-kit.zip` | 你下载的外层套件，先在电脑上解压 |
| `skill-repository.zip` | 上传到 GitHub 仓库根目录，由工作流展开 |
| `analyze-data-with-evidence.zip` | 给其他 AI 账号导入的单技能包 |

GitHub 普通网页上传本身不解压。实现后续只上传 ZIP，需要先设置下面的工作流，全程无需命令行、访问令牌或本地 Git。

## 首次设置

1. 在 GitHub 创建自己的仓库，建议名称 `analyze-data-with-evidence`。勾选初始化 README，得到默认分支。
2. 解压外层套件。用文本编辑器打开 `import-skill-zip.yml`，复制全部内容。
3. 在仓库首页点击 **Add file → Create new file**，文件名完整填写 `.github/workflows/import-skill-zip.yml`。
4. 粘贴文件内容并提交到默认分支。若仓库要求审核，先通过仓库正常流程合并该文件。
5. 回到仓库根目录，点击 **Add file → Upload files**，上传内层的 `skill-repository.zip`，保持这个文件名，然后提交。
6. 打开 **Actions → Import skill ZIP** 查看运行状态。成功后回到 **Code** 页面，会看到 README、docs、examples 和 skills 目录；ZIP 仍保留在仓库中。

流程会在上传 ZIP 的同一分支提交展开的文件。若默认分支受保护，在已有工作流的新分支上上传 ZIP，再使用正常 Pull Request 流程合并；工作流不会绕过分支保护。

## 后续更新

在根目录上传同名 `skill-repository.zip` 并替换旧文件即可。新 ZIP 必须保留本包的路径和文件集合。工作流校验整个包后覆盖其中列出的文件，不删除其他文件，不执行包内脚本，不修改工作流自身。

如果你直接编辑了 README 或 Skill，下次导入旧包会覆盖对应路径，所以应先把改动纳入新包。增加或删除包内路径时，需要同步修改工作流中的允许文件集合。

## 没有自动运行时

- 确认工作流实际路径是 `.github/workflows/import-skill-zip.yml`，不是仓库根目录中的同名文件。
- 确认 ZIP 位于仓库根目录且叫 `skill-repository.zip`，不是外层套件或单技能包。
- 确认仓库的 Actions 允许执行该工作流与官方 checkout Action。
- 工作流已在默认分支时，可到 **Actions → Import skill ZIP → Run workflow** 手动选择上传 ZIP 的分支并运行。
- 若提示写入被策略拒绝，由仓库维护者按组织规则确认 Actions 权限；工作流声明了 `contents: write`。无需把个人令牌写入 YAML。
- 若提交失败，先检查分支保护，或是否有人在运行期间新增提交。按正常流程处理后，在目标分支最新版本重新运行；不要强制推送。
- 所有有效文件相同时，运行成功但不会产生多余提交。

## 无需工作流的网页方法

解压 `skill-repository.zip`，进入解压后的目录，选中里面的 README、PACKAGE.json、docs、examples、skills 等文件和目录，拖入 **Add file → Upload files**。上传的是目录里的内容，不要再套一层外部文件夹。

这种方式适合只发布一次，上传后源码立即可浏览。仅上传 ZIP 而不配置工作流，则只能作为下载文件，不会展开为源码。

## 参考

- [GitHub 网页添加文件](https://docs.github.com/en/repositories/working-with-files/managing-files/adding-a-file-to-a-repository)
- [GitHub Actions 工作流语法](https://docs.github.com/en/actions/reference/workflows-and-actions/workflow-syntax)
- [手动运行工作流](https://docs.github.com/actions/managing-workflow-runs/manually-running-a-workflow)
