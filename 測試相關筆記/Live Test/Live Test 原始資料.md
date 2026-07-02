標籤：#AI #軟體測試 #LiveTest #原始資料

## 來源

- 與 Codex 對話：2026-06-26
- `codex://threads/019f02fc-39bc-7b43-94ec-5449e717e96e`
- Session 標題：檢查 Live Test 筆記

## 整理範圍

本篇彙整該 session 中與 Live Test 有關的原始資訊，包括 Live Test 的定義、環境差異、風險、與 E2E Test 的關係，以及 A/B Test、Canary Release、Feature Flag、Beta 與灰度發布。純粹的檔案操作、Git 操作與重複敘述未重複收錄。

## 最初待確認的筆記

在軟體測試裡，**Live Test 通常是指在「實際運作中的環境」進行測試**，也就是系統已經上線、真實使用者可能正在使用的環境。

不過要注意，**Live Test 並不是像 Unit Test、Integration Test、E2E Test 那樣定義非常統一的正式分類**。不同公司可能有不同用法。

### 常見意思

#### 1. 在正式環境測試

例如網站已經部署到 production：

```text
使用者 → 正式網站 → 正式 API → 正式資料庫
```

測試人員實際操作：

- 能不能登入
- 能不能下訂單
- 付款流程是否正常
- Email 是否真的寄出
- 第三方服務是否正常連線

這類測試可能也會叫：

- Production Testing
- Testing in Production
- Live Environment Testing

#### 2. 對真實使用者進行測試

例如：

- A/B Test
- 灰度發布
- Canary Release
- Feature Flag
- Beta Test

假設要推出新版購物車，可以先只開放給 5% 使用者：

```text
95% 使用者 → 舊版購物車
5% 使用者  → 新版購物車
```

觀察：

- 錯誤率有沒有提高
- 使用者是否能正常結帳
- 新版轉換率是否比較好
- 系統效能是否受影響

這也可能被稱為 live testing。

### 和一般測試環境有什麼不同？

| 環境 | 使用的資料 | 使用者 | 風險 |
|---|---|---|---|
| Local | 測試資料 | 開發者 | 很低 |
| Test / QA | 測試資料 | 測試人員 | 低 |
| Staging | 接近正式資料 | 內部人員 | 中 |
| Live / Production | 真實資料 | 真實使用者 | 高 |

Live Test 最大的特點是：

> 測試失敗可能真的影響使用者或真實資料。

### Live Test 的例子

假設你做了一個會員註冊功能。

在測試環境中，你可能測：

```python
def test_register_user():
    response = register_user("test@example.com")
    assert response.status_code == 200
```

Live Test 則可能是：

1. 在正式網站建立一個測試帳號。
2. 確認帳號真的寫入正式資料庫。
3. 確認驗證信真的寄到信箱。
4. 點擊驗證連結。
5. 確認可以登入。
6. 測試完成後刪除測試資料。

### Live Test 的風險

在正式環境測試時，可能發生：

- 寫入錯誤資料
- 寄信給真實使用者
- 產生真實訂單
- 觸發真實付款
- 修改或刪除正式資料
- 造成服務中斷

所以通常會使用：

- 專用測試帳號
- 測試用商品
- 測試付款模式
- Feature Flag
- 少量流量
- 可快速回滾的部署
- 完整監控與告警

### Live Test 和 E2E Test 不一樣

這兩個概念是不同維度。

**E2E Test** 描述的是：

> 測試範圍有多完整。

**Live Test** 描述的是：

> 測試在哪個環境執行。

因此可以有：

- 測試環境中的 E2E Test
- 正式環境中的 E2E Live Test
- 正式環境中的簡單 Smoke Test

例如上線後，只測登入、首頁和付款 API 是否正常，這可能是：

> Production Smoke Test，也可以算一種 Live Test。

最初的一句話總結是：

> **Live Test 就是在真正上線、接近真實使用狀況的環境中驗證系統，但它不是一個定義完全統一的測試分類。**

## 對最初筆記的修正

整體沒有明顯錯誤，核心觀念是：

> Live Test 主要是在 live/production 或接近真實使用狀況的環境中驗證系統；它描述的是「測試環境」，不是像 Unit/E2E 那樣描述「測試範圍」。

但有幾個地方需要更精準。

### Live 不一定完全等於 Production

多數情境下 live environment 確實常指 production，但有些公司也會把「已接真實外部服務、真實流量、真實資料流」的環境稱為 live，即使它不是全量 production。

原本建議改成：

