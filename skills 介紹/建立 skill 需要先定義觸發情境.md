標籤：#AI #Codex #skill #永久筆記

## 一句話

建立 skill 的第一步不是寫流程，而是先定義 agent 在什麼情境下應該使用它。

## 內容

一個好的 skill 通常要有清楚的名稱、明確的描述，以及可執行的工作步驟。描述要讓 agent 能判斷「這個任務是否需要我」，流程則要讓 agent 讀完後知道「接下來怎麼做」。

基本建立方式：

1. 建立一個 skill 資料夾。
2. 在資料夾中建立 `SKILL.md`。
3. 在 `SKILL.md` 開頭寫 frontmatter，至少包含 `name` 和 `description`。
4. 在正文寫明使用流程、限制、判斷標準和需要讀取的資源。
5. 視需要加入 `scripts/`、`assets/`、`templates/` 或 `references/`。

skill 的設計重點是讓 agent 可以穩定重複同一套工作方式，而不是只留下人類看得懂的備忘錄。

## 連結

- [[認識 skill]]
- [[skill 檔案由 SKILL.md 和輔助資源組成]]
- [[AI agent 先看 skill 描述 再按需讀取內容]]
