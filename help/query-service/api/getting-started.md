---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 查詢服務開發人員指南
topic: query templates
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 1%

---


# 查詢服務開發人員指南

本開發人員指南提供在Adobe Experience Platform Query Service API中執行各種作業的步驟。

## 快速入門

本指南需要對使用查詢服務所涉及的各種Adobe Experience Platform服務有良好的瞭解。

- [查詢服務](../home.md): 提供在Experience Platform中查詢資料集並將產生的查詢擷取為新資料集的能力。
- [體驗資料模型(XDM)系統](../../xdm/home.md): Experience Platform組織客戶體驗資料的標準化架構。
- [沙盒](../../sandboxes/home.md): Experience Platform提供虛擬沙盒，可將單一Platform實例分割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您必須知道的其他資訊，以便使用API成功使用查詢服務。

### 讀取範例API呼叫

本指南提供範例API呼叫，以示範如何格式化您的請求。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需本檔案中用於範例API呼叫之慣例的詳細資訊，請參閱「Experience Platform疑難排解指 [南」中有關如何讀取範例API呼叫的章節](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 。

### 收集必要標題的值

若要呼叫Experience Platform API，您必須先完成驗證教 [學課程](../../tutorials/authentication.md)。 完成驗證教學課程後，所有平台API呼叫中每個必要標題的值都會顯示在下方：

- 授權： `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有資源都隔離至特定的虛擬沙盒。 所有對平台API的請求都需要一個標題，該標題會指定執行操作的沙盒名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>如需在Experience Platform中使用沙盒的詳細資訊，請參閱沙盒 [概觀檔案](../../sandboxes/home.md)。

## 範例API呼叫

現在您已瞭解要使用的標題，可以開始呼叫查詢服務API。 下列檔案會逐步執行您可使用查詢服務API進行的各種API呼叫。 每個範例呼叫都包含一般API格式、顯示必要標題的範例要求，以及範例回應。

- [查詢](queries.md)
- [連接參數](connection-parameters.md)
- [排程查詢](scheduled-queries.md)
- [針對排程查詢執行](runs-scheduled-queries.md)
- [查詢範本](query-templates.md)

## 後續步驟

現在您已學習如何使用查詢服務API進行呼叫，您可以建立自己的非互動式查詢。 有關如何建立查詢的詳細資訊，請閱讀 [SQL參考指南](../sql/overview.md)。