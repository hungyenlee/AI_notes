標籤：#AI #BDD #測試設計

## 一句話

好的 BDD Scenario 描述角色想完成的行為與可觀察結果，不把規格寫成 UI 操作腳本或內部實作檢查。

## 內容

「當小明使用正確帳號密碼登入」通常比「點擊右上按鈕、在第一個輸入框輸入帳號、再按藍色按鈕」更適合作為 BDD 步驟。前者保存登入意圖，即使 UI 改版仍成立；後者綁定畫面細節，不但冗長，也會讓規格因非商業變更而頻繁破裂。

Then 同樣應驗證「使用者看到登入成功」之類的外部結果，而不是某個私有函式被呼叫一次。Scenario 應短而聚焦，Background 只放所有情境共享且讀者需要知道的前提。當規格開始像操作手冊、同義 steps 不斷增加或 step definitions 充滿商業邏輯時，就應重新整理領域語言與責任邊界。

## 範例

過度綁定 UI 的寫法：

```gherkin
When 我點擊右上角的登入按鈕
And 我在第一個輸入框輸入帳號
And 我在第二個輸入框輸入密碼
And 我點擊藍色送出按鈕
```

改成描述使用者意圖：

```gherkin
When 小明使用正確帳號密碼登入
Then 小明應進入會員首頁
```

後者即使按鈕位置或顏色改變仍然成立，也清楚說明登入成功對使用者代表什麼。

## 連結

- [[認識 BDD]]
- [[Given When Then 描述前提行為與結果]]
- [[Step Definitions 把 Gherkin 連接到產品程式]]

## 來源

- [Writing better Gherkin](https://cucumber.io/docs/bdd/better-gherkin/)
- [Gherkin Reference](https://cucumber.io/docs/gherkin/reference/)
