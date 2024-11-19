---
title: 開始使用稽核查詢API
description: 稽核查詢API可讓您擷取各種Adobe Experience Platform功能的量度資料。 本檔案介紹嘗試呼叫Audit Query API之前需要瞭解的核心概念。
role: Developer
feature: Audits, API
exl-id: 20eab0a8-98f7-4fee-8f91-88324e54ab18
source-git-commit: c0eb5b5c3a1968cae2bc19b7669f70a97379239b
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 11%

---

# 開始使用稽核查詢API

Adobe Experience Platform可讓您以稽核事件記錄的形式，稽核各種服務和功能的使用者活動。 記錄中記錄的每個動作都包含中繼資料，其指出動作型別、日期和時間、執行動作之使用者的電子郵件ID，以及與動作型別相關的其他屬性。

「稽核查詢API」可讓您以稽核事件日誌的形式稽核各種服務和功能的使用者活動。 本檔案介紹嘗試呼叫Audit Query API之前需要瞭解的核心概念。

## 先決條件

若要管理稽核事件，您必須授予&#x200B;**[!UICONTROL 檢視使用者活動記錄]**&#x200B;存取控制許可權（可在[!UICONTROL 資料控管]類別下找到）。 若要瞭解如何管理Platform功能的個別許可權，請參閱[存取控制檔案](../../../../access-control/home.md)。

### 讀取範例 API 呼叫

本指南提供範例 API 呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭和正確格式化的請求承載。 此外，也提供 API 回應中傳回的範例 JSON。 如需在範例API呼叫檔案中所使用的慣例相關資訊，請參閱Experience Platform疑難排解指南中有關[如何讀取範例API呼叫](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)的章節。

### 收集所需標頭的值

本指南要求您完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)，才能成功呼叫Platform API。 完成驗證教學課程，在所有Experience Platform API呼叫中提供每個必要標題的值，如下所示：

* 授權：持有人`{ACCESS_TOKEN}`
* x-api-key： `{API_KEY}`
* x-gw-ims-org-id： `{ORG_ID}`

[!DNL Experience Platform]中的所有資源都與特定的虛擬沙箱隔離。 對[!DNL Platform] API的所有請求都需要標頭，以指定將在其中執行作業的沙箱名稱。 如需[!DNL Platform]中沙箱的詳細資訊，請參閱[沙箱概觀檔案](../../../../sandboxes/home.md)。

* `x-sandbox-name: {SANDBOX_NAME}`

包含裝載(POST、PUT和PATCH)的所有請求都需要額外的標頭：

* Content-Type： application/json

## 後續步驟

若要開始使用[!DNL Audit Query] API進行呼叫，請參閱[事件端點指南](./events.md)和[匯出端點指南](./export.md)。
