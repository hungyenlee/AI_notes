標籤：#AI #軟體測試 #FlakyTest

## 一句話

Retry 可以暫時降低 CI 阻塞，但真正處理 Flaky Test 應回到根因：讓測試可重現、可隔離、可等待正確條件。

## 內容

重跑測試有時是必要的短期緩解，特別是在 CI 被少數不穩定測試卡住時。但如果只把 retry 當成解法，失敗訊號會被隱藏，團隊也會失去修復 Flaky Test 的壓力。

較好的處理方式是先分類失敗來源：是否依賴測試順序、共享狀態、時間亂數、外部服務、並行資源或非同步等待。接著讓測試自己準備資料、清理狀態、固定 clock 或 random seed、用 test double 隔離外部依賴，並用明確條件等待取代固定 sleep。

## 連結

- [[認識 Flaky Test]]
- [[測試彼此獨立才能穩定執行]]
- [[測試要控制時間亂數與環境]]
- [[用 test double 隔離外部依賴]]

## 來源

- [pytest：Flaky tests](https://docs.pytest.org/en/stable/explanation/flaky.html)
