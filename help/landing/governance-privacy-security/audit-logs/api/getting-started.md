---
title: 稽核查詢API快速入門
description: 稽核查詢API可讓您擷取各種Adobe Experience Platform功能的量度資料。 本檔案簡介您在嘗試呼叫稽核查詢API前，需要知道的核心概念。
exl-id: 20eab0a8-98f7-4fee-8f91-88324e54ab18
source-git-commit: c2c5778e0a3fff7f488ad7a672123c813cca59f1
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 9%

---

# 稽核查詢API快速入門

Adobe Experience Platform可讓您以稽核事件記錄形式，稽核各種服務和功能的使用者活動。 稽核記錄中所記錄的每個動作都包含中繼資料，其指出動作類型、日期和時間、執行動作之使用者的電子郵件 ID，以及與動作類型相關的其他屬性。

「稽核查詢API」可讓您以稽核事件記錄的形式，稽核各種服務和功能的使用者活動。 本檔案簡介您在嘗試呼叫稽核查詢API前，需要知道的核心概念。

## 先決條件

若要管理稽核事件，您必須具備 **[!UICONTROL 查看用戶活動日誌]** 授予的存取控制權限(可在 [!UICONTROL 資料控管] 類別)。 若要了解如何管理Platform功能的個別權限，請參閱 [存取控制檔案](../../../../access-control/home.md).

### 讀取範例API呼叫

本指南提供範例API呼叫，以示範如何設定請求格式。 這些功能包括路徑、必要標題和格式正確的請求裝載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所使用慣例的相關資訊，請參閱 [如何閱讀API呼叫範例](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) Experience Platform疑難排解指南中。

### 收集必要標題的值

本指南要求您完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en) 以便成功呼叫Platform API。 完成驗證教學課程後，所有Experience PlatformAPI呼叫中每個必要標題的值都會顯示，如下所示：

* 授權：承載 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

中的所有資源 [!DNL Experience Platform] 與特定虛擬沙箱隔離。 所有請求 [!DNL Platform] API需要標頭，以指定要進行操作的沙箱名稱。 如需中沙箱的詳細資訊，請參閱 [!DNL Platform]，請參閱 [沙箱概述檔案](../../../../sandboxes/home.md).

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含裝載(POST、PUT和PATCH)的請求都需要額外的標題：

* 內容類型：application/json

## 後續步驟

若要開始使用進行呼叫 [!DNL Audit Query] API，請參閱 [events endpoint指南](./events.md) 和 [匯出端點指南](./export.md).
