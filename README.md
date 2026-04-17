
互動學習平台
系統操作說明書

 
功能：QR Code 掃描即播放 ｜ 數位書籍瀏覽 ｜ 學習單下載
部署平台：GitHub Pages
管理方式：網頁管理工具 admin.html

版本 1.0
 
一、系統總覽
互動學習平台是一個部署在 GitHub Pages 上的靜態網站，專為教學現場設計。整個系統由以下元件組成：

檔案	用途	說明
index.html	主網站	學生 / 家長使用的前台頁面
admin.html	管理工具	老師用來管理內容的後台工具
config.json	設定檔	儲存所有音檔、書籍、學習單資料
audio/	音檔資料夾	存放 MP3 音檔
books/	書籍資料夾	存放掃描的課本圖片
worksheets/	學習單資料夾	存放可下載的學習單 PDF

二、系統運作流程
整個系統的運作邏輯非常簡單：老師在 admin.html 管理工具中編輯內容，按下「推送到 GitHub」後，config.json 會自動更新到 GitHub 倉庫，GitHub Pages 會在 1-2 分鐘內重新部署網站。學生透過手機或平板訪問網站即可使用。

💡 核心概念
你不需要懂任何程式碼！所有操作都透過管理工具的圖形介面完成，內容更新只需要一鍵推送。

三、首次部署設定
3.1 建立 GitHub 帳號
如果你還沒有 GitHub 帳號，請先到 https://github.com 註冊一個免費帳號。
3.2 建立 GitHub 倉庫
1.	登入 GitHub 後，點擊右上角的 + 按鈕，選擇 New repository
2.	輸入倉庫名稱（例如 learning-platform）
3.	將 Repository 設為 Public（GitHub Pages 免費版需要公開倉庫）
4.	點擊 Create repository
3.3 上傳網站檔案
5.	在新建的倉庫頁面，點擊「Add file」→「Upload files」
6.	將 index.html、admin.html、config.json 以及 audio/、books/、worksheets/ 資料夾一起拖入上傳
7.	輸入 Commit 訊息（例如「初始上傳」），點擊 Commit changes
3.4 啟用 GitHub Pages
8.	進入倉庫 → Settings → 左側選單點 Pages
9.	Source 選擇 Deploy from a branch
10.	Branch 選擇 main，資料夾選 / (root)
11.	點擊 Save，等待 1-2 分鐘
12.	你的網站就上線了！網址格式為：https://你的帳號.github.io/倉庫名稱/

範例：如果你的帳號是 teacher-wang，倉庫名是 learning-platform，那麼網站網址就是 https://teacher-wang.github.io/learning-platform/

四、設定 GitHub Token（實現一鍵推送）
設定 Token 後，你可以直接從管理工具將設定推送到 GitHub，不需要手動下載上傳檔案。
4.1 產生 Personal Access Token
13.	前往 https://github.com/settings/tokens?type=beta
14.	點擊 Generate new token
15.	Token name 輸入一個好記的名稱，例如 學習平台管理
16.	Expiration 選擇過期日（建議選 90 days 或 1 year）
17.	Repository access 選 Only select repositories → 選擇你的倉庫
18.	展開 Permissions → Repository permissions → 找到 Contents → 設為 Read and write
19.	點擊 Generate token
20.	複製產生的 Token（以 github_pat_ 開頭），請立即保存，離開頁面後就看不到了

⚠️ 安全提醒
Token 等同於密碼，請不要分享給他人。Token 僅儲存在你的瀏覽器中，不會傳送到任何第三方伺服器。如果 Token 過期，只需重新產生一個即可。
4.2 在管理工具中設定
21.	用瀏覽器開啟 admin.html
22.	點擊左側選單的「🐙 GitHub 連線」
23.	填入 GitHub 帳號名稱、倉庫名稱、Token
24.	點擊「🔌 測試連線」確認連線成功
25.	完成！現在你可以使用 「🚀 推送到 GitHub」 按鈕了

五、日常操作指南
5.1 管理工具介面說明
管理工具 admin.html 是一個純前端網頁，你可以直接用瀏覽器開啟本機檔案，或透過部署後的網址存取（例如 https://你的帳號.github.io/倉庫名稱/admin.html）。

頁面	功能
🔊 音檔管理	新增、編輯、刪除音檔項目
📖 書籍管理	管理數位書籍的封面與頁面圖片
📝 學習單管理	管理可下載的學習單檔案
🏷 QR Code 產生	自動產生 QR Code 並可列印或下載
📄 config.json 預覽	即時預覽產出的設定檔
🐙 GitHub 連線	設定 Token 與一鍵推送
📥 匯入 / 匯出	匯入現有設定或匯出備份
⚙️ 網站設定	修改網站名稱與歡迎訊息

5.2 新增音檔
26.	先將 MP3 音檔放入 GitHub 倉庫的 audio/ 資料夾
27.	在管理工具中點擊「🔊 音檔管理」→「＋ 新增音檔」
28.	填寫 ID（例如 lesson01）、名稱（例如 第一課 我的家人）、檔案路徑（例如 audio/lesson01.mp3）
29.	點擊「新增」
30.	按下左下角的 「🚀 推送到 GitHub」

