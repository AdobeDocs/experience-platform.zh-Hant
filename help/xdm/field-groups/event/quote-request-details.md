---
title: 報價請求詳細資訊結構欄位組
description: 本文檔概述了「報價請求詳細資訊」架構欄位組。
exl-id: 19be76fa-d212-4b00-815a-d3869c1054e2
source-git-commit: f5df893260f0772ad54ccdb00d99ed8f328d35a9
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 4%

---

# [!UICONTROL 報價請求詳細資訊] 方案欄位組

[!UICONTROL 報價請求詳細資訊] 是的標準架構欄位組 [[!DNL XDM ExperienceEvent] 類](../../classes/experienceevent.md). 欄位群組提供單一 `quotes` 對象到結構，它可捕獲各種報價類型（包括保險單、醫療保健、製造訂單和高科技訂單）的請求流程詳細資訊。

![](../../images/field-groups/quote-request-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `discount` | [[!UICONTROL 貨幣]](../../data-types/currency.md) | 對訪客顯示的報價折扣金額。 |
| `premium` | [[!UICONTROL 貨幣]](../../data-types/currency.md) | 對訪客顯示的報價溢價金額。 |
| `location` | [!UICONTROL 字串] | 用於尋找訪客位置附近零售商的郵遞區號。 |
| `requestID` | [!UICONTROL 字串] | 報價請求的唯一標識符。 |
| `selectedRetailer` | [!UICONTROL 字串] | 為報價請求選擇的零售商（如果適用）。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱 [公用XDM存放庫](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-quote-request-details.schema.json).
