---
title: 報價請求詳細資訊方案欄位組
description: 本文檔提供Quote Request Details方案欄位組的概覽。
exl-id: 19be76fa-d212-4b00-815a-d3869c1054e2
source-git-commit: f5df893260f0772ad54ccdb00d99ed8f328d35a9
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 4%

---

# [!UICONTROL 報價請求詳細資訊] 架構欄位組

[!UICONTROL 報價請求詳細資訊] 是標準架構欄位組 [[!DNL XDM ExperienceEvent] 類](../../classes/experienceevent.md)。 欄位組提供單個 `quotes` 對象到架構，它捕獲各種類型報價（包括保險單、醫療保健、製造訂單和高科技訂單）的請求流程詳細資訊。

![](../../images/field-groups/quote-request-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `discount` | [[!UICONTROL 貨幣]](../../data-types/currency.md) | 顯示給訪問者的報價的折扣金額。 |
| `premium` | [[!UICONTROL 貨幣]](../../data-types/currency.md) | 顯示給訪問者的報價的溢價金額。 |
| `location` | [!UICONTROL 字串] | 用於在訪客所在地附近找到零售商的郵遞區號。 |
| `requestID` | [!UICONTROL 字串] | 報價請求的唯一標識符。 |
| `selectedRetailer` | [!UICONTROL 字串] | 報價請求的選定零售商（如果適用）。 |

{style="table-layout:auto"}

有關欄位組的詳細資訊，請參閱 [公共XDM儲存庫](https://github.com/adobe/xdm/blob/master/docs/reference/fieldgroups/experience-event/experienceevent-quote-request-details.schema.json)。
