# TradingAgents CNB 同步技能

本技能基于以下两个最新提交提炼：

- `b6f27f4` `chore: add CNB sync workflow and CNB config files (#1)`
- `60158ad` `chore: Remove humao.rest-client extension from Dockerfile`

目标：把 TradingAgents 中新增的 CNB/GitHub 同步能力与云 IDE 环境配置，沉淀为可复用模板。

## 1) 提交学习摘要

### 提交 1：`b6f27f4`

新增 3 个关键文件：

1. `.cnb.yml`
   - 定义 CNB 的 VSCode 服务，使用 `.ide/Dockerfile` 构建环境。
   - 在 `feat*` 分支 push 时，使用 `tencentcom/git-sync` 将代码同步到 GitHub。
2. `.github/workflows/cnb_sync.yml`
   - 在 GitHub `main` 分支 push 时，反向同步到 CNB 仓库。
   - 核心依赖环境变量 `CNB_TOKEN`（GitHub Secret）。
3. `.ide/Dockerfile`
   - 提供云开发镜像：Python 3.12 + code-server + 常用插件 + uv + Node.js 22 + Go 1.24。

### 提交 2：`60158ad`

- 在 `.ide/Dockerfile` 中移除 `humao.rest-client` VSCode 插件安装。
- 含义：保留核心开发插件，降低非必要扩展依赖。

## 2) 模板文件

本技能附带模板目录：`templates/`

- `templates/.cnb.yml`
- `templates/.github/workflows/cnb_sync.yml`
- `templates/.ide/Dockerfile`

这些模板已对齐上述两次提交后的最终状态。

## 3) 集成步骤

1. 将 `templates/` 下文件复制到目标仓库根目录对应路径：
   - `.cnb.yml`
   - `.github/workflows/cnb_sync.yml`
   - `.ide/Dockerfile`
2. 按实际仓库替换变量：
   - `.cnb.yml` 中的 GitHub 目标组织 `logzh`
   - `.cnb.yml` 中的 `imports` 密钥文件来源
   - `cnb_sync.yml` 中 CNB 目标组织 `spencezhang`
3. 在 GitHub 仓库配置 Secret：
   - `CNB_TOKEN`（供 GitHub Action 推送到 CNB）
4. 验证双向同步：
   - 在 `feat*` 分支推送，检查 CNB -> GitHub 是否生效
   - 在 `main` 分支推送，检查 GitHub -> CNB 是否生效

## 4) 适配建议

- 如果你的分支策略不是 `feat*`，修改 `.cnb.yml` 中触发条件。
- 如果你不需要 Go 或 Node.js，可精简 `.ide/Dockerfile` 对应安装段。
- `actions/checkout@v3` 可视团队规范升级版本，但建议先确保与现有流水线兼容。
