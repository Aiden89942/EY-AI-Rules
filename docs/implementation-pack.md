# 多專案規範實作包（中文版）

此文件提供可直接落地的內容，包含：

1. repo 結構
2. `.mdc` 規則檔內容
3. 客戶端文件
4. GitHub Actions
5. Remote Rule 使用方式

## 1) Repo 結構

```text
private-dev-rules/
├── docs/
│   ├── git-workflow.md
│   ├── implementation-pack.md
│   ├── rollback.md
│   └── workflow-guide.md
├── global/
│   ├── core-policy.mdc
│   ├── commit-common.mdc
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

## 2) `.mdc` 規則檔

目前已實體建立於以下路徑：

- `global/commit-common.mdc`
- `global/core-policy.mdc`
- `global/safety-common.mdc`
- `global/workflow-common.mdc`
- `projects/nonFood-nuxt-web.mdc`
- `projects/member-cmsweb-vue.mdc`
- `projects/frontend-vue-cms-template.mdc`
- `projects/nonFood-vue-cms.mdc`
- `projects/infra-strict.mdc`

規則語氣統一採 `MUST` / `MUST NOT`，並以中文敘述為主，方便後續維護。

## 3) 客戶端文件（不含 AI 字樣）

已建立：

- `docs/git-workflow.md`
- `docs/rollback.md`

文件風格採企業工程規範，可直接作為內部制度文件。

## 4) 專案 Workflow 樣板（可直接複製）

已建立：

- `templates/workflows/projects/member-cmsweb-vue/deploy-uat.yaml`
- `templates/workflows/projects/member-cmsweb-vue/deploy-prod.yaml`
- `templates/workflows/projects/psp/deploy-uat.yml`
- `templates/workflows/projects/psp/deploy-prod.yml`
- `templates/workflows/projects/pspAdmin/deploy-uat.yml`
- `templates/workflows/projects/pspAdmin/deploy-prod.yml`

## 5) Remote Rule 使用方式

核心原則：

- 建議順序：`core-policy` -> `workflow-common` -> `safety-common` -> `commit-common` -> `projects/<project>.mdc`
- URL 固定到 tag 或 commit SHA
- production 專案不要直接指向 `main`
