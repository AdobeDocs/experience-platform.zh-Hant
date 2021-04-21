---
solution: Experience Platform
title: 區段定義類別
topic-legacy: overview
description: 本檔案概述Experience Data Model(XDM)中的「區段定義」類別。
exl-id: c0f7b04c-2266-4d08-89a1-67ba758a51a7
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---

# [!UICONTROL Segment definition] class

&quot;[!UICONTROL Segment definition]&quot;是標準的「體驗資料模型」(XDM)類別，可擷取區段定義的詳細資訊。 類別包含必填欄位，例如區段的ID和名稱，以及其他選用屬性。 如果要將外部系統的段定義引入Adobe Experience Platform，應使用此類。

>[!NOTE]
>
>此類別僅用於擷取區段定義本身的相關資訊。 為了在您的描述檔資料中擷取區段成員資格資訊，您應在[!UICONTROL XDM Individual Profile]結構中使用混合](../mixins/profile/segmentation.md)的[區段成員資格詳細資訊。

![](../images/classes/segment-definition.png)

| 屬性 | 說明 |
| --- | --- |
| `_repo` | 包含以下[!UICONTROL DateTime]欄位的對象： <ul><li>`createDate`:在資料儲存區中建立資源的日期和時間，例如首次擷取資料的時間。</li><li>`modifyDate`:上次修改資源的日期和時間。</li></ul> |
| `_id` | 記錄的唯一、系統生成的字串標識符。 此欄位用於追蹤個別記錄的獨特性、防止重複資料，以及在下游服務中尋找該記錄。<br><br>由於此欄位是系統生成的，因此在資料接收過程中不會提供顯式值。不過，您仍可選擇視需要提供您自己的唯一ID值。<br><br>請務必指出，此欄位不 **會** 呈現與個人相關的身分，而是資料本身的記錄。與人有關的身份資料應改為[身份欄位](../schema/composition.md#identity)。 |
| `createdByBatchID` | 導致記錄建立的收錄批的ID。 |
| `description` | 區段定義的說明。 |
| `identityMap` | 地圖欄位，包含區段套用之個人的一組命名空間身分。 系統會在擷取身分資料時自動更新此欄位。<br /><br />如需其使用案例的詳細資訊，請參 [閱架構構](../schema/composition.md#identityMap) 成基礎中有關身分映射的章節。 |
| `modifiedByBatchID` | 導致記錄更新的上次收錄批的ID。 |
| `repositoryCreatedBy` | 建立記錄的用戶的ID。 |
| `repositoryLastModifiedBy` | 上次修改記錄的用戶的ID。 |
| `segmentName` | **（必要）** 區段定義的名稱。 |
| `segmentStatus` | 外部系統的段狀態。 接受下列值： <ul><li>`ACTIVE`</li><li>`INACTIVE`</li><li>`DELETED`</li><li>`DRAFT`</li><li>`REVOKED`</li></ul> |
| `version` | 區段定義的最新版本號碼。 |
