---
keywords: Experience Platform；首頁；熱門主題；結構；結構； XDM;ExperienceEvent；欄位；結構；結構；結構；結構設計；欄位群組；欄位群組；環境；環境詳細資訊；
solution: Experience Platform
title: 環境詳細資訊架構欄位組
topic-legacy: overview
description: 本檔案提供ExperienceEvent環境詳細資料結構欄位群組的概觀。
exl-id: 1d25b98f-66ac-443f-9b1c-dfd20a168c59
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 3%

---


# [!UICONTROL 環境詳] 細資訊架構欄位組

>[!NOTE]
>
>數個架構欄位組的名稱已變更。 有關詳細資訊，請參閱[欄位組名稱更新](../name-updates.md)上的文檔。

[!UICONTROL 環境] 詳細資料是類別的標準結構欄 [[!DNL XDM ExperienceEvent] ](../../classes/individual-profile.md) 位群組，用來擷取與體驗事件相關的環境詳細資料資訊，例如裝置詳細資料、瀏覽器資訊、當地時間和其他地理位置資訊。

<img src="../../images/field-groups/environment-details.png" width="500" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `device` | [裝置](../../data-types/device.md) | 說明可跨工作階段追蹤（通常由Cookie追蹤）的已識別裝置、應用程式或裝置瀏覽器例項。 |
| `environment` | [環境](../../data-types/environment.md) | 說明事件觀測的情境環境資訊，具體說明網路或軟體版本等暫時性資訊。 |
| `placeContext` | [放置內容](../../data-types/place-context.md) | 說明與事件觀測相關的暫時情況。 例如，地區特定資訊，例如天氣、當地時間、流量、一週中某天、工作日與節日，以及工作時間。 |

{style=&quot;table-layout:auto&quot;}

如需欄位群組的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-environment-details.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-environment-details.schema.json)
