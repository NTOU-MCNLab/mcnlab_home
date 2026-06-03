
# 實驗室網站靜態資料

所有靜態頁面的資料都以JSON格式存放在此Repo。若要進行新增、修改、刪除，直接在此處更新即可，無須再對原網頁程式修改。

 - [更新規則](#更新規則)
 - [資料說明](#資料說明)

## 更新規則

 1. 請勿擅自新增或刪除已定義的欄位，必需遵守既有的規則更新資料。
 2. 更新後的資料需符合JSON格式，否則將前端將解析錯誤。
 3. 空值以空字串表示("")，不可null或留空。
 4. 成員照片壓縮至92x128，圖片格式為WebP，並放置於```/public/images/members```
 5. 實驗室照片壓縮至368x276，圖片格式為WebP，並放置於```/public/images/lab or party```

## 資料說明

### [home.json](/static/home.json)
 1. labAwards
 獲獎訊息，位於首頁左上
 ```json
 "labAwards": [
    {
      "text": "標題"
    }
 ]
```
 2. activities
 實驗室動態，位於首頁左中
 ```json
 "activities": [
    {
      "text": "標題"
    }
 ]
```
 3. conferences
 研討會訊息，位於首頁左下
 ```json
 "conferences": [
    {
      "text": "標題",
      "href": "https://連結/"
    }
]
```
 4. advisorAwards
 榮譽獎勵，位於首頁右下
 ```json
"advisorAwards": [
    {
      "text": "標題"
    }
]
```
### [courses.json](/static/courses.json)
開課資訊
```json
[
  {
    "semester": "學年度",
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
### [research.json](/static/research.json)
 1. 期刊論文
```json
"journals": [
    {
      "title": "C.-F. Cheng*, J.-A. Lin, H.-J. Lan and G.-Y. Chen, \"Intelligent...",
      "sci": "IEEE Internet Things J.(SCI, 2024 Impact Factor: 8.9, Ranking: Top 4%, Q1)",
      "href": "https://ieeexplore.ieee.org/document/11199320"
    }
]
```
2. 會議論文
```json
"conferences": [
    {
      "title": "C.-F. Cheng and B.-Y. Liao, \"An Enhanced...",
      "href": "https://ieeexplore.ieee.org/document/10314280"
    }
]
```
3. 國科會計畫
```json
"nstc": [
    {
      "title": "資料收集與邊緣計算機制於具有..."
    }
]
```
### [members.json](/static/members.json)
1. 在學研究生
```json
"postgraduate": [
    {
      "name": "姓名",
      "dept": "資工碩士班",
      "period": "2023.08~迄今",
      "img": "photo.webp"
    }
]
```
2. 畢業生
```json
"graduate": [
    {
      "name": "姓名",
      "dept": "資訊工程學系碩士班",
      "period": "2023.08~2025.06",
      "img": "photo.webp",
      "unit": "服務單位"
    }
]
```
### [service.json](/static/service.json)
```json
{
  "journal": [
    {
      "text": "Journal Editorship"
    }
  ],
  "technical": [
    {
      "text": "Technical Committees"
    }
  ],
  "chairIntl": [
    {
      "text": "Chair - International Conference"
    },
   ],
   "sessionOrg": [
    {
      "text": "Special Session Organizer"
    }
  ],
  "program": [
    {
      "text": "Technical Program Committees"
    }
  ],
  "reviewerIntJ": [
    {
      "text": "Reviewer - International Journal"
    }
  ],
  "invited": [
    {
      "text": "Invited Talk"
    }
  ],
  "evaluation": [
    {
      "text": "Evaluation Committees"
    }
  ],
}
```
### [photo.json](/static/photo.json)
1. 聚餐照片
```json
"party" : [
        {
            "title": "肉次方 台北峨嵋店",
            "img": "/images/party/20250123.webp",
            "date": "2025/01/23"
        }
]
```
2. 實驗室照片
```json
"environment":[
        {
            "title": "實驗室環境1",
            "img": "/images/lab/lab1.webp"
        }
]
```
### [english.json](/static/english.json)
```json
[
  {
    "text": "Award for Recruiting..."
  }
]
```