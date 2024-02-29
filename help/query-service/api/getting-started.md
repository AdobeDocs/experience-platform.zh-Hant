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

本開發人員指南提供在Adobe Experience Platform中執行各種操作的步驟 [!DNL Query Service] API。

## 快速入門

本指南需要您實際瞭解使用相關的各種Adobe Experience Platform服務 [!DNL Query Service].

- [[!DNL Query Service]](../home.md)：提供查詢資料集並將產生的查詢擷取為新資料集的能力 [!DNL Experience Platform].
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md)：作為依據的標準化架構 [!DNL Experience Platform] 組織客戶體驗資料。
- [[!DNL Sandboxes]](../../sandboxes/home.md)： [!DNL Experience Platform] 提供分割單一區域的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，協助開發及改進數位體驗應用程式。

以下小節提供成功使用所需的其他資訊 [!DNL Query Service] 使用API。

### 讀取範例 API 呼叫

本指南提供範例 API 呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭和正確格式化的請求承載。 此外，也提供 API 回應中傳回的範例 JSON。 如需本檔案中用於範例API呼叫之慣例的相關資訊，請參閱以下章節： [如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑難排解指南。

### 收集所需標頭的值

為了呼叫 [!DNL Experience Platform] API，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程會提供所有 [!DNL Platform] API 呼叫中每個必要標頭的值，如下所示：

- 授權： `Bearer {ACCESS_TOKEN}`
- x-api-key： `{API_KEY}`
- x-gw-ims-org-id： `{ORG_ID}`

中的所有資源 [!DNL Experience Platform] 會隔離至特定的虛擬沙箱。 所有要求至 [!DNL Platform] API需要標頭，用以指定將執行作業的沙箱名稱：

- x-sandbox-name： `{SANDBOX_NAME}`

>[!NOTE]
>
>如需在中使用沙箱的詳細資訊 [!DNL Experience Platform]，請參閱 [沙箱概述檔案](../../sandboxes/home.md).

## API呼叫範例

現在您已瞭解要使用哪些標頭，您已準備好開始呼叫 [!DNL Query Service] API。 以下檔案會逐步說明您可以使用進行的各種API呼叫。 [!DNL Query Service] API。 每個呼叫範例都包含一般API格式、顯示必要標題的範例要求以及範例回應。

- [查詢](queries.md)
- [連線參數](connection-parameters.md)
- [排定的查詢](scheduled-queries.md)
- [已排程查詢的執行](runs-scheduled-queries.md)
- [查詢範本](query-templates.md)
- [加速的查詢](./accelerated-queries.md)
- [警報訂閱](./alert-subscriptions.md)

## 後續步驟

現在您已瞭解如何使用 [!DNL Query Service] API，您可以建立自己的非互動式查詢。 如需如何建立查詢的詳細資訊，請參閱 [SQL參考指南](../sql/overview.md).
