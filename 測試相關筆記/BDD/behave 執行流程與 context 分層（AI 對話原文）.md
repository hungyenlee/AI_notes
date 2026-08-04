#AI #BDD #behave #對話原文 #原始資料卡

## 摘要

這份原始資料用購物車範例說明 `behave` 如何讀取 `.feature`、配對 step definitions 並執行情境，也補充 `context` 在不同作用域中保存測試狀態的方式。

## 可沉澱的知識卡

- [[認識 BDD]]
- [[behave 依序配對並執行 Scenario 的每個步驟]]
- [[behave context 用分層作用域管理測試狀態]]
- [[Step Definitions 把 Gherkin 連接到產品程式]]

## 原始資料一：購物車專案與 behave 執行流程

好的，我用一個完整的小專案，從資料夾架構到 `behave` 實際執行時「一句一句怎麼跑」，完整走一遍。

## 完整資料夾架構

```
shopping_cart/
├── cart.py                       ← 被測試的實際程式（production code）
│
└── features/                     ← behave 預設會掃描的資料夾（名稱固定）
    ├── cart.feature              ← 情境規格（Gherkin，給人看）
    │
    ├── environment.py            ← 選填：定義 hook（每個情境前後要做的事）
    │
    └── steps/                    ← step 定義資料夾（名稱固定為 steps）
        └── cart_steps.py         ← 把 .feature 每一句對應到 Python 程式碼
```

關鍵在於 `behave` 有**固定的命名約定**：你在專案根目錄執行 `behave` 時，它會自動去找名為 `features/` 的資料夾，讀裡面所有 `.feature` 檔，並到 `features/steps/` 裡尋找對應的 step 函式。資料夾名稱錯了它就找不到。

## 各檔案內容

**`cart.py`**（被測的程式）

```python
class Cart:
    def __init__(self):
        self.items = []

    def add(self, name, price, qty):
        self.items.append((name, price, qty))

    def total(self):
        subtotal = sum(price * qty for _, price, qty in self.items)
        return subtotal * 0.9 if subtotal >= 100 else subtotal
```

**`features/cart.feature`**（情境規格）

```gherkin
Feature: 購物車結帳金額

  Scenario: 滿百自動打折
    Given 一個空的購物車
    When 我加入 1 件 "book"，單價 120
    Then 總金額應該是 108
```

**`features/steps/cart_steps.py`**（step 定義）

```python
from behave import given, when, then
from cart import Cart

@given("一個空的購物車")
def step_empty_cart(context):
    context.cart = Cart()

@when('我加入 {qty:d} 件 "{name}"，單價 {price:d}')
def step_add_item(context, qty, name, price):
    context.cart.add(name, price=price, qty=qty)

@then("總金額應該是 {expected:d}")
def step_check_total(context, expected):
    assert context.cart.total() == expected
```

**`features/environment.py`**（選填的 hook，先放著理解概念）

```python
def before_scenario(context, scenario):
    print(f"  >> 準備執行情境：{scenario.name}")

def after_scenario(context, scenario):
    print(f"  >> 情境結束：{scenario.name}")
```

## 執行時，behave 內部到底怎麼跑

當你在 `shopping_cart/` 目錄下輸入 `behave`，它的運作流程是這樣：

**第 1 步：掃描與載入**

behave 找到 `features/` 資料夾，讀取所有 `.feature` 檔，並載入 `features/steps/` 下所有 step 定義（記住每個 `@given/@when/@then` 對應的文字樣板），同時載入 `environment.py` 的 hook。

**第 2 步：逐情境執行**

對每一個 `Scenario`，behave 會：

1. 先呼叫 `before_scenario` hook（如果有定義）。
2. 建立一個全新的 `context` 物件——**這是關鍵**。`context` 是一個跨 step 共享的暫存空間，讓 Given 準備好的東西能傳給後面的 When、Then 使用。
3. 接著一句一句往下跑。

**第 3 步：每一句的「配對 → 執行」**

這是最核心的機制。behave 拿 `.feature` 裡的每一行文字，去比對 step 定義裡的樣板，找到符合的就執行那個函式：

