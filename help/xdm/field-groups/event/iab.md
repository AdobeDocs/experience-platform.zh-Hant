---
keywords: Experience Platform；首頁；熱門主題；結構；結構； XDM;ExperienceEvent；欄位；結構；結構；結構；結構設計；欄位群組；欄位群組；iab;tcf；同意；
solution: Experience Platform
title: IAB TCF 2.0同意結構欄位群組
topic-legacy: overview
description: 本檔案概述XDM ExperienceEvent類別的IAB TCF 2.0同意結構欄位群組。
source-git-commit: 7a0ac3970713e95438c6f0fdbd6175545ea7fdd0
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 2%

---


# [!UICONTROL IAB TCF 2.0同意] 方案欄位群組

>[!IMPORTANT]
>
>本檔案涵蓋XDM ExperienceEvent類別的[!UICONTROL  IAB TCF 2.0同意]結構欄位群組。 只有在您要追蹤隨時間變化的同意變更事件時，才應使用此欄位群組。
>
>請注意，自動執行工作流程不會遵循記錄在事件資料中的同意值。 若要自動強制執行，同意值必須擷取至XDM個別設定檔類別，並啟用即時客戶設定檔。
>
>對於用於XDM個別設定檔類的欄位組，請改為參閱以下[document](../profile/iab.md)。

[!UICONTROL IAB TCF 2.0同意] 是類別的標準結構欄位群組， [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) 用於擷取時間戳記系列IAB同意字串，以追蹤隨時間變化的同意變更模式。

![](../../images/field-groups/iab-event.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `consentStrings` | [同意字串](../../data-types/consent-string.md)的陣列 | 與事件相關聯的同意字串值陣列。 |

{style=&quot;table-layout:auto&quot;}

如需此欄位群組使用案例的詳細資訊，請參閱Platform](../../../landing/governance-privacy-security/consent/iab/overview.md)中[IAB TCF 2.0支援的指南。 如需欄位群組本身的詳細資訊，請參閱公用XDM存放庫：

* [填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.example.1.json)
* [完整結構](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.schema.json)
