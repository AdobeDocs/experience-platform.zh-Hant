---
solution: Experience Platform
title: 電信行業資料模型ERD
topic-legacy: overview
description: 檢視描述電信業標準化資料模型的實體關係圖(ERD)，此模型與Experience Data Model(XDM)相容，可在Adobe Experience Platform中使用。
exl-id: 96f267ce-a177-4384-a512-841c89d942ba
source-git-commit: 421b4a448370f9903b8bc826fd9be9e5b2e11c59
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 1%

---

#  電信行業資料模型ERD

以下實體關係圖(ERD)代表電信行業的標準化資料模型。 ERD是刻意以非標準化方式呈現，並考慮資料在Adobe Experience Platform中的儲存方式。

>[!NOTE]
>
>ERD是建議，您應如何為此行業使用案例建立資料模型。 若要在Platform中使用此資料模型，您必須自行建立建議的結構描述及其關係。 如需詳細資訊，請參閱UI中管理[結構](../../ui/resources/schemas.md)和[關係](../../tutorials/relationship-ui.md)的指南。

使用下列圖例來解釋此ERD:

* 中顯示的每個實體都以基礎的[Experience Data Model(XDM)類別](../composition.md#class)為基礎。
* 對於指定實體，在&#x200B;**bold**&#x200B;中標籤的每一行代表欄位組或資料類型，其下提供的相關欄位以未粗體文字列出。
* 指定實體的最重要欄位會以紅色突出顯示。
* 可用於識別個別客戶的所有屬性都會標示為「身分」，其中一個屬性會標示為「主要身分」。
* 實體關係會標示為不相依，因為以Cookie為基礎的事件通常無法判斷進行交易的人員或個人。


![](../../images/industries/telecom.png)

>[!NOTE]
>
>「體驗事件」實體包含「_ID」欄位，代表XDM ExperienceEvent類別所提供的唯一識別碼(`_id`)屬性。 如需此值預期內容的詳細資訊，請參閱[XDM ExperienceEvent](../../classes/experienceevent.md)上的參考檔案。

##  電信用戶案例

下表概述電信行業幾個常見使用案例的建議類別和架構欄位群組。

| 使用案例 | 建議的類和欄位組 |
| --- | --- |
| 根據客戶目前的持有量和瀏覽行為，了解適合追加銷售或交叉銷售機會的客戶。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL 向上銷售詳細資訊]](../../field-groups/event/upsell-details.md)</li><li>[[!UICONTROL 升級詳細資訊]](../../field-groups/event/upgrade-details.md)</li></ul></li><li>**[[!UICONTROL XDM個別設定檔]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 電信訂閱]](../../field-groups/profile/telecom-subscription.md)</li><li>[[!UICONTROL 人口統計詳細資料]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL 個人聯繫人詳細資訊]](../../field-groups/profile/personal-contact-details.md)</li></ul></li></ul> |
| 透過相關廣告和自動個人化電子郵件重新鎖定購物車放棄者。 在廣告轉換時隱藏廣告。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL 商務詳細資料]](../../field-groups/event/upsell-details.md) （若要擷取放棄購物車）</li></ul></li><li>**[[!UICONTROL XDM個別設定檔]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 電信訂閱]](../../field-groups/profile/telecom-subscription.md)</li><li>[[!UICONTROL 人口統計詳細資料]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL 個人聯繫人詳細資訊]](../../field-groups/profile/personal-contact-details.md)</li></ul></li></ul> |
| 當客戶標示為可能流失時（根據員工互動或自動機器學習演算法），請將客戶詳細資訊傳送至數位和非數位通道。 | <ul><li>**[XDM ExperienceEvent](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL 促銷活動行銷詳細資料]](../../field-groups/event/campaign-marketing-details.md)</li><li>[[!UICONTROL 管道詳細資料]](../../field-groups/event/channel-details.md)</li><li>包含個人化內容的自訂欄位群組</li></ul></li><li>**[[!UICONTROL XDM個別設定檔]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 人口統計詳細資料]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL 個人聯繫人詳細資訊]](../../field-groups/profile/personal-contact-details.md)</li></ul></li></ul> |

{style=&quot;table-layout:auto&quot;}
