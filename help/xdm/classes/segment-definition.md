---
solution: Experience Platform
title: 段定義類
description: 本文檔概述了「體驗資料模型」(XDM)中的「段」定義類。
exl-id: c0f7b04c-2266-4d08-89a1-67ba758a51a7
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 0%

---

# [!UICONTROL 段定義] 類

&quot;[!UICONTROL 段定義]「是標準的體驗資料模型(XDM)類，用於捕獲段定義的詳細資訊。 類包括必需欄位，如段的ID和名稱，以及其他可選屬性。 如果要將段定義從外部系統引入Adobe Experience Platform，應使用此類。

>[!NOTE]
>
>此類只應用於捕獲有關段定義本身的資訊。 為了在配置檔案資料中捕獲段成員身份資訊，應使用 [段成員身份詳細資訊欄位組](../field-groups/profile/segmentation.md) 在 [!UICONTROL XDM個人配置檔案] 架構。

![](../images/classes/segment-definition.png)

| 屬性 | 說明 |
| --- | --- |
| `_repo` | 包含以下內容的對象 [!UICONTROL 日期時間] 欄位： <ul><li>`createDate`:在資料儲存中建立資源的日期和時間，例如首次接收資料的時間。</li><li>`modifyDate`:上次修改資源的日期和時間。</li></ul> |
| `_id` | 記錄的唯一系統生成的字串標識符。 此欄位用於跟蹤單個記錄的唯一性、防止重複資料以及在下游服務中查找該記錄。<br><br>由於此欄位是系統生成的，因此在資料接收期間不會提供顯式值。 但是，如果您願意，您仍然可以選擇提供您自己的唯一ID值。<br><br>要區分這一領域 **不** 代表與個人相關的身份，而是資料本身的記錄。 與個人有關的身份資料應降級到 [標識欄位](../schema/composition.md#identity) 的雙曲餘切值。 |
| `createdByBatchID` | 導致建立記錄的接收批的ID。 |
| `description` | 段定義的說明。 |
| `identityMap` | 一個映射欄位，包含段所應用的個體的一組命名空間標識。 請參閱中有關標識映射的章節 [架構組合基礎](../schema/composition.md#identityMap) 的子菜單。 |
| `modifiedByBatchID` | 導致記錄更新的上次攝取的批的ID。 |
| `repositoryCreatedBy` | 建立記錄的用戶的ID。 |
| `repositoryLastModifiedBy` | 上次修改記錄的用戶的ID。 |
| `segmentName` | **（必需）** 段定義的名稱。 |
| `segmentStatus` | 外部系統的段的狀態。 接受以下值： <ul><li>`ACTIVE`</li><li>`INACTIVE`</li><li>`DELETED`</li><li>`DRAFT`</li><li>`REVOKED`</li></ul> |
| `version` | 段定義的最新版本號。 |

{style="table-layout:auto"}
