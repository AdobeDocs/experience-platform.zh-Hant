---
title: 在Reactor API中分頁回應
description: 瞭解在Reactor API中列出資源時，如何分頁結果。
exl-id: bccb6e78-4ac8-4786-b398-6e55109d99dd
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# 在Reactor API中分頁回應

Reactor API傳回的回應會分頁。 預設頁面大小為25個元素。 分頁的詳細資訊會在API回應物件的`meta.pagination `區段中報告：

```json
"meta": {
  "pagination": {
      "current_page": 1,
      "next_page": 2,
      "prev_page": null,
      "total_pages": 4,
      "total_count": 90
  }
}
```

可以在要求路徑中加入`page`查詢引數，以取得特定頁面並修改頁面大小。

## 擷取特定頁面

若要取得特定頁面：

```http
GET /{RESOURCE_TYPE}/{RESOURCE_ID}?page[number]={PAGE_NUMBER}
```

## 變更頁面大小

若要變更頁面大小：

```http
GET /{RESOURCE_TYPE}/{RESOURCE_ID}?page[size]={PAGE_SIZE}
```

不同的選項可以合併在一起：

```http
GET /{RESOURCE_TYPE}/{RESOURCE_ID}?page[size]={PAGE_SIZE}&page[number]={PAGE_NUMBER}
```
