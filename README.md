# PTT 中職主題日 / 啦啦隊情報監控工具

這版是：

```text
GitHub Pages 前端 index.html
+
Google Apps Script 後端 Code.gs
+
可選 Google Sheet 寫入紀錄
```

用途是每天監看 PTT `Baseball`、`CheerGirlsTW` 是否有出現中職主題日、啦啦隊班表、簽名會、拍照會、見面會、球隊活動等相關情報。

---

## 一、檔案說明

```text
Code.gs      → 貼到 Google Apps Script
index.html   → 放到 GitHub Pages
README.md    → 使用說明
```

---

## 二、建立 Google Apps Script 後端

1. 開一個 Google 試算表。
2. 點上方選單：`擴充功能` → `Apps Script`。
3. 刪掉原本內容，貼上 `Code.gs`。
4. 儲存專案。

---

## 三、部署成 Web App

在 Apps Script 右上角：

1. 點 `部署`。
2. 點 `新增部署作業`。
3. 類型選 `網頁應用程式`。
4. 設定：
   - 說明：`PTT CPBL Monitor API`
   - 執行身分：`我`
   - 誰可以存取：建議先選 `任何知道連結的人` 或 `任何人`
5. 按部署。
6. 授權 Google 權限。
7. 複製 Web App URL。

網址通常長這樣：

```text
https://script.google.com/macros/s/AKfycbxxxxxxxxxxxxxxxx/exec
```

---

## 四、設定 GitHub Pages 前端

1. 建立一個 GitHub repo。
2. 上傳 `index.html`。
3. 打開 `index.html`，找到這一行：

```javascript
const GAS_API_URL = "請貼上你的 Google Apps Script Web App URL";
```

4. 改成你的 Web App URL，例如：

```javascript
const GAS_API_URL = "https://script.google.com/macros/s/AKfycbxxxxxxxxxxxxxxxx/exec";
```

5. 到 GitHub repo：
   - `Settings`
   - `Pages`
   - Source 選 `Deploy from a branch`
   - Branch 選 `main`
   - Folder 選 `/root`
6. 儲存後等待 GitHub Pages 生效。

---

## 五、每天使用方式

打開 GitHub Pages 網址後：

1. 先按 `測試後端`。
2. 成功後按 `重新抓取`。
3. 預設會抓：
   - Baseball
   - CheerGirlsTW
   - 每板最新 3 頁
4. 若想掃更多內容，可以調整頁數。
5. 若想讓它抓所有文章內文，勾選 `全文掃描`。

---

## 六、寫入 Google Sheet

前端勾選 `寫入 Sheet` 後，再按 `重新抓取`。

後端會在目前試算表建立一個分頁：

```text
PTT中職活動監控
```

欄位包含：

```text
寫入時間
看板
文章日期
標題
作者
來源連結
信心
分數
可能類型
球隊
命中關鍵字
摘要提示
```

同一篇來源連結不會重複寫入。

---

## 七、目前第一版的判斷邏輯

這版還沒有串 AI，而是用關鍵字和規則分數。

會偵測：

```text
主題日
女孩日
寵物日
動漫
聯名
合作
班表
啦啦隊
應援
簽名會
拍照會
見面會
Passion Sisters
Rakuten Girls
Fubon Angels
Uni Girls
Dragon Beauties
Wing Stars
中信兄弟
樂天桃猿
統一獅
富邦悍將
味全龍
台鋼雄鷹
```

---

## 八、常見問題

### 1. GitHub 頁面顯示「請先設定 GAS_API_URL」

代表你還沒把 Apps Script Web App URL 貼進 `index.html`。

---

### 2. 測試後端失敗

請確認：

- Apps Script 是否已部署成「網頁應用程式」
- Web App URL 是否是 `/exec` 結尾
- 存取權限是否允許 GitHub Pages 呼叫
- 你是否按過 Google 授權

---

### 3. 按重新抓取很慢

可能原因：

- 抓取頁數太多
- 勾選了全文掃描
- PTT 回應較慢
- Apps Script 執行時間限制

建議第一版先用：

```text
每板 3 頁
不勾全文掃描
```

---

### 4. 為什麼不用 fetch，而用 JSONP？

因為 GitHub Pages 前端直接呼叫 Google Apps Script Web App 時，可能遇到 CORS 限制。

所以這版使用 JSONP：

```text
GitHub Pages 用 script 載入 GAS
GAS 回傳 callback({...資料...})
```

這樣比較穩。

---

### 5. 這能不能自動每天抓？

可以，但第一版先做手動監看。

之後可以在 Apps Script 加「時間觸發器」，每天自動掃描並寫入 Google Sheet，再讓 GitHub Pages 讀取最新資料。

---

## 九、建議後續升級

第二版可以加：

```text
1. AI 自動摘要
2. 每天自動排程
3. Gmail 通知
4. 只通知新增文章
5. 圖片 OCR
6. 從新聞網站補正式來源
7. 從 Google Sheet 讀取歷史資料
8. 主題日 / 班表分頁顯示
```
