標籤：#AI #BDD #Gherkin

## 一句話

Scenario Outline 讓同一個行為範本搭配 Examples 資料表，產生多個獨立案例。

## 內容

當多個 Scenario 只有輸入與預期結果不同時，可以把變動值改寫成 `<amount>`、`<expected>` 等參數，並在 `Examples` 表格列出資料。執行器會把每一列代入範本，各自執行一次。會員折扣就能用 999、1000、1500 等金額呈現門檻前、門檻值與門檻後的結果，而不必複製整段情境。

Scenario Outline 適合表達同一條規則的資料變化，不適合把本質不同的商業情境硬塞進同一張表。如果每列需要不同的步驟或原因，拆成有意義名稱的 Scenario 通常更容易理解失敗原因。

## 範例

```gherkin
Scenario Outline: 會員在不同消費金額下結帳
  Given 小明是會員
  And 購物車金額為 <amount> 元
  When 小明進行結帳
  Then 應付金額應為 <expected> 元

  Examples:
    | amount | expected |
    |  999   |   999    |
    | 1000   |   900    |
    | 1500   |  1350    |
```

這會產生三次獨立執行，分別覆蓋折扣門檻前、剛好到達門檻及超過門檻的案例。

## 連結

- [[認識 BDD]]
- [[feature 檔是 BDD 的可執行規格]]
- [[Given When Then 描述前提行為與結果]]

## 來源

- [Gherkin Reference](https://cucumber.io/docs/gherkin/reference/)
