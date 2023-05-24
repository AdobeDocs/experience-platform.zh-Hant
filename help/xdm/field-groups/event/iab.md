---
keywords: Experience Platform；主題；熱門主題；模式；模式；XDM；經驗事件；欄位；模式；模式；模式設計；欄位組；欄位組；iab;tcf;connection;
solution: Experience Platform
title: IAB TCF 2.0事件架構的同意欄位組
description: 本文檔概述了XDM ExperienceEvent類的IAB TCF 2.0同意架構欄位組。
exl-id: c236d0d4-27bd-45d7-a912-d0e93a609254
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# [!UICONTROL IAB TCF 2.0同意] 事件架構的欄位組

>[!IMPORTANT]
>
>本文檔涵蓋 [!UICONTROL IAB TCF 2.0同意] XDM ExperienceEvent類的架構欄位組。 僅當您打算跟蹤一段時間內的同意更改事件時，才應使用此欄位組。
>
>請注意，在自動強制執行工作流中未遵守在事件資料中記錄的同意值。 為了進行自動強制，必須將同意值納入XDM Individual Profile類中，並啟用「即時客戶配置」。
>
>有關用於XDM Individual Profile類的欄位組，請參閱以下內容 [文檔](../profile/iab.md) 的雙曲餘切值。

[!UICONTROL IAB TCF 2.0同意] 是標準架構欄位組 [[!DNL XDM ExperienceEvent] 類](../../classes/experienceevent.md) 用於捕獲時間戳序列IAB同意字串，以便跟蹤隨時間變化的同意更改模式。

![](../../images/field-groups/iab-event.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `consentStrings` | 陣列 [同意字串](../../data-types/consent-string.md) | 與事件關聯的同意字串值的陣列。 |

{style="table-layout:auto"}

請參閱上的指南 [平台中的IAB TCF 2.0支援](../../../landing/governance-privacy-security/consent/iab/overview.md) 的子菜單。 有關欄位組本身的詳細資訊，請參閱公共XDM儲存庫：

* [填充示例](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.example.1.json)
* [完整架構](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-privacy.schema.json)
