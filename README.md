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

## Cursor Remote 引用方法

### 1) 基本概念

- 在 Cursor 的 Rules / Remote Rules 設定中，新增本 repo 的 raw URL。
- 每個 URL 對應一份規則檔。
- 建議按固定順序載入，避免規則覆蓋混亂。

### 1-1) 依檔案位置組出引用路徑

當你看到 repo 內任何規則檔路徑，例如：

```text
global/core-policy.mdc
projects/<project-name>.mdc
```

可直接套用這個公式：

```text
https://raw.githubusercontent.com/<GitHub帳號>/<Repo名稱>/<版本>/<檔案相對路徑>
```

你目前專案固定值為：

- GitHub 帳號：`Aiden89942`
- Repo：`EY-AI-Rules`
- 版本：`main`（或改 tag / commit SHA）

所以只要把「檔案相對路徑」代入就能得到引用 URL：

```text
global/core-policy.mdc
=> https://raw.githubusercontent.com/Aiden89942/EY-AI-Rules/main/global/core-policy.mdc

projects/<project-name>.mdc
=> https://raw.githubusercontent.com/Aiden89942/EY-AI-Rules/main/projects/<project-name>.mdc
```

### 2) 建議載入順序

1. `global/core-policy.mdc`
2. `global/workflow-common.mdc`
3. `global/safety-common.mdc`
4. `global/commit-common.mdc`
5. `projects/<project>.mdc`

### 3) `main` 版本（快速更新）

全域規則（固定四條）：

```text
https://raw.githubusercontent.com/Aiden89942/EY-AI-Rules/main/global/core-policy.mdc
https://raw.githubusercontent.com/Aiden89942/EY-AI-Rules/main/global/workflow-common.mdc
https://raw.githubusercontent.com/Aiden89942/EY-AI-Rules/main/global/safety-common.mdc
https://raw.githubusercontent.com/Aiden89942/EY-AI-Rules/main/global/commit-common.mdc
```

專案規則（擇一）：

```text
https://raw.githubusercontent.com/Aiden89942/EY-AI-Rules/main/projects/<project-name>.mdc
```

若你新增新專案（例如 `projects/new-service.mdc`），引用 URL 就是：

```text
https://raw.githubusercontent.com/Aiden89942/EY-AI-Rules/main/projects/new-service.mdc
```

### 3-1) 新增專案規則時的命名建議

- 檔名建議使用 repo 名稱或服務名（例：`member-cmsweb-vue.mdc`、`new-service.mdc`）。
- 一個專案對應一個 `projects/<project-name>.mdc`。
- 避免在檔名放空白或特殊符號，建議使用小寫與 `-`。

### 4) 版本策略建議

- 若規則還在快速調整，可直接用 `main`。
- 若需要穩定可追溯版本，改用 tag 或 commit SHA。
- 若規則更新後行為有差異，先檢查是否仍指向預期版本。

## 建議版本策略

- `v1.x`: 穩定規範版本，供正式專案掛載。
- `main`: 持續演進版本，僅供內部驗證。
- 每次調整規範時，同步更新 `docs/` 與 `templates/workflows/` 樣板。
