---
keywords: Experience Platform;home；熱門主題；模式；模式；XDM;ExperienceEvent;fields;schemas；模式設計；欄位組；欄位組；環境詳細資訊；
solution: Experience Platform
title: 環境詳細資訊方案欄位組
topic-legacy: overview
description: 本文檔提供ExperienceEvent環境詳細資料結構欄位群組的概述。
exl-id: 1d25b98f-66ac-443f-9b1c-dfd20a168c59
translation-type: tm+mt
source-git-commit: d425dcd9caf8fccd0cb35e1bac73950a6042a0f8
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 1%

---


# [!UICONTROL Environment Details] 方案欄位組

>[!NOTE]
>
>多個架構欄位組的名稱已更改。 如需詳細資訊，請參閱[欄位群組名稱updates](../name-updates.md)上的檔案。

[!UICONTROL Environment Details] 是類別的標準架構欄位群組，用 [[!DNL XDM ExperienceEvent] ](../../classes/individual-profile.md) 來擷取與體驗事件相關的環境詳細資訊，例如裝置詳細資訊、瀏覽器資訊、當地時間和其他地理資訊。

<img src="../../images/field-groups/environment-details.png" width="500" /><br />

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `device` | [裝置](../../data-types/device.md) | 說明已識別的裝置、應用程式或裝置瀏覽器例項，可跨作業追蹤，通常由Cookie追蹤。 |
| `environment` | [環境](../../data-types/environment.md) | 說明事件觀察的情境相關資訊，尤其詳細說明網路或軟體版本等暫存性資訊。 |
| `placeContext` | [置入內容](../../data-types/place-context.md) | 說明與事件觀察相關的暫時情況。 例如，地區特定資訊，例如天氣、當地時間、流量、一週中的某天、工作日與假日，以及工作時數。 |

有關欄位組的詳細資訊，請參閱公用XDM儲存庫：

* [填入的範例](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-environment-details.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-environment-details.schema.json)
