---
keywords: Experience Platform；首頁；熱門主題；沙箱開發人員指南
solution: Experience Platform
title: 沙箱API快速入門
description: 沙箱API可讓開發人員以程式設計方式管理Adobe Experience Platform中的沙箱。 請遵循本指南以了解如何使用 API 執行關鍵作業。
exl-id: 1ae27f30-2f89-4bfa-887d-a5def17b5cbc
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 5%

---

# 沙箱API快速入門

Adobe Experience Platform中的沙箱提供孤立的開發環境，可讓您測試功能、執行實驗及進行自訂設定，而不會影響您的生產環境。

本開發人員指南提供的步驟可協助您使用沙箱API來管理Experience Platform中的沙箱，並包含執行各種作業的範例API呼叫。

## 先決條件

若要管理貴組織的沙箱，您必須擁有沙箱管理權限。 沒有存取權限的使用者只能使用 [可用沙箱端點](./available.md) 列出目前使用者的作用中沙箱。 請參閱 [存取控制概觀](../../access-control/home.md) 以取得如何指派沙箱權限以進行Experience Platform的詳細資訊。

### 讀取範例API呼叫

本指南提供範例API呼叫，以示範如何設定請求格式。 這些功能包括路徑、必要標題和格式正確的請求裝載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所使用慣例的相關資訊，請參閱 [如何閱讀API呼叫範例](../../landing/troubleshooting.md#how-do-i-format-an-api-request) Experience Platform疑難排解指南中。

### 收集必要標題的值

本指南要求您完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en) 以便成功呼叫Platform API。 完成驗證教學課程後，所有Experience PlatformAPI呼叫中每個必要標題的值都會顯示，如下所示：

* 授權：承載 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

除了驗證標題外，所有要求都需要標題，以指定作業將在下列位置進行的沙箱名稱：

* x-sandbox-name: `{SANDBOX_NAME}`

所有包含裝載(POST、PUT和PATCH)的請求都需要額外的標題：

* 內容類型：application/json

## 後續步驟

現在您已收集必要的認證，您可以繼續閱讀開發人員指南的其餘部分。 每個區段都提供其端點的重要資訊，並示範執行CRUD作業的範例API呼叫。 每個呼叫都包含一般API格式、顯示必要標題和格式正確之裝載的範例要求，以及成功呼叫的範例回應。
