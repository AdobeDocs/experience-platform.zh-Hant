---
keywords: Experience Platform；首頁；熱門主題；綱要；綱要；XDM；ExperienceEvent；欄位；綱要；綱要設計；欄位群組；欄位群組；iab；tcf；同意；
solution: Experience Platform
title: 事件結構描述的IAB TCF 2.0同意欄位群組
description: 瞭解XDM ExperienceEvent類別的IAB TCF 2.0同意結構描述欄位群組。
exl-id: c236d0d4-27bd-45d7-a912-d0e93a609254
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 1%

---

# 事件結構描述的[!UICONTROL IAB TCF 2.0同意]欄位群組

>[!IMPORTANT]
>
>本文介紹XDM ExperienceEvent類別的[!UICONTROL IAB TCF 2.0 Consent]結構描述欄位群組。 只有在您想要追蹤一段時間內同意變更事件時，才應使用此欄位群組。
>
>請注意，自動執行工作流程不會遵循事件資料中記錄的同意值。 為了進行自動實施，同意值必須擷取到XDM個人設定檔類別中，並啟用即時客戶設定檔。
>
>若是用於XDM個別設定檔類別的欄位群組，請改為參閱下列[檔案](../profile/iab.md)。

[!UICONTROL IAB TCF 2.0同意]是[[!DNL XDM ExperienceEvent] 類別](../../classes/experienceevent.md)的標準結構描述欄位群組，用於擷取時間戳記系列IAB同意字串，以追蹤一段時間的同意變更模式。

![](../../images/field-groups/iab-event.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `consentStrings` | [同意字串](../../data-types/consent-string.md)的陣列 | 與事件相關的一組同意字串值。 |

{style="table-layout:auto"}

如需此欄位群組使用案例的詳細資訊，請參閱Experience Platform[&#128279;](../../../landing/governance-privacy-security/consent/iab/overview.md)中IAB TCF 2.0支援指南。 如需欄位群組本身的詳細資訊，請參閱公用XDM存放庫：

* [已填入範例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.example.1.json)
* [完整結構描述](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.schema.json)