💡 關於 ID
ID 是 QR Code 掃描時用來辨識要播放哪個音檔的代碼。建議使用英文加數字的組合，例如 lesson01、unit02_vocab 等。

5.3 新增書籍
31.	將掃描的書頁圖片放入 books/書名/ 資料夾（例如 books/chinese-book01/）
32.	在管理工具中點擊「📖 書籍管理」→「＋ 新增書籍」
33.	填寫 ID、書名、封面路徑
34.	在「頁面圖片路徑」欄位中，可使用範圍語法快速加入多頁：books/chinese-book01/page[01-30].jpg 即可一次加入 30 頁
35.	「🚀 推送到 GitHub」

5.4 新增學習單
36.	將學習單 PDF 放入 worksheets/ 資料夾
37.	在管理工具中點擊「📝 學習單管理」→「＋ 新增學習單」
38.	填寫標題、檔案路徑，選擇年級與科目
39.	「🚀 推送到 GitHub」

5.5 產生與列印 QR Code
40.	點擊左側選單的「🏷 QR Code 產生」
41.	選擇 「從音檔自動產生」 會自動為所有音檔產生 QR Code
42.	點擊 「🖨 列印全部」 可直接列印 QR Code 頁面
43.	點擊 「💾 下載全部圖片」 可下載每個 QR Code 的 PNG 圖檔
44.	將列印或下載的 QR Code 貼在課本對應頁面即可

也可以切換到「自訂內容」模式，手動輸入 QR Code 的內容，例如外部音檔連結。

六、QR Code 自動播放原理
瀏覽器基於安全考量，預設會封鎖「沒有使用者互動就自動播放音訊」的行為。本系統透過以下設計解決這個問題：

45.	使用者按下「同意並開始使用」 — 這個點擊動作觸發了 AudioContext 的解鎖
46.	在同一頁面內啟動相機掃描 — 因為已經有使用者互動紀錄，瀏覽器允許播放音訊
47.	掃描到 QR Code 後立即播放 — 不需要再按播放按鈕

iOS Safari 也已做特別處理，在同意按鈕時預先播放靜音音訊來解鎖 Audio 元件。

七、檔案結構說明
GitHub 倉庫中的檔案結構如下：

路徑	說明
index.html	主網站頁面（給學生用）
admin.html	管理工具（給老師用）
config.json	設定檔（由管理工具自動產生）
audio/lesson01.mp3	音檔（MP3 格式）
books/book01/cover.jpg	書籍封面圖片
books/book01/page01.jpg	書籍內頁圖片
worksheets/ws01.pdf	學習單檔案

⚠️ 檔案大小限制
GitHub 單一檔案上限為 100MB，整個倉庫建議不超過 1GB。音檔建議壓縮到合理大小（一般 MP3 每分鐘約 1MB）。圖片建議使用 JPG 格式並適當壓縮。

八、常見問題排解
Q：掃描 QR Code 後沒有聲音？
•	確認手機沒有開靜音模式
•	確認音檔路徑正確（檔名大小寫要完全一致）
•	確認音檔已上傳到 GitHub 倉庫的正確位置
•	嘗試重新整理頁面，再次按下「同意並開始使用」
Q：相機無法啟動？
•	確認瀏覽器已授權相機權限
•	確認網站是透過 HTTPS 開啟（GitHub Pages 自帶 HTTPS）
•	部分瀏覽器不支援網頁相機，建議使用 Chrome 或 Safari
Q：更新了檔案但網站沒變化？
•	GitHub Pages 有快取機制，通常需要等 1-2 分鐘
•	在瀏覽器中按 Ctrl + Shift + R（Mac 為 Cmd + Shift + R）強制重新整理
•	可到 GitHub 倉庫的 Actions 頁籤確認部署狀態
Q：推送到 GitHub 失敗？
•	確認 Token 沒有過期（到 GitHub Settings → Tokens 頁面檢查）
•	確認 Token 有 Contents: Read and write 權限
•	確認帳號名稱與倉庫名稱正確無誤
•	使用「🔌 測試連線」按鈕診斷問題
Q：GitHub 倉庫空間不夠？
•	考慮壓縮音檔品質（128kbps 的 MP3 對教學用途已足夠）
•	壓縮掃描圖片（JPG 品質 80% 即可）
•	如果音檔太多，可考慮使用外部音檔連結

九、快速參考表
日常更新流程

步驟	操作	位置
1	開啟管理工具	瀏覽器開啟 admin.html
2	新增 / 編輯內容	音檔管理 / 書籍管理 / 學習單管理
3	推送到 GitHub	左下角「🚀 推送到 GitHub」
4	等待部署	約 1-2 分鐘自動更新

QR Code 內容格式

格式	範例	說明
音檔 ID	lesson01	推薦！ 對應 config.json 中的 id
檔案路徑	audio/lesson01.mp3	直接指定檔案位置
外部網址	https://example.com/a.mp3	連結外部音檔

 
— 說明書結束 —
如有問題，歡迎隨時詢問！
