---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；欄位；結構；裝置；資料型別；資料型別；
solution: Experience Platform
title: 行銷資料型別
description: 瞭解行銷XDM資料型別。
exl-id: b5ac0127-15fe-42b6-b7fc-2fbcda7e7e27
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 6%

---

# [!UICONTROL 行銷] 資料型別

[!UICONTROL 行銷] 是標準XDM資料型別，說明對特定接觸點有效的行銷活動。

![](../images/data-types/marketing.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `campaignGroup` | 字串 | 行銷活動群組的名稱(當多個行銷活動分組在一起時，例如 `50%_DISCOUNT`)。 |
| `campaignName` | 字串 | 行銷活動的名稱，例如 `50%_DISCOUNT_USA` 或 `50%_DISCOUNT_ASIA`. |
| `trackingCode` | 字串 | 可用來識別與事件相關聯之行銷活動的追蹤代碼。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/marketing.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/marketing.schema.json)
