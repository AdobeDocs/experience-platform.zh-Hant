---
keywords: Experience Platform；首頁；熱門主題；結構；結構； XDM;ExperienceEvent；欄位；結構；結構；結構設計；欄位群組；欄位群組；
solution: Experience Platform
title: 促銷活動行銷詳細資料結構欄位群組
topic-legacy: overview
description: 本檔案提供「促銷活動行銷詳細資料」結構欄位群組的概觀。
source-git-commit: cb4afb0979bd65a9a82a6018323fa7beacdbf605
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 3%

---


# [!UICONTROL 促銷活動行] 銷詳細資料結構欄位群組

>[!NOTE]
>
>數個架構欄位組的名稱已變更。 有關詳細資訊，請參閱[欄位組名稱更新](../name-updates.md)上的文檔。

[!UICONTROL 促銷活] 動行銷詳細資訊是類別 [[!DNL XDM ExperienceEvent] 的標準結構欄](../../classes/experienceevent.md)位群組，用來說明行銷活動資訊，例如促銷活動群組、名稱及追蹤代碼。

![](../../images/field-groups/campaign-marketing-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `marketing` | [行銷](../../data-types/marketing.md) | 描述行銷活動資訊（例如促銷活動群組、名稱及追蹤代碼）的物件。 |

{style=&quot;table-layout:auto&quot;}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-marketing.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-marketing.schema.json)
