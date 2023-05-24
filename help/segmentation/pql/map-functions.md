---
keywords: Experience Platform；首頁；熱門主題；分段；分段；分段服務；PQL;PQL；配置檔案查詢語言；映射函式；映射；
solution: Experience Platform
title: PQL映射函式
description: 配置檔案查詢語言(PQL)提供使與映射的交互更容易的函式。
exl-id: f23616f2-c0dd-40ce-8cfc-c757542fbd05
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 6%

---

# 地圖函式

[!DNL Profile Query Language] (PQL)提供使與映射的交互更容易的功能。 有關其他PQL函式的詳細資訊，請參閱 [[!DNL Profile Query Language] 概述](./overview.md)。

## 取得

的 `get` 函式用於檢索給定鍵的映射值。

**格式**

```sql
{MAP}.get({STRING})
```

**範例**

以下PQL查詢獲取密鑰的標識映射值 `example@example.com`。

```sql
identityMap.get("example@example.com")
```

## 鍵

的 `keys` 函式用於檢索給定映射的所有鍵。

**格式**

```sql
{MAP}.keys()
```

**範例**

以下PQL查詢獲取映射的所有鍵 `identityMap`。

```sql
identityMap.keys()
```

## 值

的 `values` 函式用於檢索給定映射的所有值。

**格式**

```sql
{MAP}.values()
```

**範例**

以下PQL查詢獲取映射的所有值 `identityMap`。

```sql
identityMap.values()
```

## 後續步驟

現在您已經瞭解了映射函式，可以在PQL查詢中使用它們。 有關其他PQL功能的詳細資訊，請閱讀 [配置檔案查詢語言概述](./overview.md)。
