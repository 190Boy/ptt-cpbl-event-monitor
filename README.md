# PTT 中職活動監控工具 v7

架構：GitHub Pages 前端 + Google Apps Script 後端 + Google Sheet 資料庫。

## v7 更新

- 保留「連結匯入」：可貼 PTT、新聞、官方活動頁或售票頁，匯入後同步 Google Sheet。
- 保留「圖片 OCR 匯入」：可上傳活動海報、啦啦隊班表截圖，瀏覽器端 OCR 後同步 Google Sheet。
- 移除「匯入修正 / 手動補資料」區塊：手動修正請直接到 Google Sheet 修改。
- 網頁新增明顯的「開啟 Google Sheet」按鈕。
- `index.html` 已預填 GAS Web App URL。
- `Code.gs` 已預填 Google Sheet ID。

## 部署方式

1. 到 Google Apps Script 貼上 `Code.gs`。
2. 部署為 Web App。
3. 到 GitHub repo 更新 `index.html`。
4. 開啟 GitHub Pages 網址。

## Google Sheet

資料會同步到分頁：`中職活動監控`

欄位：

- 資料鍵
- 抓取時間
- 日期
- 地點
- 球隊
- 主題日
- 啦啦隊成員
- 狀態
- 來源
- 來源連結
- 命中關鍵字
- 信心
- 摘要
- 原始標題

## 使用建議

每天先按「重新抓取並同步 Sheet」。
若發現漏資料，可用「連結匯入」或「圖片 OCR 匯入」補進 Sheet。
若資料判讀有誤，直接開 Google Sheet 修正。

## 注意

FB / IG 連結通常無法直接抓內容，建議改用截圖後走圖片 OCR，或直接在 Google Sheet 補資料。
