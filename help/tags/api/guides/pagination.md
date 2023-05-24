---
title: 在反應器API中分頁響應
description: 瞭解如何在Repartor API中列出資源時分頁結果。
exl-id: bccb6e78-4ac8-4786-b398-6e55109d99dd
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '101'
ht-degree: 0%

---

# 在反應器API中分頁響應

Reactor API返回的響應被分頁。 預設頁面大小為25個元素。 有關分頁的詳細資訊，請參見 `meta.pagination `API響應對象的部分：

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

可以通過包含 `page` 請求路徑中的查詢參數。

## 檢索特定頁面

要獲取特定頁面：

```http
GET /{RESOURCE_TYPE}/{RESOURCE_ID}?page[number]={PAGE_NUMBER}
```

## 更改頁面大小

要更改頁面大小：

```http
GET /{RESOURCE_TYPE}/{RESOURCE_ID}?page[size]={PAGE_SIZE}
```

不同的選項可以組合在一起：

```http
GET /{RESOURCE_TYPE}/{RESOURCE_ID}?page[size]={PAGE_SIZE}&page[number]={PAGE_NUMBER}
```
