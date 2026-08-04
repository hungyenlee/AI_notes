#AI #BDD #Gherkin #知識卡

## 一句話

Given–When–Then 依序描述已知前提、發生的行為，以及外部可觀察的預期結果。

## 內容

`Given` 把系統準備到明確狀態，例如使用者是會員且購物車金額為 1000 元；`When` 描述這次真正要觀察的事件，例如使用者結帳；`Then` 則驗證應付金額為 900 元。連續的同類步驟可以用 `And` 或 `But` 增加可讀性。一個情境通常只保留一個主要行為，避免同時測試太多事情。

這個結構和 Arrange–Act–Assert 相對應，但用途不同：Given–When–Then 用領域語言表達產品行為，AAA 則常用來組織測試程式碼。Then 應驗證使用者或外部系統看得到的結果，不應綁定私有方法或內部資料結構。

## 範例

```gherkin
Given 小明是會員
And 購物車金額為 1000 元
When 小明進行結帳
Then 應付金額應為 900 元
```

對照 Arrange–Act–Assert：

```python
# Arrange
amount = 1000
is_member = True

# Act
result = calculate_price(amount, is_member)

# Assert
assert result == 900
```

## 連結

- [[認識 BDD]]
- [[feature 檔是 BDD 的可執行規格]]
- [[好的 BDD 情境描述意圖而不是操作細節]]

## 來源

- [Gherkin Reference](https://cucumber.io/docs/gherkin/reference/)
