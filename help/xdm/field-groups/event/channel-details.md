---
keywords: Experience Platform；首頁；熱門主題；綱要；綱要；XDM；ExperienceEvent；欄位；綱要；綱要；綱要設計；欄位群組；欄位群組；
solution: Experience Platform
title: 管道詳細資料結構欄位群組
description: 瞭解「管道詳細資料」結構欄位群組。
exl-id: b8ec2f57-6882-466e-9b22-61fb2178fb1e
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 3%

---

# [!UICONTROL 管道詳細資料] 結構描述欄位群組

>[!NOTE]
>
>數個結構描述欄位群組的名稱已變更。 檢視檔案： [欄位群組名稱更新](../name-updates.md) 以取得詳細資訊。

[!UICONTROL 管道詳細資料] 是的標準結構描述欄位群組 [[!DNL XDM ExperienceEvent] 類別](../../classes/experienceevent.md)，用於說明ID、頻道型別、媒體型別和位置型別等頻道資訊。

![](../../images/field-groups/channel-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `channel` | [體驗管道](../../data-types/experience-channel.md) | 說明產品退貨、保固註冊及購物車/訂單流程的物件。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-channel.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-channel.schema.json)
