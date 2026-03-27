# GitHub 到 CNB 同步技能

本技能仅关注一个目标：当 GitHub 仓库有新提交时，自动同步到 CNB 对应仓库。

## 技能内容

- `templates/.github/workflows/cnb_sync.yml`
  - GitHub Actions 工作流模板
  - 触发条件：`main` 分支 push（可改）
  - 执行方式：调用 `tencentcom/git-sync` 容器推送到 CNB

## 使用步骤

1. 将 `templates/.github/workflows/cnb_sync.yml` 复制到目标仓库同路径。
2. 修改工作流中的 CNB 目标地址组织名：
   - `https://cnb.cool/<your-cnb-org>/${{ steps.repo-name.outputs.name }}.git`
3. 在 GitHub 仓库中新增 Secret：
   - `CNB_TOKEN`（需具备写入目标 CNB 仓库权限）
4. 向触发分支推送一次提交，确认 Action 执行成功。

## 可选调整

- 若默认分支不是 `main`，修改 `on.push.branches`。
- 若不希望强制覆盖推送，可移除 `PLUGIN_FORCE=true`。
