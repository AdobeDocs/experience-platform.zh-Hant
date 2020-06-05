---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: Sensei Machine Learning API開發人員指南
topic: Developer guide
translation-type: tm+mt
source-git-commit: 83e74ad93bdef056c8aef07c9d56313af6f4ddfd
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 2%

---


# Sensei Machine Learning API開發人員指南

Sensei機器學習API為資料科學家提供機制，以組織和管理機器學習服務，從演算法上線到實驗，再到服務部署。

本開發人員指南提供協助您開始使用 [Sensei Machine Learning API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml)，並示範針對各種資料科學工作區資源執行CRUD作業的API呼叫。

## 快速入門

您必須完成驗證教 [學課程](../../tutorials/authentication.md) ，才能存取下列請求標題以呼叫 [!DNL Adobe Experience Platform] API:

* 授權： 生產者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有資源都隔離至特定的虛擬沙盒。 所有對平台API的請求都需要一個標題，該標題會指定要在中執行的操作的沙盒名稱：

* x-sandbox-name: `{SANDBOX_NAME}`

如需平台中沙盒的詳細資訊，請參閱沙盒 [概觀檔案](../../sandboxes/home.md)。

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

* 內容類型： application/json

## 後續步驟

在您收集到所需的驗證憑證後，就可繼續閱讀本開發人員指南的後續章節，以取得下列端點群組的範例API呼叫：

* [引擎](./engines.md)
* [實驗](./experiments.md)
* [見解](./insights.md)
* [MLInstances(Recipes)](./mlinstances.md)
* [MLServices](./mlservices.md)
* [模型](./models.md)
* [附錄](./appendix.md)