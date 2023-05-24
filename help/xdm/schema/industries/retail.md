---
solution: Experience Platform
title: 零售業資料模型
description: 查看適用於零售行業的標準化資料模型，該模型與在Adobe Experience Platform使用的經驗資料模型(XDM)相容。
exl-id: 40cbb243-668b-4280-815f-1f94a06b6b87
source-git-commit: 5ceb261dbf1cac58d0cfe620875b8fa7c761abf2
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 4%

---

# [!UICONTROL 零售] 行業資料模型

以下實體關係圖(ERD)代表零售行業的標準化資料模型。 ERD有意以非標準化方式呈現，並考慮資料在Adobe Experience Platform的儲存方式。

>[!NOTE]
>
>如所述，ERD是建議您如何為此行業使用案例建模資料。 要在平台中使用此資料模型，您必須自己構建推薦的架構及其關係。 請參閱管理指南 [模式](../../ui/resources/schemas.md) 和 [關係](../../tutorials/relationship-ui.md) 的子菜單。

使用以下圖例解釋此ERD:

* 所示各實體均基於 [體驗資料模型(XDM)類](../composition.md#class)。
* 對於給定實體，每行標籤在 **粗** 表示欄位組或資料類型，其提供的相關欄位以未加粗的文本列出。
* 給定實體的最重要欄位以紅色加亮。
* 可用於標識單個客戶的所有屬性都標籤為「identity」，其中一個屬性標籤為「primary identity」。
* 實體關係被標籤為非依賴關係，因為基於cookie的事件通常無法確定執行該事務的人員或個人。

![](../../images/industries/retail.png)

>[!NOTE]
>
>「體驗事件」實體包含「_ID」欄位，該欄位表示唯一標識符(`_id`)由XDM ExperienceEvent類提供的屬性。 請參閱上的參考文檔 [XDM體驗事件](../../classes/experienceevent.md) 的子菜單。

## [!UICONTROL 零售] 使用案例

下表概述了幾種常見零售使用案例的推薦類和架構欄位組。

| 使用案例 | 建議的類和欄位組 |
| --- | --- |
| 將線上和離線資料源結合起來，解決跨設備和線上/離線身份問題，提供全方位的跨通道和跨設備屬性報告。 | <ul><li>**[XDM體驗事件](../../classes/experienceevent.md)**:<ul><li>[商業詳細資訊](../../field-groups/event/commerce-details.md)</li><li>[Web詳細資訊](../../field-groups/event/web-details.md)</li></ul></li><li>**[產品](../../classes/product.md)**:<ul><li>[產品目錄](../../field-groups/product/product-catalog.md)</li><li>[產品類別](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| 為不同領域提供有針對性的個性化體驗，以增加收入並幫助增強人口協調平台。 | <ul><li>**[XDM體驗事件](../../classes/experienceevent.md)**:<ul><li>[市場活動市場營銷詳細資訊](../../field-groups/event/campaign-marketing-details.md)</li><li>[渠道詳細資訊](../../field-groups/event/channel-details.md)</li><li>[商業詳細資訊](../../field-groups/event/commerce-details.md)</li><li>[環境詳細資訊](../../field-groups/event/environment-details.md)</li><li>[Web詳細資訊](../../field-groups/event/web-details.md)</li></ul></li><li>**[XDM 個別設定檔](../../classes/individual-profile.md)**:<ul><li>[人口結構詳細資訊](../../field-groups/profile/demographic-details.md)</li><li>[個人聯繫人詳細資訊](../../field-groups/profile/personal-contact-details.md)</li><li>[工作聯繫人詳細資訊](../../field-groups/profile/work-contact-details.md)</li></ul></li></ul> |
| 分析多點觸控屬性以提高營銷效率。 | <ul><li>**[XDM體驗事件](../../classes/experienceevent.md)**:<ul><li>[市場活動市場營銷詳細資訊](../../field-groups/event/campaign-marketing-details.md)</li><li>[渠道詳細資訊](../../field-groups/event/channel-details.md)</li><li>[商業詳細資訊](../../field-groups/event/commerce-details.md)</li></ul></li><li>**[XDM 個別設定檔](../../classes/individual-profile.md)**:<ul><li>[人口結構詳細資訊](../../field-groups/profile/demographic-details.md)</li></ul></li></ul> |
| 通過改進男女分類來提高電子郵件的相關性。 | <ul><li>**[XDM體驗事件](../../classes/experienceevent.md)**:<ul><li>[商業詳細資訊](../../field-groups/event/commerce-details.md)</li></ul></li><li>**[XDM 個別設定檔](../../classes/individual-profile.md)**:<ul><li>[人口結構詳細資訊](../../field-groups/profile/demographic-details.md)</li></ul></li><li>**[產品](../../classes/product.md)**:<ul><li>[產品目錄](../../field-groups/product/product-catalog.md)</li><li>[產品類別](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| 獲取忠誠度（合作夥伴）資料，以跨Web 、電子郵件和數字營銷渠道增加相關產品資訊。 | <ul><li>**[XDM體驗事件](../../classes/experienceevent.md)**:<ul><li>[Web詳細資訊](../../field-groups/event/web-details.md)</li></ul></li><li>**[XDM 個別設定檔](../../classes/individual-profile.md)**:<ul><li>[人口結構詳細資訊](../../field-groups/profile/demographic-details.md)</li><li>[會員詳細資訊](../../field-groups/profile/loyalty-details.md)</li></ul></li><li>**[產品](../../classes/product.md)**:<ul><li>[產品目錄](../../field-groups/product/product-catalog.md)</li><li>[產品類別](../../field-groups/product/product-category.md)</li></ul></li></ul> |
| 通過自動化和個性化的電子郵件將放棄的購物車重新定位。 | <ul><li>**[XDM體驗事件](../../classes/experienceevent.md)**:<ul><li>[商業詳細資訊](../../field-groups/event/commerce-details.md)</li><li>[Web詳細資訊](../../field-groups/event/web-details.md)</li></ul></li><li>**[產品](../../classes/product.md)**:<ul><li>[產品目錄](../../field-groups/product/product-catalog.md)</li><li>[產品類別](../../field-groups/product/product-category.md)</li></ul></li></ul> |

{style="table-layout:auto"}
