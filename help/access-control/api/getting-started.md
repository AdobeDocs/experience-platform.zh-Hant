---
keywords: Experience Platform；首頁；熱門主題；存取控制；api；快速入門
solution: Experience Platform
title: Access Control API指南
description: Adobe Experience Platform中的存取控制可讓您使用Adobe Admin Console管理各種Platform功能的角色和許可權。 以下章節提供開發人員成功呼叫Schema Registry API所需的其他資訊。
role: Developer
exl-id: 6fd956fb-ade4-48d3-843f-4c9a605945c9
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 20%

---

# [!DNL Access Control] API指南

[!DNL Experience Platform]的[!DNL Access control]是透過[Adobe Admin Console](https://adminconsole.adobe.com)管理的。 此功能運用Admin Console中的產品設定檔，將使用者與許可權和沙箱連結。 如需詳細資訊，請參閱[存取控制總覽](../home.md)。

此開發人員指南提供如何格式化對[[!DNL Access Control API]](https://www.adobe.io/experience-platform-apis/references/access-control/)的請求的資訊，並涵蓋下列作業：

- [許可權和資源型別的清單名稱](./permissions-and-resource-types.md)
- [檢視目前使用者的有效存取原則](./effective-policies.md)

## 快速入門

下列章節提供您需瞭解的其他資訊，才能成功呼叫[!DNL Access Control] API。

### 讀取範例 API 呼叫

本指南提供範例 API 呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭和正確格式化的請求承載。 此外，也提供 API 回應中傳回的範例 JSON。 如需檔案中所使用範例API呼叫慣例的詳細資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集所需標頭的值

若要呼叫[!DNL Platform] API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程會提供所有 [!DNL Experience Platform] API 呼叫中每個必要標頭的值，如下所示：

- 授權：持有人`{ACCESS_TOKEN}`
- x-api-key： `{API_KEY}`
- x-gw-ims-org-id： `{ORG_ID}`

[!DNL Experience Platform]中的所有資源都與特定的虛擬沙箱隔離。 對[!DNL Platform] API的所有請求都需要標頭，以指定將在其中執行作業的沙箱名稱：

- x-sandbox-name： `{SANDBOX_NAME}`

>[!NOTE]
>
>如需[!DNL Platform]中沙箱的詳細資訊，請參閱[沙箱概觀檔案](../../sandboxes/home.md)。

所有包含承載 (POST、PUT、PATCH) 的請求都需有額外的標頭：

- Content-Type： application/json

## 後續步驟

現在您已收集到所需的認證，您可以繼續閱讀開發人員指南的其餘部分。 每個區段都提供有關其端點的重要資訊，並示範用於執行CRUD操作的範例API呼叫。 每個呼叫都包含一般API格式、顯示必要標題和正確格式負載的範例請求，以及成功呼叫的範例回應。
