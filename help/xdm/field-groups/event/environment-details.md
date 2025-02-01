---
keywords: Experience Platform；首頁；熱門主題；綱要；綱要；XDM；ExperienceEvent；欄位；綱要；綱要設計；欄位群組；欄位群組；環境；環境詳細資料；
solution: Experience Platform
title: 環境詳細資料結構欄位群組
description: 瞭解ExperienceEvent環境詳細資料結構欄位群組。
exl-id: 1d25b98f-66ac-443f-9b1c-dfd20a168c59
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 2%

---


# [!UICONTROL 環境詳細資料]結構描述欄位群組

>[!NOTE]
>
>數個結構描述欄位群組的名稱已變更。 如需詳細資訊，請參閱[欄位群組名稱更新](../name-updates.md)的檔案。

[!UICONTROL 環境詳細資料]是[[!DNL XDM ExperienceEvent] 類別](../../classes/experienceevent.md)的標準結構描述欄位群組，用於擷取與體驗事件相關的環境詳細資料相關資訊，例如裝置詳細資料、瀏覽器資訊、當地時間和其他地理資訊。

![](../../images/field-groups/environment-details.png){width=500}

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `device` | [裝置](../../data-types/device.md) | 說明通常可透過Cookie跨工作階段追蹤的已識別裝置、應用程式或裝置瀏覽器執行個體。 |
| `environment` | [環境](../../data-types/environment.md) | 說明有關事件觀察的情境環境的資訊，尤其會詳細說明網路或軟體版本之類的臨時性資訊。 |
| `placeContext` | [放置內容](../../data-types/place-context.md) | 說明與事件觀察相關的暫時性情況。 例如特定地區設定資訊，例如天氣、當地時間、交通、星期幾、工作日與假日、以及工作時間。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-environment-details.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-environment-details.schema.json)
