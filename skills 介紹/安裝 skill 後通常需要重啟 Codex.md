標籤：#AI #Codex #skill

## 一句話

把 skill 放進 Codex 可讀取的位置後，Codex 通常會自動偵測；若沒有出現，可以先重新載入 skills，必要時再重啟 Codex 並開新 session。

## 內容

Codex 需要先知道有哪些 skills 可用，才能根據 `name` 與 `description` 判斷是否要讀取某個 skill。官方文件的說法是，Codex 會偵測 skill 變更；如果新安裝或更新的 skill 沒有出現，就重啟 Codex。

在 Codex app 裡，也可以先用 command menu 的 **Force Reload Skills (強制重新載入技能)** 重新載入 skill 清單。若只是補一個 skill 或改 `SKILL.md`，這通常比整個 app 重啟更快。

「重啟 Codex」和「開新聊天視窗 / session」不是完全同一件事。重啟 Codex 是讓 app 或執行環境重新掃描 skills；開新 session 則是讓新的對話從一開始就拿到最新的 skill metadata。若你要測試 implicit invocation，或發現舊 thread 還是抓不到新 skill，最穩的做法是：先 reload 或重啟 Codex，再開一個新 session 測試。

安裝位置通常是使用者層級的 skills 目錄。以這台 Windows 環境來說，完整路徑是：

```text
C:\Users\leolee\.codex\skills\<skill-name>\
```

例如 `skill-creator` 的個人安裝位置會是：

```text
C:\Users\leolee\.codex\skills\skill-creator\
C:\Users\leolee\.codex\skills\skill-creator\SKILL.md
```

系統內建 skill 則可能在：

```text
C:\Users\leolee\.codex\skills\.system\<skill-name>\
```

例如系統內建 `skill-creator`：

```text
C:\Users\leolee\.codex\skills\.system\skill-creator\SKILL.md
```

專案層級 skill 則放在專案資料夾底下，例如這個 Obsidian vault 若要放專案專用 skill，位置可以是：

```text
C:\Users\leolee\Desktop\Obsidian\.agents\skills\<skill-name>\
C:\Users\leolee\Desktop\Obsidian\.agents\skills\<skill-name>\SKILL.md
```

資料夾中至少要有有效的 `SKILL.md`，而像 `skill-creator` 這類複雜 skill，最好安裝完整資料夾，保留 `scripts/`、`references/` 等資源。

## 連結

- [[認識 skill-creator]]
- [[skill-creator 不一定需要下載]]
- [[Codex 應優先使用 OpenAI 版 skill-creator]]
- [[skill 檔案由 SKILL.md 和輔助資源組成]]

## 來源

- [Agent Skills - Codex | OpenAI Developers](https://developers.openai.com/codex/skills)
- 對話：2026-06-18 關於 `skill-creator` 安裝與重啟
