---
keywords: Experience Platform；開發人員指南；端點；資料科學工作區；熱門主題；資料科學工作區；資料科學
solution: Experience Platform
title: Sensei Machine Learning API指南
topic-legacy: Developer guide
description: Sensei Machine Learning API可讓開發人員對各種資料科學工作區資源執行CRUD作業。 請依照本指南，瞭解如何使用API執行關鍵作業。
exl-id: d51d0eb2-b1e9-4cc1-889a-9487395703b0
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 2%

---

# [!DNL Sensei Machine Learning] API指南

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

在您收集到所需的驗證憑證後，就可繼續閱讀本開發人員指南的後續章節，以取得下列端點群組的範例API呼叫：

* [引擎](./engines.md)
* [實驗](./experiments.md)
* [見解](./insights.md)
* [MLInstances(Recipes)](./mlinstances.md)
* [MLServices](./mlservices.md)
* [模型](./models.md)
* [附錄](./appendix.md)
