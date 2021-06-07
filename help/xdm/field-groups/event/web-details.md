---
keywords: Experience Platform；首頁；熱門主題；結構；結構； XDM;ExperienceEvent；欄位；結構；結構；結構設計；欄位群組；欄位群組；
solution: Experience Platform
title: Web詳細資訊架構欄位組
topic-legacy: overview
description: 本文檔提供Web詳細資訊架構欄位組的概述。
source-git-commit: b22dce52563d5f3bbd1796c11d7c7b2a49fa6d5f
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 3%

---


# [!UICONTROL Web詳] 細資訊架構欄位組

>[!NOTE]
>
>數個架構欄位組的名稱已變更。 有關詳細資訊，請參閱[欄位組名稱更新](../name-updates.md)上的文檔。

[!UICONTROL Web詳] 細資訊是類別 [[!DNL XDM ExperienceEvent] 的標準結構欄](../../classes/experienceevent.md)位群組，用於說明與Web詳細資訊事件（例如互動、頁面詳細資料和反向連結）相關的資訊。

![](../../images/field-groups/web-details.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `web` | [網路資訊](../../data-types/web-information.md) | 說明連結點按、網頁詳細資訊、反向連結資訊和瀏覽器詳細資訊。 |

{style=&quot;table-layout:auto&quot;}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-web.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-web.schema.json)
