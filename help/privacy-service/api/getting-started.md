---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 隱私權服務開發人員指南
description: 使用REST風格的API，跨Adobe Experience Cloud應用程式管理資料主體的個人資料
topic: developer guide
translation-type: tm+mt
source-git-commit: 6a28ad2725094e0748e2860276ab2e7581d790ac

---


# 隱私權服務開發人員指南

Adobe Experience Platform Privacy Service提供REST風格的API和使用者介面，可讓您跨Adobe Experience Cloud應用程式管理（存取和刪除）您資料主體（客戶）的個人資料。 隱私權服務也提供集中稽核和記錄機制，讓您存取與Experience Cloud應用程式有關的工作狀態和結果。

本指南涵蓋如何使用隱私權服務API。 如需如何使用UI的詳細資訊，請參閱隱 [私服務UI概觀](../ui/overview.md)。 如需隱私權服務API中所有可用端點的完整清單，請參閱 [API參考](https://www.adobe.io/apis/experiencecloud/gdpr/api-reference.html)。

## 快速入門

本指南需要有效瞭解下列Experience Platform功能：

* [隱私權服務](../home.md):提供REST風格的API和使用者介面，可讓您跨Adobe Experience Cloud應用程式管理資料主體（客戶）的存取和刪除要求。

以下各節提供您必須知道的其他資訊，以便成功呼叫隱私權服務API。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱「Experience Platform疑難排解指 [南」中有關如何讀取範例API呼叫的章節](https://www.adobe.io/apis/experienceplatform/home/services/troubleshooting.html#!api-specification/markdown/narrative/technical_overview/platform_faq_and_troubleshooting/platform_faq_and_troubleshooting.md) 。

### 收集必要標題的值

若要呼叫平台API，您必須先完成驗證教 [學課程](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html#!api-specification/markdown/narrative/tutorials/authenticate_to_acp_tutorial/authenticate_to_acp_tutorial.md)。 完成驗證教學課程後，所有Experience Platform API呼叫中每個必要標題的值都會顯示在下方：

* 授權：生產者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

* 內容類型：application/json

## 後續步驟

現在您已瞭解要使用的標題，可以開始呼叫隱私權服務API。 隱私權工 [作的檔案](privacy-jobs.md) ，會逐步說明您可使用隱私權服務API進行的各種API呼叫。 每個範例呼叫都包含一般API格式、顯示必要標題的範例要求，以及範例回應。
