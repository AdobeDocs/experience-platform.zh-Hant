---
title: 排序Reactor API中的回應
description: 了解在Reactor API中列出資源時如何篩選結果。
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---

# 在Reactor API中排序回應

列出Reactor API中的端點，可讓您根據指定的屬性來排序傳回的資源。 您可以在請求路徑中提供`sort`參數，以設定回應的排序順序。

## 遞增排序

資源可以通過指定
要排序的屬性，並加上`+`前置詞：

`GET /companies/:company_id/properties?sort=+name`

## 降序排序

資源可以通過指定
要排序的屬性，並加上`-`前置詞：

`GET /companies/:company_id/properties?sort=-name`

## 多項排序

要按多個值排序，請以逗號分隔的形式提供排序指令
清單：

`GET /companies/:company_id/properties?sort=+name,-org_id`
