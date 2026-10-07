# 立法院議題關注地圖

網站：https://hardy1yang.github.io/ly-issue-atlas/

逐年看 2016–2025 年立法院每個議題由哪些立委關注、關注怎麼移轉，以及政黨席次、議題重心與法案進程。網站上的數字都能回到公開的會議紀錄、議案與影片連結。

這個 repo 只放建置好的靜態網站與一份已驗證的資料（gh-pages 分支）。資料處理的原始碼、原始快照與資料庫不公開。

## 這份資料

- 資料版本：run `fetch-20261006T122600Z-dfc47335`（匯出 2026-10-07，部署 2026-10-07）
- 期間：2016–2025 議事年度。議事年度 Y 指 Y 年 2 月 1 日至 Y+1 年 1 月 31 日（臺北時間）。每個議事年度的批次都已完整取得。
- 議題分類：以關鍵詞規則離線分類全部紀錄；taxonomy v2.1、標註 v2.1-f4676a0b（探索版，沒有人工驗證）。語言模型對 88 筆保留樣本的 model review macro-F1 為 0.62，這是模型比對，不是人工驗證。
- 指標版本 2；各指標的公式、分子分母與限制寫在 `data/fetch-20261006T122600Z-dfc47335/meta.json` 的 metrics。

## 「關注」怎麼算

某位立委在某議事年度「關注」某議題，指當年至少 3 筆有該議題證據的實質發言或主提案（不含純連署），且這些紀錄占他當年同類紀錄的 5% 以上（一筆紀錄涉及多個議題時按權重拆分，未分類紀錄計入分母）。網站也能切換成含連署的定義。
門檻是設計選擇，不是學術上認定「關心」的標準；未達門檻、未在職或資料不足都不代表不關心。

## 資料來源

- 立法院 LYAPI（第三方整理的立法院開放資料）：立委名冊、議案、會議、公報議程與逐字稿、IVOD 影片索引
- 立法院資料開放平臺：議案編號對照
- 中央選舉委員會：區域、原住民、不分區當選名單（當選時黨籍）

各來源逐年的取得狀態列在網站「方法與資料」頁，也在 meta.json 的 sources。

## 已知限制

- 數字描述公開議事紀錄中可觀察的活動，不是政策功勞，也不是因果效果。
- 空值代表無法比較（資料不完整或沒有可計算的活動），不是零。
- 除非標註狀態為 validated_for_comparison，議題分類都是探索版。
- 黨籍依活動發生時判定；任內轉黨而日期不明者，該期間標為黨籍未知。
- 「新出現」只相對所比較的兩個年度，不代表生涯第一次關注；「未再觀察到」不等於不關心。
- 發言只含會議中的口頭發言；公報「質詢事項」（書面質詢與行政院答復）不在取得範圍內。
- 公報附錄「本期委員發言紀錄索引」只是頁碼索引、不含發言內容，不在取得範圍內。
- 公報議程 1078701_00012 是第 9 屆第 4 會期質詢事項全文的補刊，同屬書面質詢，不在取得範圍內。
- 2025 年 2 份會議紀錄（2025-12-30 院會、司法及法制與社福衛環委員會聯席會議）在 LYAPI 各格式都無法取得，這兩場會議的發言只來自 IVOD 影片索引，沒有逐字稿摘錄。

## 如何查證

- `data/fetch-20261006T122600Z-dfc47335/manifest.json` 列出每個公開檔的 SHA-256；`data/latest.json` 記錄 manifest 的雜湊（`deaef7ba3de347ec…`）。
- 發布前在乾淨環境從原始快照離線重播整理、身分、分類、評估與指標每一步，比對所有衍生表與公開檔；並稽核公開檔不含本機路徑、資料庫或憑證。
- 網站「方法與資料」頁可下載 CSV 與 datapackage.json；「資料處理流程」頁列出這個版本每一步的數量。

## English summary

A static atlas of issue attention in Taiwan's Legislative Yuan for legislative years 2016–2025 (each runs Feb 1 to Jan 31). It shows who attended to each issue year by year, how that changed, party seats and issue focus, and how far bills progressed, with links back to official records. A legislator attends to an issue in a year with at least 3 substantive speeches or primary proposals on it that make up at least 5% of their weighted records that year. Issue classification uses keyword rules and is exploratory (no human validation). Data version: run `fetch-20261006T122600Z-dfc47335`. Only the built site and one verified data bundle are published here; source code, raw snapshots and databases are not.
