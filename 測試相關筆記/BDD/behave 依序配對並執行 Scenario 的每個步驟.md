#AI #BDD #behave #測試自動化 #知識卡

## 一句話

behave 會先載入 feature、Step Definitions 與 hooks，再逐一將 Scenario 中的 Gherkin 步驟配對到 Python 函式並執行。

## 內容

未指定路徑時，behave 預設從目前目錄下的 `features/` 尋找 `.feature`，並載入對應 feature base directory 裡 `steps/` 的 Python 模組及選用的 `environment.py`。`features/` 是預設名稱而非絕對限制；也能在命令列或設定檔指定其他 feature 路徑。

執行 Scenario 時，behave 先進入 scenario 作用域並呼叫 `before_scenario`，再依序處理 Given、When、Then。每句文字會與 `@given`、`@when`、`@then` 登錄的 expression 配對；例如 `{qty:d}` 會擷取文字並轉成整數後傳給 step function。函式正常結束就通過，拋出例外或 assertion 失敗就失敗，剩餘步驟通常標為 skipped；`after_scenario` 仍負責收尾，之後 scenario 作用域才被移除。

```text
載入 feature、steps、environment.py
→ 進入 Scenario 作用域
→ before_scenario
→ 配對並執行 Given／When／Then
→ after_scenario
→ 移除 Scenario 作用域
→ 彙整結果
```

hook 中的 `print()` 雖會執行，但 stdout 預設可能被 capture；要即時顯示可使用 `behave --no-capture`。

## 連結

- [[認識 BDD]]
- [[Step Definitions 把 Gherkin 連接到產品程式]]
- [[behave context 用分層作用域管理測試狀態]]
- [[BDD 專案應分離規格轉接層與產品程式]]

## 來源

- [[behave 執行流程與 context 分層（AI 對話原文）]]
- [behave Tutorial](https://behave.readthedocs.io/en/stable/tutorial/)
- [behave API Reference](https://behave.readthedocs.io/en/stable/api/)

