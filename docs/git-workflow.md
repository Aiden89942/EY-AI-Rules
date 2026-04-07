# Git 命名與 Commit 規範

本文件僅保留兩件事：分支命名與 commit 規範。  
完整流程步驟請參考 `docs/workflow-guide.md`。

## 分支命名規範

- 功能分支：
  - `feature/PROJ-<數字>-<描述>`
  - `feature/GH-<數字>-<描述>`
- 修復分支：
  - `fix/PROJ-<數字>-<描述>`
  - `fix/GH-<數字>-<描述>`
- 熱修復分支：
  - `hotfix/PROJ-<數字>-<描述>`
  - `hotfix/GH-<數字>-<描述>`

範例：

```text
feature/PROJ-123-user-registration
feature/GH-123-user-registration
fix/PROJ-456-login-error
fix/GH-456-login-timeout
hotfix/PROJ-789-critical-error
```

## Commit 訊息規範

格式僅允許以下二選一：

```text
<type> #<ticket>: <summary>
[PROJ-123] <type>: <summary>
```

`type` 僅允許：

- `feat`
- `fix`

範例：

```text
feat #123: 新增商品搜尋篩選
fix #456: 修正重複送單問題
[PROJ-789] fix: 更新回滾流程文件
```
