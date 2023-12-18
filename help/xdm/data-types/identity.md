---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；身分；資料型別；資料型別；
solution: Experience Platform
title: 身分資料型別
description: 瞭解身分XDM資料型別。
exl-id: fb02b6b4-255b-442f-895c-600022231a1c
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 4%

---

# [!UICONTROL 身分] 資料型別

[!UICONTROL 身分] 是標準的XDM資料型別，用來明確區分與數位體驗互動的人。 身分由身分提供者建立，提供者本身會在中參照 `namespace` 屬性。 在每個 `namespace`，此身分是唯一的。

<img src="../images/data-types/identity.png" width="550" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `namespace` | 物件 | 包含單一字串欄位(`code`)，表示與提供的相關聯的名稱空間 `id` 屬性。 |
| `authenticatedState` | 字串 | 觀察體驗事件時此身分的已驗證狀態。 請參閱 [附錄](#authenticatedState) 以取得接受的值和定義。 |
| `id` | 字串 | 相關名稱空間中的消費者身分。 |
| `primary` | 布林值 | 指出這是否為個人的主要身分。 每個個人只能有一個主要身分。 |
| `xid` | 字串 | 當出現時，這個值代表跨名稱空間的識別碼，在所有名稱空間中都是唯一，也就是所有名稱空間中的範圍識別碼。 |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/identity.schema.json)

## 附錄

下節包含更多關於 [!UICONTROL 身分] 資料型別。

## authenticatedState的接受值 {#authenticatedState}

下表概述下列專案可接受的值 `authenticatedState` 及其相關意義：

| 值 | 說明 |
| --- | --- |
| `ambiguous` | 驗證狀態不明確。 |
| `authenticated` | 使用者是以登入或類似的動作來識別，這些動作在事件觀察時有效。 |
| `loggedOut` | 使用者是在先前的某個時間點由登入動作識別，但在事件觀察時未登入。 |
