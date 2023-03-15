---
title: 排序Reactor API中的回應
description: 了解在Reactor API中列出資源時如何篩選結果。
exl-id: 49dcf0b6-4ce8-41d9-9e3a-e44f5c0ff905
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---

# 在Reactor API中排序回應

列出Reactor API中的端點，可讓您根據指定的屬性來排序傳回的資源。 您可以提供 `sort` 參數。

## 遞增排序

通過指定要排序的屬性並用前置詞來按屬性遞增順序排序資源 `+`:

`GET /companies/:company_id/properties?sort=+name`

## 降序排序

通過指定要排序的屬性並用前置詞來按屬性降序排序資源 `-`:

`GET /companies/:company_id/properties?sort=-name`

## 多項排序

要按多個值排序，請以逗號分隔清單提供排序指令：

`GET /companies/:company_id/properties?sort=+name,-org_id`
