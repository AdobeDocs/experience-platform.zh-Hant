---
keywords: Experience Platform；首頁；熱門主題；屬性型存取控制；屬性型存取控制
title: 屬性式存取控制API快速入門
description: 以屬性為基礎的存取控制API可讓您以程式設計方式管理Adobe Experience Platform中的角色和存取原則。 請遵循本指南以了解如何使用 API 執行關鍵作業。
role: Developer
exl-id: d1a66afa-dff4-49d7-b57c-527f05977155
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 17%

---

# 屬性式存取控制API快速入門

本開發人員指南提供步驟，協助您使用屬性式存取控制API來管理Adobe Experience Platform中的角色、產品、許可權類別和許可權集，並包含執行各種作業的範例API呼叫。

## 讀取範例 API 呼叫

本指南提供範例 API 呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭和正確格式化的請求承載。 此外，也提供 API 回應中傳回的範例 JSON。 如需檔案中用於範例API呼叫的慣例相關資訊，請參閱以下章節： [如何讀取範例API呼叫](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在Experience Platform疑難排解指南中。

## 收集所需標頭的值

本指南要求您已完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en) 才能成功呼叫Platform API。 完成驗證教學課程，在所有Experience Platform API呼叫中提供每個必要標題的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

除了驗證標頭之外，所有請求都需要標頭，指定將在其中進行操作的沙箱名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

包含裝載(POST、PUT和PATCH)的所有請求都需要額外的標頭：

* `Content-Type: application/json`

## 後續步驟

現在您已收集到所需的認證，您可以繼續閱讀開發人員指南的其餘部分。 每個區段都提供有關其端點的重要資訊，並示範用於執行CRUD操作的範例API呼叫。 每個呼叫都包含一般API格式、顯示必要標題和正確格式負載的範例請求，以及成功呼叫的範例回應。

請參閱下列API教學課程，以開始呼叫屬性型存取控制API：

* [角色端點](./roles.md)
* [產品端點](./products.md)
