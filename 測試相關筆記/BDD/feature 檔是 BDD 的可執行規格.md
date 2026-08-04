#AI #BDD #Gherkin #知識卡

## 一句話

`.feature` 是以 Gherkin 撰寫的純文字行為規格，可以同時供團隊閱讀並作為自動化測試入口。

## 內容

一個 `.feature` 檔只能包含一個 `Feature`，用來描述一項產品能力；其下可以用 `Rule` 分組商業規則，再用多個 `Scenario` 提供具體案例。`Background` 適合放每個情境都需要的簡短共同前提，Tags 則可分類案例或控制執行範圍。`#` 可以加入註解，Data Table 與 Doc String 可傳遞表格或多行資料。

檔案的主要價值不是把測試程式翻譯成自然語言，而是保存團隊對行為的共同理解。Feature 名稱、Rule 和 Scenario 應使用領域語言，讓它能持續充當需求文件、驗收條件與回歸規格。

## 範例

```gherkin
@discount
Feature: 會員滿額折扣
  為了鼓勵會員消費
  會員購物滿 1000 元時應享有九折優惠

  Background:
    Given 商品價格皆以新台幣計算

  Rule: 只有會員可以獲得滿額折扣

    Scenario: 非會員購物滿 1000 元
      Given 小明不是會員
      And 購物車金額為 1000 元
      When 小明進行結帳
      Then 應付金額應為 1000 元
```

這裡的 `Feature` 表示產品能力、`Rule` 表示商業規則，`Scenario` 則用一個反例證明規則的邊界。

## 連結

- [[認識 BDD]]
- [[Given When Then 描述前提行為與結果]]
- [[Scenario Outline 用資料表驗證多組案例]]

## 來源

- [Gherkin Reference](https://cucumber.io/docs/gherkin/reference/)
