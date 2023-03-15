---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；結構；身分；資料類型；資料類型；
solution: Experience Platform
title: 身分資料類型
description: 本檔案概述Identity XDM資料類型。
exl-id: fb02b6b4-255b-442f-895c-600022231a1c
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 3%

---

# [!UICONTROL 身分] 資料類型

[!UICONTROL 身分] 是標準的XDM資料類型，可用來清楚區分與數位體驗互動的人員。 身分識別是由身分提供者建立，其本身會在 `namespace` 屬性。 在每個 `namespace`，則身分不重複。

<img src="../images/data-types/identity.png" width="550" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `namespace` | 物件 | 包含單一字串欄位(`code`)，指出與提供的相關聯的命名空間 `id` 屬性。 |
| `authenticatedState` | 字串 | 觀察到的體驗事件時此身分的已驗證狀態。 請參閱 [附錄](#authenticatedState) 以取得接受的值和定義。 |
| `id` | 字串 | 相關命名空間中的消費者身分。 |
| `primary` | 布林值 | 指出這是否為個人的主要身分。 每個個人只能有一個主要身分。 |
| `xid` | 字串 | 如果存在，此值代表跨命名空間識別碼，此識別碼在所有命名空間中所有命名空間範圍的識別碼中都是唯一的。 |

{style="table-layout:auto"}

如需資料類型的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.schema.json)

## 附錄

下節包含 [!UICONTROL 身分] 資料類型。

## authenticatedState的接受值 {#authenticatedState}

下表概述 `authenticatedState` 及其相關含義：

| 值 | 說明 |
| --- | --- |
| `ambiguous` | 驗證狀態不明確。 |
| `authenticated` | 使用者是透過登入或事件觀察時有效的類似動作來識別。 |
| `loggedOut` | 先前某個時間點的登入動作已識別使用者，但事件觀察時並未登入。 |
