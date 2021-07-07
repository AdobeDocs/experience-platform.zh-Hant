---
keywords: Experience Platform；首頁；熱門主題；結構；結構；XDM；個別設定檔；欄位；結構；結構；身分對應；身分對應；結構設計；對應；聯合結構；聯合
solution: Experience Platform
title: XDM個別設定檔類別
topic-legacy: overview
description: 本檔案概述XDM個別設定檔類別。
exl-id: 83b22462-79ce-4024-aa50-a9bd800c0f81
source-git-commit: 79fcc44ec5e08f63bfd5eed6e90d7538273f4dab
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 1%

---

# [!DNL XDM Individual Profile] 類

[!DNL XDM Individual Profile] is a standard Experience Data Model (XDM) class which forms a singular representation (or &quot;profile&quot;) of an individual person. 具體而言，類別（及其相容的欄位群組）會擷取已識別和部分已識別與您的品牌互動之個人的屬性和興趣。

Profiles can range from anonymous behavioral signals (such as browser cookies), to highly identified profiles containing detailed information such as name, date of birth, location, and email address. 隨著設定檔的成長，它會成為個人資訊、身分、聯絡詳情和通訊偏好設定的強大存放庫。 For more high-level information on the use of this class in the Platform ecosystem, refer to the [XDM overview](../home.md#data-behaviors).

[!DNL XDM Individual Profile]類本身提供數個系統生成的值，這些值在資料被內嵌時自動填充，而所有其他欄位必須通過使用[相容的架構欄位組](#field-groups)來添加：

![](../images/classes/individual-profile.png)

| 屬性 | 說明 |
| --- | --- |
| `_repo` | 包含下列[!UICONTROL DateTime]欄位的對象： <ul><li>`createDate`: The date and time when the resource was created in the data store, such as when data was first ingested.</li><li>`modifyDate`: The date and time when the resource was last modified.</li></ul> |
| `_id` | 記錄的唯一字串標識符。 此欄位可用來追蹤個別記錄的獨特性、防止資料重複，以及在下游服務中尋找該記錄。 在某些情況下，`_id`可以是[通用唯一識別碼(UUID)](https://tools.ietf.org/html/rfc4122)或[全域唯一識別碼(GUID)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0)。<br><br>如果您是從來源連線串流資料或直接從Parquet檔案擷取資料，應串連使記錄唯一的特定欄位組合（例如主要ID、時間戳記、記錄類型等），以產生此值。串連值必須是`uri-reference`格式字串，表示必須移除任何冒號字元。 之後，串連值應該會使用SHA-256或您選擇的其他演算法來雜湊。<br><br>It is important to distinguish that **this field does not represent an identity related to an individual person**, but rather the record of data itself. 與人員相關的身份資料應降級為由相容欄位群組提供的[身分欄位](../schema/composition.md#identity)。 |
| `createdByBatchID` | The ID of the ingested batch that caused the record to be created. |
| `modifiedByBatchID` | 導致記錄更新的上次擷取批次的ID。 |
| `personID` | A unique identifier for the individual person this record relates to. 除非此欄位也指定為[identity欄位](../schema/composition.md#identity)，否則此欄位不一定代表與人員相關的身分。 |
| `repositoryCreatedBy` | 建立記錄的用戶ID。 |
| `repositoryLastModifiedBy` | 上次修改記錄的用戶ID。 |

{style=&quot;table-layout:auto&quot;}

## 相容欄位群組 {#field-groups}

>[!NOTE]
>
>The names of several field groups have changed. See the document on [field group name updates](../field-groups/name-updates.md) for more information.

Adobe提供多個標準欄位組以用於[!DNL XDM Individual Profile]類。 以下是類別一些常用欄位群組的清單：

* [[!UICONTROL 人口統計詳細資料]](../field-groups/profile/demographic-details.md)
* [[!UICONTROL IdentityMap]](../field-groups/profile/identitymap.md)
* [[!UICONTROL 忠誠度詳細資料]](../field-groups/profile/loyalty-details.md)
* [[!UICONTROL 個人聯繫人詳細資訊]](../field-groups/profile/personal-contact-details.md)
* [[!UICONTROL 隱私權/個人化/行銷偏好設定（同意）]](../field-groups/profile/consents.md)
* [[!UICONTROL 區段成員資格詳細資料]](../field-groups/profile/segmentation.md)
* [[!UICONTROL Work Contact Details]](../field-groups/profile/work-contact-details.md)

For a complete list of all compatible field groups for [!DNL XDM Individual Profile], refer to the [XDM GitHub repo](https://github.com/adobe/xdm/tree/master/components/fieldgroups/profile).
