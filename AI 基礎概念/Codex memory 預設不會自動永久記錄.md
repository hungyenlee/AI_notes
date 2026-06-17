標籤：#AI #memory #Codex #永久筆記

## 一句話

Codex 的 memory 是產品層功能，預設關閉；啟用後才可能在背景從符合條件的舊 threads 產生記憶，並存到 Codex home 的 memories 目錄。

## 內容

模型本身不會把資訊永久寫進「腦袋」。它每次回答時主要依靠當下 context。若要跨對話保存資訊，必須由產品或應用層提供 memory 機制。

以 Codex 來說，Memories 預設是關閉的。使用者啟用後，Codex 才可能把先前 threads 裡有用的穩定資訊整理成 memory，例如偏好、常見工作流程、技術棧、專案慣例或已知陷阱。這個過程不是每一輪對話結束後立刻發生，而是背景處理；Codex 會避開仍在進行中的 thread、太短暫的 session，並等 thread idle 一段時間後才可能產生記憶。

Codex memories 預設存放在 Codex home 底下的 `~/.codex/memories/`。如果使用者設定了 `CODEX_HOME`，位置會跟著改變。這些檔案是 generated state，可以檢查，但不應該把手動編輯它們當成主要控制方式。

## 連結

- [[認識 prompt、context、memory]]
- [[memory 是跨對話保存的長期資訊]]
- [[context 是 AI 當下能參考的資料包]]

## 來源

- [Memories - Codex | OpenAI Developers](https://developers.openai.com/codex/memories)
- 對話整理，2026-06-12
