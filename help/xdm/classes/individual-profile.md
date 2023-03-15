---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；個別設定檔；欄位；結構；結構；身分對應；身分對應；結構設計；對應；聯合結構；聯合
solution: Experience Platform
title: XDM個別設定檔類別
description: 本檔案概述XDM個別設定檔類別。
exl-id: 83b22462-79ce-4024-aa50-a9bd800c0f81
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 1%

---

# [!DNL XDM Individual Profile] 類

[!DNL XDM Individual Profile] 是標準的Experience Data Model(XDM)類別，可形成個別人員的單一表示法（或「設定檔」）。 具體而言，類別（及其相容的欄位群組）會擷取已識別和部分已識別與您的品牌互動之個人的屬性和興趣。

設定檔的範圍包括匿名行為訊號（例如瀏覽器Cookie），以及包含詳細資訊（例如名稱、出生日期、位置及電子郵件地址）的高識別設定檔。 隨著設定檔的成長，它會成為個人資訊、身分、聯絡詳情和通訊偏好設定的強大存放庫。 如需在Platform生態系統中使用此類別的詳細資訊，請參閱 [XDM概觀](../home.md#data-behaviors).

此 [!DNL XDM Individual Profile] 類別本身提供數個系統產生的值，在資料擷取時會自動填入，而所有其他欄位則必須透過使用 [相容架構欄位群組](#field-groups):

![](../images/classes/individual-profile.png)

| 屬性 | 說明 |
| --- | --- |
| `_repo` | 包含下列項目的物件 [!UICONTROL DateTime] 欄位： <ul><li>`createDate`:在資料存放區中建立資源的日期和時間，例如首次擷取資料的時間。</li><li>`modifyDate`:上次修改資源的日期和時間。</li></ul> |
| `_id` | 記錄的唯一字串標識符。 此欄位可用來追蹤個別記錄的獨特性、防止資料重複，以及在下游服務中尋找該記錄。 在某些情況下， `_id` 可以是 [通用唯一識別碼(UUID)](https://tools.ietf.org/html/rfc4122) 或 [全局唯一標識符(GUID)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0).<br><br>如果您是從來源連線串流資料或直接從Parquet檔案擷取資料，應串連使記錄唯一的特定欄位組合（例如主要ID、時間戳記、記錄類型等），以產生此值。 串連值必須是 `uri-reference` 格式字串，表示必須移除任何冒號字元。 之後，串連值應該會使用SHA-256或您選擇的其他演算法來雜湊。<br><br>必須區分 **此欄位不代表與個人相關的身分**，而是資料本身的記錄。 與個人有關的身份資料應被降級為 [身分欄位](../schema/composition.md#identity) 由相容的欄位群組提供。 |
| `createdByBatchID` | 導致建立記錄的所擷取批次ID。 |
| `modifiedByBatchID` | 導致記錄更新的上次擷取批次的ID。 |
| `personID` | 此記錄相關的個人的唯一標識符。 此欄位不一定代表與該人員相關的身分，除非亦指定為 [身分欄位](../schema/composition.md#identity). |
| `repositoryCreatedBy` | 建立記錄的用戶ID。 |
| `repositoryLastModifiedBy` | 上次修改記錄的用戶ID。 |

{style="table-layout:auto"}

## 相容欄位群組 {#field-groups}

>[!NOTE]
>
>數個欄位組的名稱已變更。 請參閱 [欄位群組名稱更新](../field-groups/name-updates.md) 以取得更多資訊。

Adobe提供數個標準欄位群組，以搭配 [!DNL XDM Individual Profile] 類別。 以下是類別一些常用欄位群組的清單：

* [[!UICONTROL 同意和偏好設定]](../field-groups/profile/consents.md)
* [[!UICONTROL 人口統計詳細資料]](../field-groups/profile/demographic-details.md)
* [[!UICONTROL IdentityMap]](../field-groups/profile/identitymap.md)
* [[!UICONTROL 忠誠度詳細資料]](../field-groups/profile/loyalty-details.md)
* [[!UICONTROL 個人聯繫人詳細資訊]](../field-groups/profile/personal-contact-details.md)
* [[!UICONTROL 區段成員資格詳細資料]](../field-groups/profile/segmentation.md)
* [[!UICONTROL 電信訂閱]](../field-groups/profile/telecom-subscription.md)
* [[!UICONTROL 工作聯繫人詳細資訊]](../field-groups/profile/work-contact-details.md)
* [[!UICONTROL XDM企業人員元件]](../field-groups/profile/business-person-components.md)\*
* [[!UICONTROL XDM業務人員詳細資訊]](../field-groups/profile/business-person-details.md)\*

*\*此欄位群組僅適用於可存取B2B版Adobe Real-time Customer Data Platform的組織。*

要獲取的所有相容欄位組的完整清單 [!DNL XDM Individual Profile]，請參閱 [XDM GitHub存放庫](https://github.com/adobe/xdm/tree/master/components/fieldgroups/profile).
