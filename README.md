# PTT 中職主題日 / 啦啦隊情報監控工具 v4

架構：

- GitHub Pages：前端 `index.html`
- Google Apps Script：後端 `Code.gs`
- 可選 Google Sheet：保存掃描結果

## v4 新增功能

1. **連結匯入**
   - 可貼 PTT、新聞、球團官網、售票頁等連結。
   - 後端會抓取頁面文字並解析成活動情報表。
   - FB / IG 可能因平台限制無法抓取，建議改用截圖 OCR 或貼文字。

2. **圖片 OCR 匯入**
   - 可匯入活動海報、啦啦隊班表截圖。
   - 使用瀏覽器端 Tesseract.js 免費 OCR，不需要 OpenAI API，不會產生 OpenAI 費用。
   - 第一次載入繁中文字庫可能較慢。

3. **匯入修正 / 手動補資料**
   - 可貼 Excel 複製出來的 TSV、CSV，或 Markdown 表格。
   - 建議欄位：日期、地點、球隊、主題日、啦啦隊成員、狀態、來源、來源連結。
   - 若資料與現有列相同，會用新匯入的欄位覆蓋修正。

## 檔案說明

- `Code.gs`：貼到 Google Apps Script。
- `index.html`：放到 GitHub Pages。
- `README.md`：使用說明。

## 安裝步驟

### 1. Google Apps Script

1. 建立 Google Sheet。
2. 點「擴充功能」→「Apps Script」。
3. 將 `Code.gs` 全部貼上。
4. 按「部署」→「新增部署作業」。
5. 類型選「網頁應用程式」。
6. 執行身分選「我」。
7. 存取權限建議選「任何知道連結的人」或依你的需求設定。
8. 部署後複製 Web App URL。

### 2. GitHub Pages

1. 建立 repo，例如：`ptt-cpbl-event-monitor`。
2. 上傳 `index.html`。
3. 到 repo Settings → Pages，啟用 GitHub Pages。
4. 打開 `index.html`，找到：

```js
const DEFAULT_GAS_API_URL = "請貼上你的 Google Apps Script Web App URL";
```

改成你的 Google Apps Script Web App URL。

## 匯入修正格式範例

可以直接從 Excel 複製貼上：

```text
日期	地點	球隊	主題日	啦啦隊成員	狀態	來源
6/15	桃園棒球場	樂天桃猿	XXX主題日	籃籃、Yuri、若潼	已確認	手動修正
6/16	臺中洲際棒球場	中信兄弟	未命名活動	峮峮、短今	疑似班表	啦啦隊貼文
```

也可以貼 Markdown 表格：

```markdown
| 日期 | 地點 | 球隊 | 主題日 | 啦啦隊成員 | 狀態 | 來源 |
| ---- | ---- | ---- | ------ | ---------- | ---- | ---- |
| 6/15 | 桃園棒球場 | 樂天桃猿 | XXX主題日 | 籃籃、Yuri、若潼 | 已確認 | 手動修正 |
```

## 注意事項

- 這版沒有使用 OpenAI API，因此不會產生 OpenAI API 費用。
- OCR 是免費瀏覽器端辨識，但準確度會受圖片清晰度、字體、排版影響。
- FB / IG 連結不保證能被後端抓取，建議用截圖或貼文文字匯入。
- 自動解析仍是規則式，不是 AI，因此欄位可能需要手動修正。
