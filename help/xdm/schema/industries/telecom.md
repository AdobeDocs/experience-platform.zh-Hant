---
solution: Experience Platform
title: 電信行業資料模型ERD
description: 查看描述電信行業標準化資料模型的實體關係圖(ERD)，該資料模型與在Adobe Experience Platform使用的經驗資料模型(XDM)相容。
exl-id: 96f267ce-a177-4384-a512-841c89d942ba
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 2%

---

# [!UICONTROL 電信] 工業資料模型ERD

以下實體關係圖(ERD)代表電信行業的標準化資料模型。 ERD有意以非標準化方式呈現，並考慮資料在Adobe Experience Platform的儲存方式。

>[!NOTE]
>
>如所述，ERD是建議您如何為此行業使用案例建模資料。 要在平台中使用此資料模型，您必須自己構建推薦的架構及其關係。 請參閱管理指南 [模式](../../ui/resources/schemas.md) 和 [關係](../../tutorials/relationship-ui.md) 的子菜單。

使用以下圖例解釋此ERD:

* 所示各實體均基於 [體驗資料模型(XDM)類](../composition.md#class)。
* 對於給定實體，每行標籤在 **粗** 表示欄位組或資料類型，其提供的相關欄位以未加粗的文本列出。
* 給定實體的最重要欄位以紅色加亮。
* 可用於標識單個客戶的所有屬性都標籤為「identity」，其中一個屬性標籤為「primary identity」。
* 實體關係被標籤為非依賴關係，因為基於cookie的事件通常無法確定執行該事務的人員或個人。


![](../../images/industries/telecom.png)

>[!NOTE]
>
>「體驗事件」實體包含「_ID」欄位，該欄位表示唯一標識符(`_id`)由XDM ExperienceEvent類提供的屬性。 請參閱上的參考文檔 [XDM體驗事件](../../classes/experienceevent.md) 的子菜單。

## [!UICONTROL 電信] 使用案例

下表概述了電信行業幾種常見使用案例的推薦類和模式欄位組。

| 使用案例 | 建議的類和欄位組 |
| --- | --- |
| 瞭解那些非常適合追加銷售或交叉銷售機會的客戶，這些客戶基於其當前持有的資產及其瀏覽行為。 | <ul><li>**[XDM體驗事件](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL 追加銷售詳細資訊]](../../field-groups/event/upsell-details.md)</li><li>[[!UICONTROL 升級詳細資訊]](../../field-groups/event/upgrade-details.md)</li></ul></li><li>**[[!UICONTROL XDM 個別設定檔]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 電信訂閱]](../../field-groups/profile/telecom-subscription.md)</li><li>[[!UICONTROL 人口結構詳細資訊]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL 個人聯繫人詳細資訊]](../../field-groups/profile/personal-contact-details.md)</li></ul></li></ul> |
| 通過相關廣告和自動化個性化電子郵件將放棄的購物車重新定位。 當廣告轉換時禁止顯示。 | <ul><li>**[XDM體驗事件](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL 商業詳細資訊]](../../field-groups/event/upsell-details.md) （要捕獲購物車放棄）</li></ul></li><li>**[[!UICONTROL XDM 個別設定檔]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 電信訂閱]](../../field-groups/profile/telecom-subscription.md)</li><li>[[!UICONTROL 人口結構詳細資訊]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL 個人聯繫人詳細資訊]](../../field-groups/profile/personal-contact-details.md)</li></ul></li></ul> |
| 當客戶被標為可能出現流失時（基於員工交互或自動機器學習算法），將客戶詳細資訊發送到數字和非數字渠道。 | <ul><li>**[XDM體驗事件](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL 市場活動市場營銷詳細資訊]](../../field-groups/event/campaign-marketing-details.md)</li><li>[[!UICONTROL 渠道詳細資訊]](../../field-groups/event/channel-details.md)</li><li>包含個性化內容的自定義欄位組</li></ul></li><li>**[[!UICONTROL XDM 個別設定檔]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 人口結構詳細資訊]](../../field-groups/profile/demographic-details.md)</li><li>[[!UICONTROL 個人聯繫人詳細資訊]](../../field-groups/profile/personal-contact-details.md)</li></ul></li></ul> |

{style="table-layout:auto"}
