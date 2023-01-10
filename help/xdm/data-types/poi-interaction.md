---
keywords: Experience Platform；首頁；熱門主題；結構；結構； XDM；欄位；結構；結構；poi；互動；地標；地標；資料類型；資料類型；
solution: Experience Platform
title: 興趣點互動資料類型
description: 本檔案概述興趣點互動XDM資料類型。
exl-id: 398f56d9-1802-458d-b565-4096beb5b014
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 3%

---

# [!UICONTROL 興趣點互動] 資料類型

[!UICONTROL 興趣點互動] 是標準的XDM資料類型，說明當行動裝置在範圍內時，無線裝置可將身分資訊傳送至行動應用程式。

<img src="../images/data-types/poi-interaction.png" width="400" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `poiDetail` | [[!UICONTROL 興趣點詳細資訊]](./poi-details.md) | 說明造成事件的POI詳細資訊。 |
| `poiEntries` | 物件 | 說明使用者輸入POI的次數。 包含兩個屬性： <ul><li>`id`:度量的唯一標識符。</li><li>`value`:度量的可量化值。</li></ul> |
| `poiExits` | 物件 | 說明人員退出POI的次數。 包含兩個屬性： <ul><li>`id`:度量的唯一標識符。</li><li>`value`:度量的可量化值。</li></ul> |

{style=&quot;table-layout:auto&quot;}

如需資料類型的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/poi-interaction.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/poi-interaction.schema.json)
