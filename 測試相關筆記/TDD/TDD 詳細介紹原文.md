#AI #TDD #測試 #原文 #原始資料卡

## 來源

- AI 對話原始整理

## 摘要

這份原始資料完整說明 TDD 的 Red-Green-Refactor 循環、用測試描述下一個行為、以最小實作通過測試，以及在測試安全網下重構設計。

## 可沉澱的知識卡

- [[認識 TDD]]
- [[Red Green Refactor 是 TDD 的基本循環]]
- [[TDD 用失敗測試引導下一小步需求]]
- [[TDD 的價值來自快速回饋和重構安全網]]
- [[TDD 測試應關注可觀察行為]]

## 原文

當然。TDD（Test-Driven Development，測試驅動開發）不只是「先寫測試」，而是一種透過測試逐步探索需求、設計介面與建立程式碼的開發節奏。

## 核心循環：Red → Green → Refactor

### 1. Red：先描述下一個行為

先寫一個小型測試，表達「系統接下來應該做到什麼」。

```python
def test_total_applies_discount():
    cart = Cart()
    cart.add(price=100)

    assert cart.total(discount=0.1) == 90
```

此時 `Cart` 可能還不存在。執行測試後，應確認它確實因為缺少這項功能而失敗。

這一步的價值在於：寫實作之前，先釐清使用方式和預期結果。

### 2. Green：用最小實作通過測試

接著只寫足以讓測試通過的程式碼：

```python
class Cart:
    def __init__(self):
        self.prices = []

    def add(self, price):
        self.prices.append(price)

    def total(self, discount=0):
        return sum(self.prices) * (1 - discount)
```

「最小實作」不是鼓勵寫糟糕的程式，而是避免提前設計尚未確認需要的抽象功能。

### 3. Refactor：在安全網下改善設計

測試通過後，再整理：

- 消除重複
- 改善命名
- 拆分過長函式
- 調整物件責任
- 簡化條件判斷

每次修改後重新執行測試。只要測試保持通過，就比較能確定行為沒有被意外改變。

---

## 一個更完整的開發過程

假設要建立密碼驗證功能，需求是：

- 密碼至少 8 個字元
- 必須包含數字

首先處理最簡單的案例：

```python
def test_rejects_password_shorter_than_8_characters():
    assert is_valid_password("abc123") is False
```

最小實作：

```python
def is_valid_password(password):
    return len(password) >= 8
```

接著加入新的失敗測試：

```python
def test_rejects_password_without_number():
    assert is_valid_password("abcdefgh") is False
```

更新實作：

```python
def is_valid_password(password):
    return (
        len(password) >= 8
        and any(char.isdigit() for char in password)
    )
```

最後加入成功案例：

```python
def test_accepts_password_with_8_characters_and_number():
    assert is_valid_password("abcdefg1") is True
```

這種「一次增加一個行為」的節奏，可以避免同時處理太多問題。

## TDD 的測試在測什麼？

TDD 通常優先測試可觀察的行為，而不是內部實作細節。

較好的測試：

```python
def test_withdraw_reduces_account_balance():
    account = Account(balance=100)

    account.withdraw(30)

    assert account.balance == 70
```

比較脆弱的測試：

```python
def test_withdraw_calls_internal_method():
    account._calculate_new_balance.assert_called_once()
```

第二種測試綁定了內部方法。即使重構後對外行為完全相同，測試仍可能失敗，降低重構自由。

## TDD、單元測試與測試先行的差異

- **單元測試**：測試一個小範圍的程式單元，不要求測試先寫。
- **測試先行**：先寫測試再寫功能，但不一定包含設計與重構循環。
- **TDD**：利用失敗測試引導下一步實作，通過後再重構，持續進行小循環。

因此，有測試不代表使用了 TDD。

## TDD 的優點

### 需求變得具體

「購物車要支援折扣」很模糊；測試則必須明確回答輸入、輸出、邊界與錯誤處理。

### 提供快速回饋

每完成一個小變更就驗證一次，比功能全部完成後才整合更容易定位問題。

### 建立回歸測試安全網

未來修改程式時，既有測試能檢查舊功能是否被破壞。

### 改善可測試性與模組化

難以測試的程式通常存在：

- 相依關係過多
- 全域狀態
- 職責混雜
- 輸入與輸出不清楚

測試先行會迫使開發者提早面對這些問題。

### 減少不必要的功能

只實作目前測試要求的行為，有助於避免過早抽象與過度設計。

## 限制與常見誤區

### TDD 不會自動保證正確

測試只證明程式符合已寫出的案例。漏掉需求或邊界條件，錯誤仍然可能存在。

### 不適合只測實作細節

如果大量 mock 私有方法、檢查呼叫次數或依賴內部結構，重構時測試會頻繁破裂。

### 無法取代其他測試

實際系統通常還需要：

- 整合測試
- API 測試
- 端到端測試
- 效能測試
- 安全測試
- 人工探索性測試

### 初期可能比較慢

不熟悉時，測試環境、測試案例選擇與重構會增加開發時間。不過對於需要長期維護的系統，這些成本通常能在修改與除錯階段回收。

### 並非所有工作都適合嚴格使用

視覺 UI、探索性原型、機器學習實驗等需求不確定或難以精確斷言的工作，可能比較適合先探索，再為穩定下來的核心邏輯補測試。

## 一個好的 TDD 測試通常具有的特徵

- 一次描述一項行為
- 名稱清楚表達情境與結果
- 執行快速
- 結果穩定
- 不依賴測試順序
- 盡量不依賴網路、時間或外部資料庫
- 關注公開行為而非內部結構
- 失敗時能指出具體問題

常見結構是 Arrange–Act–Assert：

```python
def test_withdraw_reduces_balance():
    # Arrange：準備
    account = Account(balance=100)

    # Act：執行
    account.withdraw(30)

    # Assert：驗證
    assert account.balance == 70
```

## 實務上的入門方式

不必一開始要求所有功能都嚴格採用 TDD。可以先從以下項目開始：

1. 純函式與商業規則
2. 曾經發生過的 bug
3. 輸入驗證
4. 金額與日期計算
5. 邊界條件較多的邏輯

修復 bug 時尤其適合：

1. 先寫一個能重現 bug 的失敗測試。
2. 修正程式，讓測試通過。
3. 整理實作並執行完整測試。
4. 保留測試，防止同一問題再次發生。

簡單來說，TDD 的精神是：

> 用下一個失敗測試定義一小步需求，用最小實作完成它，再透過重構改善設計。

它的真正價值不是測試數量，而是讓開發工作形成一連串可驗證、可調整的小步驟。

## 連結

- [[認識 TDD]]

## 來源

- 與 Codex 對話：2026-06-29
