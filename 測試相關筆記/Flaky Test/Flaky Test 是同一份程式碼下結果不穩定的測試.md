#AI #軟體測試 #FlakyTest #知識卡

## 一句話

Flaky Test 是在程式碼與測試條件看起來沒有改變時，仍可能時而通過、時而失敗的測試。

## 內容

一般測試失敗應該代表行為真的壞了；Flaky Test 的問題是失敗訊號不穩定。它可能這次 CI 失敗、下一次重跑又通過，讓人很難判斷是產品 bug、測試 bug，還是環境暫時異常。

因此 Flaky Test 的核心不是「偶爾失敗」而已，而是測試結果失去可重現性。當測試不能穩定重現同一個結果，測試就不再是可靠的回饋機制，修復與除錯成本也會被放大。

## 連結

- [[認識 Flaky Test]]
- [[測試彼此獨立才能穩定執行]]
- [[測試要控制時間亂數與環境]]

## 來源

- [pytest：Flaky tests](https://docs.pytest.org/en/stable/explanation/flaky.html)
