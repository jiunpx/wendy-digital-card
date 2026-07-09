# 復刻簡報（第四步 · 素材評審交接）

**狀態：** 待使用者確認後進入第五步  
**日期：** 2026-07-09

## 構建負責方

- 兜底：`personal-website` skill 第五步 + 靜態 HTML/CSS 單頁實作  
- 若本機有 `frontend-app-builder` 可並用；本專案以輕量單頁為主，無需框架

## 主視覺基準與分區順序

1. `references/sections/01-hero.jpg` — Hero  
2. `references/sections/02-contact.jpg` — 聯絡（重產版，無假地址）  
3. `references/sections/03-trust.jpg` — 信任／證照  
4. `references/sections/04-social.jpg` — 社群  
5. `references/sections/05-store-footer.jpg` — 門市＋頁尾  

## 全局外框

- 單頁、無多頁路由、無假瀏覽器 chrome  
- 無固定多連導覽（可選：頂部極簡字標 + 錨點）  
- 手機優先：聯絡三卡改直向堆疊  
- CTA：橘 `tel:`、綠 LINE（QR）、地圖外連  

## 字體鎖定

| 角色 | 規格 |
|------|------|
| 大標題姓名 | 系統無襯線 Black/Bold，約分區寬 8–10% 字高 |
| 正文 | Regular / Medium |
| 標籤 chips | Medium 小字 |
| 導覽／按鈕 | SemiBold |

`font-family: "Noto Sans TC", "PingFang TC", "Microsoft JhengHei", system-ui, sans-serif`

## 配色 token（實作必須用 CSS 變數）

```css
--brand-yellow: #F5B800;
--brand-orange: #F07A00;
--ink: #1A1A1A;
--muted: #5C5C5C;
--bg: #F7F7F5;
--surface: #FFFFFF;
--line-green: #06C755;
--phone-red: #E11D48;
--cta-orange: #F07A00;
```

## 最終素材路徑

| ID | 路徑 | 檢查 | 來源 |
|----|------|------|------|
| A1 | `assets/portrait.png` | **接受** — 真實人物、橘圓構圖完整 | 使用者肖像 |
| A2 | `assets/line-qr.png` | **接受** — 緊裁可掃 QR + LINE 標 | 名片裁切 |
| A3 | `assets/yongyi-logo.png` | **接受** — 標誌+字標+slogan | 名片裁切 |
| A3b | `assets/yongyi-mark.png` | 可選小標 | logo 上半 |
| — | 其餘 UI | code-native | SVG/CSS |

## 代碼／素材邊界

- 文字、按鈕、三卡、徽章、波浪黃橙帶、地圖按鈕 → **只許 code**  
- 臉、LINE QR、永義 logo → **只許上表真實檔**  
- 禁止：AI 換臉、假 QR、山寨 logo、參考圖切片當素材  

## 允許偏差

- 參考圖幻覺文案一律改名片事實  
- 03 右側插畫地圖 → 黃卡 + pin SVG 或併入 05  
- 04 假 @handle 刪除；無 URL 則不可點  
- 05 地圖用 Google Maps 外連，不嵌假截圖  
- 傳真可顯示（名片有）  

## QA 對照

| 分區 | 對照參考圖 |
|------|------------|
| Hero | 01-hero.jpg |
| 聯絡 | 02-contact.jpg |
| 信任 | 03-trust.jpg |
| 社群 | 04-social.jpg |
| 門市 | 05-store-footer.jpg |

## 風險觸發

- LINE 無官方加入網址 → 僅展示 QR（已就緒）  
- FB/TikTok 無 URL → 純文字（replace-later）  
- 上線前請用手機實掃 `line-qr.png` 驗證可加好友  

## 建議技術

- 單檔或 `index.html` + `styles.css` + `assets/`  
- 零建置，可直接開檔或丟 GitHub Pages / Netlify  
