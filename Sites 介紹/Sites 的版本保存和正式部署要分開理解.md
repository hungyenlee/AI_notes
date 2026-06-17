標籤：#AI #Codex #Sites #永久筆記

## 一句話

在 Sites 裡，save a version 是建立可檢查的候選版本，deploy a version 才是把網站正式發布出去。

## 內容

Sites 的發布流程可以分成兩步。第一步是保存版本，Codex 會建立可部署的網站版本，並把它和當時的來源 Git commit 關聯起來。這適合用來先檢查畫面、內容、功能和 build 結果。

第二步才是部署版本。部署成功後，Sites 會回報 production URL，代表這個版本已經是正式網站。官方文件特別提醒，每個 Sites deployment URL 都是 production deployment，所以如果只是想先看成果，應該要求 Codex 先保存版本，不要直接部署。

## 連結

- [[認識 Codex Sites]]
- [[Sites 是 Codex 的網站建立與部署功能]]
- [[使用 Sites 架站前要先想清楚網站需要什麼]]

## 來源

- [Sites - Codex | OpenAI Developers](https://developers.openai.com/codex/sites)
