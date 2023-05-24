---
title: 醫療保健行業資料模型ERD
description: 查看描述醫療保健行業標準化資料模型的實體關係圖(ERD)。 此資料模型與在Adobe Experience Platform使用的經驗資料模型(XDM)相容。
exl-id: ebcf97ec-f5a4-46e5-b1ad-c80d55aa2c6e
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 4%

---

# [!UICONTROL 保健] 工業資料模型ERD

以下實體關係圖(ERD)代表醫療保健行業的標準化資料模型。 ERD有意以非標準化方式呈現，並考慮資料在Adobe Experience Platform的儲存方式。

>[!NOTE]
>
>如所述，ERD是建議您如何為此行業使用案例建模資料。 要在平台中使用此資料模型，您必須自己構建推薦的架構及其關係。 請參閱管理指南 [模式](../../ui/resources/schemas.md) 和 [關係](../../tutorials/relationship-ui.md) 的子菜單。

使用以下圖例解釋此ERD:

* 所示各實體均基於 [體驗資料模型(XDM)類](../composition.md#class)。
* 對於給定實體，每行標籤在 **粗** 表示欄位組或資料類型，其提供的相關欄位以未加粗的文本列出。
* 給定實體的最重要欄位以紅色加亮。
* 可用於標識單個客戶的所有屬性都標籤為「identity」，其中一個屬性標籤為「primary identity」。
* 實體關係被標籤為非依賴關係，因為基於cookie的事件通常無法確定執行該事務的人員或個人。

![顯示醫療保健行業資料模型的實體關係圖的影像](../../images/industries/healthcare.png)

>[!NOTE]
>
>每個實體都包括一個「_ID」欄位，它表示唯一字串標識符(`_id`)的屬性。 此欄位用於跟蹤單個記錄或事件的唯一性、防止重複資料並在下游服務中查找該資料。 有時， `_id` 可以是 [通用唯一標識符(UUID)](https://tools.ietf.org/html/rfc4122) 或 [全局唯一標識符(GUID)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0)。<br><br>必須要區分 **此欄位不表示與個人相關的標識**&#x200B;而是資料本身的記錄。 與個人、事件或業務實體相關的身份資料應降級到 [標識欄位](../composition.md#identity) 由相容欄位組提供。

## [!UICONTROL 保健] 使用案例

下表概述了幾種常見醫療保健使用案例的推薦類和架構欄位組。

| 使用案例 | 建議的類和欄位組 |
| --- | --- |
| 改善購買保險的消費者的數字購買和體驗。 例如： <ul><li>當人們訪問包含一般資訊（如計畫、計畫名稱/層次、醫療補助、健康計畫等）的頁面時，瞭解他們的行為和他們正在查找什麼以便發送宣傳電子郵件或在帶有廣告的第三方平台上將他們作為目標。</li><li>當人們搜索心臟健康和疫苗資訊時，將與疫苗相關的心臟健康資訊發送給他們，以創造品牌意識或要求他們安排疫苗接種。</li></ul> | <ul><li>**[[!UICONTROL XDM 個別設定檔]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 醫療保健成員詳細資訊]](../../field-groups/profile/healthcare-member-details.md)</li><li>建立於 `planID` 使用屬性和架構的 [!UICONTROL 計畫] 類。</li></ul></li><li>**[[!UICONTROL 付款人]](../../classes/payer.md)**</li><li>**[[!UICONTROL 計劃]](../../classes/plan.md)**:<ul><li>[[!UICONTROL 醫療保健計畫詳細資訊]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li><li>**[[!UICONTROL XDM體驗事件]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL 應用程式詳細資訊]](../../field-groups/event/application-details.md)</li><li>[[!UICONTROL 站點工具詳細資訊]](../../field-groups/event/sitetool-details.md)</li><li>[[!UICONTROL  市場活動市場營銷詳細資訊]](../../field-groups/event/campaign-marketing-details.md)</li></ul></li></ul> |
| 通過基於過去線上行為和健康資料的定向廣告，增加患者的數字獲取。 | <ul><li>**[[!UICONTROL XDM 個別設定檔]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 醫療保健成員詳細資訊]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL 提供程式]](../../classes/provider.md)**:<ul><li>[[!UICONTROL 醫療保健提供商]](../../field-groups/provider/healthcare-provider.md)</li></ul></li><li>**[[!UICONTROL XDM體驗事件]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Web詳細資訊]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL 廣告詳細資訊]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |
| 通過跟蹤通過不同渠道進行保險營銷來改進健康計畫中的註冊和帳戶建立，以便瞭解客戶如何瞭解保險公司。 | <ul><li>**[[!UICONTROL XDM 個別設定檔]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 醫療保健成員詳細資訊]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL 付款人]](../../classes/payer.md)**</li><li>**[[!UICONTROL 計劃]](../../classes/plan.md)**:<ul><li>[[!UICONTROL 醫療保健計畫詳細資訊]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li><li>**[[!UICONTROL XDM體驗事件]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Web詳細資訊]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL 廣告詳細資訊]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |
| 避免醫療保險漏洞。 | <ul><li>**[[!UICONTROL XDM 個別設定檔]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 醫療保健成員詳細資訊]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL 計劃]](../../classes/plan.md)**:<ul><li>[[!UICONTROL 醫療保健計畫詳細資訊]](../../field-groups/plan/healthcare-plan-details.md)</li></ul></li></ul> |
| 使用直接向客戶(DTC)廣告向提供商宣傳藥品資訊。 | <ul><li>**[[!UICONTROL XDM 個別設定檔]](../../classes/individual-profile.md)**:<ul><li>[[!UICONTROL 醫療保健成員詳細資訊]](../../field-groups/profile/healthcare-member-details.md)</li></ul></li><li>**[[!UICONTROL 藥物]](../../classes/medication.md)**:<ul><li>[[!UICONTROL 一種保健藥物]](../../field-groups/medication/healthcare-medication.md)</li></ul></li><li>**[[!UICONTROL XDM體驗事件]](../../classes/experienceevent.md)**:<ul><li>[[!UICONTROL Web詳細資訊]](../../field-groups/event/web-details.md)</li><li>[[!UICONTROL 廣告詳細資訊]](../../field-groups/event/advertising-details.md)</li></ul></li></ul> |
