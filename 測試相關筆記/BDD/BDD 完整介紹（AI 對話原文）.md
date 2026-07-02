標籤：#AI #BDD #對話原文

## 原始資料

BDD（Behavior-Driven Development，行為驅動開發）是一種以「具體行為範例」協助產品、測試與開發共同釐清需求的開發方法。`.feature` 是其中常見的可執行規格檔，但 **BDD 不等於寫 `.feature` 測試**。

## 1. BDD 的核心流程

BDD 通常包含三個環節：

1. **Discovery**：一起討論需求、規則、例外與邊界。
2. **Formulation**：把案例寫成清楚的 Given–When–Then。
3. **Automation**：將案例連接到自動化測試程式。

```text
討論商業需求
→ 找出規則與具體案例
→ 寫成 .feature
→ 實作 Step Definitions
→ 呼叫系統程式
→ 驗證行為
```

Cucumber 官方也特別強調 BDD 的重點是 discovery、collaboration 和 examples，而不只是測試工具。[Cucumber Introduction](https://cucumber.io/docs/)

## 2. `.feature` 檔是什麼？

`.feature` 是使用 Gherkin 語法撰寫的純文字檔案。它同時扮演：

- 需求規格
- 驗收條件
- 行為範例
- 自動化測試入口
- 團隊共同文件

一個 `.feature` 檔只能有一個 `Feature`，但可以包含多個規則與情境。[Gherkin Reference](https://cucumber.io/docs/gherkin/reference/)

完整範例：

```gherkin
@discount
Feature: 會員滿額折扣
  為了鼓勵會員消費
  會員購物滿 1000 元時應享有九折優惠

  Background:
    Given 商品價格皆以新台幣計算

  Rule: 只有會員可以獲得滿額折扣

    Scenario: 會員購物剛好滿 1000 元
      Given 小明是會員
      And 購物車金額為 1000 元
      When 小明進行結帳
      Then 應付金額應為 900 元

    Scenario: 非會員購物滿 1000 元
      Given 小明不是會員
      And 購物車金額為 1000 元
      When 小明進行結帳
      Then 應付金額應為 1000 元

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

## 3. Gherkin 關鍵字

### Feature

描述一項完整功能及其商業目的：

```gherkin
Feature: 會員滿額折扣
```

一個 `.feature` 檔通常聚焦一項可理解的產品能力，而不是一個程式類別。

### Rule

描述 Feature 內的一條商業規則：

```gherkin
Rule: 只有會員可以獲得滿額折扣
```

同一功能有多條規則時，可以用 `Rule` 將相關 Scenario 分組。

### Scenario

用具體案例說明規則：

```gherkin
Scenario: 會員購物剛好滿 1000 元
```

Scenario 也是實際執行的測試案例。

### Given

準備測試開始前的情境：

```gherkin
Given 小明是會員
And 購物車金額為 1000 元
```

對應 AAA 的 `Arrange`。

### When

描述主要行為或事件：

```gherkin
When 小明進行結帳
```

對應 AAA 的 `Act`。一個 Scenario 通常只保留一個主要 When，讓測試焦點明確。

### Then

描述外部可觀察的結果：

```gherkin
Then 應付金額應為 900 元
```

對應 AAA 的 `Assert`。官方建議驗證使用者或外部系統可觀察的結果，避免綁定內部方法或資料庫細節。

### Background

放置每個 Scenario 都需要的共同前提：

```gherkin
Background:
  Given 商品價格皆以新台幣計算
```

它會在每個 Scenario 前執行。Background 應保持簡短；如果內容太多，讀者會很難記住目前情境。

### Scenario Outline 與 Examples

用相同流程測試多組資料：

```gherkin
Scenario Outline: 會員結帳
  Given 購物車金額為 <amount> 元
  When 會員結帳
  Then 應付金額應為 <expected> 元

  Examples:
    | amount | expected |
    |  999   |   999    |
    | 1000   |   900    |
```

每一列 Examples 都會產生一次獨立執行。

### Tags

用來分類或選擇執行範圍：

```gherkin
@discount @critical
Scenario: 會員滿額折扣
```

例如只執行 `@critical` 情境。Tags 可以放在 Feature、Rule、Scenario、Scenario Outline 或 Examples 上，但不能直接放在 Given／When／Then 上。[Cucumber API](https://cucumber.io/docs/cucumber/api/)

## 4. BDD 專案資料夾架構

BDD 沒有跨框架完全統一的資料夾結構。以下使用 Python `behave` 示範一個實用架構：

```text
shopping-project/
├─ src/
│  └─ pricing/
│     ├─ __init__.py
│     └─ discount.py
│
├─ features/
│  ├─ membership_discount.feature
│  ├─ coupon.feature
│  │
│  ├─ steps/
│  │  ├─ membership_steps.py
│  │  ├─ checkout_steps.py
│  │  └─ discount_steps.py
│  │
│  ├─ environment.py
│  │
│  └─ support/
│     ├─ fixtures.py
│     └─ test_data.py
│
├─ tests/
│  └─ unit/
│     └─ test_discount.py
│
└─ behave.ini
```

各部分的責任：

| 路徑 | 用途 |
|---|---|
| `src/` | 真正的產品程式 |
| `features/*.feature` | 使用者行為與驗收案例 |
| `features/steps/` | 將 Gherkin 句子連接到程式碼 |
| `environment.py` | 測試前後的 hooks、環境初始化與清理 |
| `support/` | fixtures、測試資料等輔助程式 |
| `tests/unit/` | 使用 TDD 或單元測試驗證細部邏輯 |
| `behave.ini` | behave 執行設定 |

`behave` 最小結構只需要 `.feature` 與 `steps/`；`environment.py` 是選用的 hooks 檔案。[behave Tutorial](https://behave.readthedocs.io/en/stable/tutorial/)

## 5. Step Definitions 是什麼？

`.feature` 只有規格描述，不能直接呼叫產品程式。Step Definitions 負責把每句 Gherkin 連接到可執行程式。

例如：

```gherkin
Given 小明是會員
And 購物車金額為 1000 元
When 小明進行結帳
Then 應付金額應為 900 元
```

對應的 Python step definitions：

```python
# features/steps/discount_steps.py

from behave import given, when, then
from src.pricing.discount import calculate_price


@given("小明是會員")
def step_member(context):
    context.is_member = True


@given("小明不是會員")
def step_non_member(context):
    context.is_member = False


@given("購物車金額為 {amount:d} 元")
def step_cart_amount(context, amount):
    context.amount = amount


@when("小明進行結帳")
def step_checkout(context):
    context.result = calculate_price(
        amount=context.amount,
        is_member=context.is_member,
    )


@then("應付金額應為 {expected:d} 元")
def step_verify_price(context, expected):
    assert context.result == expected
```

Step Definition 的文字或 expression 會匹配 `.feature` 中的步驟；參數則會被取出並傳入函式。[Cucumber Step Definitions](https://cucumber.io/docs/cucumber/step-definitions/)

真正的產品程式仍放在 `src/`：

```python
# src/pricing/discount.py

def calculate_price(amount, is_member):
    if is_member and amount >= 1000:
        return int(amount * 0.9)

    return amount
```

關係如下：

```text
membership_discount.feature
        ↓ 文字匹配
discount_steps.py
        ↓ 呼叫
discount.py
        ↓ 回傳結果
Step Definition 執行 assertion
```

Step Definition 應該是薄薄的轉接層，不要把折扣規則直接寫在裡面，否則測試程式會變成另一套產品程式。

## 6. `environment.py` 的用途

`environment.py` 可以定義測試生命週期 hooks：

```python
# features/environment.py

def before_all(context):
    print("開始執行所有 BDD 測試")


def before_scenario(context, scenario):
    context.test_database = create_test_database()


def after_scenario(context, scenario):
    context.test_database.close()


def after_all(context):
    print("所有 BDD 測試完成")
```

常見 hooks 包含：

- `before_all`／`after_all`
- `before_feature`／`after_feature`
- `before_scenario`／`after_scenario`
- `before_step`／`after_step`
- `before_tag`／`after_tag`

它們適合處理瀏覽器、測試資料庫、API client 或測試資料的建立與清理。

## 7. Step Definitions 如何分類？

不建議機械式地替每個 `.feature` 建立一個完全綁定的 step 檔案：

```text
membership_discount.feature
membership_discount_steps.py
```

小型專案可以這樣開始，但大型專案比較適合依「領域概念」分類：

```text
features/steps/
├─ membership_steps.py
├─ cart_steps.py
├─ checkout_steps.py
└─ payment_steps.py
```

如此 `Given 小明是會員` 可以被不同功能重用，也不會產生大量意思相同、文字稍有不同的 steps。Cucumber 官方同樣建議依主要 domain concept 組織，而不是讓 step definitions 與單一 Feature 緊密耦合。[Step Organization](https://cucumber.io/docs/gherkin/step-organization/)

## 8. BDD 和 TDD 如何搭配？

兩者可以共同使用：

```text
BDD
定義「會員滿 1000 元結帳時應付 900 元」
        ↓
TDD
開發 calculate_price() 的計算規則
        ↓
BDD
驗證完整會員結帳行為
```

分工可以理解為：

- **BDD**：我們是否實作了正確的產品行為？
- **TDD**：程式內部是否透過小步驟形成正確、可維護的設計？

BDD 不一定是 UI 或端到端測試。`.feature` 背後可以呼叫 API、application service，甚至純函式；測試層級取決於 Step Definition 如何連接系統。

## 9. 常見錯誤

### 寫成操作說明書

不理想：

```gherkin
When 我點擊右上角的登入按鈕
And 我在第一個輸入框輸入帳號
And 我在第二個輸入框輸入密碼
And 我點擊藍色送出按鈕
```

較好：

```gherkin
When 小明使用正確帳號密碼登入
```

BDD 應描述意圖與行為，不應過度綁定目前的 UI。

### Then 驗證內部實作

不理想：

```gherkin
Then calculate_discount 函式應被呼叫一次
```

較好：

```gherkin
Then 應付金額應為 900 元
```

### Scenario 太長

一個 Scenario 如果包含十幾個操作，通常代表同時測試太多行為。Cucumber 建議案例保持精簡，常見約 3–5 個 steps。

### 把所有準備工作塞進 Background

Background 太長會隱藏重要前提。只有每個 Scenario 都需要、而且讀者必須知道的情境才適合放進去。

### 只有開發者在寫 Feature

如果 `.feature` 只是開發者把既有測試翻成 Given–When–Then，而產品與測試沒有共同討論，它仍可執行，卻失去了 BDD 最重要的協作價值。

一句話總結：

> BDD 用具體案例建立共同理解；`.feature` 描述行為，Step Definitions 將描述接到產品程式，而資料夾架構則把規格、轉接層與真正實作分開。

## 來源

- 與 Codex 對話：2026-06-29
