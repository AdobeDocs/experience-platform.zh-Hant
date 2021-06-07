---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；個別設定檔；欄位；結構；結構；身分對應；身分對應；結構設計；對應；聯合結構；聯合
solution: Experience Platform
title: XDM個別設定檔類別
topic-legacy: overview
description: 本檔案概述XDM個別設定檔類別。
exl-id: 83b22462-79ce-4024-aa50-a9bd800c0f81
source-git-commit: eddaa7090af2d2c947f154272bb219dc2e3bca08
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 1%

---

# [!DNL XDM Individual Profile] 類

[!DNL XDM Individual Profile] 是標準的Experience Data Model(XDM)類別，可形成個別人員的單一表示法（或「設定檔」）。具體而言，類別（及其相容的Mixin）會擷取已識別和部分識別之個人與您的品牌互動的屬性和興趣。

設定檔的範圍包括匿名行為訊號（例如瀏覽器Cookie），以及包含詳細資訊（例如名稱、出生日期、位置及電子郵件地址）的高識別設定檔。 隨著設定檔的成長，它會成為個人資訊、身分、聯絡詳情和通訊偏好設定的強大存放庫。 如需在Platform生態系統中使用此類別的詳細資訊，請參閱[XDM概述](../home.md#data-behaviors)。

[!DNL XDM Individual Profile]類本身提供數個系統生成的值，這些值在資料被內嵌時自動填充，而所有其他欄位必須通過使用[相容的架構欄位組](#field-groups)來添加：

![](../images/classes/individual-profile.png)

| 屬性 | 說明 |
| --- | --- |
| `_repo` | 包含下列[!UICONTROL DateTime]欄位的對象： <ul><li>`createDate`:在資料存放區中建立資源的日期和時間，例如首次擷取資料的時間。</li><li>`modifyDate`:上次修改資源的日期和時間。</li></ul> |
| `_id` | 記錄的唯一字串標識符。 此欄位可用來追蹤個別記錄的獨特性、防止資料重複，以及在下游服務中尋找該記錄。 在某些情況下，`_id`可以是[通用唯一識別碼(UUID)](https://tools.ietf.org/html/rfc4122)或[全域唯一識別碼(GUID)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0)。<br><br>如果您是從來源連線串流資料或直接從Parquet檔案擷取資料，應串連使記錄唯一的特定欄位組合（例如主要ID、時間戳記、記錄類型等），以產生此值。串連值必須是`uri-reference`格式字串，表示必須移除任何冒號字元。 之後，串連值應該會使用SHA-256或您選擇的其他演算法來雜湊。<br><br>請務必區分， **此欄位不代表與個人相關的身分**，而是資料本身的記錄。與人員相關的身份資料應降級為由相容欄位群組提供的[身分欄位](../schema/composition.md#identity)。 |
| `createdByBatchID` | 導致建立記錄的所擷取批次ID。 |
| `modifiedByBatchID` | 導致記錄更新的上次擷取批次的ID。 |
| `personID` | 此記錄相關的個人的唯一標識符。 除非此欄位也指定為[identity欄位](../schema/composition.md#identity)，否則此欄位不一定代表與人員相關的身分。 |
| `repositoryCreatedBy` | 建立記錄的用戶ID。 |
| `repositoryLastModifiedBy` | 上次修改記錄的用戶ID。 |

{style=&quot;table-layout:auto&quot;}

## 相容欄位組{#field-groups}

>[!NOTE]
>
>數個欄位組的名稱已變更。 有關詳細資訊，請參閱[欄位組名稱更新](../field-groups/name-updates.md)上的文檔。

Adobe提供多個標準欄位組以用於[!DNL XDM Individual Profile]類。 以下是類別一些常用欄位群組的清單：

* [[!UICONTROL IdentityMap]](../field-groups/profile/identitymap.md)
* [[!UICONTROL 人口統計詳細資料]](../field-groups/profile/demographic-details.md)
* [[!UICONTROL 個人聯繫人詳細資訊]](../field-groups/profile/personal-contact-details.md)
* [[!UICONTROL 工作聯繫人詳細資訊]](../field-groups/profile/work-contact-details.md)
* [[!UICONTROL 區段成員資格詳細資料]](../field-groups/profile/segmentation.md)

如需[!DNL XDM Individual Profile]所有相容欄位群組的完整清單，請參閱[ XDM GitHub repo](https://github.com/adobe/xdm/tree/master/components/mixins/profile)。
