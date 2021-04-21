---
keywords: Experience Platform；首頁；熱門主題；沙盒開發人員指南
solution: Experience Platform
title: 沙盒API指南
topic-legacy: developer guide
description: 沙盒API可讓開發人員以程式設計方式管理Adobe Experience Platform的沙盒。 請依照本指南，瞭解如何使用API執行關鍵作業。
exl-id: 1ae27f30-2f89-4bfa-887d-a5def17b5cbc
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 0%

---

# 沙盒API指南

Adobe Experience Platform的沙盒提供獨立的開發環境，讓您測試功能、執行實驗並製作自訂組態，而不會影響您的生產環境。

本開發人員指南提供步驟，協助您使用沙盒API來管理Experience Platform中的沙盒，並包含執行各種作業的範例API呼叫。

## 沙盒API快速入門

若要管理IMS組織的沙盒，您必須擁有沙盒管理權限。 不具存取權限的使用者只能使用[的端點，列出目前使用者](./list-active-sandboxes.md)的作用中沙盒。 如需如何指派沙盒權限以進行Experience Platform的詳細資訊，請參閱[存取控制概觀](../../access-control/home.md)。

### 讀取範例API呼叫

本指南提供範例API呼叫，以示範如何格式化您的請求。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫說明檔案中使用之慣例的詳細資訊，請參閱Experience Platform疑難排解指南中[如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集必要標題的值

本指南要求您完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)，才能成功呼叫平台API。 完成驗證教學課程後，將提供所有Experience PlatformAPI呼叫中每個必要標題的值，如下所示：

* 授權：載體`{ACCESS_TOKEN}`
* x-api-key:`{API_KEY}`
* x-gw-ims-org-id:`{IMS_ORG}`

除了驗證標題外，所有請求都需要一個標題，該標題會指定執行下列操作的沙盒名稱：

* x-sandbox-name:`{SANDBOX_NAME}`

所有包含裝載(POST、PUT和PATCH)的請求都需要額外的標題：

* 內容類型：application/json

## 後續步驟

現在您已收集到必要的認證，您可以繼續閱讀其餘的開發人員指南。 每個區段都提供其端點的重要資訊，並示範執行CRUD作業的範例API呼叫。 每個呼叫都包含一般API格式、顯示必要標題和正確格式化負載的範例要求，以及成功呼叫的範例回應。
