---
keywords: Experience Platform；開發人員指南；端點；Data Science Workspace；熱門主題；Data Science Workspace；資料科學
solution: Experience Platform
title: Sensei Machine Learning API指南
description: Sensei機器學習API可讓開發人員對各種Data Science Workspace資源執行CRUD作業。 請遵循本指南以了解如何使用 API 執行關鍵作業。
exl-id: d51d0eb2-b1e9-4cc1-889a-9487395703b0
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 9%

---

# [!DNL Sensei Machine Learning] API指南

此 [!DNL Sensei Machine Learning] API為資料科學家提供一種機制，用於組織和管理機器學習服務，從演算法上線、實驗到服務部署。

本開發人員指南提供步驟，協助您開始使用 [Sensei機器學習API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml)，並示範API呼叫，以對各種Data Science Workspace資源執行CRUD作業。

## 快速入門

您必須完成 [驗證](https://www.adobe.com/go/platform-api-authentication-en) 本教學課程，可存取下列要求標題，以呼叫 [!DNL Adobe Experience Platform] API:

* 授權：承載 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

中的所有資源 [!DNL Experience Platform] 與特定虛擬沙箱隔離。 所有請求 [!DNL Platform] API需要標頭，以指定要在中執行操作的沙箱名稱：

* x-sandbox-name: `{SANDBOX_NAME}`

如需中沙箱的詳細資訊，請參閱 [!DNL Platform]，請參閱 [沙箱概述檔案](../../sandboxes/home.md).

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

* 內容類型：application/json

## 後續步驟

收集到所需的驗證憑證後，您可以繼續參閱本開發人員指南的後續章節，以取得對下列端點群組發出的範例API呼叫：

* [引擎](./engines.md)
* [實驗](./experiments.md)
* [Insights](./insights.md)
* [MLInstances（訣竅）](./mlinstances.md)
* [MLServices](./mlservices.md)
* [模型](./models.md)
* [附錄](./appendix.md)
