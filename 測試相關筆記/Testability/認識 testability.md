標籤：#AI #軟體測試 #Testability #程式設計

## 一句話

Testable 指程式碼容易被測試，而不是已經有測試；核心在於輸入與環境可控制、結果與副作用可觀察、外部依賴可替換。

## 內容

在軟體測試裡，**testable** 指的是：

> 一段程式碼是否「容易被測試」。

它不是指「已經有測試」，而是指程式的設計，能不能讓你方便地控制輸入、觀察輸出，並隔離外部依賴。

> 補充：更精確地說，testability 也包含測試是否能快速、穩定、可重現地執行，以及失敗時是否容易定位原因。

## 一段程式碼是否 testable，可以看三件事

### 1. 輸入能不能控制

例如函式直接接收參數，就很好測：

```python
def calculate_total(price, quantity):
    return price * quantity
```

測試時可以直接給不同輸入：

```python
def test_calculate_total():
    assert calculate_total(100, 2) == 200
```

但如果函式自己去讀鍵盤、讀環境變數或取得目前時間，就比較難控制。

> 補充：這不代表程式不能使用時間、亂數或環境變數，而是應讓測試能注入 clock、固定 random seed，或以參數替換環境設定，使執行條件可控制、結果可重現。

---

### 2. 結果能不能觀察

有明確回傳值通常比直接印出結果更容易測試。

較好測：

```python
def greet(name):
    return f"Hello, {name}"
```

較難測：

```python
def greet(name):
    print(f"Hello, {name}")
```

因為 `return` 可以直接用 `assert` 驗證；`print` 則需要額外攔截標準輸出。

> 補充：`print` 並非不能測，例如 pytest 可以使用 `capsys` 攔截標準輸出，只是測試成本通常比直接驗證回傳值高。如果輸出文字本來就是程式的公開行為，攔截並驗證輸出仍是合理的測試方式。

---

### 3. 外部依賴能不能替換

例如寄信、資料庫、API、檔案系統，都屬於外部依賴。

較難測的寫法：

```python
class UserService:
    def register(self, email):
        user = save_to_database(email)
        send_email(email)
        return user
```

這個測試一執行，可能真的會：

* 寫入資料庫
* 寄出 Email
* 依賴網路
* 因外部服務失敗而測試失敗

較容易測的寫法，是把依賴從外面傳進來：

```python
class UserService:
    def __init__(self, repository, email_sender):
        self.repository = repository
        self.email_sender = email_sender

    def register(self, email):
        user = self.repository.save(email)
        self.email_sender.send(email)
        return user
```

測試時就可以換成假的物件：

```python
class FakeRepository:
    def save(self, email):
        return {"email": email}


class FakeEmailSender:
    def __init__(self):
        self.sent_to = []

    def send(self, email):
        self.sent_to.append(email)


def test_register_user():
    repository = FakeRepository()
    email_sender = FakeEmailSender()

    service = UserService(repository, email_sender)
    user = service.register("test@example.com")

    assert user == {"email": "test@example.com"}
    assert email_sender.sent_to == ["test@example.com"]
```

> 補充：範例中的 `FakeRepository` 與 `FakeEmailSender` 較精確的名稱是 fake 或 test double，不一定是 mock。Mock 通常還會驗證互動，例如某方法是否被呼叫，以及被呼叫幾次。

這就是為什麼 **依賴注入、依賴反轉** 常被認為能提升 testability。

> 補充：依賴不一定都要透過建構子注入，也可以透過函式參數或方法參數傳入。依賴注入是一種手段，不宜為了可測試性而過度增加抽象與設計複雜度。

> 補充：單元測試可以用 fake 隔離外部系統，但仍需要整合測試確認程式真的能與資料庫、Email 服務或 API 正確協作。可替換依賴不代表所有測試都應避開真實依賴。

> 補充：這個註冊範例還涉及「資料庫儲存成功，但寄信失敗」時的部分成功問題。這屬於交易一致性與錯誤處理，不是 testability 定義本身的錯誤，但正式設計時仍需處理。

## Testable 程式通常有這些特徵

* 職責單一，不會一個函式同時做十件事
* 輸入和輸出明確
* 外部依賴可以替換
* 不過度依賴全域變數
* 不會在物件內部偷偷建立資料庫、API Client
* 商業邏輯和 UI、資料庫、網路分開
* 執行結果穩定，不受目前時間或隨機數影響，或這些依賴可被控制

> 補充：「執行結果穩定」可理解成測試條件可控制、結果可重現；程式並非不能使用時間、亂數、非同步或並行機制。

## Testable 不等於一定要把所有方法拆得很小

重點不是「函式越小越好」，而是：

> 測試時，能否只驗證你真正想驗證的邏輯，而不被其他系統牽連。

例如你只是想測試「會員是否符合折扣資格」，卻必須啟動網站、登入、連接資料庫、呼叫付款 API，這段邏輯通常就不夠 testable。

可以把它簡單記成：

> **Testable = 輸入可控制、結果可觀察、依賴可替換。**

> 補充後的完整版本：**Testable = 輸入與環境可控制、結果與副作用可觀察、依賴可替換，而且測試能快速、穩定、可重現地執行。**

## 連結

- [[testable 的測試技巧]]
- [[認識 TDD]]
- [[TDD 測試應關注可觀察行為]]
- [[harness 是把測試流程包起來的執行環境]]

## 來源

- 與 Codex 對話：2026-06-24
