---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；POI；互動；興趣點；興趣點；資料型別；資料型別；
solution: Experience Platform
title: 興趣點互動資料型別
description: 瞭解興趣點互動XDM資料型別。
exl-id: 398f56d9-1802-458d-b565-4096beb5b014
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 3%

---

# [!UICONTROL 興趣點互動]資料型別

[!UICONTROL 興趣點互動]是標準的XDM資料型別，說明在行動裝置進入範圍內時，將身分資訊傳達給行動應用程式的無線裝置。

<img src="../images/data-types/poi-interaction.png" width="400" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `poiDetail` | [[!UICONTROL 興趣點詳細資料]](./poi-details.md) | 說明造成事件之POI的詳細資料。 |
| `poiEntries` | 物件 | 說明個人已進入POI的次數。 包含兩個屬性： <ul><li>`id`：量值的唯一識別碼。</li><li>`value`：量值的可量化值。</li></ul> |
| `poiExits` | 物件 | 說明個人已退出POI的次數。 包含兩個屬性： <ul><li>`id`：量值的唯一識別碼。</li><li>`value`：量值的可量化值。</li></ul> |

{style="table-layout:auto"}

如需資料型別的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/poi-interaction.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/poi-interaction.schema.json)
