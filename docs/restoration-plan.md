# 復刻計畫 / 素材拆分（第三步）

**狀態：** 待使用者確認  
**專案：** 陳蓮婷（溫蒂）數字名片 · 視覺方向 A  
**已接受參考圖：** `references/sections/01-hero.jpg` … `05-store-footer.jpg`  
**真實來源素材：** `assets/source/portrait-circle.jpg`、`assets/source/business-card.jpg`

> 硬性停止：本文件確認前，不生成新圖、不寫 HTML/CSS/JS。

---

## 全局規則

| 規則 | 內容 |
|------|------|
| 站點形態 | 單頁、手機優先、無假瀏覽器 chrome |
| 配色 token | `#F5B800` 主黃 · `#F07A00` 陽光橙 · `#1A1A1A` 墨字 · `#FFFFFF` 白 · `#22C55E` LINE 綠 · `#EF4444` 電話紅數字 |
| 字體 | 系統無襯線（`"Noto Sans TC", "PingFang TC", "Microsoft JhengHei", sans-serif`） |
| 文字來源 | **僅名片事實**；參考圖上的幻覺字串一律丟棄 |
| 人物 | **真實肖像 only**，禁止 AI 換臉或生成替身臉 |
| 品牌 logo | 從使用者名片抽取／向量重繪近似；禁止生成山寨標 |
| 互動預設 | 聯絡卡可點（`tel:` / LINE / 地圖）；其餘靜態 |

---

## 參考圖 → 構建映射

### 01 · Hero（`01-hero.jpg`）

```text
參考圖：01-hero.jpg
代碼層：卡片圓角外框、黃橙波浪頂帶（CSS 漸層/clip-path）、左上簡化日出海 logo（SVG）、姓名/職稱/公司/定位句、橘 CTA、綠 CTA、圓形頭像裁切框與陰影
背景素材：無 — 波浪與色帶用 CSS（code-native）
前景素材：portrait.png — 右側圓形內真實半身照，約佔分區寬 32–38%，1:1 圓裁
必須保留：左文右圓像、黃→橙頂波浪、雙 CTA（橘撥打 + 綠 LINE）、大號姓名
允許偏差：參考圖上的白線日出海 logo 可改為永義官方標（從名片抽取）或簡化 SVG；外層灰桌面背景改為頁面底色而非「卡片漂浮在灰底」若全頁更乾淨
風險觸發：必須使用 assets/source/portrait-circle.jpg，不可用參考圖裁切臉
```

| 元素 | 角色 | 代碼可行性 | 若硬編碼風險 | 決策 | 來源/動作 |
|------|------|------------|--------------|------|-----------|
| 黃橙波浪頂 | static-decor | 高（CSS gradient） | 低 | code-native | CSS |
| 日出海 / 永義標 | identity | 中 | 畫錯損品牌 | find/copy 或 SVG 近似 | 名片 logo / SVG |
| 姓名等文字 | content | 高 | — | code-native | 名片文案 |
| 撥打電話 / 加入 LINE | CTA | 高 | — | code-native | `<a href="tel:">` / LINE |
| 圓形肖像 | identity / media-slot | 低（照片） | 失真/換臉 | find/copy → ready | `portrait-circle.jpg` → 去背或保留橘圓 |

**交互假設（推薦）：** 雙 CTA 可點；肖像不可點。  
**備選：** 整張 hero 卡可分享（Web Share API）— 非必須，預設不做。

---

### 02 · 聯絡（`02-contact.jpg`）

```text
參考圖：02-contact.jpg
代碼層：標題「聯絡方式」、三欄卡片布局、邊框色、圖示（SVG）、所有文字與按鈕、tel: 連結
背景素材：無 — 淺灰底 + 頂部細黃橙條 CSS
前景素材：line-qr.png — 中央卡真實可掃 QR（非參考圖假 QR）
必須保留：三卡結構、手機紅字大號、LINE 綠、門市電話與屏東地址事實
允許偏差：桌面三欄 / 手機直向堆疊；QR 用名片真碼
風險觸發：禁止高雄等幻覺；LINE QR 必須來自 business-card 真碼
```

| 元素 | 角色 | 決策 | 來源 |
|------|------|------|------|
| 三張白卡 + 文案 | content-card | code-native | HTML/CSS |
| 電話 / 座機 icon | 圖示 | code-native | inline SVG |
| LINE icon | 圖示 | code-native | 簡化綠圓 SVG 或官方色塊字 |
| LINE QR | identity / 可掃碼 | find/copy | 從 `business-card.jpg` 裁切真 QR → `assets/line-qr.png` |
| 頂部細色條 | static-decor | code-native | CSS |

**交互假設（推薦）：**  
- 卡1 → `tel:0909750013`  
- 卡2 → 若有 LINE URL 則開啟；否則放大顯示 QR  
- 卡3 → `tel:087335666`  

**備選：** 三卡皆僅展示、底部另做固定 CTA bar。

---

### 03 · 信任／證照（`03-trust.jpg`）

```text
參考圖：03-trust.jpg
代碼層：徽章 chips、店名、證照字號、文傳團隊/主任標籤、地址黃卡文字、右側簡圖可用 CSS 小地圖示意或省略
背景素材：無
前景素材：無（官方認證徽章用 CSS/emoji/簡單 SVG，不偽造內政部印章圖）
必須保留：店名全文、證照 (111)登字第414195號、地址廣東路1293號
允許偏差：參考圖右側「假小地圖插畫」改為 code 黃卡 + 地圖 pin SVG，或併入 05
風險觸發：不生成假「內政部」徽章點陣圖；可用文字「合法執照」chip
```

