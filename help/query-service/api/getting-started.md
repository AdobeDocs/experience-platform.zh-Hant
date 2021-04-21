---
keywords: Experience Platform;home;popular topics;query service；查詢服務；query
solution: Experience Platform
title: 查詢服務API指南
topic-legacy: query templates
description: Query Service API可讓開發人員使用標準SQL查詢其Adobe Experience Platform資料。 請依照本指南，瞭解如何使用API執行關鍵作業。
exl-id: 2f4a156b-5623-419a-a9b2-72310f755708
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 1%

---

# [!DNL Query Service] API指南

本開發人員指南提供在Adobe Experience Platform[!DNL Query Service] API中執行各種操作的步驟。

## 快速入門

本指南要求對使用[!DNL Query Service]的Adobe Experience Platform各服務部門有切實的瞭解。

- [[!DNL Query Service]](../home.md):提供查詢資料集並將生成的查詢捕獲為中的新資料集的能力 [!DNL Experience Platform]。
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):組織客戶體驗資 [!DNL Experience Platform] 料的標準化架構。
- [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙盒，可將單一執行個體分 [!DNL Platform] 割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您必須知道的其他資訊，才能使用API成功使用[!DNL Query Service]。

### 讀取範例API呼叫

本指南提供範例API呼叫，以示範如何格式化您的請求。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 有關本文檔中用於示例API調用的約定的資訊，請參閱[!DNL Experience Platform]故障排除指南中[如何讀取示例API調用](../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集必要標題的值

若要呼叫[!DNL Experience Platform] API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程後，所有[!DNL Platform] API呼叫中每個所需標題的值都會顯示在下面：

- Authorization: `Bearer {ACCESS_TOKEN}`
- x-api-key:`{API_KEY}`
- x-gw-ims-org-id:`{IMS_ORG}`

[!DNL Experience Platform]中的所有資源都隔離到特定的虛擬沙盒。 對[!DNL Platform] API的所有請求都需要一個標題，該標題指定執行操作的沙盒的名稱：

- x-sandbox-name:`{SANDBOX_NAME}`

>[!NOTE]
>
>如需在[!DNL Experience Platform]中使用沙盒的詳細資訊，請參閱[沙盒概觀檔案](../../sandboxes/home.md)。

## 範例API呼叫

現在您已瞭解要使用哪些標題，可以開始呼叫[!DNL Query Service] API。 以下檔案會逐步瞭解您可使用[!DNL Query Service] API進行的各種API呼叫。 每個範例呼叫都包含一般API格式、顯示必要標題的範例要求，以及範例回應。

- [查詢](queries.md)
- [連接參數](connection-parameters.md)
- [排程查詢](scheduled-queries.md)
- [針對排程查詢執行](runs-scheduled-queries.md)
- [查詢範本](query-templates.md)

## 後續步驟

現在您已學會如何使用[!DNL Query Service] API進行呼叫，您可以建立自己的非互動式查詢。 有關如何建立查詢的詳細資訊，請閱讀[SQL參考指南](../sql/overview.md)。
