---
solution: Experience Platform
title: 統一標籤API快速入門
description: 以下檔案提供成功使用統一標籤API所需瞭解的其他資訊。
role: Developer
exl-id: 8f33707f-b46d-4054-802c-9e42ecabd9ba
source-git-commit: 717a4ea0568200c940cf9b8f26f4dd2aa9c00a3e
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 9%

---

# 統一標籤API快速入門 {#getting-started}

統一標籤API可讓您在Adobe Experience Platform中分類及管理您的企業物件。

以下小節提供成功使用統一標籤API所需瞭解的其他資訊。

## 讀取範例 API 呼叫

統一標籤API檔案提供範例API呼叫，示範如何設定請求格式。 這些包括路徑、必要的標頭和正確格式化的請求承載。 此外，也提供 API 回應中傳回的範例 JSON。 如需檔案中所使用之範例API呼叫慣例的詳細資訊，請參閱Experience Platform疑難排解指南中有關[如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request)的章節。

## 必要的標頭

API檔案也要求您完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)，才能成功呼叫Platform端點。 完成驗證教學課程，提供Experience Platform API呼叫中每個必要標題的值，如下所示：

- 授權： `Bearer {ACCESS_TOKEN}`
- x-api-key： `{API_KEY}`
- x-gw-ims-org-id： `{ORG_ID}`

[!DNL Experience Platform]中的所有資源都與特定的虛擬沙箱隔離。 對[!DNL Platform] API的所有請求都需要一個標頭，以指定將執行操作的沙箱名稱：

- x-sandbox-name： `{SANDBOX_NAME}`

>[!NOTE]
>
>如需在[!DNL Experience Platform]中使用沙箱的詳細資訊，請參閱[沙箱概觀檔案](../../sandboxes/home.md)。

## 後續步驟

若要使用整合標籤API進行呼叫，請使用左側導覽或在[開發人員指南概覽](./overview.md)中，選取其中一個可用的端點指南
