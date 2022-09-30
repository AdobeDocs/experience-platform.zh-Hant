---
keywords: Experience Platform；首頁；熱門主題；基於屬性的訪問控制；基於屬性的訪問控制
title: 基於屬性的訪問控制快速入門
description: 基於屬性的存取控制可讓您以程式設計方式管理Adobe Experience Platform中的角色和原則。 請遵循本指南以了解如何使用 API 執行關鍵作業。
exl-id: d1a66afa-dff4-49d7-b57c-527f05977155
source-git-commit: 9e44e647e4647a323fa9d1af55266d6f32b5ccb9
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 4%

---

# 開始使用基於屬性的訪問控制

本開發人員指南提供的步驟可協助您使用屬性型存取控制來管理Adobe Experience Platform中的角色、產品、權限類別和權限集，並包含執行各種作業的範例API呼叫。

## 讀取範例API呼叫

本指南提供範例API呼叫，以示範如何設定請求格式。 這些功能包括路徑、必要標題和格式正確的請求裝載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所使用慣例的相關資訊，請參閱 [如何閱讀API呼叫範例](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) Experience Platform疑難排解指南中。

## 收集必要標題的值

本指南要求您完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en) 以便成功呼叫Platform API。 完成驗證教學課程後，所有Experience PlatformAPI呼叫中每個必要標題的值都會顯示，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

除了驗證標題外，所有要求都需要標題，以指定作業將在下列位置進行的沙箱名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含裝載(POST、PUT和PATCH)的請求都需要額外的標題：

* `Content-Type: application/json`

## 後續步驟

現在您已收集必要的認證，您可以繼續閱讀開發人員指南的其餘部分。 每個區段都提供其端點的重要資訊，並示範執行CRUD作業的範例API呼叫。 每個呼叫都包含一般API格式、顯示必要標題和格式正確之裝載的範例要求，以及成功呼叫的範例回應。

請參閱下列API教學課程，以開始呼叫屬性型存取控制API:

* [角色端點](./roles.md)
* [產品端點](./products.md)
