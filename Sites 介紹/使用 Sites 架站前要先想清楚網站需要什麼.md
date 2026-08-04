#AI #Codex #Sites #知識卡

## 一句話

使用 Sites 架站前，先判斷網站是否需要資料保存、檔案上傳、登入權限、環境變數或秘密設定。

## 內容

最簡單的 Sites 專案可以只是內容型網站，不需要資料庫或檔案儲存。但如果網站要記住使用者進度、表單資料、分數或其他結構化資料，就可能需要 D1 這類資料庫；如果要處理圖片、文件、影音或上傳檔案，就可能需要 R2 這類物件儲存。

架站前也要想清楚誰可以看網站。新網站最好先限制給 owner 和 workspace admins，確認內容、資料處理和目標受眾後，再開放給 workspace 或指定使用者。若網站需要 API key、token 或其他秘密值，應該透過 Sites 面板設定 hosted environment variables 和 secrets，不要把秘密寫進 `.openai/hosting.json` 或 source files。

## 連結

- [[認識 Codex Sites]]
- [[Sites 是 Codex 的網站建立與部署功能]]
- [[Sites 的版本保存和正式部署要分開理解]]

## 來源

- [Sites - Codex | OpenAI Developers](https://developers.openai.com/codex/sites)
