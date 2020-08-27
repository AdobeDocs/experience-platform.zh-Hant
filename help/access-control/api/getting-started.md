---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 存取控制開發人員指南
topic: developer guide
translation-type: tm+mt
source-git-commit: d059f48a2a3ba6398418fd3d5b0b3fd837ff69a2
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 1%

---


# [!DNL Access control] 開發人員指南

[!DNL Access control] for [!DNL Experience Platform] 是透過 [Adobe Admin Console管理](https://adminconsole.adobe.com)。 此功能運用Admin Console中的產品設定檔，可連結使用者與權限和沙盒。 如需詳細 [資訊，請參閱存取控制概觀](../home.md) 。

本開發人員指南提供如何格式化您對 [[!DNL存取控制API]的請求](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/access-control.yaml)，並涵蓋下列作業：

- [權限和資源類型的清單名稱](./permissions-and-resource-types.md)
- [查看當前用戶的有效策略](./effective-policies.md)

## 快速入門

以下章節提供您成功呼叫 [!DNL Schema Registry] API時需要知道的其他資訊。

### 讀取範例API呼叫

本指南提供範例API呼叫，以示範如何格式化您的請求。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱疑難排解指 [南中有關如何讀取範例API呼叫的](../../landing/troubleshooting.md#how-do-i-format-an-api-request)[!DNL Experience Platform] 章節。

### 收集必要標題的值

若要呼叫API，您必 [!DNL Platform] 須先完成驗證教 [學課程](../../tutorials/authentication.md)。 完成驗證教學課程後，將提供所有 [!DNL Experience Platform] API呼叫中每個必要標題的值，如下所示：

- 授權：生產者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

中的所有資 [!DNL Experience Platform] 源都與特定虛擬沙盒隔離。 對API的所 [!DNL Platform] 有請求都需要一個標題，該標題會指定要在中執行的操作的沙盒名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>如需中沙盒的詳細資訊 [!DNL Platform]，請參閱沙 [盒概述檔案](../../sandboxes/home.md)。

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

- 內容類型：application/json

## 後續步驟

現在您已收集到必要的認證，您可以繼續閱讀其餘的開發人員指南。 每個區段都提供其端點的重要資訊，並示範執行CRUD作業的範例API呼叫。 每個呼叫都包含一般 **API格式**、顯示必要標題 **和正確格式化負載的範例請求，以及成功呼叫** 的範例回應 **** 。
