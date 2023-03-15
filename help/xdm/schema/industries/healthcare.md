---
title: 醫療保健行業資料模型ERD
description: 查看描述醫療保健行業標準化資料模型的實體關係圖(ERD)。 此資料模型與Experience Data Model(XDM)相容，可在Adobe Experience Platform中使用。
exl-id: ebcf97ec-f5a4-46e5-b1ad-c80d55aa2c6e
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 1%

---

# [!UICONTROL 醫療保健] 工業資料模型ERD

以下實體關係圖(ERD)代表醫療保健行業的標準化資料模型。 ERD是刻意以非標準化方式呈現，並考慮資料在Adobe Experience Platform中的儲存方式。

>[!NOTE]
>
>ERD是建議，您應如何為此行業使用案例建立資料模型。 若要在Platform中使用此資料模型，您必須自行建立建議的結構描述及其關係。 請參閱管理指南 [綱要](../../ui/resources/schemas.md) 和 [關係](../../tutorials/relationship-ui.md) ，以取得詳細資訊。

使用下列圖例來解釋此ERD:

* 中顯示的每個實體均以 [Experience Data Model(XDM)類別](../composition.md#class).
* 對於指定實體，每一行都標有 **粗體** 代表欄位群組或資料類型，其提供的相關欄位以未加粗的文字列於下方。
* 指定實體的最重要欄位會以紅色突出顯示。
* 可用於識別個別客戶的所有屬性都會標示為「身分」，其中一個屬性會標示為「主要身分」。
* 實體關係會標示為不相依，因為以Cookie為基礎的事件通常無法判斷進行交易的人員或個人。

![顯示醫療保健行業資料模型的實體關係圖的影像](../../images/industries/healthcare.png)

>[!NOTE]
>
>每個實體都包含「_ID」欄位，代表唯一字串識別碼(`_id`)屬性。 此欄位可用來追蹤個別記錄或事件的獨特性、防止資料重複，以及在下游服務中尋找該資料。 在某些情況下， `_id` 可以是 [通用唯一識別碼(UUID)](https://tools.ietf.org/html/rfc4122) 或 [全局唯一標識符(GUID)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0).<br><br>必須區分 **此欄位不代表與個人相關的身分**，而是資料本身的記錄。 與人員、活動或商業實體相關的身分資料應降級為 [身分欄位](../composition.md#identity) 由相容的欄位群組提供。

## [!UICONTROL 醫療保健] 使用案例

下表概述了幾個常見醫療保健使用案例的建議類和架構欄位組。

| 使用案例 | 建議的類和欄位組 |
| --- | --- |
| 改善消費者購買保險的數位化購買和體驗。 例如： <ul><li>當人們存取包含一般資訊的頁面時（例如計畫、計畫名稱/階層、醫療補助、健康計畫等），請了解他們的行為和所尋找的項目，以便傳送促銷電子郵件或在有廣告的第三方平台上鎖定他們。</li><li>當人們搜索心臟健康和疫苗資訊時，把與疫苗相關的心臟健康資訊發送給他們，以建立品牌認知度，或者要求他們安排疫苗接種。</li></ul> | <ul><li>**[[!UICONTROL XDM個別設定檔]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 醫療保健會員詳細資訊]](../../field-groups/profile/healthcare-member-details.md)</li><li>建立於 `planID` 使用的屬性和結構 [!UICONTROL 計畫] 類別。</li></ul></li><li>**[[!UICONTROL 付款人]](../../classes/payer.md)**</li><li>**[[!UICONTROL 計劃]](../../classes/plan.md)**:<ul><li>[[!UICONTROL 醫療保健計畫詳細資訊]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL 應用程式詳細資訊]](../../field-groups/event/application-details.md)</li><li>[[!UICONTROL 網站工具詳細資訊]](../../field-groups/event/sitetool-details.md)</li><li>[[!UICONTROL  促銷活動行銷詳細資料]](../../field-groups/event/campaign-marketing-details.md)</li></ul></li></ul> |
| 根據過去的線上行為和健康資料，透過有針對性的廣告增加患者的數位獲取。 | <ul><li>**[[!UICONTROL XDM個別設定檔]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 醫療保健會員詳細資訊]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL 提供者]](../../classes/provider.md)**:<ul><li>[[!UICONTROL 醫療保健提供商]](../../field-groups/provider/healthcare-provider.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Web詳細資訊]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL 廣告詳細資訊]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |
| 通過跟蹤不同渠道的保險營銷，改善健康計畫中的註冊和帳戶建立，以便了解客戶如何了解保險公司。 | <ul><li>**[[!UICONTROL XDM個別設定檔]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 醫療保健會員詳細資訊]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL 付款人]](../../classes/payer.md)**</li><li>**[[!UICONTROL 計劃]](../../classes/plan.md)**:<ul><li>[[!UICONTROL 醫療保健計畫詳細資訊]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Web詳細資訊]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL 廣告詳細資訊]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |
| 避免醫療保險的漏洞。 | <ul><li>**[[!UICONTROL XDM個別設定檔]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 醫療保健會員詳細資訊]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL 計劃]](../../classes/plan.md)**:<ul><li>[[!UICONTROL 醫療保健計畫詳細資訊]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li></ul> |
| 使用直接向客戶(DTC)廣告，將藥品資訊提升至提供者。 | <ul><li>**[[!UICONTROL XDM個別設定檔]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 醫療保健會員詳細資訊]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL 藥物]](../../classes/medication.md)**:<ul><li>[[!UICONTROL 保健藥物]](../../field-groups/medication/healthcare-medication.md)</li></ul></li><li>**[[!UICONTROL XDM ExperienceEvent]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Web詳細資訊]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL 廣告詳細資訊]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |
