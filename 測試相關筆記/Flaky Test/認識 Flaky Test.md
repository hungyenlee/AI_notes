#AI #軟體測試 #FlakyTest #索引卡

## 核心問題

Flaky Test 是什麼？為什麼它會讓自動化測試從品質防線變成不可靠的噪音？

## 相關卡片

- [[Flaky Test 是同一份程式碼下結果不穩定的測試]]
- [[Flaky Test 會消耗團隊對測試的信任]]
- [[Flaky Test 常來自不可控的外部條件]]
- [[處理 Flaky Test 應先找根因而不是只重跑]]
- [[測試彼此獨立才能穩定執行]]
- [[測試要控制時間亂數與環境]]
- [[用 test double 隔離外部依賴]]

## 初步理解

Flaky Test 是結果不穩定的測試：同一份程式碼與測試，在看似相同的條件下有時通過、有時失敗。它最危險的地方不是單次失敗，而是讓團隊開始不相信 CI 紅燈，進而忽略真正的回歸問題。處理 Flaky Test 的重點是讓測試變得可重現、可隔離、可診斷，而不是只靠 retry 把失敗藏起來。

## 來源

- [pytest：Flaky tests](https://docs.pytest.org/en/stable/explanation/flaky.html)
