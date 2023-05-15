# 學呀平臺資源 API - Beta 

我們還在想辦法讓伺服器安全地開放 CORS 給特定的接點 🥲

[此 API 文件的 GitHub](https://github.com/zetria-org/public-api)

學呀成立於 2019 年，任務為「整合零散於網路上教育資源項目，並藉由開放式的線上教科書，拉近學生與教育資源間的距離。」歷經第一個版本的開發後，學呀於 2022 年底開始重新整建，至 2023 年中已經完成大部分的開發。

為了吸引更多志同道合的合作夥伴投入教育科技的領域，並且希望更多人能重視新興科技教材對教育所造成的影響，學呀將部分的 API 開放讓大眾能夠使用。這個檔案將描述學呀平臺資源 API 的使用方法。

> ⚠️ 注意：使用學呀的資源 API 即代表您同意學呀的[服務條款和隱私政策](https://zetria.tw/announcement)。學呀不保證 API 的持續運作和正確性。目前此 API 尚在 Beta 測試階段，此檔案描述的規格可能會有所改變，請您留意。
  
---
  
## API 基本資訊

學呀平臺資源 API 基底網址為 `https://use.zetria.tw`，請務必以 `https` 的方式連接。在此網址之上有各不同的 API 端點，分別有著不同的功能。此處列出目前開放大眾使用的各 API 端點和其功能概述：

測試用：

- [`/test_connection`](#test_connection)：測試與伺服器之連結，確認伺服器狀態。

開放式課程：

- [`/courses`](#courses)：獲取所有科目的概略內容。
- [`/course/<str:course_id>`](#coursestrcourse_id)：獲取對應 `course_id` 的科目。
- [`/section/<str:section_id>`](#sectionstrsection_id)：獲取對應 `section_id` 的單元資訊。
- [`/chapters`](#chapters)：獲取所有章節的概略內容。
- [`/chapter/<str:chapter_id>`](#chapterstrchapter_id)：獲取對應 `chapter_id` 的章節。

教育資源項目：

- [`/shared_items/images`](#shared_itemsimages)：獲取所有圖庫中的圖片資訊。
- [`/shared_item/<int:id>`](#shared_itemintid)：獲取對應 `id` 的分享資源項目。
- [`/shared_item/search`](#shared_itemsearch)：搜尋分享資源項目。

---
   
## API 詳細使用說明

### `/test_connection`

使用 `GET` 方法，將回傳：
```json
{
  "status": "success",
  "detail": "GET method is working :)"
}
```

---

### `/chapter/<str:chapter_id>`

使用 `GET` 方法，將回傳：
```json
{
  "chapter_id": <str>,
  "chapter_name": <str>,
  "chapter_type": <str>,
  "chapter_content": <str>,
  "chapter_questions": <list<str>>,
  "chapter_tags": <list<str>>,
  "chapter_importance": <int> 
}
```
回傳的資料內容解釋，請見 [Model｜Chapter](#modelchapter)

---

### `/chapters`

使用 `GET` 方法，將回傳：
```json
[
  {
    "chapter_id": <str>,
    "chapter_name": <str>,
    "chapter_type": <str>,
    "chapter_tags": <list<str>>
  },
  // ...
]
```
回傳的資料內容解釋，請見 [Model｜Chapter](#modelchapter)

---

### `/shared_items/images`

使用 `GET` 方法，將回傳：
```json
[
  {
    "id": <int>,
    "shared_item_name": <str>,
    "shared_item_type": <str>,
    "shared_item_approved": <bool>,
    "shared_item_content": <str>,
    "shared_item_tags": <list<str>>,
    "shared_item_upvote": <int>,
  }, 
  // ...
]
```
回傳的資料內容解釋，請見 [Model｜Shared Item](#modelshared-item)

---

### `/shared_item/<int:id>`

使用 `GET` 方法，將回傳：
```json
{
  "id": <int>,
  "shared_item_name": <str>,
  "shared_item_type": <str>,
  "shared_item_approved": <bool>,
  "shared_item_content": <str>,
  "shared_item_tags": <list<str>>,
  "shared_item_upvote": <int>,
}
```
回傳的資料內容解釋，請見 [Model｜Shared Item](#modelshared-item)

---

### `/shared_item/search`

使用 `GET` 方法，將回傳：
```json
[
  {
    "id": <int>,
    "shared_item_name": <str>,
    "shared_item_type": <str>,
    "shared_item_approved": <bool>,
    "shared_item_content": <str>,
    "shared_item_tags": <list<str>>,
    "shared_item_upvote": <int>,
  }, 
  // ...
]
```
回傳的資料內容解釋，請見 [Model｜Shared Item](#modelshared-item)

---

### `/course/<str:course_id>`

使用 `GET` 方法，將回傳：
```json
{
  "course_id": <str>,
  "course_name": <str>,
  "course_category": <str>,
  "course_description": <str>,
  "sections": [
    {
      "section_name": <str>, 
      "section_id": <str>, 
      "chapters": [
        {
          "chapter_type": <str>, 
          "chapter_name": <str>, 
          "chapter_id": <str>, 
          "chapter_tags": <list<str>>,
        },
        // ...
      ]
    }, 
    // ...
  ]
}
```
回傳的資料內容解釋，請見 [Model｜Course](#modelcourse)

---

### `/courses`

使用 `GET` 方法，將回傳：
```json
[
  {
    "course_id": <str>,
    "course_name": <str>,
    "course_category": <str>,
    "course_description": <str>,
    "sections": <list<str:section_id>>,
  },
  // ...
]
```
回傳的資料內容解釋，請見 [Model｜Course](#modelcourse)

---

### `/section/<str:section_id>`
```json
{
  "section_name": <str>, 
  "section_id": <str>, 
  "chapters": [
    {
      "chapter_type": <str>, 
      "chapter_name": <str>, 
      "chapter_id": <str>, 
      "chapter_tags": <list<str>>,
    }
    // ...
  ]
}
```
回傳的資料內容解釋，請見 [Model｜Section](#modelsection)

---
   
## API 回傳內容結構

### Model｜Chapter
| Key | Value Type | Explanation |
| --- | --- | --- |
| `chapter_id` | `str` | 章節的編號 |
| `chapter_name` | `str` | 章節的名稱 |
| `chapter_type` | `str` | 章節的類別 | 
| `chapter_content` | `str` | 章節的內容 |
| `chapter_questions` | `list<str>` | 章節對應的的題目編號 |
| `chapter_tags` | `list<str>` | 章節的相關標籤 | 
| `chapter_importance` | `int` | 章節的重要性 |

其中的 `chapter_type` 和 `chapter_content` 關係如下：

| `chapter_type` | Meaning | 
| --- | --- |
| `md` | `chapter_content` 的格式為[學呀擴充的教育用 Markdown 標準](https://github.com/zetria-org/edu-md)。
| 待決定 | 待決定 |

> 注意：`chapter_content` 中的圖片網址可能包含已不符時宜的網址。在獲取回覆後，請將其取代為新網址（`chapter_content.replace(old_url_regex g, "new_url")`即可）。舊網址有：
> - https://zetria-images.ap-south-1.linodeobjects.com
> - https://zetria.org/content_img
> - https://www.zetria.org/content_img  
> 
> 新網址為：https://raw.githubusercontent.com/zetria-org/content/main/images 。

---

### Model｜Section
| Key | Value Type | Explanation |
| --- | --- | --- |
| `section_id` | `str` | 單元的編號 |
| `section_name` | `str` | 單元的名稱 |
| `chapters` | `list<Chapter>` | 單元中所包含的所有章節，章節資訊包含了 `chapter_type` 、 `chapter_id` 、 `chapter_type` 、 `chapter_tags` ，其意義在 [Model｜Chapter](#modelchapter) 中有所解釋。 |
---

### Model｜Course

| Key | Value Type | Explanation |
| --- | --- | --- |
| `course_id` | `str` | 課程（即科目）的編號 |
| `course_name` | `str` | 課程（即科目）的名稱 |
| `course_category` | `str` | 課程（即科目）的名稱 |
| `course_description` | `str` | 課程（即科目）的名稱 |
| `sections` | `list<Section>` | 課程（即科目）所包含的章節。章節資料的結構在 [Model｜Section](#modelsection) 中有所解釋。

---

### Model｜Shared Item
| Key | Value Type | Explanation |
| --- | --- | --- |
| `id` | `int` | 資源項目的編號 |
| `shared_item_name` | `str` | 資源項目的名稱 |
| `shared_item_type` | `str` | 資源項目的類別 |
| `shared_item_approved` | `bool` | 資源項目是否通過審查 |
| `shared_item_content` | `str` | 資源項目的內容 |
| `shared_item_tags` | `list<str>` | 資源項目的相關標籤 |
| `shared_item_upvote` | `int` | 資源項目的點讚數量 |

