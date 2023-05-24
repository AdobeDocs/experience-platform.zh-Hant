---
title: 在反應堆API中排序響應
description: 瞭解在Repartor API中列出資源時如何篩選結果。
exl-id: 49dcf0b6-4ce8-41d9-9e3a-e44f5c0ff905
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---

# 在反應器API中排序響應

在Reactor API中列出端點允許您根據指定的屬性對返回的資源進行排序。 通過提供 `sort` 參數。

## 升序排序

通過指定要排序的屬性，並使用 `+`:

`GET /companies/:company_id/properties?sort=+name`

## 降序排序

通過指定要排序的屬性，並使用 `-`:

`GET /companies/:company_id/properties?sort=-name`

## 多重排序

要按多個值排序，請將排序指令作為逗號分隔的清單提供：

`GET /companies/:company_id/properties?sort=+name,-org_id`
