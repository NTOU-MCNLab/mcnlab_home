
# MCN Lab 網站

**行動計算與網路實驗室（MCN Lab）** 的官方網站。

- 網址：[https://mcnlab.ntou.edu.tw](https://mcnlab.ntou.edu.tw)
- 技術架構：純靜態 HTML + CSS，內容資料以 JSON 格式存放於 `/static/`，頁面透過 JavaScript `fetch` 動態載入渲染。

**若只需要更新網站內容（公告、成員、論文等），只需編輯 `/static/` 裡的 JSON 檔案即可，不需要動 HTML 或 CSS。**

---

## 目錄

- [資料夾結構](#資料夾結構)
- [本地測試](#本地測試)
- [部署流程](#部署流程)
- [更新規則](#更新規則)
- [常見操作步驟](#常見操作步驟)
- [資料說明](#資料說明)

---

## 資料夾結構

```
/
├── index.html          # 首頁
├── teaching.html       # 教學
├── research.html       # 研究
├── service.html        # 服務
├── members.html        # 成員
├── eng.html            # English（英文版個人頁）
├── album.html          # 照片集
├── style.css           # 全站樣式
├── static/             # ← 網站內容資料（JSON），一般更新只需改這裡
│   ├── home.json       # 首頁公告（獲獎、動態、研討會）
│   ├── courses.json    # 開課資訊
│   ├── research.json   # 期刊／會議論文、國科會計畫
│   ├── members.json    # 成員名單
│   ├── service.json    # 學術服務
│   ├── photo.json      # 照片集（聚餐、實驗室環境）
│   └── english.json    # 英文頁獲獎清單
└── images/
    ├── members/        # 成員照片（92×128 px，WebP）
    ├── party/          # 聚餐照片（368×276 px，WebP）
    └── Lab/            # 實驗室環境照片（368×276 px，WebP）
```

---

## 本地測試

直接以瀏覽器開啟 HTML 檔案**無法**測試，因為 `fetch('/static/...')` 在 `file://` 協定下會被 CORS 擋住。請用以下任一方式啟動本地伺服器：

**方法一：Python（不需安裝額外套件）**
```bash
python -m http.server 8080
```
瀏覽器開啟 `http://localhost:8080`

**方法二：VS Code Live Server 擴充套件**
安裝 [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer)，右鍵點 HTML 檔案 → `Open with Live Server`

---

## 部署流程

修改完 JSON（或其他檔案）後：

```bash
git add .
git commit -m "說明這次改了什麼"
git push
```

push 後伺服器會自動更新，稍候幾秒重新整理網站即可看到變更。

---

## 更新規則

1. 請勿擅自新增或刪除已定義的欄位，必須遵守既有的格式更新資料。
2. 更新後的資料必須符合 JSON 格式，否則前端將解析錯誤（可用 [jsonlint.com](https://jsonlint.com) 驗證）。
3. 空值以空字串表示（`""`），不可用 `null` 或留空。
4. 成員照片規格：**92×128 px，WebP 格式**，放置於 `/images/members/`
5. 聚餐／實驗室照片規格：**368×276 px，WebP 格式**，放置於 `/images/party/` 或 `/images/Lab/`

---

## 常見操作步驟

### 新增在學研究生

1. 準備大頭照，壓縮至 **92×128 px**，轉為 **WebP** 格式
2. 命名規則：`{入學年份}-{英文名縮寫}.webp`
   - 例：113 學年入學、姓名 Chang Cheng-Yu → `113-cychang.webp`
3. 將照片放到 `/images/members/`
4. 在 `static/members.json` 的 `postgraduate` 陣列新增一筆（`img` 只填檔名，不含路徑）：
   ```json
   {
     "name": "姓名",
     "dept": "資工碩士班",
     "period": "2024.08~迄今",
     "img": "113-cychang.webp"
   }
   ```
5. `git add`、`git commit`、`git push`

### 研究生畢業

將該筆資料從 `postgraduate` 移到 `graduate`，並補上 `unit` 欄位：
```json
{
  "name": "姓名",
  "dept": "資工碩士班",
  "period": "2022.08~2024.06",
  "img": "111-example.webp",
  "unit": "服務單位（可留空字串）"
}
```

### 新增聚餐照片

1. 準備照片，壓縮至 **368×276 px**，轉為 **WebP** 格式
2. 命名規則：`YYYYMMDD.webp`（聚餐日期）
3. 將照片放到 `/images/party/`
4. 在 `static/photo.json` 的 `party` 陣列**最前面**新增一筆（最新的放最上面）：
   ```json
   {
     "title": "餐廳名稱",
     "img": "/images/party/20251201.webp",
     "date": "2025/12/01"
   }
   ```

### 更新首頁公告

編輯 `static/home.json`，對應區塊如下：

| 欄位 | 首頁位置 |
|---|---|
| `labAwards` | 左欄「獲獎訊息」 |
| `activities` | 左欄「實驗室動態」 |
| `conferences` | 左欄「研討會訊息」 |
| `advisorAwards` | 右欄「榮譽獎勵」 |

---

## 資料說明

### [home.json](/static/home.json)

```json
{
  "labAwards": [
    { "text": "獎項描述" }
  ],
  "activities": [
    { "text": "動態描述" }
  ],
  "conferences": [
    {
      "text": "研討會名稱",
      "href": "https://研討會網址/"
    }
  ],
  "advisorAwards": [
    { "text": "獎項描述" }
  ]
}
```

---

### [courses.json](/static/courses.json)

```json
[
  {
    "semester": "113-2",
    "course": [
      {
        "name": "課名",
        "department": "開課單位",
        "credit": 3
      }
    ]
  }
]
```

---

### [research.json](/static/research.json)

`href` 為選填（無 DOI 連結時可省略）。

```json
{
  "journals": [
    {
      "title": "完整論文引用格式",
      "sci": "期刊名稱（Impact Factor、Ranking 等）",
      "href": "https://ieeexplore.ieee.org/..."
    }
  ],
  "conferences": [
    {
      "title": "完整論文引用格式",
      "href": "https://ieeexplore.ieee.org/..."
    }
  ],
  "nstc": [
    { "title": "計畫名稱" }
  ]
}
```

---

### [members.json](/static/members.json)

> **注意：** `img` 欄位只填**檔名**，不含路徑前綴（程式會自動補上 `/images/members/`）。

```json
{
  "postgraduate": [
    {
      "name": "姓名",
      "dept": "資工碩士班",
      "period": "2024.08~迄今",
      "img": "113-cychang.webp"
    }
  ],
  "graduate": [
    {
      "name": "姓名",
      "dept": "資訊工程學系碩士班",
      "period": "2022.08~2024.06",
      "img": "111-example.webp",
      "unit": "服務單位"
    }
  ]
}
```

---

### [service.json](/static/service.json)

```json
{
  "journal": [
    { "text": "Journal Editorship 說明" }
  ],
  "technical": [
    { "text": "Technical Committees 說明" }
  ],
  "chairIntl": [
    { "text": "Chair - International Conference 說明" }
  ],
  "sessionOrg": [
    { "text": "Special Session Organizer 說明" }
  ],
  "program": [
    { "text": "Technical Program Committees 說明" }
  ],
  "reviewerIntJ": [
    {
      "publisher": "出版商名稱（如 IEEE）",
      "journals": [
        { "text": "期刊名稱" }
      ]
    }
  ],
  "invited": [
    { "text": "Invited Talk 說明" }
  ],
  "evaluation": [
    { "text": "Evaluation Committees 說明" }
  ]
}
```

---

### [photo.json](/static/photo.json)

> **注意：** `img` 欄位填**完整路徑**（含 `/images/` 前綴）。

```json
{
  "party": [
    {
      "title": "餐廳名稱",
      "img": "/images/party/20251201.webp",
      "date": "2025/12/01"
    }
  ],
  "environment": [
    {
      "title": "照片說明",
      "img": "/images/Lab/lab1.webp"
    }
  ]
}
```

---

### [english.json](/static/english.json)

指導教授個人獲獎清單，顯示於 `eng.html` 的 Awards 區塊。

```json
[
  { "text": "Award name, Institution, Year" }
]
```
