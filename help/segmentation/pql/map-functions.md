---
solution: Experience Platform
title: PQL Map函式
description: Profile Query Language (PQL)提供的功能可讓您更輕鬆地與地圖互動。
exl-id: f23616f2-c0dd-40ce-8cfc-c757542fbd05
source-git-commit: c4d034a102c33fda81ff27bee73a8167e9896e62
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 5%

---

# 地圖函式

[!DNL Profile Query Language] (PQL)提供可讓您更輕鬆與地圖互動的功能。 如需其他PQL函式的詳細資訊，請參閱[[!DNL Profile Query Language] 總覽](./overview.md)。

## 取得

`get`函式用來擷取特定索引鍵對應值，做為物件。

**格式**

```sql
{MAP}.get({STRING})
```

**範例**

下列PQL查詢取得索引鍵`example@example.com`的身分對應值。

```sql
identityMap.get("example@example.com")
```

## 索引鍵

`keys`函式用來以陣列或清單形式擷取給定對應的所有索引鍵。

**格式**

```sql
{MAP}.keys()
```

**範例**

下列PQL查詢取得對應`identityMap`的所有索引鍵。

```sql
identityMap.keys()
```

## 值

`values`函式用來以陣列或清單形式擷取給定對應的所有值。

**格式**

```sql
{MAP}.values()
```

**範例**

下列PQL查詢取得對應`identityMap`的所有值。

```sql
identityMap.values()
```

## 後續步驟

現在您已瞭解對應函式，可以在PQL查詢中使用它們。 如需其他PQL功能的詳細資訊，請參閱[Profile Query Language概觀](./overview.md)。
