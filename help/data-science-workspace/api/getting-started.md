---
keywords: Experience Platform；開發人員指南；端點；資料科學工作區；熱門主題；資料科學工作區；資料科學
solution: Experience Platform
title: Sensei機器學習API指南
description: Sensei機器學習API允許開發人員對各種資料科學工作區資源執行CRUD操作。 請遵循本指南以了解如何使用 API 執行關鍵作業。
exl-id: d51d0eb2-b1e9-4cc1-889a-9487395703b0
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 9%

---

# [!DNL Sensei Machine Learning] API指南

的 [!DNL Sensei Machine Learning] API為資料科學家提供了一種機制來組織和管理機器學習服務，從算法登陸到實驗和服務部署。

本開發人員指南提供了幫助您開始使用 [Sensei機器學習API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml)，並演示對各種Data Science Workspace資源執行CRUD操作的API調用。

## 快速入門

您必須完成 [認證](https://www.adobe.com/go/platform-api-authentication-en) 教程，以便能夠訪問以下請求標頭以調用 [!DNL Adobe Experience Platform] API:

* 授權：持 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

中的所有資源 [!DNL Experience Platform] 與特定虛擬沙箱隔離。 所有請求 [!DNL Platform] API需要一個標頭，該標頭指定操作將在以下位置進行的沙盒的名稱：

* x-sandbox-name: `{SANDBOX_NAME}`

有關中的沙箱的詳細資訊 [!DNL Platform]，請參見 [沙盒概述文檔](../../sandboxes/home.md)。

包含負載(POST、PUT、PATCH)的所有請求都需要附加的標頭：

* 內容類型：應用程式/json

## 後續步驟

收集了所需的身份驗證憑據後，您可以繼續閱讀本開發人員指南的後續部分，瞭解對以下端點組的示例API調用：

* [引擎](./engines.md)
* [實驗](./experiments.md)
* [Insights](./insights.md)
* [MLInstances（配方）](./mlinstances.md)
* [MLS服務](./mlservices.md)
* [模型](./models.md)
* [附錄](./appendix.md)
