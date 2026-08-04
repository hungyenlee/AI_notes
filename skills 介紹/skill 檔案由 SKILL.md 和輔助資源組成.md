#AI #Codex #skill #知識卡

## 一句話

一個 skill 通常以 `SKILL.md` 作為入口，並用腳本、模板、參考資料或素材補足完整工作流程。

## 內容

`SKILL.md` 是 agent 判斷與執行 skill 的主要入口。它通常包含兩部分：

- frontmatter：放 `name`、`description` 等 metadata，協助 agent 發現與判斷 skill。
- 正文：放工作流程、使用規則、注意事項、範例、資源路徑和驗證方式。

除了 `SKILL.md`，skill 也可以包含輔助資料：

- `scripts/`：可執行腳本，適合放重複、精確、容易出錯的操作。
- `templates/`：輸出格式或文件模板。
- `references/`：較長的參考資料，避免全部塞進 `SKILL.md`。
- `assets/`：圖片、範例檔、設計素材或其他靜態資源。

好的 skill 組成方式，是讓 `SKILL.md` 負責導航與決策，把較長或較機械的內容放到輔助檔案中，讓 agent 需要時再讀。

## 連結

- [[認識 skill]]
- [[SKILL.md 的資料夾結構與撰寫模板]]
- [[建立 skill 需要先定義觸發情境]]
- [[AI agent 先看 skill 描述 再按需讀取內容]]
