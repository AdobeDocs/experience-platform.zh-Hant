---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;identity;datatype;data-type;data type;
solution: Experience Platform
title: 身分資料類型
topic: overview
description: 本文檔概述了Identity XDM資料類型。
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 2%

---


# [!UICONTROL 身分資料] 類型

[!UICONTROL Identity] 是標準的XDM資料類型，用來清楚區分與數位體驗互動的人。 身分由身分提供者建立，其本身在屬性中 `namespace` 參考。 在每個組 `namespace`件中，身份都是唯一的。

<img src="../images/data-types/identity.png" width="550" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `namespace` | 物件 | 包含單一字串欄位(`code`)的物件，指出與所提供屬性相關聯的命名空 `id` 間。 |
| `authenticatedState` | 字串 | 在觀察到的體驗事件時，此身分的已驗證狀態。 請參閱附 [錄](#authenticatedState) ，瞭解接受的值和定義。 |
| `id` | 字串 | 相關名稱空間中的消費者身份。 |
| `primary` | 布林值 | 指出這是否為個人的主要身分。 每個個人只能有一個主要身份。 |
| `xid` | 字串 | 當存在時，此值表示跨名稱空間標識符，該標識符在所有名稱空間中所有命名空間範圍內的標識符中都是唯一的。 |

有關混音的詳細資訊，請參閱公用XDM存放庫：

* [填入的範例](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.schema.json)

## 附錄

以下部分包含有關 [!UICONTROL Identity] 資料類型的其他資訊。

## authenticatedState的接受值 {#authenticatedState}

下表概述接受的值及其 `authenticatedState` 相關意義：

| 值 | 說明 |
| --- | --- |
| `ambiguous` | 驗證狀態是不明確的。 |
| `authenticated` | 使用者是透過登入或事件觀察時有效的類似動作來識別。 |
| `loggedOut` | 使用者在先前某個時間點由登入動作識別，但在事件觀察時未登入。 |