> Live Test 通常是在 production，或其他已接近真實使用狀況的 live environment 中進行測試。

後續討論發現這句仍有點不嚴謹，因為 production 本身通常就是 live environment，而且「接近真實使用狀況的 live environment」語意容易和 staging、production-like 混淆。

更嚴謹的定義是：

> **Live Test 是在已承接真實使用者、真實流量、真實資料或真實外部服務副作用的環境中驗證系統。最典型的 live environment 是 production，但也可能包含 canary、beta 或灰度發布環境。**

白話版本：

> **Live Test 是在真正有使用者或真實營運風險的環境中測試。它通常發生在 production，也可能發生在承接部分真實流量的 canary、beta 或灰度環境。**

若只是複製 production、但沒有真實使用者或真實營運風險，通常稱為 production-like testing 或 staging testing，不算嚴格意義上的 Live Test。

### A/B Test、Canary、Feature Flag 不一定都叫 Live Test

A/B Test、Canary Release、Feature Flag 可以是在 live environment 中進行驗證、實驗或漸進式發布的常見手段，但它們本身不等於 Live Test。

它們本身比較常被歸類為：

- experimentation
- progressive delivery
- release strategy

如果這些手段只是在 staging 或 production-like environment 裡使用，通常不算嚴格的 live testing。

### Staging 的資料要注意隱私與法規

Staging 不應直接使用未脫敏的 production data。較精準的寫法是：

| 環境 | 使用的資料 |
|---|---|
| Staging | 接近正式結構的測試資料、脫敏資料或仿真資料 |

### 正式環境的測試資料必須受控

「確認真的寫入正式資料庫」在概念上沒有錯，但正式環境測試通常不鼓勵直接製造普通正式資料，而是使用：

- 專用測試帳號
- 標記為 test 的 tenant、user 或 order
- 可追蹤、可清理的測試資料
- 不觸發真實金流或真實通知的保護機制

較安全的寫法是：

> 確認資料以受控的測試身分寫入正式環境，並能在測試後清理。

### Email 測試要限制收件者

Live Test 可以測真信件，但要避免寄給真實使用者。較安全的說法是：

> Email 是否能透過正式寄信流程送達指定測試信箱。

## Product、Production、Staging 與 Live Environment

用購物網站作為例子：

| 名稱 | 例子 | 說明 |
|---|---|---|
| Product | 購物網站這個產品 | 使用者會用來瀏覽商品、加入購物車、結帳 |
| Local environment | 工程師電腦上的購物網站 | 只有工程師自己測 |
| Staging environment | 公司內部測試用購物網站 | 長得很像正式站，但不給真實客戶用 |
| Production environment | 正式購物網站 | 真實客戶真的在這裡下單 |
| Live environment | 正在真實運作的環境 | 通常就是 production，也可能是承接部分真實流量的 canary 或 beta |

所以差別是：

```text
Product = 購物網站這個東西
Environment = 這個購物網站跑在哪裡
```

同一個 product 可以有很多環境：

```text
購物網站 product
├─ local：工程師自己電腦
├─ test：測試機
├─ staging：正式站的模擬環境
└─ production/live：真實客戶使用的正式環境
```

如果測試「新版結帳功能」：

```text
在 local 測
→ 工程師自己操作，沒有真實使用者

在 staging 測
→ QA 使用測試信用卡與測試商品，像正式環境但不是真實營運

在 production 測
→ 真實使用者可能下單、付款、收到 Email
```

因此：

```text
在 staging 測新版結帳
= production-like testing

在 production 測新版結帳
= live test
```

最短版：

```text
Product：你做出來的東西
Production：正式上線的那套環境
Live environment：正在被真實使用的環境
Live Test：在 live environment 裡測試
```

### Production-like 與 Live Environment 的差異

複製出的 production-like 或 staging 可以非常接近 production，但最大差異不是「長得像不像」，而是：

> 有沒有承受真實使用者、真實流量、真實資料變化、真實外部副作用。

| 面向 | Production-like / Staging | Live / Production |
|---|---|---|
| 使用者 | 通常是內部人員或測試人員 | 真實使用者 |
| 流量 | 人造流量、少量測試流量 | 真實流量，時間分布不可控 |
| 資料 | 測試資料、脫敏正式資料、快照資料 | 持續變動的真實資料 |
| 外部服務 | 常接 sandbox、mock、測試帳號 | 常接真實付款、寄信、第三方 API |
| 風險 | 測壞通常影響測試環境 | 測壞可能影響客戶與正式資料 |
| 監控壓力 | 可以模擬，但不一定完整 | 真實告警、SLA、營運壓力 |
| 權限與安全 | 可能簡化或隔離 | 真實資安規則與稽核要求 |
| 資料量 | 可能是部分資料或固定快照 | 真實規模與即時變化 |

