---
title: XDM個別潛在客戶設定檔類別
description: 瞭解Experience Data Model (XDM)中的XDM個別潛在客戶設定檔類別。
exl-id: 10fd9d16-4123-4ad4-971f-b715231ee6a9
source-git-commit: f4ddcf14de7a5cec42b5ebc521203cfdd1498a9f
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 5%

---

# [!UICONTROL XDM個別潛在客戶設定檔] 類別

在Experience Data Model (XDM)中， [!UICONTROL XDM個別潛在客戶設定檔] class會擷取潛在客戶設定檔，這些設定檔通常來自漏斗頂端客戶贏取使用案例的資料合作夥伴。

>[!NOTE]
>
>若要將XDM個別潛在客戶設定檔中的欄位設定為身分，您必須先建立至少一個合作夥伴ID名稱空間。 如需有關合作夥伴 ID 命名空間的詳細資訊，請閱讀[身分類型章節](../../identity-service/features/namespaces.md)。

![XDM潛在客戶類別的結構描述圖。](../images/classes/individual-prospect-profile.png)

| 屬性 | 資料類型 | 說明 |
| --- | --- | --- |
| `_repo` | 物件 | 此類別可讓您引進來自資料廠商的潛在客戶設定檔，以漏斗客戶贏取使用案例。 |
| `_repo.createDate` | [!UICONTROL 日期時間] | 在存放庫中建立資源的伺服器日期和時間。 建立時間可能是第一次上傳資產檔案，或是伺服器將目錄建立為新資產的父級時。 datetime屬性應符合ISO 8601標準。 此格式的範例為「2004-10-23T12」:00:00-06:00英吋 |
| `_repo.modifyDate` | [!UICONTROL 日期時間] | 上次在存放庫中修改資源的伺服器日期和時間，例如，何時上傳新版本的資產或新增或移除目錄的子資源。 datetime屬性應符合ISO 8601標準。 範例形式為「2004-10-23T12」:00:00-06:00英吋 |
| `_id` | [!UICONTROL 字串] | 記錄的唯一、系統產生的字串識別碼。 此欄位用於追蹤個別記錄的唯一性、防止資料重複，以及在下游服務中查詢該記錄。<br><br>由於此欄位是系統產生的，因此在資料擷取期間不會提供明確值。 不過，您可以視需要選擇提供自己的唯一ID值。 |
| `createdByBatchID` | [!UICONTROL 字串] | 造成記錄建立的擷取批次識別碼。 |
| `modifiedByBatchID` | [!UICONTROL 字串] | 導致記錄更新的上次擷取批次識別碼。 |
| `partnerID` | [!UICONTROL 字串] | 通常是指用來識別個別潛在客戶的不重複假名識別碼。 請參閱以下檔案： [身分型別](../../identity-service/features/namespaces.md#identity-type) 以進一步瞭解合作夥伴ID以及Adobe Experience Platform中提供的其他身分型別。 |
| `repositoryCreatedBy` | [!UICONTROL 字串] | 建立紀錄的使用者ID。 |
| `repositoryLastModifiedBy` | [!UICONTROL 字串] | 上次修改紀錄的使用者ID。 建立記錄時， `modifiedByUser` 值設為 `createdByUser` 值。 |

{style="table-layout:auto"}
