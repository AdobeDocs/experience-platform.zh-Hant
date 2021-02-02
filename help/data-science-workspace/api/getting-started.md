---
keywords: Experience Platform；開發人員指南；端點；Data Science Workspace；熱門主題；資料科學工作區；資料科學
solution: Experience Platform
title: Sensei Machine Learning API開發人員指南
topic: Developer guide
description: 本開發人員指南提供協助您開始使用Sensei Machine Learning API的步驟，並示範針對各種資料科學工作區資源執行CRUD作業的API呼叫。
translation-type: tm+mt
source-git-commit: ece2ae1eea8426813a95c18096c1b428acfd1a71
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 2%

---


# [!DNL Sensei Machine Learning] API開發人員指南

[!DNL Sensei Machine Learning] API為資料科學家提供機制，以組織和管理機器學習服務，從演算法上線到實驗，再到服務部署。

本開發人員指南提供步驟，協助您開始使用[Sensei Machine Learning API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml)，並示範針對各種資料科學工作區資源執行CRUD作業的API呼叫。

## 快速入門

您必須完成[authentication](https://www.adobe.com/go/platform-api-authentication-en)教學課程，才能存取下列請求標題以呼叫[!DNL Adobe Experience Platform] API:

* 授權：載體`{ACCESS_TOKEN}`
* x-api-key:`{API_KEY}`
* x-gw-ims-org-id:`{IMS_ORG}`

[!DNL Experience Platform]中的所有資源都隔離到特定的虛擬沙盒。 對[!DNL Platform] API的所有請求都需要一個標題，該標題指定要在中執行操作的沙盒的名稱：

* x-sandbox-name:`{SANDBOX_NAME}`

如需[!DNL Platform]中沙盒的詳細資訊，請參閱[沙盒概述檔案](../../sandboxes/home.md)。

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

* 內容類型：application/json

## 後續步驟

在您收集到所需的驗證憑證後，就可繼續閱讀本開發人員指南的後續章節，以取得對下列端點群組的範例API呼叫：

* [引擎](./engines.md)
* [實驗](./experiments.md)
* [見解](./insights.md)
* [MLInstances(Recipes)](./mlinstances.md)
* [MLServices](./mlservices.md)
* [模型](./models.md)
* [附錄](./appendix.md)