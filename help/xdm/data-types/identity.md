---
keywords: Experience Platform;home；熱門主題；模式；模式；XDM;fields；模式；標識；資料類型；資料類型；
solution: Experience Platform
title: 身分資料類型
topic-legacy: overview
description: 本文檔概述了Identity XDM資料類型。
exl-id: fb02b6b4-255b-442f-895c-600022231a1c
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 3%

---

# [!UICONTROL Identity] 資料類型

[!UICONTROL Identity] 是標準的XDM資料類型，用來清楚區分與數位體驗互動的人。身分由身分提供者建立，身分提供者本身在`namespace`屬性中參考。 在每個`namespace`中，身分是唯一的。

<img src="../images/data-types/identity.png" width="550" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `namespace` | 物件 | 包含單一字串欄位(`code`)的物件，指出與所提供之`id`屬性相關的命名空間。 |
| `authenticatedState` | 字串 | 在觀察到的體驗事件時，此身分的已驗證狀態。 有關接受的值和定義，請參見[附錄](#authenticatedState)。 |
| `id` | 字串 | 相關名稱空間中的消費者身份。 |
| `primary` | 布林值 | 指出這是否為個人的主要身分。 每個個人只能有一個主要身份。 |
| `xid` | 字串 | 當存在時，此值表示跨名稱空間標識符，該標識符在所有名稱空間中所有命名空間範圍內的標識符中都是唯一的。 |

有關資料類型的詳細資訊，請參閱公共XDM儲存庫：

* [填入的範例](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.schema.json)

## 附錄

以下部分包含有關[!UICONTROL Identity]資料類型的其他資訊。

## authenticatedState {#authenticatedState}的接受值

下表概述`authenticatedState`的接受值及其相關含義：

| 值 | 說明 |
| --- | --- |
| `ambiguous` | 驗證狀態是不明確的。 |
| `authenticated` | 使用者是透過登入或事件觀察時有效的類似動作來識別。 |
| `loggedOut` | 使用者在先前某個時間點由登入動作識別，但在事件觀察時未登入。 |
