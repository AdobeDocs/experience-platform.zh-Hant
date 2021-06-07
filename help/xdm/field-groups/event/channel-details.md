---
keywords: Experience Platform；首頁；熱門主題；結構；結構； XDM;ExperienceEvent；欄位；結構；結構；結構設計；欄位群組；欄位群組；
solution: Experience Platform
title: 渠道詳細資訊結構欄位組
topic-legacy: overview
description: 本檔案提供「管道詳細資料」結構欄位群組的概觀。
source-git-commit: b9168052174c250810e59e403cb77419d510df3b
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 3%

---


# [!UICONTROL 管道詳] 細資訊結構欄位群組

>[!NOTE]
>
>數個架構欄位組的名稱已變更。 有關詳細資訊，請參閱[欄位組名稱更新](../name-updates.md)上的文檔。

[!UICONTROL 管道] 詳細資訊：類別的標準架 [[!DNL XDM ExperienceEvent] 構欄位群組](../../classes/experienceevent.md)，用來說明管道資訊，例如ID、管道類型、媒體類型和位置類型。

![](../../images/field-groups/channel-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `channel` | [體驗管道](../../data-types/experience-channel.md) | 描述產品退貨、保修註冊和購物車/訂單流程的對象。 |

{style=&quot;table-layout:auto&quot;}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-channel.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-channel.schema.json)
