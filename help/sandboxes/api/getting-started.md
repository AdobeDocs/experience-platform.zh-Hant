---
keywords: Experience Platform；首頁；熱門主題；沙箱開發人員指南
solution: Experience Platform
title: 開始使用沙箱API
description: 沙箱API可讓開發人員以程式設計方式管理Adobe Experience Platform中的沙箱。 請遵循本指南以了解如何使用 API 執行關鍵作業。
role: Developer
exl-id: 1ae27f30-2f89-4bfa-887d-a5def17b5cbc
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 15%

---

# 開始使用沙箱API

Adobe Experience Platform中的沙箱提供獨立的開發環境，可讓您測試功能、執行實驗及進行自訂設定，而不會影響您的生產環境。

此開發人員指南提供步驟，協助您使用沙箱API管理Experience Platform中的沙箱，並包含執行各種操作的範例API呼叫。

## 先決條件

若要管理組織的沙箱，您必須擁有沙箱管理許可權。 沒有存取許可權的使用者只能使用[可用的沙箱端點](./available.md)來列出目前使用者的使用中沙箱。 如需如何為Experience Platform指派沙箱許可權的詳細資訊，請參閱[存取控制總覽](../../access-control/home.md)。

### 讀取範例 API 呼叫

本指南提供範例 API 呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭和正確格式化的請求承載。 此外，也提供 API 回應中傳回的範例 JSON。 如需在範例API呼叫檔案中所使用的慣例相關資訊，請參閱Experience Platform疑難排解指南中有關[如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request)的章節。

### 收集所需標頭的值

本指南要求您完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)，才能成功呼叫Platform API。 完成驗證教學課程，在所有Experience Platform API呼叫中提供每個必要標題的值，如下所示：

* 授權：持有人`{ACCESS_TOKEN}`
* x-api-key： `{API_KEY}`
* x-gw-ims-org-id： `{ORG_ID}`

除了驗證標頭之外，所有請求都需要標頭，指定將在其中進行操作的沙箱名稱：

* x-sandbox-name： `{SANDBOX_NAME}`

包含裝載(POST、PUT和PATCH)的所有請求都需要額外的標頭：

* Content-Type： application/json

## 後續步驟

現在您已收集到所需的認證，您可以繼續閱讀開發人員指南的其餘部分。 每個區段都提供有關其端點的重要資訊，並示範用於執行CRUD操作的範例API呼叫。 每個呼叫都包含一般API格式、顯示必要標題和正確格式負載的範例請求，以及成功呼叫的範例回應。
