#AI #Codex #skill #知識卡

## 一句話

`skill-creator` 在許多 Codex 環境中已經預裝，只有在可用 skills 清單裡找不到時，才需要另外安裝。

## 內容

使用 `skill-creator` 前，應先檢查目前環境是否已經有這個 skill。若它出現在可用 skills 清單中，或本機已有下列路徑，就可以直接用，不需要下載。

系統內建版：

```text
C:\Users\leolee\.codex\skills\.system\skill-creator\SKILL.md
```

個人安裝版：

```text
C:\Users\leolee\.codex\skills\skill-creator\SKILL.md
```

如果沒有，才需要透過 `skill-installer` 或手動方式安裝。可行做法是把完整的 skill 資料夾放到：

```text
C:\Users\leolee\.codex\skills\skill-creator\
```

要注意的是，只放單一 `SKILL.md` 可能不足以保留完整功能，因為 `skill-creator` 通常還包含 `scripts/`、`references/`、`agents/` 等輔助資源。

## 連結

- [[認識 skill-creator]]
- [[安裝 skill 後通常需要重啟 Codex]]
- [[Codex 應優先使用 OpenAI 版 skill-creator]]

## 來源

- [OpenAI skill-creator](https://github.com/openai/skills/tree/main/skills/.system/skill-creator)
- 對話：2026-06-18 關於 `skill-creator` 是否需要下載
