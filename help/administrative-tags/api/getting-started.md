---
solution: Experience Platform
title: 統一標籤API快速入門
description: 以下檔案提供成功使用統一標籤API所需瞭解的其他資訊。
role: Developer
source-git-commit: 8280281fa8b676b13c0601e2c9a50515ce8979c3
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 9%

---

# 統一標籤API快速入門 {#getting-started}

統一標籤API可讓您在Adobe Experience Platform中分類及管理您的企業物件。

以下小節提供成功使用統一標籤API所需瞭解的其他資訊。

## 讀取範例 API 呼叫

統一標籤API檔案提供範例API呼叫，示範如何設定請求格式。 這些包括路徑、必要的標頭和正確格式化的請求承載。 此外，也提供 API 回應中傳回的範例 JSON。 如需檔案中用於範例API呼叫的慣例相關資訊，請參閱以下章節： [如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在Experience Platform疑難排解指南中。

## 必要的標頭

此API檔案也要求您完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en) 以成功呼叫Platform端點。 完成驗證教學課程，提供Experience Platform API呼叫中每個必要標題的值，如下所示：

- 授權： `Bearer {ACCESS_TOKEN}`
- x-api-key： `{API_KEY}`
- x-gw-ims-org-id： `{ORG_ID}`

中的所有資源 [!DNL Experience Platform] 會隔離至特定的虛擬沙箱。 所有要求至 [!DNL Platform] API需要標頭，用以指定將執行作業的沙箱名稱：

- x-sandbox-name： `{SANDBOX_NAME}`

>[!NOTE]
>
>如需在中使用沙箱的詳細資訊 [!DNL Experience Platform]，請參閱 [沙箱概述檔案](../../sandboxes/home.md).

## 後續步驟

若要使用統一標籤API進行呼叫，請使用左側導覽或在 [開發人員指南概觀](./overview.md)
