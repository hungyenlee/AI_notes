標籤：#AI #Codex #skill #筆記

## 相關連結

- [[認識 skill]]
- [[skill 檔案由 SKILL.md 和輔助資源組成]]
- [[建立 skill 需要先定義觸發情境]]
- [[AI agent 先看 skill 描述 再按需讀取內容]]
- [[skill-creator 是用來建立與改善 skill 的 skill]]

## 整理版

如果要在電腦上實際建立一個 Codex skill，最小單位通常是一個資料夾，裡面放一份主要說明文件 `SKILL.md`。

## 最小結構

```text
my-skill/
└── SKILL.md
```

`SKILL.md` 是 skill 的核心入口。它告訴 Agent：

- 這個 skill 做什麼
- 什麼時候使用
- 要按照哪些步驟執行
- 可以參考哪些檔案或使用哪些已可用工具
- 輸出要長什麼樣子
- 完成前要檢查什麼

Codex 官方要求 `SKILL.md` 至少要有 frontmatter，並包含 `name` 和 `description`：

```markdown
---
name: skill-name
description: Explain exactly when this skill should and should not trigger.
---

Skill instructions for Codex to follow.
```

其中 `description` 很重要，因為 Codex 一開始會先看到 skill 的 `name`、`description` 和檔案路徑。只有當使用者明確呼叫 skill，或任務符合 `description` 時，Codex 才會讀完整的 `SKILL.md`。

## 範例 SKILL.md

```markdown
---
name: analyze-receipt
description: 從收據、發票或帳單圖片擷取商品名稱、數量與價格，整理成表格；當使用者提供消費收據圖片並希望整理消費明細時使用，不適用於單純翻譯或非收據圖片。
---

# 收據分析 Skill

## 目的

從收據圖片整理消費明細，輸出商品名稱、數量、單價、小計、店家、日期與帳單總額。

## 觸發條件

在以下情況使用：

- 使用者提供收據、發票或帳單圖片
- 使用者希望整理消費明細
- 使用者需要將收據內容轉成表格

不要在以下情況使用：

- 圖片不是消費收據
- 使用者只想翻譯收據內容
- 圖片模糊到無法辨識主要文字

## 執行流程

1. 確認圖片中是否包含店名、日期與商品明細。
2. 逐項辨識商品名稱、數量、單價與小計。
3. 檢查商品小計加總是否接近帳單總額。
4. 無法確認的文字不得自行猜測，標記為「待確認」。
5. 將結果整理成指定表格。

## 輸出格式

| 商品名稱 | 數量 | 單價 | 小計 | 備註 |
|---|---:|---:|---:|---|

最後補充：

- 消費日期
- 店家名稱
- 帳單總額
- 無法辨識的項目

## 檢查標準

完成前確認：

- 沒有遺漏清楚可見的商品
- 數量、單價與小計欄位沒有錯位
- 加總結果與帳單總額的差異已說明
- 不確定的內容有明確標記
```

## 較完整的資料夾結構

當 skill 開始變複雜，不建議把所有內容都塞進 `SKILL.md`。比較穩的做法是讓 `SKILL.md` 保持精簡，其他材料拆到輔助資料夾。

Codex 官方最核心的延伸結構是：

```text
skill-name/
├── SKILL.md          # skill 入口與主要指令
├── references/       # 背景知識、規則、文件、範例說明
├── scripts/          # 可執行程式
├── assets/           # Excel、圖片、設定檔、模板檔等素材
└── agents/
    └── openai.yaml   # Codex app 可選 metadata
```

實務上，也可以依團隊習慣加入：

```text
templates/            # 固定輸出模板
examples/             # 輸入與輸出範例
```

但 `templates/` 和 `examples/` 比較像實務約定，不是 Codex 最小標準的必要資料夾。它們也可以放進 `references/` 或 `assets/`，依 skill 的複雜度決定。

## 各部分用途

### `SKILL.md`

Skill 的入口與主要規則。

Agent 通常會先讀這份文件，因此應該放：

- skill 的目的
- frontmatter 的 `name` 和 `description`
- 核心觸發條件
- 核心執行流程
- 必須遵守的規範
- 其他檔案的使用方式

不要把所有背景知識都塞進去，否則會太長，也會浪費 context。

### `references/`

放背景知識、規則、查詢資料或長範例。

適合放：

- 名詞定義
- 業務規則
- API 說明
- 資料欄位說明
- 常見例外情況
- 公司內部規範
- 較長的輸入與輸出範例

在 `SKILL.md` 裡可以寫：

```markdown
辨識商品名稱時，視需要閱讀：
`references/product-name-normalization.md`
```

### `scripts/`

放需要實際執行的程式。

適合處理：

- 數字加總
- 格式轉換
- 建立檔案
- 驗證 JSON
- 修改 Excel
- 呼叫 API
- 批次處理資料

重要原則是：腳本負責「確定性的工作」，`SKILL.md` 負責「決定何時以及如何使用腳本」。

例如：

```python
from decimal import Decimal


def validate_total(items: list[dict], expected_total: str) -> bool:
    actual_total = sum(
        Decimal(str(item["subtotal"]))
        for item in items
    )

    return actual_total == Decimal(expected_total)
```

