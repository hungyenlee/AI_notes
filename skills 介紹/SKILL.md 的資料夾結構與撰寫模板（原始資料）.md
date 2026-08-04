#AI #Codex #skill #原始資料卡

## 來源

- 使用者提供的原始資料

## 摘要

這份原始資料保存建立 Codex skill 的資料夾結構與 `SKILL.md` 撰寫模板。它適合作為理解 skill 最小組成、觸發描述、執行流程與輸出格式的來源材料。

## 可沉澱的知識卡

- [[認識 skill]]
- [[SKILL.md 的資料夾結構與撰寫模板]]
- [[skill 檔案由 SKILL.md 和輔助資源組成]]
- [[建立 skill 需要先定義觸發情境]]

## 說明

這份檔案保留使用者提供的原始資料，未依官方修正重寫。整理版請見 [[SKILL.md 的資料夾結構與撰寫模板]]。

## 原始資料

如果你要在電腦上實際建立一個 Skill，最小單位通常就是一個資料夾，裡面放一份主要說明文件。

## 最小結構

```text
my-skill/
└── SKILL.md
```

`SKILL.md` 就是 Skill 的核心，告訴 Agent：

* 這個 Skill 做什麼
* 什麼時候使用
* 要按照哪些步驟執行
* 可以使用哪些工具
* 輸出要長什麼樣子
* 完成前要檢查什麼

例如：

```markdown
---
name: analyze-receipt
description: 從收據圖片擷取商品名稱、數量與價格，整理成表格。
---

# 收據分析 Skill

## 何時使用

當使用者提供收據、發票或帳單圖片，並希望整理消費明細時使用。

以下情況不要使用：

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

---

## 比較完整的資料夾結構

當 Skill 開始變複雜，不建議把所有內容都塞進 `SKILL.md`，可以拆成：

```text
analyze-receipt/
├── SKILL.md
├── references/
│   ├── receipt-fields.md
│   └── store-rules.md
├── templates/
│   └── output-template.md
├── examples/
│   ├── input-example.md
│   └── output-example.md
├── scripts/
│   └── validate_total.py
└── assets/
    └── accounting-template.xlsx
```

每個部分的用途如下。

### `SKILL.md`

Skill 的入口與主要規則。

Agent 通常會先閱讀這份文件，因此應該放：

* Skill 的目的
* 觸發條件
* 核心執行流程
* 必須遵守的規範
* 其他檔案的使用方式

不要把所有背景知識都塞進去，否則會太長。

---

### `references/`

放背景知識、規則或查詢資料。

例如：

```text
references/
├── product-name-normalization.md
├── accounting-rules.md
└── common-costco-items.md
```

適合放：

* 名詞定義
* 業務規則
* API 說明
* 資料欄位說明
* 常見例外情況
* 公司內部規範

在 `SKILL.md` 裡可以寫：

```markdown
辨識商品名稱時，請參考：
`references/product-name-normalization.md`
```

---

### `templates/`

放固定的輸出模板。

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

在 Skill 裡規定：

```markdown
最終輸出必須依照 `templates/output-template.md` 的格式。
```

這樣輸出會比只寫「整理成表格」穩定很多。

---

### `examples/`

放輸入與輸出範例。

例如：

```text
examples/
├── simple-receipt.md
├── discounted-item.md
└── unreadable-item.md
```

範例適合說明：

* 正常情況怎麼處理
* 有折扣時怎麼處理
* 同一商品買多件時怎麼處理
* 看不清楚時怎麼標記
* 錯誤輸出長什麼樣子

Agent 通常能從範例更精準地理解你的要求。

---

### `scripts/`

放需要實際執行的程式。

例如：

```text
scripts/
├── validate_total.py
├── convert_csv.py
└── create_accounting_file.py
```

適合處理：

* 數字加總
* 格式轉換
* 建立檔案
* 驗證 JSON
* 修改 Excel
* 呼叫 API
* 批次處理資料

例如 `validate_total.py`：

```python
from decimal import Decimal


def validate_total(items: list[dict], expected_total: str) -> bool:
    actual_total = sum(
        Decimal(str(item["subtotal"]))
        for item in items
    )

    return actual_total == Decimal(expected_total)
```

`SKILL.md` 則寫：

```markdown
整理完商品明細後，必須執行：

python scripts/validate_total.py

如果驗證失敗，不得直接輸出為已完成，必須列出差異。
```

重要的是，腳本負責「確定性的工作」，Skill 文件負責「決定何時以及如何使用腳本」。

---

### `assets/`

放 Skill 執行時需要使用的原始檔案。

例如：

* Excel 模板
* Word 模板
* 圖片
* 字型以外的設計素材
* JSON Schema
* 預設設定檔
* 範例資料

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

---

## 建議的標準結構

一般可以使用這個架構：

```text
skill-name/
├── SKILL.md          # Skill 入口與主要指令
├── references/       # 背景知識、規則、文件
├── templates/        # 輸出模板
├── examples/         # 輸入與輸出範例
├── scripts/          # 可執行程式
└── assets/           # Excel、圖片、設定檔等素材
```

不是每個 Skill 都需要全部資料夾。可以依複雜度逐步增加。

---

## 如何判斷內容應該放在哪裡

可以用這個原則區分：

| 內容               | 放置位置          |
| ---------------- | ------------- |
| Agent 何時使用 Skill | `SKILL.md`    |
| Agent 要按照什麼順序執行  | `SKILL.md`    |
| 一定要遵守的限制         | `SKILL.md`    |
| 詳細的業務知識          | `references/` |
| 固定輸出格式           | `templates/`  |
| 正確與錯誤示範          | `examples/`   |
| 加總、驗證、轉檔等確定性操作   | `scripts/`    |
| Excel、圖片或設定檔     | `assets/`     |

---

## `SKILL.md` 建議模板

可以直接從這份開始：

```markdown
---
name: skill-name
description: 用一句話說明這個 Skill 解決什麼問題，以及何時使用。
---

# Skill 名稱

## 目的

說明這個 Skill 要完成的任務，以及預期結果。

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

- 什麼情況使用哪一個工具
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

可以把檔案型 Skill 理解成：

> **SKILL.md 負責指揮，references 提供知識，templates 規定輸出，scripts 負責執行，examples 幫助理解。**

最開始不需要一次建立全部內容。先從：

```text
my-skill/
└── SKILL.md
```

開始；當文件太長、流程需要程式執行，或輸出容易不一致時，再拆出其他資料夾。

