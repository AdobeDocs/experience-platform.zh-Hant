---
keywords: Experience Platform；首頁；熱門主題；模式；模式；XDM；經驗事件；欄位；模式；模式；模式設計；欄位組；欄位組；環境；環境詳細資訊；
solution: Experience Platform
title: 環境詳細資訊架構欄位組
description: 本文檔提供ExperienceEvent Environment Details架構欄位組的概述。
exl-id: 1d25b98f-66ac-443f-9b1c-dfd20a168c59
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 1%

---


# [!UICONTROL 環境詳細資訊] 架構欄位組

>[!NOTE]
>
>多個架構欄位組的名稱已更改。 查看上的文檔 [欄位組名稱更新](../name-updates.md) 的子菜單。

[!UICONTROL 環境詳細資訊] 是標準架構欄位組 [[!DNL XDM ExperienceEvent] 類](../../classes/experienceevent.md) 用於捕獲與「體驗事件」相關的環境詳細資訊的資訊，如設備詳細資訊、瀏覽器資訊、本地時間和其他地理資訊。

<img src="../../images/field-groups/environment-details.png" width="500" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `device` | [裝置](../../data-types/device.md) | 描述可跨會話跟蹤的已標識設備、應用程式或設備瀏覽器實例，通常由cookie跟蹤。 |
| `environment` | [環境](../../data-types/environment.md) | 描述有關事件觀察的情境上下文的資訊，特別是詳細描述諸如網路或軟體版本等暫時性資訊。 |
| `placeContext` | [放置上下文](../../data-types/place-context.md) | 描述與事件觀測相關的瞬態環境。 示例包括特定於區域的資訊，如天氣、當地時間、流量、星期幾、工作日與假日以及工作時間。 |

{style="table-layout:auto"}

有關欄位組的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-environment-details.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-environment-details.schema.json)
