---
keywords: Experience Platform；主題；熱門主題；架構；架構；XDM；個人配置檔案；欄位；架構；架構；身份映射；身份映射；架構設計；映射；聯合架構；聯合
solution: Experience Platform
title: XDM個人配置檔案類
description: 本文檔概述了XDM Individual Profile類。
exl-id: 83b22462-79ce-4024-aa50-a9bd800c0f81
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 1%

---

# [!DNL XDM Individual Profile] 類

[!DNL XDM Individual Profile] 是一個標準的經驗資料模型(XDM)類，它形成個人的奇異表示（或「配置檔案」）。 具體來說，類（及其相容的欄位組）可捕獲已識別和部分識別的與您的品牌交互的個人的屬性和興趣。

配置檔案可以從匿名行為信號（如瀏覽器cookie）到包含詳細資訊（如姓名、出生日期、位置和電子郵件地址）的高度識別的配置檔案。 隨著配置檔案的增長，它會成為個人的個人資訊、身份、聯繫資訊和通信首選項的強健儲存庫。 有關此類在平台生態系統中使用的更高級別資訊，請參閱 [XDM概述](../home.md#data-behaviors)。

的 [!DNL XDM Individual Profile] 類本身提供了幾個系統生成的值，這些值在接收資料時自動填充，而所有其他欄位必須通過使用 [相容架構欄位組](#field-groups):

![](../images/classes/individual-profile.png)

| 屬性 | 說明 |
| --- | --- |
| `_repo` | 包含以下內容的對象 [!UICONTROL 日期時間] 欄位： <ul><li>`createDate`:在資料儲存中建立資源的日期和時間，例如首次接收資料的時間。</li><li>`modifyDate`:上次修改資源的日期和時間。</li></ul> |
| `_id` | 記錄的唯一字串標識符。 此欄位用於跟蹤單個記錄的唯一性、防止重複資料以及在下游服務中查找該記錄。 有時， `_id` 可以是 [通用唯一標識符(UUID)](https://tools.ietf.org/html/rfc4122) 或 [全局唯一標識符(GUID)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0)。<br><br>如果是從源連接流式傳輸資料或直接從Parce檔案接收資料，則應通過連接使記錄唯一的特定欄位組合來生成此值，如主ID、時間戳、記錄類型等。 連接的值必須是 `uri-reference` 格式化字串，表示必須刪除任何冒號字元。 然後，應使用SHA-256或您選擇的其他算法對連接值進行散列。<br><br>必須要區分 **此欄位不表示與個人相關的標識**&#x200B;而是資料本身的記錄。 與個人有關的身份資料應降級到 [標識欄位](../schema/composition.md#identity) 由相容欄位組提供。 |
| `createdByBatchID` | 導致建立記錄的接收批的ID。 |
| `modifiedByBatchID` | 導致記錄更新的上次攝取的批的ID。 |
| `personID` | 此記錄所涉及的個人的唯一標識符。 此欄位不一定表示與該人相關的身份，除非它也被指定為 [標識欄位](../schema/composition.md#identity)。 |
| `repositoryCreatedBy` | 建立記錄的用戶的ID。 |
| `repositoryLastModifiedBy` | 上次修改記錄的用戶的ID。 |

{style="table-layout:auto"}

## 相容欄位組 {#field-groups}

>[!NOTE]
>
>幾個欄位組的名稱已更改。 查看上的文檔 [欄位組名稱更新](../field-groups/name-updates.md) 的子菜單。

Adobe提供幾個標準欄位組，用於 [!DNL XDM Individual Profile] 類。 以下是類中一些常用欄位組的清單：

* [[!UICONTROL 同意和首選項]](../field-groups/profile/consents.md)
* [[!UICONTROL 人口結構詳細資訊]](../field-groups/profile/demographic-details.md)
* [[!UICONTROL 標識映射]](../field-groups/profile/identitymap.md)
* [[!UICONTROL 會員詳細資訊]](../field-groups/profile/loyalty-details.md)
* [[!UICONTROL 個人聯繫人詳細資訊]](../field-groups/profile/personal-contact-details.md)
* [[!UICONTROL 段成員身份詳細資訊]](../field-groups/profile/segmentation.md)
* [[!UICONTROL 電信訂閱]](../field-groups/profile/telecom-subscription.md)
* [[!UICONTROL 工作聯繫人詳細資訊]](../field-groups/profile/work-contact-details.md)
* [[!UICONTROL XDM業務人員元件]](../field-groups/profile/business-person-components.md)\*
* [[!UICONTROL XDM業務人員詳細資訊]](../field-groups/profile/business-person-details.md)\*

*\*此欄位組僅對訪問Adobe Real-time Customer Data PlatformB2B版的組織可用。*

要獲取所有相容欄位組的完整清單 [!DNL XDM Individual Profile]，請參閱 [XDM GitHub回購](https://github.com/adobe/xdm/tree/master/components/fieldgroups/profile)。
