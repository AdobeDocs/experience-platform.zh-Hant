---
keywords: Experience Platform; home；熱門主題；分段；分段；分段服務；pql;PQL；配置檔案查詢語言；映射函式；映射；
solution: Experience Platform
title: PQL映射函式
topic: developer guide
description: 描述檔查詢語言(PQL)提供函式，讓與地圖的互動更輕鬆。
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 5%

---


# 地圖函式

[!DNL Profile Query Language] (PQL)提供函式，讓與地圖的互動更輕鬆。有關其他PQL函式的詳細資訊，請參閱[[!DNL Profile Query Language] overview](./overview.md)。

## 取得

`get`函式用於檢索給定鍵的映射值。

**Format**

```sql
{MAP}.get({STRING})
```

**範例**

以下PQL查詢獲取鍵`example@example.com`的標識映射值。

```sql
identityMap.get("example@example.com")
```

## 按鍵

`keys`函式用於檢索給定映射的所有鍵。

**格式**

```sql
{MAP}.keys()
```

**範例**

以下PQL查詢獲取映射`identityMap`的所有鍵。

```sql
identityMap.keys()
```

## 值

`values`函式用於檢索給定映射的所有值。

**格式**

```sql
{MAP}.values()
```

**範例**

以下PQL查詢獲取映射`identityMap`的所有值。

```sql
identityMap.values()
```

## 後續步驟

現在，您已經瞭解了映射函式，可以在PQL查詢中使用它們。 有關其他PQL函式的詳細資訊，請閱讀[配置檔案查詢語言概述](./overview.md)。