| 元素 | 決策 | 備註 |
|------|------|------|
| 驗證 chips | code-native | 綠勾 + 文字即可 |
| 證照 / 店名 | code-native | 名片事實 |
| 地址黃卡 | code-native | 可連到地圖 |
| 假官方章圖 | cut / code-native 文字 | 不複製不明章 |

**交互假設（推薦）：** 地址卡點擊 → 開啟 Google Maps。靜態徽章。

---

### 04 · 社群（`04-social.jpg`）

```text
參考圖：04-social.jpg
代碼層：標題「追蹤溫蒂」、FB/TikTok 兩條橫卡、品牌色圓點裝飾、Follow 按鈕樣式
背景素材：無 — 底波浪 CSS
前景素材：無
必須保留：顯示名「屏東買好房丨金牌房仲溫蒂」
允許偏差：去掉參考圖假 @handle；有 URL 才可點，否則顯示文字 + 禁用態
風險觸發：無真實 URL 時不要連到錯誤帳號
```

| 元素 | 決策 | 狀態 |
|------|------|------|
| 雙橫條 UI | code-native | ready |
| FB / TikTok 官方標色 | code-native SVG | ready |
| 帳號 URL | replace-later | 使用者可補；否則純文字 |

**交互假設（推薦）：** 有 URL 才 `target=_blank`；無則 `aria-disabled`。

---

### 05 · 門市＋頁尾（`05-store-footer.jpg`）

```text
參考圖：05-store-footer.jpg
代碼層：區塊標題、黃底資訊帶、電話/傳真/證照文字、導航按鈕
背景素材：無
前景素材：無 — 地圖用 iframe 或「開啟地圖」外連，不用烘焙地圖截圖
必須保留：店名、屏東縣屏東市廣東路1293號、店電、傳真、證照
允許偏差：可精簡傳真；地圖用 Google Maps embed（需網路）或僅按鈕
風險觸發：embed 金鑰/政策 — 預設用 `https://maps.google.com/?q=...` 外連最穩
```

| 元素 | 決策 | 來源 |
|------|------|------|
| 地圖區 | code-native | 外連或 embed，非生成圖 |
| 黃底 footer 文案 | code-native | 名片 |
| 開啟地圖導航 | code-native | 連結 |

**交互假設（推薦）：** 主按鈕開 Google Maps 導航；電話可點。

---

## 素材清單（Asset Manifest）

| ID | 素材 | 層 | 角色 | 長寬比 | 約佔寬 | 來源 | 狀態 | 目標路徑 |
|----|------|----|------|--------|--------|------|------|----------|
| A1 | 半身肖像（圓裁） | 前景 | identity | 1:1 | Hero ~36% | 使用者 `portrait-circle.jpg` | find/copy | `assets/portrait.png` |
| A2 | LINE 可掃 QR | 前景 | media-slot | 1:1 | 聯絡卡中 ~40% 卡寬 | 使用者 `business-card.jpg` 裁切 | find/copy | `assets/line-qr.png` |
| A3 | 永義房屋 logo | 前景/identity | identity | ~1:1 | Hero 頂 ~8–12% | 名片裁切或 SVG 重繪 | find/copy | `assets/yongyi-logo.png` 或 `logo.svg` |
| A4 | 黃橙波浪/色帶 | 背景 | static-decor | — | 全幅 | — | code-native | — |
| A5 | 圖示組（電話/LINE/地圖 pin） | — | UI | — | — | — | code-native | inline SVG |
| A6 | 地圖視覺 | — | media-slot | 16:9 | 分區 ~100% 寬 | — | code-native | Maps 連結/embed |
| A7 | FB/TikTok 裝飾 | — | static-decor | — | — | — | code-native | CSS + SVG |

### 不生成（generate = 0）

本專案**不需要** AI 生成裝飾圖：方向 A 以品牌色塊 + 真實肖像 + 真 QR 為主。第四步僅做 **find/copy 整理**（裁切 QR、輸出 portrait、可選 logo），不開圖生。

### 被阻塞 / 待補

| 項 | 狀態 | 說明 |
|----|------|------|
| LINE 加入網址 | replace-later | 有則按鈕直達；無則只顯示 QR |
| FB / TikTok URL | replace-later | 有則可點；無則純文字 |
| 永義 logo 高清檔 | 可選 | 無則用名片裁切或簡化 SVG |

---

## 面向實作的頁面結構（確認後第五步用）

```text
單頁 index
1. header/hero
2. section#contact
3. section#trust
4. section#social
5. section#store + footer
```

技術傾向（確認後再定）：純靜態 HTML + CSS（可單檔），零建置，方便傳 LINE / Hosting。

---

## 第三步確認清單

請使用者確認：

1. 代碼原生 vs 素材邊界（上表）  
2. 僅整理 A1 肖像、A2 真 QR、（可選）A3 logo — **不 AI 生成新圖**  
3. 真人臉 / 真 QR / 品牌標 **禁止生成替身**  
4. 交互：tel + LINE QR + 地圖外連為預設  
5. 社群 URL、LINE URL 可之後再補（replace-later）  
