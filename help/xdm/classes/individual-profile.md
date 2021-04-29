---
keywords: Experience Platform;home；熱門主題；模式；模式；XDM；個人配置檔案；欄位；模式；模式；標識圖；標識圖；標識圖；模式設計；映射；聯合模式；聯合模式
solution: Experience Platform
title: XDM個別配置檔案類
topic-legacy: overview
description: 本文檔概述了XDM Individual Profile類。
exl-id: 83b22462-79ce-4024-aa50-a9bd800c0f81
translation-type: tm+mt
source-git-commit: 81d96b629ce628f663a86701d8f076eb771fdf77
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

---

# [!DNL XDM Individual Profile] class

[!DNL XDM Individual Profile] 是標準XDM類，它對已識別和部分已識別個體的屬性和興趣形成單一表示（或「描述檔」）。

描述檔可以包括匿名行為訊號（例如瀏覽器Cookie），以及包含詳細資訊（例如姓名、出生日期、位置和電子郵件地址）的高度識別描述檔。 隨著個人檔案的增長，它會成為個人資訊、身分、聯絡資訊和通訊偏好的強穩存放庫。 有關在平台生態系統中使用此類的更高級別資訊，請參閱[XDM概述](../home.md#data-behaviors)。

[!DNL XDM Individual Profile]類別本身提供數個系統產生的值，這些值會在擷取資料時自動填入，而所有其他欄位則必須使用[相容的mixins](#mixins)加入：

![](../images/classes/individual-profile.png)

| 屬性 | 說明 |
| --- | --- |
| `_repo` | 包含以下[!UICONTROL DateTime]欄位的對象： <ul><li>`createDate`:在資料儲存區中建立資源的日期和時間，例如首次擷取資料的時間。</li><li>`modifyDate`:上次修改資源的日期和時間。</li></ul> |
| `_id` | 記錄的唯一識別碼。 此欄位用於追蹤個別記錄的獨特性、防止重複資料，以及在下游服務中尋找該記錄。<br><br>請務必指出，此欄位不 **會** 呈現與個人相關的身分，而是資料本身的記錄。與人有關的身份資料應改為[身份欄位](../schema/composition.md#identity)。 |
| `createdByBatchID` | 導致記錄建立的收錄批的ID。 |
| `modifiedByBatchID` | 導致記錄更新的上次收錄批的ID。 |
| `personID` | 此記錄相關之個人的唯一識別碼。 除非此欄位也指定為[識別欄位](../schema/composition.md#identity)，否則此欄位不一定代表與該人相關的識別。 |
| `repositoryCreatedBy` | 建立記錄的用戶的ID。 |
| `repositoryLastModifiedBy` | 上次修改記錄的用戶的ID。 |

## 相容混音{#mixins}

>[!NOTE]
>
>幾個混音的名字已經改變。 如需詳細資訊，請參閱[mixin name updates](../mixins/name-updates.md)上的檔案。

Adobe提供數種標準混音，以便與[!DNL XDM Individual Profile]類一起使用。 以下是類別中常用混合詞的清單：

* [[!UICONTROL IdentityMap]](../mixins/profile/identitymap.md)
* [[!UICONTROL Demographic Details]](../mixins/profile/person-details.md)
* [[!UICONTROL Personal Contact Details]](../mixins/profile/personal-details.md)
* [[!UICONTROL Work Contact Details]](../mixins/profile/work-details.md)
* [[!UICONTROL Segment Membership Details]](../mixins/profile/segmentation.md)

有關[!DNL XDM Individual Profile]的所有相容混合的完整清單，請參閱[ XDM GitHub repo](https://github.com/adobe/xdm/tree/master/components/mixins/profile)。