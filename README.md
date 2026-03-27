# cnb-sync-skill

将 `logzh/TradingAgents` 最新两次提交提炼为可复用技能，便于在其他仓库快速复刻 CNB/GitHub 双向同步与云开发环境配置。

## 来源提交

- `b6f27f4` chore: add CNB sync workflow and CNB config files (#1)
- `60158ad` chore: Remove humao.rest-client extension from Dockerfile

## 技能内容

- `skills/tradingagents-cnb-sync/README.md`：技能说明与使用步骤
- `skills/tradingagents-cnb-sync/templates/.cnb.yml`：CNB 配置模板
- `skills/tradingagents-cnb-sync/templates/.github/workflows/cnb_sync.yml`：GitHub -> CNB 同步工作流模板
- `skills/tradingagents-cnb-sync/templates/.ide/Dockerfile`：云 IDE 开发环境模板（已移除 `humao.rest-client` 扩展）

## 快速使用

1. 阅读技能文档：`skills/tradingagents-cnb-sync/README.md`
2. 将 `templates/` 内文件按原路径复制到目标仓库根目录
3. 按文档替换仓库属主、密钥来源与 Secrets 名称
