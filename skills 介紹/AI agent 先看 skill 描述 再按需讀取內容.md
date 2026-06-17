標籤：#AI #Codex #skill #永久筆記

## 一句話

AI agent 通常先根據已提供的 skill metadata 判斷是否需要某個 skill，而不是一開始就讀取所有 skill 的完整內容。

## 內容

AI agent 通常不會一開始就把所有 skill 的完整內容全部讀進 context。它一開始看到的，通常是平台已經 discovery、註冊或提供給當前 session 的 skill metadata，例如名稱、`description`、位置或來源。

也就是說，agent 先面對的是一份「目前可用的 skill 清單」，而不是整個檔案系統裡所有可能存在的 skill。這份清單怎麼產生，取決於平台的 discovery 規則：有些平台會掃描固定資料夾，有些需要安裝或註冊 skill，有些則由 plugin、connector 或系統設定提供。

在 skill 已經被平台發現或提供給 agent 的前提下，`description` 就很重要。它像是觸發條件，幫助 agent 判斷目前任務是否符合這個 skill 的用途。當任務符合時，agent 才會打開對應的 `SKILL.md`，閱讀完整流程；如果 `SKILL.md` 指向其他參考資料、腳本或模板，agent 也會再按需要逐步讀取。

因此，如果專案下有多層資料夾，每一層都有 skill，agent 不一定會讀每一層的每一個 skill metadata。它通常只會使用已被 discovery、註冊或提供給當前 session 的 skill metadata。至於 discovery 是否會遞迴掃描所有子資料夾，取決於平台實作，不是 skill 概念本身保證的行為。

skill 的使用也不只靠 agent 自己判斷語意。使用者可以直接指定要使用哪個 skill，例如說「使用某個 skill」或點名 skill 名稱。這種明確指定可以降低語意判斷的不確定性，但前提仍是 agent 能讀到或找到該 skill。

## 連結

- [[認識 skill]]
- [[建立 skill 需要先定義觸發情境]]
- [[skill 檔案由 SKILL.md 和輔助資源組成]]
