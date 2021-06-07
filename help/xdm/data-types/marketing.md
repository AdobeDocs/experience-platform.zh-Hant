---
keywords: Experience Platform；首頁；熱門主題；結構；結構； XDM；欄位；結構；結構；裝置；資料類型；資料類型；
solution: Experience Platform
title: 行銷資料類型
topic-legacy: overview
description: 本檔案概述Marketing XDM資料類型。
source-git-commit: cb4afb0979bd65a9a82a6018323fa7beacdbf605
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 5%

---


#  行銷資料類型

 行銷是一種標準XDM資料類型，可說明在特定接觸點處於作用中狀態的行銷活動。

![](../images/data-types/marketing.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `campaignGroup` | 字串 | 促銷活動群組的名稱（若多個促銷活動分組在一起，如`50%_DISCOUNT`）。 |
| `campaignName` | 字串 | 行銷活動的名稱，例如`50%_DISCOUNT_USA`或`50%_DISCOUNT_ASIA`。 |
| `trackingCode` | 字串 | 可用來識別事件關聯之行銷活動的追蹤代碼。 |

{style=&quot;table-layout:auto&quot;}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/marketing.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/marketing.schema.json)
