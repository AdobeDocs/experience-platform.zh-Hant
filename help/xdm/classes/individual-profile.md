---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;identityMap;identity map;Identity map;Schema design;map;Map;union schema;union
solution: Experience Platform
title: XDM個別配置檔案類
topic: overview
description: 本文檔概述了XDM Individual Profile類。
translation-type: tm+mt
source-git-commit: b7b57c0b70b1af3a833f0386bc809bb92c9b50f8
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---


# [!DNL XDM Individual Profile] class

[!DNL XDM Individual Profile] 是標準XDM類，它對已識別和部分已識別個體的屬性和興趣形成單一表示（或「描述檔」）。

描述檔可以包括匿名行為訊號（例如瀏覽器Cookie），以及包含詳細資訊（例如姓名、出生日期、位置和電子郵件地址）的高度識別描述檔。 隨著個人檔案的增長，它會成為個人資訊、身分、聯絡資訊和通訊偏好的強穩存放庫。 有關此類在平台生態系統中使用的詳細資訊，請參閱 [XDM概述](../home.md#data-behaviors)。

類別 [!DNL XDM Individual Profile] 本身提供數個系統產生的值，這些值會在擷取資料時自動填入，而所有其他欄位則必須透過使用相容的混音來 [新增](#mixins):

![](../images/classes/individual-profile.png)

| 屬性 | 說明 |
| --- | --- |
| `_repo` | 包含下列 [!UICONTROL DateTime欄位的物件] : <ul><li>`createDate`:在資料儲存區中建立資源的日期和時間，例如首次擷取資料的時間。</li><li>`modifyDate`:上次修改資源的日期和時間。</li></ul> |
| `_id` | 記錄的唯一、系統生成的字串標識符。 此欄位用於追蹤個別記錄的獨特性、防止重複資料，以及在下游服務中尋找該記錄。 由於此欄位是系統生成的，因此在資料接收期間不應提供顯式值。<br><br>請務必指出，此欄位不 **代表與個人** ，而是資料本身的記錄。 與個人有關的身份資料應該被降級到 [身份欄位](../schema/composition.md#identity) 。 |
| `createdByBatchID` | 導致記錄建立的收錄批的ID。 |
| `modifiedByBatchID` | 導致記錄更新的上次收錄批的ID。 |
| `repositoryCreatedBy` | 建立記錄的用戶的ID。 |
| `repositoryLastModifiedBy` | 上次修改記錄的用戶的ID。 |

## 相容混音 {#mixins}

Adobe提供數種標準混音，以搭配該類 [!DNL XDM Individual Profile] 使用。 以下是該類別最常使用的混音清單：

* [[!UICONTROL IdentityMap]](../mixins/profile/identitymap.md)
* [[!UICONTROL 個人資料詳細資訊]](../mixins/profile/person-details.md)
* [[!UICONTROL 個人資料詳細資訊]](../mixins/profile/personal-details.md)
* [[!UICONTROL 概要檔案工作詳細資訊]](../mixins/profile/work-details.md)
* [[!UICONTROL 描述檔區段]](../mixins/profile/segmentation.md)