最穩的記法是：

> **Production-like 是「像正式環境」；Live 是「正在真實運作」。**

### Live Environment 的判斷標準

Live environment 可以固定理解成：

> **已經承接真實使用情境與營運風險的環境。**

判斷重點包括：

- 真實使用者
- 真實流量
- 真實資料
- 真實外部服務副作用，例如寄信、付款、通知、第三方 API
- 真實營運風險

因此 `live environment` 這個名詞可以保留，但不要寫成「接近正式環境的 live environment」。若只是複製 production，卻沒有承接真實使用情境與營運風險，通常應稱為 staging、pre-production 或 production-like environment。

## A/B Test、Canary Release 與 Feature Flag

這三種方法常發生在正式環境，因此可以成為 Live Test 的手段，但它們本身不等於 Live Test。

### A/B Test

A/B Test 把使用者分成不同組別，例如：

```text
50% 使用者 → 舊版購物車
50% 使用者 → 新版購物車
```

觀察：

- 哪一版結帳率比較高
- 哪一版錯誤率比較低
- 使用者是否更容易完成流程

A/B Test 的重點是：

> 比較不同版本的效果。

它常用於產品決策，例如按鈕文案、頁面流程、推薦演算法或購物車設計。

實際運作時，通常會先定義版本與指標，例如舊版結帳頁是 A，新版結帳頁是 B，主要觀察結帳完成率、錯誤率或平均訂單金額。系統會用使用者 ID、session、cookie 或實驗平台，把使用者穩定分到不同組別，避免同一個人一下看到 A、一下看到 B。測試期間會收集資料，最後用統計方式判斷新版是否真的比較好。

### Canary Release

Canary Release 是先讓少量真實流量使用新版：

```text
95% 使用者 → 舊版
5% 使用者  → 新版
```

如果 5% 沒有問題，再慢慢擴大到 10%、25%、50%、100%。

Canary Release 的重點是：

> 降低新版本上線風險。

常見觀察指標：

- 錯誤率
- API latency
- CPU / memory
- crash rate
- 訂單或付款是否異常

若指標變差，就停止擴大、切回舊版或回滾部署。它的重點不是比較哪個版本更受歡迎，而是確認新版在真實流量下是否安全穩定。

### Feature Flag

Feature Flag 使用開關控制功能是否啟用。程式碼可能已經部署到 production，但新版功能先關閉：

```text
new_checkout = off
```

只對內部測試帳號、特定公司、特定地區或少量使用者打開：

```text
new_checkout = on for beta users
```

Feature Flag 的重點是：

> 功能可以部署，但是否啟用可以另外控制。

它可以細緻控制誰看到新功能，也能在出問題時快速關閉功能，而不一定要重新部署或回滾整個版本。Feature Flag 常和 A/B Test 或 Canary Release 搭配使用。

### 三者與 Live Test 的關係

```text
Live Test = 在真實運作的環境測試
A/B Test = 比較不同版本效果
Canary Release = 小流量逐步釋出新版
Feature Flag = 用開關控制功能開放範圍
```

可以用這個結構理解：

```text
Live Environment
├─ Production Smoke Test
├─ E2E Live Test
├─ A/B Test
├─ Canary Release
└─ Feature Flag 驗證
```

當 A/B Test、Canary Release 或 Feature Flag 發生在 production 或真實使用者流量上時，可以算是 live testing 的實務手段；如果只是在 staging 中使用，就不算典型的 Live Test。

## Beta、Canary 與灰度發布

### Canary

Canary 通常指 **Canary Release**，也就是先把新版開給一小部分真實流量，觀察系統穩不穩。

例如：

```text
99% 使用者 → 舊版
1% 使用者  → 新版
```

如果沒有問題，再逐步放大：

```text
1% → 5% → 10% → 50% → 100%
```

Canary 的重點是：

> 用少量真實流量驗證新版是否安全、穩定。

它偏工程與上線風險控管。

### Beta

Beta 通常指 **Beta Test / Beta Release**，也就是先開放給一群特定測試使用者試用，收集回饋。

```text
一般使用者 → 看不到新版功能
Beta 使用者 → 可以試用新版功能
```

Beta 使用者可能是：

