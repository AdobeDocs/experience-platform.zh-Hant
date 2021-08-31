---
keywords: Experience Platform；首頁；熱門主題；存取控制；api；快速入門
solution: Experience Platform
title: 存取控制API指南
topic-legacy: developer guide
description: Adobe Experience Platform中的存取控制可讓您使用Adobe Admin Console管理各種平台功能的角色和權限。 以下小節提供開發人員需要知道的其他資訊，以便成功呼叫結構註冊表API。
exl-id: 6fd956fb-ade4-48d3-843f-4c9a605945c9
source-git-commit: 2a73571d806f1653dad29d2c0b0067c5ce63e0e7
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 2%

---

# [!DNL Access Control] API指南

[!DNL Access control] 的 [!DNL Experience Platform] 管理方式為 [Adobe Admin Console](https://adminconsole.adobe.com)。此功能會運用Admin Console中的產品設定檔，將使用者與權限和沙箱連結。 有關詳細資訊，請參閱[訪問控制概述](../home.md)。

本開發人員指南提供如何將請求格式化到[[!DNL Access Control API]](https://www.adobe.io/experience-platform-apis/references/access-control/)的資訊，並涵蓋下列操作：

- [權限和資源類型的清單名稱](./permissions-and-resource-types.md)
- [查看當前用戶的有效策略](./effective-policies.md)

## 快速入門

以下各節提供您需要了解的其他資訊，以便成功呼叫[!DNL Schema Registry] API。

### 讀取範例API呼叫

本指南提供範例API呼叫，以示範如何設定請求格式。 這些功能包括路徑、必要標題和格式正確的請求裝載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所使用慣例的資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集必要標題的值

若要呼叫[!DNL Platform] API，您必須先完成[authentication tutorial](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程後，將提供所有[!DNL Experience Platform] API呼叫中每個必要標題的值，如下所示：

- 授權：承載`{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

[!DNL Experience Platform]中的所有資源都與特定虛擬沙箱隔離。 對[!DNL Platform] API的所有請求都需要標題，以指定作業將在下列位置進行的沙箱名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>如需[!DNL Platform]中沙箱的詳細資訊，請參閱[沙箱概觀檔案](../../sandboxes/home.md)。

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

- 內容類型：application/json

## 後續步驟

現在您已收集必要的認證，您可以繼續閱讀開發人員指南的其餘部分。 每個區段都提供其端點的重要資訊，並示範執行CRUD作業的範例API呼叫。 每個呼叫都包含一般API格式、顯示必要標題和格式正確之裝載的範例要求，以及成功呼叫的範例回應。
