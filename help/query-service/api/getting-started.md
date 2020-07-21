---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 查詢服務開發人員指南
topic: query templates
translation-type: tm+mt
source-git-commit: 3b710e7a20975880376f7e434ea4d79c01fa0ce5
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 1%

---


# [!DNL Query Service] 開發人員指南

本開發人員指南提供在Adobe Experience Platform [!DNL Query Service] API中執行各種作業的步驟。

## 快速入門

本指南需要有效瞭解與使用相關的各種Adobe Experience Platform服務 [!DNL Query Service]。

- [!DNL Query Service](../home.md): 提供查詢資料集並將生成的查詢捕獲為中的新資料集的能力 [!DNL Experience Platform]。
- [!DNL Experience Data Model (XDM) System](../../xdm/home.md): 組織客戶體驗資料 [!DNL Experience Platform] 的標準化架構。
- [!DNL Sandboxes](../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙盒，可將單一執行個體分 [!DNL Platform] 割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您必須知道的其他資訊，以便成功使 [!DNL Query Service] 用API。

### 讀取範例API呼叫

本指南提供範例API呼叫，以示範如何格式化您的請求。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需本檔案中用於範例API呼叫之慣例的詳細資訊，請參閱疑難排解指 [南中有關如何讀取範例API呼叫的](../../landing/troubleshooting.md#how-do-i-format-an-api-request)[!DNL Experience Platform] 章節。

### 收集必要標題的值

若要呼叫API，您必 [!DNL Experience Platform] 須先完成驗證教 [學課程](../../tutorials/authentication.md)。 完成驗證教學課程後，將提供所有 [!DNL Platform] API呼叫中每個必要標題的值，如下所示：

- 授權： `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

中的所有資 [!DNL Experience Platform] 源都與特定虛擬沙盒隔離。 對API的所 [!DNL Platform] 有請求都需要一個標題，該標題指定執行操作的沙盒的名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>如需有關在中使用沙盒的詳細資訊，請 [!DNL Experience Platform]參閱沙盒 [概觀檔案](../../sandboxes/home.md)。

## 範例API呼叫

現在，您已瞭解要使用哪些標題，可以開始呼叫 [!DNL Query Service] API。 下列檔案會逐步說明您可使用 [!DNL Query Service] API進行的各種API呼叫。 每個範例呼叫都包含一般API格式、顯示必要標題的範例要求，以及範例回應。

- [查詢](queries.md)
- [連接參數](connection-parameters.md)
- [排程查詢](scheduled-queries.md)
- [針對排程查詢執行](runs-scheduled-queries.md)
- [查詢範本](query-templates.md)

## 後續步驟

現在您已學會如何使用 [!DNL Query Service] API進行呼叫，您可以建立自己的非互動式查詢。 有關如何建立查詢的詳細資訊，請閱讀 [SQL參考指南](../sql/overview.md)。