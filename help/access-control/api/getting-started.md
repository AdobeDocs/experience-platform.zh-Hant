---
keywords: Experience Platform；首頁；熱門主題；存取控制；api；快速入門
solution: Experience Platform
title: 存取控制API指南
description: Adobe Experience Platform中的存取控制可讓您使用Adobe Admin Console管理各種平台功能的角色和權限。 以下小節提供開發人員需要知道的其他資訊，以便成功呼叫結構註冊表API。
exl-id: 6fd956fb-ade4-48d3-843f-4c9a605945c9
source-git-commit: 7b197f253aa5ce04a682040814cf749407154ebc
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 2%

---

# [!DNL Access Control] API指南

[!DNL Access control] for [!DNL Experience Platform] 是透過 [Adobe Admin Console](https://adminconsole.adobe.com). 此功能會運用Admin Console中的產品設定檔，將使用者與權限和沙箱連結。 請參閱 [存取控制概觀](../home.md) 以取得更多資訊。

本開發人員指南提供如何將請求格式化至 [[!DNL Access Control API]](https://www.adobe.io/experience-platform-apis/references/access-control/)，並涵蓋下列操作：

- [權限和資源類型的清單名稱](./permissions-and-resource-types.md)
- [查看當前用戶的有效訪問策略](./effective-policies.md)

## 快速入門

以下小節提供您需要知道的其他資訊，以便成功呼叫 [!DNL Access Control] API。

### 讀取範例API呼叫

本指南提供範例API呼叫，以示範如何設定請求格式。 這些功能包括路徑、必要標題和格式正確的請求裝載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所使用慣例的相關資訊，請參閱 [如何閱讀API呼叫範例](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑難排解指南。

### 收集必要標題的值

若要對 [!DNL Platform] API，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程會提供所有 [!DNL Experience Platform] API呼叫，如下所示：

- 授權：承載 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

中的所有資源 [!DNL Experience Platform] 與特定虛擬沙箱隔離。 所有請求 [!DNL Platform] API需要標頭，以指定要在中執行操作的沙箱名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>如需中沙箱的詳細資訊，請參閱 [!DNL Platform]，請參閱 [沙箱概述檔案](../../sandboxes/home.md).

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

- 內容類型：application/json

## 後續步驟

現在您已收集必要的認證，您可以繼續閱讀開發人員指南的其餘部分。 每個區段都提供其端點的重要資訊，並示範執行CRUD作業的範例API呼叫。 每個呼叫都包含一般API格式、顯示必要標題和格式正確之裝載的範例要求，以及成功呼叫的範例回應。
