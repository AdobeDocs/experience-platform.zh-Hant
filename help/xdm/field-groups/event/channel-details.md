---
keywords: Experience Platform；首頁；熱門主題；模式；模式；XDM；經驗事件；欄位；模式；模式；模式設計；欄位組；欄位組；
solution: Experience Platform
title: 渠道詳細資訊架構欄位組
description: 本文檔概述了「渠道詳細資訊」架構欄位組。
exl-id: b8ec2f57-6882-466e-9b22-61fb2178fb1e
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 1%

---

# [!UICONTROL 渠道詳細資訊] 架構欄位組

>[!NOTE]
>
>多個架構欄位組的名稱已更改。 查看上的文檔 [欄位組名稱更新](../name-updates.md) 的子菜單。

[!UICONTROL 渠道詳細資訊] 是標準架構欄位組 [[!DNL XDM ExperienceEvent] 類](../../classes/experienceevent.md)，用於描述通道資訊，如ID、通道類型、媒體類型和位置類型。

![](../../images/field-groups/channel-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `channel` | [體驗渠道](../../data-types/experience-channel.md) | 描述產品退貨、保修註冊和購物車/訂單流程的對象。 |

{style="table-layout:auto"}

有關欄位組的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-channel.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-channel.schema.json)
