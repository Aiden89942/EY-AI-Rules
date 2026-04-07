# Workflows 樣板索引

此目錄放「可直接複製到各專案」的 GitHub Actions workflow 樣板，依專案分類。

## 目錄結構

- `projects/member-cmsweb-vue/`
  - `deploy-uat.yaml`
  - `deploy-prod.yaml`
- `projects/psp/`
  - `deploy-uat.yml`
  - `deploy-prod.yml`
- `projects/pspAdmin/`
  - `deploy-uat.yml`
  - `deploy-prod.yml`

## 使用方式

1. 先選擇專案目錄（例如 `projects/member-cmsweb-vue/`）。
2. 依環境挑選對應檔案（`deploy-uat` / `deploy-prod`）。
3. 複製到目標專案的 `.github/workflows/`。
4. 依專案實際參數調整 runner、secret、環境名稱、部署路徑。

## 注意事項

- 這些檔案來自現有專案實際 workflow，內容可能包含特定 infra 參數。
- 複製後務必二次檢查：
  - runner labels
  - secret 名稱
  - Dockerfile 路徑
  - ECS / 伺服器部署目標
