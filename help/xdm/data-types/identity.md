---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；結構；身分；資料類型；資料類型；
solution: Experience Platform
title: 身分資料類型
topic-legacy: overview
description: 本檔案概述Identity XDM資料類型。
exl-id: fb02b6b4-255b-442f-895c-600022231a1c
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 4%

---

#  Identitydata類型

 Identity是標準的XDM資料類型，可用來清楚區分與數位體驗互動的使用者。標識由標識提供程式建立，該提供程式本身在`namespace`屬性中引用。 在每個`namespace`中，標識是唯一的。

<img src="../images/data-types/identity.png" width="550" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `namespace` | 物件 | 包含單字串欄位(`code`)的對象，它指示與提供的`id`屬性關聯的命名空間。 |
| `authenticatedState` | 字串 | 觀察到的體驗事件時此身分的已驗證狀態。 有關接受的值和定義，請參閱[附錄](#authenticatedState)。 |
| `id` | 字串 | 相關命名空間中的消費者身分。 |
| `primary` | 布林值 | 指出這是否為個人的主要身分。 每個個人只能有一個主要身分。 |
| `xid` | 字串 | 如果存在，此值代表跨命名空間識別碼，此識別碼在所有命名空間中所有命名空間範圍的識別碼中都是唯一的。 |

{style=&quot;table-layout:auto&quot;}

如需資料類型的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.schema.json)

## 附錄

下節包含有關[!UICONTROL Identity]資料類型的其他資訊。

## authenticatedState的接受值 {#authenticatedState}

下表概述`authenticatedState`的接受值及其相關含義：

| 值 | 說明 |
| --- | --- |
| `ambiguous` | 驗證狀態不明確。 |
| `authenticated` | 使用者是透過登入或事件觀察時有效的類似動作來識別。 |
| `loggedOut` | 先前某個時間點的登入動作已識別使用者，但事件觀察時並未登入。 |
