---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢
solution: Experience Platform
title: 查詢服務API指南
description: 查詢服務API可讓開發人員使用標準SQL查詢其Adobe Experience Platform資料。 請遵循本指南以了解如何使用 API 執行關鍵作業。
exl-id: 2f4a156b-5623-419a-a9b2-72310f755708
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 5%

---

# [!DNL Query Service] API指南

本開發人員指南提供在Adobe Experience Platform中執行各種作業的步驟 [!DNL Query Service] API。

## 快速入門

本指南需要妥善了解使用時涉及的各種Adobe Experience Platform服務 [!DNL Query Service].

- [[!DNL Query Service]](../home.md):提供查詢資料集的功能，並將產生的查詢擷取為 [!DNL Experience Platform].
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。
- [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] 提供可分割單一沙箱的虛擬沙箱 [!DNL Platform] 例項放入個別的虛擬環境，以協助開發及改進數位體驗應用程式。

以下章節提供您需要了解的其他資訊，以便順利使用 [!DNL Query Service] 使用API。

### 讀取範例API呼叫

本指南提供範例API呼叫，以示範如何設定請求格式。 這些功能包括路徑、必要標題和格式正確的請求裝載。 也提供API回應中傳回的範例JSON。 如需本檔案中用於範例API呼叫之慣例的相關資訊，請參閱 [如何閱讀API呼叫範例](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑難排解指南。

### 收集必要標題的值

若要對 [!DNL Experience Platform] API，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程會提供所有 [!DNL Platform] API呼叫，如下所示：

- Authorization: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

中的所有資源 [!DNL Experience Platform] 與特定虛擬沙箱隔離。 所有請求 [!DNL Platform] API需要標頭，以指定要進行操作的沙箱名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>如需使用沙箱的詳細資訊，請參閱 [!DNL Experience Platform]，請參閱 [沙箱概述檔案](../../sandboxes/home.md).

## 範例API呼叫

現在您已了解要使用的標題，可以開始對 [!DNL Query Service] API。 下列檔案會逐步說明您可使用 [!DNL Query Service] API。 每個範例呼叫都包含一般API格式、顯示必要標題的範例要求，以及範例回應。

- [查詢](queries.md)
- [連線參數](connection-parameters.md)
- [排程查詢](scheduled-queries.md)
- [針對排程查詢執行](runs-scheduled-queries.md)
- [查詢範本](query-templates.md)
- [加速查詢](./accelerated-queries.md)
- [警報訂閱](./alert-subscriptions.md)

## 後續步驟

現在您已學會如何使用 [!DNL Query Service] API，您可以建立自己的非互動式查詢。 有關如何建立查詢的詳細資訊，請閱讀 [SQL參考指南](../sql/overview.md).
