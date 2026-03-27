# cnb-sync-skill

通用技能仓库：将 GitHub 仓库自动同步到 CNB 仓库。

## 技能内容

- `skills/github-sync-to-cnb/README.md`：技能说明与接入步骤
- `skills/github-sync-to-cnb/templates/.github/workflows/cnb_sync.yml`：GitHub -> CNB 同步工作流模板

## 快速使用

### 方式 A：使用 npx（推荐）

在你的目标仓库根目录执行（需 Node.js 18+）：

```bash
npx degit logzh/cnb-sync-skill/skills/github-sync-to-cnb .cursor/skills/github-sync-to-cnb
```

然后在 Cursor 中使用该技能，或按技能 README 将模板复制到仓库对应路径。

### 方式 B：使用 git sparse-checkout（无 npx）

```bash
git clone --depth 1 --filter=blob:none --sparse https://github.com/logzh/cnb-sync-skill.git /tmp/cnb-sync-skill
cd /tmp/cnb-sync-skill
git sparse-checkout set skills/github-sync-to-cnb
cp -r skills/github-sync-to-cnb /path/to/your-repo/.cursor/skills/
```

### 方式 C：手动复制（最直接）

1. 阅读技能文档：`skills/github-sync-to-cnb/README.md`
2. 将 `templates/.github/workflows/cnb_sync.yml` 复制到目标仓库同路径
3. 替换 CNB 组织名并配置 Secret（GitHub 路径：`Settings -> Secrets and variables -> Actions`）
