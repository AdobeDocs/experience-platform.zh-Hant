---
title: 排序Reactor API中的回應
description: 瞭解如何在Reactor API中列出資源時篩選結果。
exl-id: 49dcf0b6-4ce8-41d9-9e3a-e44f5c0ff905
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---

# 排序Reactor API中的回應

列出Reactor API中的端點，可讓您根據指定的屬性排序傳回的資源。 您可以在要求路徑中提供`sort`引數，以設定回應的排序順序。

## 升序排序

資源可透過指定
排序依據的屬性，並以`+`加上前置詞：

`GET /companies/:company_id/properties?sort=+name`

## 降序排序

資源可透過指定
排序依據的屬性，並以`-`加上前置詞：

`GET /companies/:company_id/properties?sort=-name`

## 多重排序

若要依多個值排序，請以逗號分隔的方式提供排序指令
清單：

`GET /companies/:company_id/properties?sort=+name,-org_id`
