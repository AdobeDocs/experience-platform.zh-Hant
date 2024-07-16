---
keywords: Experience Platform；開發人員指南；端點；資料科學Workspace；熱門主題；資料科學工作區；資料科學
solution: Experience Platform
title: Sensei Machine Learning API指南
description: Sensei機器學習API可讓開發人員對各種資料科學Workspace資源執行CRUD操作。 請遵循本指南以了解如何使用 API 執行關鍵作業。
role: Developer
exl-id: d51d0eb2-b1e9-4cc1-889a-9487395703b0
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 14%

---

# [!DNL Sensei Machine Learning] API指南

[!DNL Sensei Machine Learning] API為資料科學家提供組織和管理機器學習服務的機制，從演演算法上線到實驗，再到服務部署。

本開發人員指南提供步驟，協助您開始使用[Sensei Machine Learning API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml)，並示範在各種資料科學Workspace資源上執行CRUD作業的API呼叫。

## 快速入門

您必須完成[驗證](https://www.adobe.com/go/platform-api-authentication-en)教學課程，才能存取下列要求標頭來呼叫[!DNL Adobe Experience Platform] API：

* 授權：持有人`{ACCESS_TOKEN}`
* x-api-key： `{API_KEY}`
* x-gw-ims-org-id： `{ORG_ID}`

[!DNL Experience Platform]中的所有資源都與特定的虛擬沙箱隔離。 對[!DNL Platform] API的所有請求都需要標頭，以指定將在其中執行作業的沙箱名稱：

* x-sandbox-name： `{SANDBOX_NAME}`

如需[!DNL Platform]中沙箱的詳細資訊，請參閱[沙箱概觀檔案](../../sandboxes/home.md)。

所有包含承載 (POST、PUT、PATCH) 的請求都需有額外的標頭：

* Content-Type： application/json

## 後續步驟

收集完所需的驗證認證後，您可以繼續參閱本開發人員指南的後續章節，以取得對以下端點群組的範例API呼叫：

* [引擎](./engines.md)
* [實驗](./experiments.md)
* [Insights](./insights.md)
* [MLInstances （配方）](./mlinstances.md)
* [MLServices](./mlservices.md)
* [模型](./models.md)
* [附錄](./appendix.md)
