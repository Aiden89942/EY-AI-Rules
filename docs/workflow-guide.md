# Workflow Guide

## 標準工作流程說明

本文件定義 Feature Development、Bug Fix、Hot Fix 的標準流程，支援 JIRA 與 GitHub Issue 兩種編號格式。

---

## Feature Development 流程

### 1. 任務準備

- 從 JIRA 取得任務編號（例如：`PROJ-123`）或建立 GitHub Issue（例如：`#123`）。
- 確認需求細節與驗收標準。
- 必要時與 PM / 團隊成員討論實作方案。
- 定義版本號（Semantic Versioning）。

### 2. 開發前置作業

```bash
# 更新本地 develop 分支
git checkout develop
git pull origin develop

# 建立功能分支
# JIRA 格式
git checkout -b feature/PROJ-123-user-registration
# GitHub 格式
git checkout -b feature/GH-123-user-registration
```

### 3. 開發與提交

```bash
# JIRA 格式的 commit
git commit -m "[PROJ-123] feat: 實作使用者註冊表單"
git commit -m "[PROJ-123] feat: 新增資料驗證"

# GitHub 格式的 commit
git commit -m "feat #123: 實作使用者註冊表單"
git commit -m "feat #123: 新增資料驗證"

# 定期同步 develop 的更新
git checkout develop
git pull origin develop
git checkout feature/PROJ-123-user-registration
git merge develop
```

### 4. 提交 Pull Request

- 推送分支到遠端：

```bash
git push origin feature/PROJ-123-user-registration
```

- 建立 PR。
- 標題格式：
  - JIRA：`[PROJ-123] 實作使用者註冊功能`
  - GitHub：`feat: 實作使用者註冊功能 (#123)`
- PR 說明需包含：
  - 功能描述
  - 測試項目
  - 注意事項
- Code Review：
  - 至少一位團隊成員 review
  - 根據回饋進行修改
  - 確保 CI 檢查通過

### 5. 合併與完成

```bash
# 合併進 develop（由負責人或 maintainer 執行）
git checkout develop
git merge --no-ff feature/PROJ-123-user-registration
git push origin develop

# 清理分支
git branch -d feature/PROJ-123-user-registration
git push origin --delete feature/PROJ-123-user-registration
```

---

## Bug Fix 流程

### 1. 問題分析

- 記錄問題重現步驟。
- 評估影響範圍。
- 建立 JIRA 任務或 GitHub Issue。

### 2. 修復流程

```bash
# 從 develop 建立修復分支
git checkout develop
git pull origin develop

# JIRA 格式
git checkout -b fix/PROJ-456-login-error
# GitHub 格式
git checkout -b fix/GH-456-login-error

# 提交修改
# JIRA 格式
git commit -m "[PROJ-456] fix: 修復登入驗證邏輯"
# GitHub 格式
git commit -m "fix #456: 修復登入驗證邏輯"
```

### 3. 測試與驗證

- 執行單元測試。
- 執行整合測試。
- 確認問題已修復。
- 檢查是否有引入新問題。

### 4. 提交 PR 與合併

- 遵循與 Feature Development 相同的 PR 流程。
- 標記為 bug fix。
- 合併至 `develop`。

---

## Hot Fix 流程

### 1. 緊急問題評估

- 確認問題嚴重性。
- 評估是否需要立即修復。
- 通知相關人員。

### 2. 建立 Hot Fix 分支

```bash
# 從 main/master 建立 hotfix 分支
git checkout main
git pull origin main

# JIRA 格式
git checkout -b hotfix/PROJ-789-critical-error
# GitHub 格式
git checkout -b hotfix/GH-789-critical-error
```

### 3. 修復與測試

```bash
# JIRA 格式
git commit -m "[PROJ-789] fix: 修復重大錯誤"
# GitHub 格式
git commit -m "fix #789: 修復重大錯誤"
```

- 確保完整測試：
  - 單元測試
  - 整合測試
  - 手動測試關鍵功能

### 4. 緊急發布流程

```bash
# 合併至 main/master
git checkout main
git merge --no-ff hotfix/PROJ-789-critical-error
git tag -a v1.2.1 -m "Hotfix 1.2.1"
git push origin main --tags

# 同步到 develop
git checkout develop
git merge --no-ff hotfix/PROJ-789-critical-error
git push origin develop

# 清理分支
git branch -d hotfix/PROJ-789-critical-error
git push origin --delete hotfix/PROJ-789-critical-error
```

### 5. 後續處理

- 更新發布文件。
- 通知相關人員與用戶。
- 記錄事件供後續改進。

---

## 注意事項

### 通用規則

- 分支命名需清楚表達用途。
- Commit message 需具體說明修改內容。
- 重要修改必須經過 code review。
- 持續與 `develop` 分支同步。
- 定期清理已合併分支。

### 版本號規則

- 主版本號：重大更新
- 次版本號：功能更新
- 修訂號：bug 修復
- 熱修復：修訂號遞增

### 文件更新

- 更新 `README`
- 更新 API 文件
- 維護 Change Log
