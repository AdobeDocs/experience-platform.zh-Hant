---
solution: Experience Platform
title: 區段定義類別
description: 本檔案概述Experience Data Model(XDM)中的區段定義類別。
exl-id: c0f7b04c-2266-4d08-89a1-67ba758a51a7
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 1%

---

# [!UICONTROL 區段定義] 類

&quot;[!UICONTROL 區段定義]「 」是標準的Experience Data Model(XDM)類別，可擷取區段定義的詳細資訊。 類別包含必填欄位，例如區段的ID、名稱，以及其他選用屬性。 如果您要將外部系統的區段定義匯入Adobe Experience Platform，應使用此類別。

>[!NOTE]
>
>此類別僅應用於擷取區段定義本身的相關資訊。 若要在您的設定檔資料中擷取區段成員資格資訊，您應使用 [區段成員資格詳細資料欄位群組](../field-groups/profile/segmentation.md) 在 [!UICONTROL XDM個別設定檔] 綱要。

![](../images/classes/segment-definition.png)

| 屬性 | 說明 |
| --- | --- |
| `_repo` | 包含下列項目的物件 [!UICONTROL DateTime] 欄位： <ul><li>`createDate`:在資料存放區中建立資源的日期和時間，例如首次擷取資料的時間。</li><li>`modifyDate`:上次修改資源的日期和時間。</li></ul> |
| `_id` | 記錄的唯一、系統生成的字串標識符。 此欄位用於追蹤個別記錄的獨特性、防止資料重複，以及在下游服務中尋找該記錄。<br><br>由於此欄位是系統產生的，因此在資料擷取期間不會提供明確值。 不過，您仍可以選擇提供您自己的唯一ID值（如果您想要的話）。<br><br>必須區分此欄位 **不** 代表與個人相關的身分，而非資料本身的記錄。 與個人有關的身份資料應被降級為 [身分欄位](../schema/composition.md#identity) 。 |
| `createdByBatchID` | 導致建立記錄的所擷取批次ID。 |
| `description` | 區段定義的說明。 |
| `identityMap` | 一個地圖欄位，其中包含區段所套用之個人的命名空間身分識別集。 請參閱 [綱要構成基本知識](../schema/composition.md#identityMap) 以取得其使用案例的詳細資訊。 |
| `modifiedByBatchID` | 導致記錄更新的上次擷取批次的ID。 |
| `repositoryCreatedBy` | 建立記錄的用戶ID。 |
| `repositoryLastModifiedBy` | 上次修改記錄的用戶ID。 |
| `segmentName` | **（必要）** 區段定義的名稱。 |
| `segmentStatus` | 來自外部系統的區段狀態。 接受下列值： <ul><li>`ACTIVE`</li><li>`INACTIVE`</li><li>`DELETED`</li><li>`DRAFT`</li><li>`REVOKED`</li></ul> |
| `version` | 區段定義的最新版本號碼。 |

{style=&quot;table-layout:auto&quot;}
