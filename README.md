# taiwan-address-tool 台灣地址填寫工具 https://achir1015.github.io/taiwan-address-tool/
<img width="624" height="876" alt="{92C7DF4F-A195-4AC4-B237-63B13F96365E}" src="https://github.com/user-attachments/assets/e750f91b-45ad-4ac0-8e39-c1c245659cf6" />
台灣地址填寫工具 — 開發總結

專案目標
製作一個純前端、單一 HTML 檔案的台灣地址填寫工具，具備三層下拉選單、3+2 郵遞區號自動帶入、中英文地址轉換，以及 Google Maps 地圖顯示功能。

功能架構
三層級聯下拉
縣市（24個）→ 鄉鎮市區（374個）→ 路名（43,521條）
                                        ↓
                               3+2 郵遞區號自動填入
英文地址轉換流程
路名（下拉）  →  translateRoadName()  →  Yuying St.
門牌號（輸入）→  translateHouseNum()  →  4F., No. 14-4, Ln. 135
縣市          →  COUNTY_EN 對照表    →  New Taipei City
鄉鎮市區      →  DISTRICT_EN 對照表  →  Shulin Dist.

結果：4F., No. 14-4, Ln. 135, Yuying St., Shulin Dist., New Taipei City, Taiwan

技術說明
項目內容資料來源jQuery-TWzipcode（舊3碼） + 使用者提供 Excel（新3+2碼，61,531筆）郵遞區號3+2 碼，格式 238-48，同路多號段時顯示警示路名拼音自建 700+ 字元對照表，逐字轉漢語拼音（育英→Yuying）地址結構解析正則表達式解析段/巷/弄/號/之/樓，轉成郵政英文格式地圖Google Maps iframe 嵌入，免 API Key、免 fetch字型大小全站 ×1.4 放大（11px～26px → 15px～36px）檔案大小約 668 KB（含完整地址資料）

開發過程解決的問題

英文地址中文殘留 → 拆分路名翻譯與門牌號翻譯兩個函式
路名拼音缺失（育英 St. → Yuying St.）→ 新增 700+ 字元拼音對照表
郵遞區號升級 → 從舊版 3 碼改為 Excel 資料的 3+2 碼，新增路名第三層下拉
地圖 Failed to fetch → 從 Nominatim API 改為 Google Maps iframe，徹底排除 fetch 與 CORS 問題


檔案交付
單一 taiwan-address-tool.html，下載後用任何瀏覽器直接開啟即可使用，無需伺服器或安裝任何套件。
