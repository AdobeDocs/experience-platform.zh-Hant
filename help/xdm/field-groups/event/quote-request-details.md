---
title: 報價請求詳細資料結構欄位群組
description: 瞭解報價請求詳細資料結構欄位群組。
exl-id: 19be76fa-d212-4b00-815a-d3869c1054e2
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 6%

---

# [!UICONTROL 報價請求細節] 結構描述欄位群組

[!UICONTROL 報價請求細節] 是的標準結構描述欄位群組 [[!DNL XDM ExperienceEvent] 類別](../../classes/experienceevent.md). 欄位群組提供單一 `quotes` object to a schema （物件至結構描述），其會擷取各種報價型別（包括保單、醫療保健、製造訂單及高科技訂單）的請求流程詳細資料。

![](../../images/field-groups/quote-request-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `discount` | [[!UICONTROL 貨幣]](../../data-types/currency.md) | 向訪客顯示的報價的折扣金額。 |
| `premium` | [[!UICONTROL 貨幣]](../../data-types/currency.md) | 向訪客顯示的報價優惠金額。 |
| `location` | [!UICONTROL 字串] | 用於尋找接近訪客地點的零售商的郵遞區號。 |
| `requestID` | [!UICONTROL 字串] | 報價請求的唯一識別碼。 |
| `selectedRetailer` | [!UICONTROL 字串] | 報價請求的所選零售商（如果適用）。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱 [公用XDM存放庫](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-quote-request-details.schema.json).
