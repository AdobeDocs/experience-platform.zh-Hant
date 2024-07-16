---
solution: Experience Platform
title: 區段定義類別
description: 瞭解體驗資料模型(XDM)中的區段定義類別。
exl-id: c0f7b04c-2266-4d08-89a1-67ba758a51a7
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# [!UICONTROL 區段定義]類別

「[!UICONTROL 區段定義]」是標準的體驗資料模型(XDM)類別，可擷取區段定義的詳細資料。 類別包含必要欄位，例如對象的ID和名稱，以及其他選用屬性。 如果您要將外部系統的區段定義匯入Adobe Experience Platform，應使用此類別。

>[!NOTE]
>
>此類別只應用於擷取有關區段定義本身的資訊。 若要擷取設定檔資料中的對象成員資格資訊，您應該使用[!UICONTROL XDM個人設定檔]結構描述中的[區段成員資格詳細資料欄位群組](../field-groups/profile/segmentation.md)。

![](../images/classes/segment-definition.png)

| 屬性 | 說明 |
| --- | --- |
| `_repo` | 包含下列[!UICONTROL 日期時間]欄位的物件： <ul><li>`createDate`：在資料存放區中建立資源的日期和時間，例如首次擷取資料的時間。</li><li>`modifyDate`：上次修改資源的日期和時間。</li></ul> |
| `_id` | 記錄的唯一、系統產生的字串識別碼。 此欄位用於追蹤個別記錄的唯一性、防止資料重複，以及在下游服務中查詢該記錄。<br><br>由於此欄位是由系統產生，因此在資料擷取期間不會提供明確的值。 不過，您仍然可以視需要選擇提供自己的唯一ID值。<br><br>請務必注意，此欄位&#x200B;**不代表與個人相關的身分，而是資料本身的記錄。** 與個人相關的身分資料應改為[身分欄位](../schema/composition.md#identity)。 |
| `createdByBatchID` | 造成記錄建立的擷取批次識別碼。 |
| `description` | 區段定義的說明。 |
| `identityMap` | 包含受眾套用之個人的一組名稱空間身分的對映欄位。 如需有關其使用案例的詳細資訊，請參閱[結構描述構成基本概念](../schema/composition.md#identityMap)中身分對應一節。 |
| `modifiedByBatchID` | 導致記錄更新的上次擷取批次識別碼。 |
| `repositoryCreatedBy` | 建立紀錄的使用者ID。 |
| `repositoryLastModifiedBy` | 上次修改紀錄的使用者ID。 |
| `segmentName` | **（必要）**&#x200B;區段定義的名稱。 |
| `segmentStatus` | 來自外部系統的對象狀態。 接受下列值： <ul><li>`ACTIVE`</li><li>`INACTIVE`</li><li>`DELETED`</li><li>`DRAFT`</li><li>`REVOKED`</li></ul> |
| `version` | 區段定義的最新版本號碼。 |

{style="table-layout:auto"}
