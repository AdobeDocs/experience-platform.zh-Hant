---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;pql;PQL;Profile Query Language;map functions;map;
solution: Experience Platform
title: 地圖函式
topic: developer guide
translation-type: tm+mt
source-git-commit: 17ef6c1c6ce58db2b65f1769edf719b98d260fc6
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 6%

---


# 地圖函式

[!DNL Profile Query Language] (PQL)提供函式，讓與地圖的互動更輕鬆。 有關其他PQL函式的詳細資訊，請參閱 [[!DNL Profile Query Language] 概述](./overview.md)。

## 取得

函 `get` 數用於檢索給定鍵的映射值。

**Format**

```sql
{MAP}.get({STRING})
```

**範例**

以下PQL查詢獲取密鑰的標識映射值 `example@example.com`。

```sql
identityMap.get("example@example.com")
```

## 按鍵

函式 `keys` 用於檢索給定映射的所有鍵。

**Format**

```sql
{MAP}.keys()
```

**範例**

以下PQL查詢獲取映射的所有鍵 `identityMap`。

```sql
identityMap.keys()
```

## 值

函 `values` 數用於檢索給定映射的所有值。

**Format**

```sql
{MAP}.values()
```

**範例**

以下PQL查詢獲取映射的所有值 `identityMap`。

```sql
identityMap.values()
```

## 後續步驟

現在，您已經瞭解了映射函式，可以在PQL查詢中使用它們。 有關其他PQL函式的詳細資訊，請閱讀配置式查 [詢語言概述](./overview.md)。
