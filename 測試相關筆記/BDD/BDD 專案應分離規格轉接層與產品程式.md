標籤：#AI #BDD #專案結構

## 一句話

BDD 專案應把 `.feature` 規格、Step Definitions 轉接層與真正產品程式分開管理。

## 內容

BDD 沒有跨框架統一的資料夾格式，但責任分離是一個實用原則。以 Python behave 為例，`features/*.feature` 保存行為規格，`features/steps/*.py` 保存步驟實作，`features/environment.py` 處理測試生命週期 hooks，產品程式仍放在 `src/`，細部單元測試則可放在 `tests/unit/`。

`environment.py` 可在所有測試、Feature、Scenario 或 Step 前後建立與清理瀏覽器、資料庫、API client 等資源。fixtures 和共用測試資料可再放入支援模組。這種結構讓 `.feature` 保持業務可讀性，steps 專注翻譯，而產品邏輯不被埋進測試框架。

## 範例

```text
shopping-project/
├─ src/ 真正的產品程式
│  └─ pricing/
│     └─ discount.py
├─ features/
│  ├─ membership_discount.feature
│  ├─ steps/
│  │  ├─ membership_steps.py
│  │  ├─ checkout_steps.py
│  │  └─ discount_steps.py
│  ├─ environment.py
│  └─ support/
│     └─ fixtures.py
└─ tests/
   └─ unit/
      └─ test_discount.py
```

這裡以領域概念拆分 step files；`discount.py` 是產品實作，`test_discount.py` 則可用 TDD 驗證細部計算。

## 連結

- [[認識 BDD]]
- [[Step Definitions 把 Gherkin 連接到產品程式]]
- [[behave 依序配對並執行 Scenario 的每個步驟]]
- [[behave context 用分層作用域管理測試狀態]]
- [[BDD 和 TDD 分別關注產品行為與程式設計]]

## 來源

- [behave Tutorial](https://behave.readthedocs.io/en/stable/tutorial/)
