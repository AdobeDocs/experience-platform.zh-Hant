---
keywords: Experience Platform;home；熱門主題；模式；模式；XDM;fields;schemas;Schemas;poi;interaction；興趣點；興趣點；資料類型；資料類型；
solution: Experience Platform
title: 興趣點互動資料類型
topic-legacy: overview
description: 本檔案提供興趣點互動XDM資料類型的概觀。
exl-id: 398f56d9-1802-458d-b565-4096beb5b014
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 2%

---

# [!UICONTROL Point of interest interaction] 資料類型

[!UICONTROL Point of interest interaction] 是標準的XDM資料類型，可說明當行動裝置在範圍內時，可將身分資訊傳送至行動應用程式的無線裝置。

<img src="../images/data-types/poi-interaction.png" width="400" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `poiDetail` | [[!UICONTROL Point of interest details]](./poi-details.md) | 說明導致事件的POI的詳細資訊。 |
| `poiEntries` | 物件 | 說明人員輸入POI的次數。 包含兩個屬性： <ul><li>`id`:度量的唯一標識符。</li><li>`value`:度量的可量化值。</li></ul> |
| `poiExits` | 物件 | 說明人員退出POI的次數。 包含兩個屬性： <ul><li>`id`:度量的唯一標識符。</li><li>`value`:度量的可量化值。</li></ul> |

有關資料類型的詳細資訊，請參閱公共XDM儲存庫：

* [填入的範例](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-interaction.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-interaction.schema.json)