`SKILL.md` 則可以寫：

```markdown
整理完商品明細後，必須執行：

python scripts/validate_total.py

如果驗證失敗，不得直接輸出為已完成，必須列出差異。
```

### `assets/`

放 skill 執行時需要使用的原始檔案或素材。

例如：

- Excel 模板
- Word 模板
- 圖片
- 設計素材
- JSON Schema
- 預設設定檔
- 範例資料

例如：

```text
assets/
└── monthly-accounting-template.xlsx
```

Skill 可以規定：

```markdown
建立記帳檔案時，複製
`assets/monthly-accounting-template.xlsx`，
不得直接修改原始模板。
```

### `templates/`

放固定的輸出模板。這是實務上常見的拆法，但不是 Codex 官方最小標準的必要資料夾。

例如：

```markdown
# 帳單整理結果

## 基本資訊

- 日期：
- 店家：
- 總額：

## 商品明細

| 商品 | 數量 | 單價 | 小計 |
|---|---:|---:|---:|

## 待確認項目

-
```

在 skill 裡可以規定：

```markdown
最終輸出必須依照 `templates/output-template.md` 的格式。
```

若模板是實際要複製或修改的檔案，也可以放在 `assets/`。

### `examples/`

放輸入與輸出範例。這也是實務上常見的拆法，但不是必備標準。

範例適合說明：

- 正常情況怎麼處理
- 有折扣時怎麼處理
- 同一商品買多件時怎麼處理
- 看不清楚時怎麼標記
- 錯誤輸出長什麼樣子

若範例主要是讓 Agent 閱讀理解，可以放在 `references/`；若範例是測試用檔案或素材，也可以放在 `assets/`。

### `agents/openai.yaml`

這是 Codex app 可選的 metadata 檔案。它可以設定 UI 顯示資訊、implicit invocation policy、工具依賴等。

例如可以設定：

- 顯示名稱
- 簡短描述
- 預設 prompt
- 是否允許隱性觸發
- 依賴哪些 MCP 工具

不是每個 skill 都需要 `agents/openai.yaml`。若只是本機個人使用的簡單 skill，通常先有 `SKILL.md` 就夠。

## 如何判斷內容應該放在哪裡

| 內容 | 放置位置 |
|---|---|
| Agent 何時使用 skill | `SKILL.md` 的 `description`，正文可再補充 |
| Agent 要按照什麼順序執行 | `SKILL.md` |
| 一定要遵守的限制 | `SKILL.md` |
| 詳細的業務知識 | `references/` |
| 固定輸出格式 | `templates/`、`references/` 或 `assets/` |
| 正確與錯誤示範 | `examples/` 或 `references/` |
| 加總、驗證、轉檔等確定性操作 | `scripts/` |
| Excel、圖片或設定檔 | `assets/` |
| Codex app UI metadata 或工具依賴宣告 | `agents/openai.yaml` |

## SKILL.md 建議模板

可以直接從這份開始：

```markdown
---
name: skill-name
description: 用一句話說明這個 skill 解決什麼問題，以及何時使用；把最重要的觸發條件寫在這裡。
---

# Skill 名稱

## 目的

說明這個 skill 要完成的任務，以及預期結果。

## 觸發條件

在以下情況使用：

-
-

不要在以下情況使用：

-
-

## 輸入需求

執行前需要：

-
-

缺少必要資料時：

- 說明缺少什麼
- 能合理處理時繼續執行
- 不得自行捏造關鍵資料

## 執行流程

1.
2.
3.
4.

## 工具使用

- 什麼情況使用哪一個已可用工具
- 工具呼叫的順序
- 工具失敗時如何處理
- 哪些步驟必須透過腳本完成

## 參考資料

執行時視需要閱讀：

- `references/example.md`

## 輸出格式

最終輸出必須依照：

- `templates/output-template.md`

或者直接在此定義格式。

## 限制

- 不得……
- 必須……
- 無法確認時……

## 完成檢查

輸出前確認：

- [ ] 任務要求已全部完成
- [ ] 必要欄位沒有遺漏
- [ ] 數字或格式已驗證
- [ ] 不確定內容有清楚標記
- [ ] 輸出符合指定模板

## 範例

參考：

- `examples/example-input.md`
- `examples/example-output.md`
```

## 最核心的概念

可以把檔案型 skill 理解成：

> `SKILL.md` 負責指揮，`references/` 提供知識與範例，`scripts/` 負責確定性操作，`assets/` 存放執行時會使用的素材。`templates/` 和 `examples/` 可以獨立拆出，也可以放在 `references/` 或 `assets/`，看 skill 的複雜度決定。

最開始不需要一次建立全部內容。先從：

```text
my-skill/
└── SKILL.md
```

開始；當文件太長、流程需要程式執行，或輸出容易不一致時，再拆出其他資料夾。

## 原始資料

原始資料已另存：[[SKILL.md 的資料夾結構與撰寫模板（原始資料）]]

## 來源

- [Agent Skills - Codex | OpenAI Developers](https://developers.openai.com/codex/skills)
- 對話：2026-06-23 關於 `SKILL.md` 組成與資料夾結構的整理

