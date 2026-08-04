#AI #軟體測試 #Testability #Python #知識卡

## 一句話

One behavior per test 指每個測試只鎖定一個可命名的行為；同一個行為的多個可觀察結果，可以在同一個測試中一起驗證。

## 內容

這個原則的重點不是限制 `assert` 數量，而是讓每個測試案例有清楚焦點。當測試失敗時，測試名稱和失敗訊息應該能快速指出是哪個規則、情境或行為不符合預期。

例如金卡會員有折扣、普通會員沒有折扣，通常應拆成兩個測試，因為它們描述的是不同情境。若放在同一個測試裡，失敗時還要再判斷到底是哪個規則壞掉。

但同一個測試可以有多個 `assert`。只要這些 `assert` 都在回答同一個問題，它們就可以放在同一個測試裡。

例如建立使用者時，系統可能同時初始化 email、啟用狀態、角色和通知設定。這些檢查都在描述「建立使用者會套用預設設定」這個行為：

```python
from dataclasses import dataclass


@dataclass
class User:
    email: str
    is_active: bool = True
    role: str = "member"
    notification_enabled: bool = True


def create_user(email: str) -> User:
    return User(email=email)


def test_creates_user_with_default_settings():
    user = create_user(email="a@example.com")

    assert user.email == "a@example.com"
    assert user.is_active is True
    assert user.role == "member"
    assert user.notification_enabled is True
```

比較不好的情況，是把多個行為放進同一個測試：

```python
def test_user_flow():
    user = create_user(email="a@example.com")
    assert user.is_active is True

    deactivate_user(user)
    assert user.is_active is False

    send_welcome_email(user)
    assert email_was_sent(user.email)
```

這個測試同時測了：

- 建立使用者
- 停用使用者
- 寄送歡迎信

這些是不同的行為，應該拆成不同測試。

判斷方式是：如果某個 `assert` 失敗時，你會覺得「這是在測另一件事」，那就該拆。如果多個 `assert` 都是在回答同一個問題，就可以放在同一個 test 裡。

## 連結

- [[testable 的測試技巧]]
- [[測試名稱應寫出情境與預期結果]]
- [[TDD 測試應關注可觀察行為]]

## 來源

- 與 Codex 對話：2026-07-08
- 原始資料：與 Codex 對話〈testable 的 12 個測試技巧〉第 3 點，2026-06-26
