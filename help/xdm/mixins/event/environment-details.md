---
keywords: Experience Platform;home；熱門主題；架構；架構；Schema;XDM;ExperienceEvent;fields;schemas；架構設計；mixin;mixin;environment；環境詳細資訊；
solution: Experience Platform
title: 混合環境詳細資訊
topic: overview
description: 本檔案提供ExperienceEvent環境詳細資訊混合的概觀。
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 2%

---


# [!UICONTROL 環境詳] 細資訊

>[!NOTE]
>
>幾個混音的名字已經改變。 如需詳細資訊，請參閱[mixin name updates](../name-updates.md)上的檔案。

[!UICONTROL 環境] 詳細資訊是用來擷取與體驗事 [[!DNL XDM ExperienceEvent] ](../../classes/individual-profile.md) 件相關之環境詳細資訊（例如裝置詳細資訊、瀏覽器資訊、當地時間和其他地理資訊）之類別的標準混合。

<img src="../../images/mixins/environment-details.png" width="500" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `device` | [裝置](../../data-types/device.md) | 說明已識別的裝置、應用程式或裝置瀏覽器例項，可跨作業追蹤，通常由Cookie追蹤。 |
| `environment` | [環境](../../data-types/environment.md) | 說明事件觀察的情境相關資訊，尤其詳細說明網路或軟體版本等暫存性資訊。 |
| `placeContext` | [置入內容](../../data-types/place-context.md) | 說明與事件觀察相關的暫時情況。 例如，地區特定資訊，例如天氣、當地時間、流量、一週中的某天、工作日與假日，以及工作時數。 |

有關混音的詳細資訊，請參閱公用XDM存放庫：

* [填入的範例](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-environment-details.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-environment-details.schema.json)