```
.feature 的句子                          配對到的 step 函式
─────────────────────────────────────────────────────────
Given 一個空的購物車          ──比對──►   @given("一個空的購物車")
                                          → 執行 step_empty_cart
                                          → context.cart = Cart()

When 我加入 1 件 "book"，單價 120 ─比對─►  @when('我加入 {qty:d} 件 "{name}"，單價 {price:d}')
                                          → 解析出 qty=1, name="book", price=120
                                          → 執行 step_add_item
                                          → context.cart.add("book", 120, 1)

Then 總金額應該是 108         ──比對──►   @then("總金額應該是 {expected:d}")
                                          → 解析出 expected=108
                                          → 執行 step_check_total
                                          → assert context.cart.total() == 108
```

注意 `{qty:d}`、`{name}` 這種樣板：behave 會從句子裡**自動把對應位置的值抽出來**，當成參數傳進函式。`:d` 代表轉成整數。所以同一個 step 樣板能套用到不同數字、不同商品，不必每個情境都重寫。

**第 4 步：判定結果**

- 一個 step 函式如果跑完沒拋出例外 → 該 step 標記為 **passed**。
- 如果 `assert` 失敗或拋出例外 → 該 step 標記為 **failed**，且該情境**後續的 step 會直接跳過**（不再執行）。
- 全部 step 都通過，該情境才算 passed。
- 跑完該情境後呼叫 `after_scenario` hook。

## 執行後你會看到的輸出

成功時，終端機大致顯示：

```
Feature: 購物車結帳金額 # features/cart.feature:1

  Scenario: 滿百自動打折        # features/cart.feature:3
    Given 一個空的購物車        # features/steps/cart_steps.py:4
    When 我加入 1 件 "book"，單價 120  # features/steps/cart_steps.py:8
    Then 總金額應該是 108        # features/steps/cart_steps.py:12

1 feature passed, 0 failed, 0 skipped
1 scenario passed, 0 failed, 0 skipped
3 steps passed, 0 failed, 0 skipped, 0 undefined
```

它會把每一句連同**對應到的 step 程式碼位置**一起列出，綠色代表通過。

如果 `Then` 那句算錯了（例如實際算出 100 但你寫 108），則會看到那一句變紅，顯示 `Assertion Failed`，並標示出錯的檔案與行號，統計那行也會變成 `1 failed`。

## 用一張圖總結整個流程

```
你輸入 behave
      │
      ▼
掃描 features/ ──► 讀 cart.feature（情境）
      │           載入 steps/cart_steps.py（step 對應表）
      │           載入 environment.py（hook）
      ▼
對每個 Scenario：
      │
      ├─► before_scenario hook
      ├─► 建立全新的 context（跨 step 共享資料）
      │
      ├─► 讀「Given 一個空的購物車」
      │        └─ 比對樣板 → 執行 step_empty_cart → 存進 context.cart
      │
      ├─► 讀「When 我加入...」
      │        └─ 比對樣板 + 抽參數 → 執行 step_add_item → 改動 context.cart
      │
      ├─► 讀「Then 總金額應該是 108」
      │        └─ 比對樣板 + 抽參數 → 執行 step_check_total → assert 驗證
      │
      ├─► after_scenario hook
      ▼
彙整結果 ──► 印出 passed / failed 統計
```

## 幾個容易絆倒新手的重點

- **`context` 是串起整個情境的關鍵**：Given 把東西放進 `context`，When 拿出來改，Then 拿出來驗證。沒有它，三個獨立的 step 函式之間無法傳遞資料。
- **句子要跟 step 樣板對得上**：如果 `.feature` 寫了一句，但 `steps/` 裡沒有對應的樣板，behave 會回報該 step 為 **undefined**（未定義），並貼心地印出建議你補上的函式骨架。
- **資料夾名稱不能改**：`features/` 和 `features/steps/` 是約定俗成的固定名稱。
- **執行位置**：通常在專案根目錄（`features/` 的上一層）執行 `behave`，這樣 `from cart import Cart` 才找得到 `cart.py`。

