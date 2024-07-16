---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；查詢
solution: Experience Platform
title: 查詢服務API指南
description: 查詢服務API可讓開發人員使用標準SQL查詢其Adobe Experience Platform資料。 請遵循本指南以了解如何使用 API 執行關鍵作業。
role: Developer
exl-id: 2f4a156b-5623-419a-a9b2-72310f755708
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 20%

---

# [!DNL Query Service] API指南

此開發人員指南提供在Adobe Experience Platform [!DNL Query Service] API中執行各種作業的步驟。

## 快速入門

本指南需要您實際瞭解使用[!DNL Query Service]所涉及的各種Adobe Experience Platform服務。

- [[!DNL Query Service]](../home.md)：提供在[!DNL Experience Platform]中查詢資料集並擷取結果查詢作為新資料集的功能。
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md)： [!DNL Experience Platform]用來組織客戶體驗資料的標準化架構。
- [[!DNL Sandboxes]](../../sandboxes/home.md)： [!DNL Experience Platform]提供的虛擬沙箱可將單一[!DNL Platform]執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

下列章節提供您需瞭解的其他資訊，才能使用API成功使用[!DNL Query Service]。

### 讀取範例 API 呼叫

本指南提供範例 API 呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭和正確格式化的請求承載。 此外，也提供 API 回應中傳回的範例 JSON。 如需本檔案中用於範例API呼叫之慣例的相關資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request)的相關章節。

### 收集所需標頭的值

若要呼叫[!DNL Experience Platform] API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程會提供所有 [!DNL Platform] API 呼叫中每個必要標頭的值，如下所示：

- 授權： `Bearer {ACCESS_TOKEN}`
- x-api-key： `{API_KEY}`
- x-gw-ims-org-id： `{ORG_ID}`

[!DNL Experience Platform]中的所有資源都與特定的虛擬沙箱隔離。 對[!DNL Platform] API的所有請求都需要一個標頭，以指定將執行操作的沙箱名稱：

- x-sandbox-name： `{SANDBOX_NAME}`

>[!NOTE]
>
>如需在[!DNL Experience Platform]中使用沙箱的詳細資訊，請參閱[沙箱概觀檔案](../../sandboxes/home.md)。

## API呼叫範例

現在您已瞭解要使用哪些標頭，您已準備好開始呼叫[!DNL Query Service] API。 下列檔案會逐步說明您可以使用[!DNL Query Service] API進行的各種API呼叫。 每個呼叫範例都包含一般API格式、顯示必要標題的範例要求以及範例回應。

- [查詢](queries.md)
- [連線參數](connection-parameters.md)
- [排定的查詢](scheduled-queries.md)
- [已排程查詢的執行](runs-scheduled-queries.md)
- [查詢範本](query-templates.md)
- [加速的查詢](./accelerated-queries.md)
- [警報訂閱](./alert-subscriptions.md)

## 後續步驟

現在您已瞭解如何使用[!DNL Query Service] API進行呼叫，您可以建立自己的非互動式查詢。 如需有關如何建立查詢的詳細資訊，請參閱[SQL參考指南](../sql/overview.md)。
