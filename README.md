# 📚 互動學習平台

一個部署在 GitHub Pages 上的互動學習網站，專為教學現場設計。

## ✨ 功能特色

### 📷 QR Code 掃描即播放
- 使用者按下「同意」後，相機自動啟動
- 掃描 QR Code 後**立即播放音檔**，不需要再按播放鍵
- 原理：利用使用者的同意動作解鎖瀏覽器的音訊限制（AudioContext）

### 📖 數位書籍瀏覽
- 將掃描的課本圖片以翻頁方式呈現
- 支援左右滑動翻頁（平板與手機）
- 支援鍵盤方向鍵翻頁（電腦）

### 📝 學習單下載
- 提供學習單的下載連結
- 顯示年級與科目標籤，方便查找

---

## 🚀 部署步驟（GitHub Pages）

### 第一步：建立 GitHub 倉庫

1. 登入 [GitHub](https://github.com)
2. 點擊右上角 `+` → `New repository`
3. 輸入倉庫名稱（例如 `learning-platform`）
4. 設定為 **Public**
5. 點擊 `Create repository`

### 第二步：上傳檔案

將以下檔案與資料夾上傳到倉庫：

```
your-repo/
├── index.html          ← 主網頁（已建好）
├── config.json         ← 設定檔（修改此檔來管理內容）
├── audio/              ← 放音檔的資料夾
│   ├── lesson01.mp3
│   ├── lesson02.mp3
│   └── ...
├── books/              ← 放書籍掃描圖的資料夾
│   ├── book01/
│   │   ├── cover.jpg
│   │   ├── page01.jpg
│   │   ├── page02.jpg
│   │   └── ...
│   └── book02/
│       └── ...
├── worksheets/         ← 放學習單的資料夾
│   ├── worksheet01.pdf
│   └── ...
└── README.md
```

### 第三步：啟用 GitHub Pages

1. 進入倉庫 → `Settings` → 左側選單點 `Pages`
2. Source 選擇 `Deploy from a branch`
3. Branch 選擇 `main`，資料夾選 `/ (root)`
4. 點擊 `Save`
5. 等待 1-2 分鐘，你的網站就會上線！

網站網址：`https://你的帳號.github.io/倉庫名稱/`

---

## 📝 如何管理內容

所有內容都透過 **`config.json`** 來管理，不需要修改任何程式碼。

### 新增音檔

1. 將 `.mp3` 檔案放入 `audio/` 資料夾
2. 編輯 `config.json`，在 `audioFiles` 陣列中新增：

```json
{
  "id": "lesson01",
  "name": "第一課 我的家人",
  "file": "audio/lesson01.mp3",
  "description": "國語第一課課文朗讀"
}
```

3. 製作 QR Code：內容填入音檔的 `id`（例如 `lesson01`）或檔案路徑（例如 `audio/lesson01.mp3`）

### 新增書籍

1. 將掃描圖片放入 `books/你的書名/` 資料夾
2. 編輯 `config.json`，在 `books` 陣列中新增：

```json
{
  "id": "book01",
  "title": "國語課本第一冊",
  "cover": "books/book01/cover.jpg",
  "pages": [
    "books/book01/page01.jpg",
    "books/book01/page02.jpg",
    "books/book01/page03.jpg"
  ],
  "description": "三年級上學期國語課本"
}
```

### 新增學習單

1. 將學習單檔案（PDF、Word 等）放入 `worksheets/` 資料夾
2. 編輯 `config.json`，在 `worksheets` 陣列中新增：

```json
{
  "id": "ws01",
  "title": "第一課生字練習",
  "file": "worksheets/vocab01.pdf",
  "description": "第一課生字筆順與造詞練習",
  "grade": "三年級",
  "subject": "國語"
}
```

---

## 🏷 QR Code 製作方式

QR Code 的內容可以是以下任一格式：

| 格式 | 範例 | 說明 |
|------|------|------|
| 音檔 ID | `lesson01` | 對應 config.json 中的 id |
| 檔案路徑 | `audio/lesson01.mp3` | 直接指定檔案路徑 |
| 完整網址 | `https://example.com/audio.mp3` | 外部音檔連結 |

### 推薦的 QR Code 產生器

- [QR Code Generator](https://www.qr-code-generator.com/)
- [草料二維碼](https://cli.im/)
- Google 試算表 + `=IMAGE("https://chart.googleapis.com/chart?cht=qr&chs=200x200&chl=" & A1)`

---

## 🔄 如何更新內容

更新音檔、書籍或學習單只需要 3 個步驟：

1. **替換檔案**：在 GitHub 倉庫中上傳新檔案（覆蓋舊檔即可）
2. **更新 config.json**：如果有新增或修改項目，編輯 config.json
3. **等待部署**：GitHub Pages 會在幾分鐘內自動更新

> 💡 小技巧：如果只是替換音檔（檔名不變），只需上傳新檔案，不需要改 config.json！

---

## ⚠️ 注意事項

- **音檔格式**：建議使用 `.mp3`，相容性最佳
- **圖片格式**：建議使用 `.jpg`，檔案較小、載入較快
- **檔案大小**：GitHub 單檔上限 100MB，整個倉庫建議不超過 1GB
- **瀏覽器支援**：支援 Chrome、Safari、Edge 等現代瀏覽器
- **HTTPS**：GitHub Pages 自帶 HTTPS，相機功能需要 HTTPS 才能使用
- **iOS 相容**：已針對 iOS Safari 做特別處理，確保音檔可自動播放

---

## 📱 使用流程

1. 學生/家長用手機或平板開啟網站
2. 點擊「**同意並開始使用**」按鈕
3. 授權相機權限
4. 將 QR Code 對準鏡頭 → 音檔自動播放！
5. 也可以切換到「數位書籍」或「學習單」分頁

---

## 💡 常見問題

**Q：掃描後沒有聲音？**
A：請確認手機沒有開靜音，並確認音檔路徑正確。

**Q：相機無法啟動？**
A：請確認已授權瀏覽器使用相機，且網站是透過 HTTPS 開啟。

**Q：更新了檔案但網站沒變化？**
A：GitHub Pages 有快取，可能需要等幾分鐘。在瀏覽器中按 Ctrl+Shift+R 強制重新整理。

**Q：GitHub 倉庫空間不夠？**
A：可以考慮將大型音檔存放在 Google Drive 並使用直接下載連結。
