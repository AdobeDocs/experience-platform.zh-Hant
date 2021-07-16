---
title: 在Reactor API中為回應分頁
description: 了解在Reactor API中列出資源時，如何對結果分頁。
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 0%

---

# 在Reactor API中為回應分頁

Reactor API傳回的回應會編頁。 預設頁面大小為25個元素。 有關分頁的詳細資訊會報告在API回應物件的`meta.pagination `區段中：

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

您可以在請求路徑中加入`page`查詢參數，以取得特定頁面並修改頁面大小。

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

不同的選項可以結合在一起：

```http
GET /{RESOURCE_TYPE}/{RESOURCE_ID}?page[size]={PAGE_SIZE}&page[number]={PAGE_NUMBER}
```
