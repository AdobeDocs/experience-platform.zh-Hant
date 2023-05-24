---
keywords: Experience Platform；首頁；熱門主題；訪問控制；api；入門
solution: Experience Platform
title: 訪問控制API指南
description: Adobe Experience Platform的訪問控制允許您使用Adobe Admin Console管理各種平台功能的角色和權限。 以下各節提供了開發人員需要瞭解的其他資訊，以便成功調用架構註冊表API。
exl-id: 6fd956fb-ade4-48d3-843f-4c9a605945c9
source-git-commit: 7b197f253aa5ce04a682040814cf749407154ebc
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 2%

---

# [!DNL Access Control] API指南

[!DNL Access control] 為 [!DNL Experience Platform] 通過 [Adobe Admin Console](https://adminconsole.adobe.com)。 此功能利用Admin Console中的產品配置檔案，將用戶與權限和沙箱連結起來。 查看 [訪問控制概述](../home.md) 的子菜單。

此開發人員指南提供有關如何將請求格式化到 [[!DNL Access Control API]](https://www.adobe.io/experience-platform-apis/references/access-control/)，並包括以下操作：

- [權限和資源類型的清單名](./permissions-and-resource-types.md)
- [查看當前用戶的有效訪問策略](./effective-policies.md)

## 快速入門

以下各節提供了您需要瞭解的其他資訊，以便成功呼叫 [!DNL Access Control] API。

### 讀取示例API調用

本指南提供了示例API調用，以演示如何格式化請求。 這些包括路徑、必需的標頭和正確格式化的請求負載。 還提供了API響應中返回的示例JSON。 有關示例API調用文檔中使用的約定的資訊，請參見上的 [如何讀取示例API調用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 的 [!DNL Experience Platform] 疑難解答指南。

### 收集所需標題的值

為了呼叫 [!DNL Platform] API，必須首先完成 [驗證教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份驗證教程將提供所有中每個必需標頭的值 [!DNL Experience Platform] API調用，如下所示：

- 授權：持 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

中的所有資源 [!DNL Experience Platform] 與特定虛擬沙箱隔離。 所有請求 [!DNL Platform] API需要一個標頭，該標頭指定操作將在以下位置進行的沙盒的名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有關中的沙箱的詳細資訊 [!DNL Platform]，請參見 [沙盒概述文檔](../../sandboxes/home.md)。

包含負載(POST、PUT、PATCH)的所有請求都需要附加的標頭：

- 內容類型：應用程式/json

## 後續步驟

現在，您已收集了所需的憑據，現在可以繼續閱讀開發人員指南的其餘部分。 每個部分都提供有關其端點的重要資訊，並演示用於執行CRUD操作的示例API調用。 每個調用都包括一般API格式、顯示所需標頭和正確格式化負載的示例請求，以及成功調用的示例響應。
