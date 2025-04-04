---
title: 開始使用沙箱工具API
description: 使用沙箱工具API來檢查成品，並匯出和匯入沙箱之間的沙箱設定快照。 請遵循本指南以了解如何使用 API 執行關鍵作業。
exl-id: 0b34d153-a603-4397-a375-9cc846efe23a
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 15%

---

# 開始使用沙箱工具API {#getting-started}

此開發人員指南提供步驟，協助您使用沙箱工具API管理Adobe Experience Platform中的套件和工具，並包含執行各種操作的範例API呼叫。

## 讀取範例 API 呼叫 {#api-calls}

本指南提供範例 API 呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭和正確格式化的請求承載。 此外，也提供傳回至API回應的範例JSON資料。 如需範例API呼叫檔案中所使用慣例的詳細資訊，請參閱Experience Platform疑難排解指南中有關[如何讀取範例API呼叫](/help/landing/troubleshooting.md#how-do-i-format-an-api-request)的章節。

## 收集所需標頭的值 {#headers}

本指南要求您完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)，才能成功呼叫Experience Platform API。 完成驗證教學課程，在所有Experience Platform API呼叫中提供每個必要標題的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

除了驗證標頭之外，所有請求都需要標頭，指定將在其中進行操作的沙箱名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

包含裝載(POST、PUT和PATCH)的所有請求都需要額外的標頭：

* `Content-Type: application/json`

## 後續步驟 {#next-steps}

現在您已收集到所需的認證，您可以繼續閱讀開發人員指南的其餘部分。 每個區段都提供有關其端點的重要資訊，並示範用於執行CRUD操作的範例API呼叫。 每個呼叫都包含一般API格式、顯示必要標題和正確格式負載的範例請求，以及成功呼叫的範例回應。

請參閱下列API教學課程，以開始呼叫沙箱工具API：

* [套件端點](./packages.md)
* [工具端點](./tools.md)
