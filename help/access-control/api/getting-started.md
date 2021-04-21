---
keywords: Experience Platform;home；熱門主題；訪問控制；api；快速入門
solution: Experience Platform
title: 存取控制API指南
topic-legacy: developer guide
description: Adobe Experience Platform的訪問控制允許您使用Adobe Admin Console來管理各種平台功能的角色和權限。 以下各節提供開發人員需要知道的其他資訊，以便成功呼叫架構註冊表API。
exl-id: 6fd956fb-ade4-48d3-843f-4c9a605945c9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 3%

---

# [!DNL Access Control] API指南

[!DNL Access control] 通 [!DNL Experience Platform] 過Adobe Admin Console [管](https://adminconsole.adobe.com)。此功能運用Admin Console中的產品設定檔，將使用者與權限和沙盒連結。 有關詳細資訊，請參閱[訪問控制概述](../home.md)。

本開發人員指南提供如何格式化您的要求至[[!DNL Access Control API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/access-control.yaml)的資訊，並涵蓋下列作業：

- [權限和資源類型的清單名稱](./permissions-and-resource-types.md)
- [查看當前用戶的有效策略](./effective-policies.md)

## 快速入門

以下各節提供您必須知道的其他資訊，才能成功呼叫[!DNL Schema Registry] API。

### 讀取範例API呼叫

本指南提供範例API呼叫，以示範如何格式化您的請求。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集必要標題的值

若要呼叫[!DNL Platform] API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程後，所有[!DNL Experience Platform] API呼叫中每個所需標題的值都會顯示在下面：

- 授權：載體`{ACCESS_TOKEN}`
- x-api-key:`{API_KEY}`
- x-gw-ims-org-id:`{IMS_ORG}`

[!DNL Experience Platform]中的所有資源都隔離到特定的虛擬沙盒。 對[!DNL Platform] API的所有請求都需要一個標題，該標題指定要在中執行操作的沙盒的名稱：

- x-sandbox-name:`{SANDBOX_NAME}`

>[!NOTE]
>
>如需[!DNL Platform]中沙盒的詳細資訊，請參閱[沙盒概述檔案](../../sandboxes/home.md)。

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

- 內容類型：application/json

## 後續步驟

現在您已收集到必要的認證，您可以繼續閱讀其餘的開發人員指南。 每個區段都提供其端點的重要資訊，並示範執行CRUD作業的範例API呼叫。 每個呼叫都包含一般API格式、顯示必要標題和正確格式化負載的範例要求，以及成功呼叫的範例回應。