- 公司內部員工
- 受邀客戶
- 早期使用者
- 報名測試計畫的人
- 特定企業客戶

常見觀察項目：

- 使用者覺得好不好用
- 功能是否符合需求
- 有沒有流程卡住
- 有沒有 edge case bug
- 文件或介面是否容易理解

Beta 的重點是：

> 讓特定使用者提前試用，收集產品回饋與問題。

它偏產品驗證與使用者回饋。

### 灰度發布

「灰度空間」不是固定的正式名詞，通常指的是 **灰度發布** 或有時被稱為「灰度環境」的發布狀態。

灰度發布的意思是：

> 新版本不要一次開給所有人，而是先開給一小部分真實使用者，觀察沒問題後再逐步擴大。

例如：

```text
90% 使用者 → 舊版
10% 使用者 → 新版
```

穩定後逐步放大：

```text
第 1 天：5% 使用者 → 新版
第 2 天：20% 使用者 → 新版
第 3 天：50% 使用者 → 新版
第 4 天：100% 使用者 → 新版
```

它叫「灰度」是因為它不是非黑即白：

```text
黑：完全不上線
白：完全上線
灰：只開給一部分人
```

Canary Release 與灰度發布非常接近。Canary Release 比較常見於 DevOps 或 release strategy 語境；灰度發布是中文技術語境常用的說法，強調逐步放量。

### Beta 與灰度發布的差異

最簡單的分法是：

```text
Beta：重點在「誰可以用」
灰度發布：重點在「怎麼逐步放量」
```

| 名詞 | 核心問題 | 常見對象 | 主要目的 |
|---|---|---|---|
| Beta | 誰先試用？ | 受邀使用者、早期客戶、內部員工 | 收集回饋、驗證產品體驗 |
| 灰度發布 | 要放多少流量？ | 某比例使用者、某地區、某租戶 | 逐步放量、控制上線風險 |

兩者可以重疊。例如先讓 beta 使用者中的 10% 使用新版，沒問題後再開到 50%，最後開給全部 beta 使用者。

但概念上不要完全等同：

> **Beta 是使用者範圍的概念；灰度發布是逐步釋出的策略。**

「灰度環境」這個詞容易混淆，實際上有時指的是：

- 灰度發布狀態
- 灰度流量
- 灰度版本
- Canary 環境

因此在筆記裡使用「灰度發布」會比「灰度環境」更清楚。

### 三者比較

| 名詞 | 對象 | 主要目的 |
|---|---|---|
| Canary | 少量真實流量 | 驗證新版穩定性 |
| Beta | 特定測試使用者 | 收集回饋、找問題 |
| 灰度發布 | 部分使用者或流量 | 逐步放量、降低上線風險 |

用購物網站舉例：

```text
Canary：
先讓 1% 真實使用者進新版結帳流程，看錯誤率和付款成功率。

Beta：
邀請 50 位老客戶試用新版結帳流程，詢問流程是否清楚、哪裡不好用。

灰度發布：
先開給台灣使用者 10%，再開 30%，最後全量開放。
```

若 Canary、Beta 或灰度發布已經承接部分真實流量或真實客戶，就可能被視為 live environment。判斷重點仍然是：它是否真的承接真實使用者、真實流量、真實資料或真實營運風險。

## 綜合結論

- Live Test 不是像 Unit Test、Integration Test、E2E Test 那樣定義統一的測試分類。
- Live Test 描述的是測試發生在哪一種環境；E2E Test 描述的是測試範圍。
- Live environment 的核心是「正在真實運作」，而不是單純「很像 production」。
- Production 通常是 live environment；Staging 或 production-like 通常不是。
- A/B Test、Canary Release、Feature Flag、Beta 與灰度發布可能在 live environment 中執行，但它們本身不等於 Live Test。
- Live Test 可能影響真實使用者、資料、交易或外部服務，因此必須控制帳號、資料、通知、付款、流量、回滾、監控與告警。

## 連結

- [[認識 Live Test]]
- [[Live Test 是在真實運作環境中驗證系統]]
- [[Live environment 是正在真實運作的環境]]
- [[Live Test 描述測試環境而不是測試範圍]]
- [[Live Test 需要控制真實使用者與資料風險]]
- [[A B Test 和 Canary Release 是 live environment 中的驗證手段]]
- [[A B Test 用分組比較不同版本的效果]]
- [[Canary Release 用少量流量驗證新版穩定性]]
- [[Feature Flag 用開關控制功能是否啟用]]
- [[Canary Beta 和灰度發布的差異]]
