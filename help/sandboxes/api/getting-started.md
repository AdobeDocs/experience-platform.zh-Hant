---
keywords: Experience Platform；首頁；熱門主題；沙盒開發人員指南
solution: Experience Platform
title: 沙盒API入門
description: 沙盒API允許開發人員以寫程式方式管理Adobe Experience Platform的沙盒。 請遵循本指南以了解如何使用 API 執行關鍵作業。
exl-id: 1ae27f30-2f89-4bfa-887d-a5def17b5cbc
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 5%

---

# 沙盒API入門

Adobe Experience Platform的沙箱提供獨立的開發環境，使您能夠test功能、運行實驗和進行定制配置，而不會影響您的生產環境。

本開發人員指南提供了一些步驟，幫助您使用沙盒API管理Experience Platform中的沙盒，並包括執行各種操作的示例API調用。

## 先決條件

為了管理組織的沙箱，您必須具有「沙箱管理」權限。 沒有訪問權限的用戶只能使用 [可用沙箱端點](./available.md) 列出當前用戶的活動沙箱。 查看 [訪問控制概述](../../access-control/home.md) 的子菜單。

### 讀取示例API調用

本指南提供了示例API調用，以演示如何格式化請求。 這些包括路徑、必需的標頭和正確格式化的請求負載。 還提供了API響應中返回的示例JSON。 有關示例API調用文檔中使用的約定的資訊，請參見上的 [如何讀取示例API調用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) Experience Platform疑難解答指南。

### 收集所需標題的值

本指南要求您完成 [驗證教程](https://www.adobe.com/go/platform-api-authentication-en) 以便成功調用平台API。 完成Experience Platform教程將提供所有驗證API調用中每個必需標頭的值，如下所示：

* 授權：持 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

除了驗證標頭之外，所有請求都需要一個標頭，該標頭指定操作將在以下位置進行的沙盒的名稱：

* x-sandbox-name: `{SANDBOX_NAME}`

包含負載(POST、PUT和PATCH)的所有請求都需要附加標頭：

* 內容類型：應用程式/json

## 後續步驟

現在，您已收集了所需的憑據，現在可以繼續閱讀開發人員指南的其餘部分。 每個部分都提供有關其端點的重要資訊，並演示用於執行CRUD操作的示例API調用。 每個調用都包括一般API格式、顯示所需標頭和正確格式化負載的示例請求，以及成功調用的示例響應。
