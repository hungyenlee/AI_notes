標籤：#AI #Codex #skill #AGENTS

## 一句話

Codex 對 `AGENTS.md` 和 `skill` 採用不同載入策略：前者會在任務開始前組成指令鏈，後者先提供 metadata，等任務命中時才讀完整 `SKILL.md`。

## 內容

`AGENTS.md` 比較像 durable guidance。Codex 開始工作前會建立一條指令鏈：先看 Codex home 裡的全域指令，再從專案 root 一路走到目前工作目錄，逐層加入專案指令。越靠近目前工作目錄的檔案越晚出現，所以能覆蓋前面的規則。需要注意的是，同一層若有 `AGENTS.override.md`，它會優先於 `AGENTS.md`；若有設定 fallback filenames，Codex 也可能讀取其他指定檔名。

`skill` 的策略不同。Codex 會先從 repository、user、admin、system 等位置發現可用 skills；repository skills 是從目前工作目錄一路往 repo root 的每層 `.agents/skills` 掃描。Codex 會把每個 skill 的 `name`、`description` 和檔案路徑放入初始 context。當使用者明確點名某個 skill，或任務內容符合某個 skill 的 `description` 時，Codex 才讀取該 skill 的完整 `SKILL.md`。因此，`description` 不是普通摘要，而是觸發 skill 的判斷入口。

還有一個容易漏掉的限制：初始 skill 清單有 context 預算。當 skills 太多時，Codex 會先縮短 description；如果仍然太多，部分 skills 可能不會出現在初始清單中。同名 skills 也不會自動合併，而是可以同時出現在 skill selector 裡。所以比較精準的說法不是「所有 skills 一開始都會被完整讀取」，而是「先暴露可用 skills 的 metadata，再按任務需要展開完整內容」。

## 連結

- [[認識 skill]]
- [[AI agent 先看 skill 描述 再按需讀取內容]]
- [[skill 檔案由 SKILL.md 和輔助資源組成]]

## 來源

- [Custom instructions with AGENTS.md - Codex | OpenAI Developers](https://developers.openai.com/codex/guides/agents-md)
- [Agent Skills - Codex | OpenAI Developers](https://developers.openai.com/codex/skills)
