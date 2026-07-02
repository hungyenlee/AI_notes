標籤：#AI #BDD #behave #context

## 一句話

behave 沿用同一個 `Context` 實例，藉由 test run、feature 與 scenario 等作用域層控制資料的可見範圍與清理時機。

## 內容

behave 不會替每個 Scenario 建立全新的 `Context` 物件；進入新層級時，它會在既有物件上 push 新的 namespace layer，離開時再 pop。寫在 step、`before_step` 或 `before_scenario` 的使用者屬性屬於 scenario scope，因此 `context.cart = Cart()` 可供同一 Scenario 的後續步驟共用，情境結束後則會隨該層移除。`before_feature` 設定的屬性活到 Feature 結束，`before_all` 設定的屬性則活到整次 test run 結束。

這種機制隔離的是 `context` 上的 scenario 層屬性，不等於自動還原所有測試狀態。若 Scenario 修改了 root／feature 層持有的可變物件、共用資料庫或其他外部系統，變更仍可能影響下一個 Scenario；必須用 hooks、fixtures 或 transaction rollback 主動清理。因此「每個 Scenario 像乾淨白板」只適用於 scenario-scoped 屬性，不能取代完整的 test isolation 設計。

| 設定位置 | 作用域 | 移除時機 |
|---|---|---|
| step、`before_step`、`before_scenario` | Scenario | Scenario 結束後 |
| `before_feature` | Feature | Feature 結束後 |
| `before_all` | Test run | 全部測試結束後 |

## 連結

- [[認識 BDD]]
- [[behave 依序配對並執行 Scenario 的每個步驟]]
- [[Step Definitions 把 Gherkin 連接到產品程式]]
- [[BDD 專案應分離規格轉接層與產品程式]]

## 來源

- [[behave 執行流程與 context 分層（AI 對話原文）]]
- [behave Context Attributes](https://behave.readthedocs.io/en/stable/appendix.context_attributes/)
- [behave Tutorial：Context](https://behave.readthedocs.io/en/stable/tutorial/#context)