簡單說，`behave` 的本質就是一台**「翻譯兼執行機」**：把 `.feature` 裡人看得懂的每一句話，逐句翻譯成 `steps/` 裡的 Python 函式並執行，再用 `context` 把這些函式串成一個有前後關係的完整情境，最後告訴你每一句是通過還是失敗。

## 原始資料二：context 分層與 Scenario 隔離

好問題，而且這正好可以把我前一則為了好懂而做的簡化講得更精準。

## 直接回答

嚴格說起來，**behave 從頭到尾只建立「一個」context 物件**，整個測試過程共用它。但它有一套**分層（layer）清理機制**，讓每個 Scenario 開始時，上一個 Scenario 留下的資料會被清掉——所以從你寫測試的角度看，**每個 Scenario 都像是拿到一塊乾淨的白板**。

我前一則說「建立一個全新的 context 物件」是為了直覺好懂的講法，更準確的說法是：**物件沒換，但屬於 Scenario 這層的東西會被重置**，效果上等同於全新的。

## 實際機制：同一個物件，但分層

behave 在執行時會像疊盤子一樣，push / pop 不同層級：

```
測試開始
│  建立唯一的 context 物件（root 層）
│
├─ 進入 Feature ──► push 一層「feature 層」
│   │
│   ├─ Scenario 1 ──► push 一層「scenario 層」
│   │      context.cart = Cart()   ← 寫在 scenario 層
│   │   結束 ──────► pop 掉 scenario 層 ← context.cart 在此消失
│   │
│   ├─ Scenario 2 ──► push 一層「全新的 scenario 層」
│   │      此時讀 context.cart 會發現「沒有這個屬性」
│   │      （上一個情境的 cart 已被清掉，不會殘留）
│   │   結束 ──────► pop 掉 scenario 層
│   │
│   結束 Feature ──► pop 掉 feature 層
```

重點是：**你在某個 Scenario 裡設定的 `context.cart`，只活在那個 Scenario 的「scenario 層」**。情境一結束，那一層被 pop 掉，屬性就跟著消失，所以絕對不會洩漏到下一個情境。這也是為什麼每個情境的 Given 都要重新 `context.cart = Cart()`——因為上一輪的早就清乾淨了。

## 為什麼這個設計很重要

這帶來一個很關鍵的好處：**情境之間彼此隔離（test isolation）**。每個 Scenario 都從乾淨狀態開始，不會因為「剛好前一個情境跑過、留了某些資料」而影響結果。測試的順序變了、單獨跑某一個情境，結果都一樣，不會有隱藏的依賴。

## 那「想刻意跨情境共用」可以嗎？

可以——你只要把資料設在**更高的層級**，它就不會被 scenario 層的 pop 清掉。常見做法：

```python
# environment.py

def before_all(context):
    # 設在最外層（root），整個測試過程都活著
    context.db_connection = connect_to_test_db()

def before_feature(context, feature):
    # 設在 feature 層，這個 Feature 底下所有 Scenario 共用
    context.shared_config = load_config()
```

設在 `before_all` 的東西活整場，設在 `before_feature` 的活整個 feature，設在 step 裡（scenario 層）的只活該情境。**層級越高活越久**，你想讓資料活多久，就設在對應的層。

## 整理

| 你設定資料的位置 | 存活範圍 | 何時被清掉 |
|---|---|---|
| step 函式裡（如 `context.cart`） | 只在當前 Scenario | 該 Scenario 結束時 |
| `before_feature` hook | 整個 Feature 內所有 Scenario | 該 Feature 結束時 |
| `before_all` hook | 整個測試過程 | 全部跑完才結束 |

**一句話總結**：context 物件本身全程只有一個、被沿用下去；但「Scenario 層級的資料」每個情境都會重置，所以實務上你可以放心把每個 Scenario 當成從乾淨白板開始。如果某些東西（像資料庫連線）你想共用、不想每個情境重建，就把它設在 `before_feature` 或 `before_all` 這種更高的層級。

## 整理筆記

- [[behave 依序配對並執行 Scenario 的每個步驟]]
- [[behave context 用分層作用域管理測試狀態]]

## 來源

- 與 Codex 對話：2026-06-29

