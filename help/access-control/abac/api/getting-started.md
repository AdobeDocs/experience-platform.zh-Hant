---
keywords: Experience Platform；首頁；熱門主題；基於屬性的訪問控制；基於屬性的訪問控制
title: 基於屬性的訪問控制API入門
description: 基於屬性的訪問控制API允許您以寫程式方式管理Adobe Experience Platform內的角色和訪問策略。 請遵循本指南以了解如何使用 API 執行關鍵作業。
exl-id: d1a66afa-dff4-49d7-b57c-527f05977155
source-git-commit: 54e15234d1b1050ea2cdb8b7d37c79a133a339f1
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 4%

---

# 基於屬性的訪問控制API入門

本開發人員指南提供了一些步驟，幫助您使用基於屬性的訪問控制API管理Adobe Experience Platform的角色、產品、權限類別和權限集，並包括執行各種操作的示例API調用。

## 讀取示例API調用

本指南提供了示例API調用，以演示如何格式化請求。 這些包括路徑、必需的標頭和正確格式化的請求負載。 還提供了API響應中返回的示例JSON。 有關示例API調用文檔中使用的約定的資訊，請參見上的 [如何讀取示例API調用](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) Experience Platform疑難解答指南。

## 收集所需標題的值

本指南要求您完成 [驗證教程](https://www.adobe.com/go/platform-api-authentication-en) 以便成功調用平台API。 完成Experience Platform教程將提供所有驗證API調用中每個必需標頭的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

除了驗證標頭之外，所有請求都需要一個標頭，該標頭指定操作將在以下位置進行的沙盒的名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

包含負載(POST、PUT和PATCH)的所有請求都需要附加標頭：

* `Content-Type: application/json`

## 後續步驟

現在，您已收集了所需的憑據，現在可以繼續閱讀開發人員指南的其餘部分。 每個部分都提供有關其端點的重要資訊，並演示用於執行CRUD操作的示例API調用。 每個調用都包括一般API格式、顯示所需標頭和正確格式化負載的示例請求，以及成功調用的示例響應。

請參閱以下API教程以開始調用基於屬性的訪問控制API:

* [角色終結點](./roles.md)
* [產品終結點](./products.md)
