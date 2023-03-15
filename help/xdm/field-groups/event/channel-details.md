---
keywords: Experience Platform；首頁；熱門主題；結構；結構； XDM;ExperienceEvent；欄位；結構；結構；結構設計；欄位群組；欄位群組；
solution: Experience Platform
title: 渠道詳細資訊結構欄位組
description: 本檔案提供「管道詳細資料」結構欄位群組的概觀。
exl-id: b8ec2f57-6882-466e-9b22-61fb2178fb1e
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 1%

---

# [!UICONTROL 管道詳細資料] 方案欄位組

>[!NOTE]
>
>數個架構欄位組的名稱已變更。 請參閱 [欄位群組名稱更新](../name-updates.md) 以取得更多資訊。

[!UICONTROL 管道詳細資料] 是的標準架構欄位組 [[!DNL XDM ExperienceEvent] 類](../../classes/experienceevent.md)，用於說明通道資訊，例如ID、通道類型、媒體類型和位置類型。

![](../../images/field-groups/channel-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `channel` | [體驗管道](../../data-types/experience-channel.md) | 描述產品退貨、保修註冊和購物車/訂單流程的對象。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-channel.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-channel.schema.json)
