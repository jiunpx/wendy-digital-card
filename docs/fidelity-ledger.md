# 保真台帳（第五步 QA）

| 分區 | 參考圖 | 必須保留錨點 | 實作 | 狀態 |
|------|--------|--------------|------|------|
| Hero | 01-hero | 左文右圓像、黃橙頂、雙 CTA、真肖像 | `index.html` hero | 對齊；logo 用真檔 |
| 聯絡 | 02-contact | 三卡、手機紅字、真 QR、門市事實 | contact grid | 對齊；無假地址 |
| 信任 | 03-trust | 店名、證照、chips、地址黃卡 | trust section | 對齊；無假章 |
| 社群 | 04-social | 雙橫條、帳號顯示名 | social | 對齊；無假 URL |
| 門市 | 05-store | 地圖+黃底店訊 | iframe + footer | 對齊 |

## 測量契約

- 肖像：手機約 72vw 圓；桌面約 36% 分區寬（max 320px）
- QR：約 180px 方塊於聯絡卡中央
- 色票：CSS 變數鎖定於 `styles.css :root`

## 有意偏差

- 底部固定快捷 dock（手機）— 提升轉換，參考圖無但合理
- 社群無外連（待補 URL）
- LINE 按鈕開啟 QR 圖（無 line.me 網址時）
