---
solution: Experience Platform
title: PQL對應函式
description: 設定檔查詢語言(PQL)提供的函式可讓您更輕鬆地與地圖互動。
exl-id: f23616f2-c0dd-40ce-8cfc-c757542fbd05
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 7%

---

# 地圖函式

[!DNL Profile Query Language] (PQL)提供的函式可讓您更輕鬆地與地圖互動。 如需其他PQL函式的詳細資訊，請參閱 [[!DNL Profile Query Language] 概述](./overview.md).

## 取得

此 `get` 函式來擷取給定索引鍵的對映值。

**格式**

```sql
{MAP}.get({STRING})
```

**範例**

以下PQL查詢取得索引鍵的身分對應值 `example@example.com`.

```sql
identityMap.get("example@example.com")
```

## 金鑰

此 `keys` 函式來擷取給定對應的所有索引鍵。

**格式**

```sql
{MAP}.keys()
```

**範例**

以下PQL查詢取得對應的所有索引鍵 `identityMap`.

```sql
identityMap.keys()
```

## 值

此 `values` 函式來擷取給定對應的所有值。

**格式**

```sql
{MAP}.values()
```

**範例**

下列PQL查詢取得對應的所有值 `identityMap`.

```sql
identityMap.values()
```

## 後續步驟

現在您已瞭解對應函式，可以在PQL查詢中使用它們。 如需其他PQL函式的詳細資訊，請參閱 [設定檔查詢語言概觀](./overview.md).
