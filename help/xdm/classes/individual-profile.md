---
keywords: Experience Platform;home；熱門主題；模式；模式；XDM；個人配置檔案；欄位；模式；模式；標識圖；標識圖；標識圖；模式設計；映射；聯合模式；聯合模式
solution: Experience Platform
title: XDM個別配置檔案類
topic-legacy: overview
description: 本文檔概述了XDM Individual Profile類。
exl-id: 83b22462-79ce-4024-aa50-a9bd800c0f81
source-git-commit: 9fbb40a401250496761dcce63a3f033a8746ae7e
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---

# [!DNL XDM Individual Profile] class

[!DNL XDM Individual Profile] 是標準的「體驗資料模型」(XDM)類別，可形成個人的單一表示（或「描述檔」）。具體而言，類別（及其相容的混合）會擷取已識別和部分識別個人與您的品牌互動的屬性和興趣。

描述檔可以包括匿名行為訊號（例如瀏覽器Cookie），以及包含詳細資訊（例如姓名、出生日期、位置和電子郵件地址）的高度識別描述檔。 隨著個人檔案的增長，它會成為個人資訊、身分、聯絡資訊和通訊偏好的強穩存放庫。 有關在平台生態系統中使用此類的更高級別資訊，請參閱[XDM概述](../home.md#data-behaviors)。

[!DNL XDM Individual Profile]類別本身提供數個系統產生的值，這些值在擷取資料時會自動填入，而所有其他欄位則必須透過使用[相容的架構欄位群組](#field-groups)來新增：

![](../images/classes/individual-profile.png)

| 屬性 | 說明 |
| --- | --- |
| `_repo` | 包含下列[!UICONTROL DateTime]欄位的物件： <ul><li>`createDate`:在資料儲存區中建立資源的日期和時間，例如首次擷取資料的時間。</li><li>`modifyDate`:上次修改資源的日期和時間。</li></ul> |
| `_id` | 記錄的唯一識別碼。 此欄位用於追蹤個別記錄的獨特性、防止重複資料，以及在下游服務中尋找該記錄。<br><br>請務必指出，此欄位不 **會** 呈現與個人相關的身分，而是資料本身的記錄。與人有關的身份資料應改為[身份欄位](../schema/composition.md#identity)。 |
| `createdByBatchID` | 導致記錄建立的收錄批的ID。 |
| `modifiedByBatchID` | 導致記錄更新的上次收錄批的ID。 |
| `personID` | 此記錄相關之個人的唯一識別碼。 除非此欄位也指定為[識別欄位](../schema/composition.md#identity)，否則此欄位不一定代表與該人相關的識別。 |
| `repositoryCreatedBy` | 建立記錄的用戶的ID。 |
| `repositoryLastModifiedBy` | 上次修改記錄的用戶的ID。 |

## 相容欄位群組{#field-groups}

>[!NOTE]
>
>數個欄位群組的名稱已變更。 如需詳細資訊，請參閱[欄位群組名稱updates](../field-groups/name-updates.md)上的檔案。

Adobe提供多個標準欄位組，用於[!DNL XDM Individual Profile]類。 以下是類中一些常用欄位組的清單：

* [[!UICONTROL IdentityMap]](../field-groups/profile/identitymap.md)
* [[!UICONTROL 人口統計詳細資訊]](../field-groups/profile/demographic-details.md)
* [[!UICONTROL 個人聯絡資訊]](../field-groups/profile/personal-contact-details.md)
* [[!UICONTROL 工作聯繫人詳細資訊]](../field-groups/profile/work-contact-details.md)
* [[!UICONTROL 區段會籍詳細資訊]](../field-groups/profile/segmentation.md)

有關[!DNL XDM Individual Profile]的所有相容欄位組的完整清單，請參閱[ XDM GitHub repo](https://github.com/adobe/xdm/tree/master/components/mixins/profile)。
