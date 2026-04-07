# EY-AI-Rules

私人規範 repo，集中管理多專案可重用的 AI rules、Git / Commit / Deploy 文件範本，以及 GitHub Actions 防呆樣板。

## 目標

- 客戶 repo 不出現 `.cursor/`、AI 規則檔或工具痕跡。
- AI 仍可透過 remote rule 套用共用規範與專案規範。
- 多專案共用一套可維護、可擴充、可版本化的治理結構。
- 部署流程預設保守，避免誤 deploy production。

## 結構

```text
EY-AI-Rules/
├── docs/
│   ├── git-workflow.md
│   ├── rollback.md
│   └── workflow-guide.md
├── global/
│   ├── commit-common.mdc
│   ├── core-policy.mdc
│   ├── safety-common.mdc
│   └── workflow-common.mdc
├── projects/
│   ├── frontend-vue-cms-template.mdc
│   ├── infra-strict.mdc
│   ├── member-cmsweb-vue.mdc
│   ├── nonFood-nuxt-web.mdc
│   └── nonFood-vue-cms.mdc
└── templates/
    └── workflows/
        ├── README.md
        └── projects/
            ├── member-cmsweb-vue/
            ├── psp/
            └── pspAdmin/
```

## 使用原則

1. AI 載入順序建議為：`global/core-policy.mdc` -> `global/workflow-common.mdc` -> `global/safety-common.mdc` -> `global/commit-common.mdc` -> `projects/<project>.mdc`。
2. remote rule URL 建議固定到 tag 或 commit SHA，不要直接指向 `main`。
3. 客戶 repo 僅放中性工程文件與 CI 規則，不放任何 AI 專屬設定。
4. production 相關流程必須要求人工核准與額外檢查。

## 建議版本策略

- `v1.x`: 穩定規範版本，供正式專案掛載。
- `main`: 持續演進版本，僅供內部驗證。
- 每次調整規範時，同步更新 `docs/` 與 `templates/workflows/` 樣板。
