---
keywords: Experience Platform；首頁；熱門主題；模式；模式；XDM；欄位；模式；模式；設備；資料類型；資料類型；
solution: Experience Platform
title: 市場營銷資料類型
description: 此文檔概述了「營銷XDM」資料類型。
exl-id: b5ac0127-15fe-42b6-b7fc-2fbcda7e7e27
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 3%

---

# [!UICONTROL 營銷] 資料類型

[!UICONTROL 營銷] 是一個標準XDM資料類型，它描述與特定觸點活動的市場營銷活動。

![](../images/data-types/marketing.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `campaignGroup` | 字串 | 市場活動組的名稱（在多個市場活動按類似方式組合在一起的情況下） `50%_DISCOUNT`)。 |
| `campaignName` | 字串 | 市場營銷活動的名稱，如 `50%_DISCOUNT_USA` 或 `50%_DISCOUNT_ASIA`。 |
| `trackingCode` | 字串 | 用於標識事件關聯的市場營銷市場活動的跟蹤代碼。 |

{style="table-layout:auto"}

有關欄位組的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/marketing.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/marketing.schema.json)
