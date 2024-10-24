---
keywords: Experience Platform；首頁；熱門主題；綱要；綱要；XDM；ExperienceEvent；欄位；綱要；綱要；綱要設計；欄位群組；欄位群組；
solution: Experience Platform
title: Web詳細資料結構欄位群組
description: 瞭解「網頁詳細資料」結構欄位群組。
exl-id: eb42606b-ade4-4d72-b601-c560009c98e8
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 3%

---

# [!UICONTROL 網頁詳細資料]結構描述欄位群組

>[!NOTE]
>
>數個結構描述欄位群組的名稱已變更。 如需詳細資訊，請參閱[欄位群組名稱更新](../name-updates.md)的檔案。

[!UICONTROL 網頁詳細資料]是[[!DNL XDM ExperienceEvent] 類別](../../classes/experienceevent.md)的標準結構描述欄位群組，用於描述有關網頁詳細資料事件的資訊，例如互動、頁面詳細資料和反向連結。

![](../../images/field-groups/web-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `web` | [網頁資訊](../../data-types/web-information.md) | 說明連結點按次數、網頁詳細資料、反向連結資訊和瀏覽器詳細資料。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-web.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-web.schema.json)
