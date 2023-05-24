---
keywords: Experience Platform；主題；熱門主題；模式；模式；XDM；欄位；模式；模式；方案；交互；興趣點；興趣點；資料類型；資料類型；
solution: Experience Platform
title: 興趣點交互資料類型
description: 本文檔概述了興趣點交互XDM資料類型。
exl-id: 398f56d9-1802-458d-b565-4096beb5b014
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 2%

---

# [!UICONTROL 興趣點交互] 資料類型

[!UICONTROL 興趣點交互] 是標準XDM資料類型，它描述當移動設備在範圍內時向移動應用程式傳送身份資訊的無線設備。

<img src="../images/data-types/poi-interaction.png" width="400" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `poiDetail` | [[!UICONTROL 興趣點詳細資訊]](./poi-details.md) | 描述導致事件的POI的詳細資訊。 |
| `poiEntries` | 物件 | 描述人員輸入POI的次數。 包含兩個屬性： <ul><li>`id`:度量的唯一標識符。</li><li>`value`:度量的可量化值。</li></ul> |
| `poiExits` | 物件 | 描述人員退出POI的次數。 包含兩個屬性： <ul><li>`id`:度量的唯一標識符。</li><li>`value`:度量的可量化值。</li></ul> |

{style="table-layout:auto"}

有關資料類型的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/poi-interaction.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/poi-interaction.schema.json)
