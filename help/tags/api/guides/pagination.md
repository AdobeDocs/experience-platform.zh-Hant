---
title: 在Reactor API中為回應分頁
description: 了解在Reactor API中列出資源時，如何對結果分頁。
exl-id: bccb6e78-4ac8-4786-b398-6e55109d99dd
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 0%

---

# 在Reactor API中為回應分頁

Reactor API傳回的回應會編頁。 預設頁面大小為25個元素。 分頁的詳細資訊會報告於 `meta.pagination `API回應物件的區段：

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

您可以取得特定頁面，並借由加入 `page` 請求路徑中的查詢參數。

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
