標籤：#AI #BDD #測試自動化

## 一句話

Step Definitions 是把 `.feature` 中的自然語言步驟匹配到可執行程式碼的轉接層。

## 內容

Cucumber 或 behave 執行 Scenario 時，會依步驟文字或 expression 找到對應函式，取出其中的參數，再執行準備、操作或斷言。例如「購物車金額為 1000 元」可以由一個帶整數參數的 step definition 接收；「進行結帳」則呼叫真正的 application service；最後由 Then 比較實際與預期金額。

Step Definitions 應保持薄而清楚，只負責翻譯領域語言、準備測試狀態與呼叫系統。折扣計算等商業規則仍應留在產品程式，否則測試會形成另一套實作。步驟檔也宜依會員、購物車、結帳等 domain concept 分組，而不是與單一 Feature 緊密綁定。

## 範例

`.feature` 中的參數步驟：

```gherkin
Given 購物車金額為 1000 元
When 小明進行結帳
Then 應付金額應為 900 元
```

可連接到 Python behave 的 Step Definitions：

```python
@given("購物車金額為 {amount:d} 元")
def step_cart_amount(context, amount):
    context.amount = amount

@when("小明進行結帳")
def step_checkout(context):
    context.result = calculate_price(
        context.amount,
        context.is_member,
    )

@then("應付金額應為 {expected:d} 元")
def step_verify_price(context, expected):
    assert context.result == expected
```

`calculate_price()` 屬於產品程式；step functions 只保存情境狀態、呼叫功能並驗證結果。

## 連結

- [[認識 BDD]]
- [[feature 檔是 BDD 的可執行規格]]
- [[BDD 專案應分離規格轉接層與產品程式]]
- [[behave 依序配對並執行 Scenario 的每個步驟]]
- [[behave context 用分層作用域管理測試狀態]]

## 來源

- [Cucumber Step Definitions](https://cucumber.io/docs/cucumber/step-definitions/)
- [Cucumber Step Organization](https://cucumber.io/docs/gherkin/step-organization/)
