---
keywords: Experience Platform；配置；即時客戶配置；故障排除；API
title: 資料接收API入門
type: Documentation
description: 「資料接收API入門」指南概述了在開始使用API將資料導入Experience Platform之前需要瞭解的關鍵概念和基本功能。
exl-id: 0653de2b-3268-478b-a23f-c458b6d3df7c
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 0%

---

# 資料接收API入門 {#getting-started}

使用資料接收API端點，可以執行基本的CRUD操作以在Adobe Experience Platform中接收資料。

使用API指南需要瞭解與處理資料有關的多個Adobe Experience Platform服務。 在使用資料接收API之前，請查看以下服務的文檔：

* [批量攝取](./overview.md):允許您將資料作為批處理檔案插入Adobe Experience Platform。
* [[!DNL Real-Time Customer Profile]](../home.md):根據來自多個來源的聚合資料即時提供統一的客戶配置檔案。
* [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):平台組織客戶體驗資料的標準化框架。
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙箱，將單個沙箱 [!DNL Platform] 實例到獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

以下各節提供了您需要瞭解的其他資訊，以便成功撥打 [!DNL Profile] API終結點。

## 讀取示例API調用

Data Ingestion API文檔提供了示例API調用，以演示如何正確格式化請求。 這些包括路徑、必需的標頭和正確格式化的請求負載。 還提供了API響應中返回的示例JSON。 有關示例API調用文檔中使用的約定的資訊，請參見上的 [如何讀取示例API調用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 的 [!DNL Experience Platform] 疑難解答指南。

## 必需的標題

API文檔還要求您完成 [驗證教程](https://www.adobe.com/go/platform-api-authentication-en) 以便成功撥打 [!DNL Platform] 端點。 完成身份驗證教程將提供中每個必需標頭的值 [!DNL Experience Platform] API調用，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

請求主體中具有負載的所有請求(如POST、PUT和PATCH呼叫)必須包括 `Content-Type` 標題。 在呼叫參數中提供特定於每個呼叫的接受值。

中的所有資源 [!DNL Experience Platform] 與特定虛擬沙箱隔離。 請求 [!DNL Platform] API需要一個標頭，該標頭指定操作將在以下位置進行的沙盒的名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

有關中的沙箱的詳細資訊 [!DNL Platform]，請參見 [沙盒概述文檔](../../sandboxes/home.md)。
