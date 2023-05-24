---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；查詢服務；查詢
solution: Experience Platform
title: 查詢服務API指南
description: 查詢服務API允許開發人員使用標準SQL查詢其Adobe Experience Platform資料。 請遵循本指南以了解如何使用 API 執行關鍵作業。
exl-id: 2f4a156b-5623-419a-a9b2-72310f755708
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 5%

---

# [!DNL Query Service] API指南

本開發人員指南提供了在Adobe Experience Platform執行各種操作的步驟 [!DNL Query Service] API。

## 快速入門

本指南要求對Adobe Experience Platform與使用有關的各種服務有工作的瞭解 [!DNL Query Service]。

- [[!DNL Query Service]](../home.md):提供查詢資料集和將生成的查詢捕獲為 [!DNL Experience Platform]。
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。
- [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙箱，將單個沙箱 [!DNL Platform] 實例到獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

以下各節提供了成功使用所需的其他資訊 [!DNL Query Service] 使用API。

### 讀取示例API調用

本指南提供了示例API調用，以演示如何格式化請求。 這些包括路徑、必需的標頭和正確格式化的請求負載。 還提供了API響應中返回的示例JSON。 有關本文檔中用於示例API調用的約定的資訊，請參見上的 [如何讀取示例API調用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 的 [!DNL Experience Platform] 疑難解答指南。

### 收集所需標題的值

為了呼叫 [!DNL Experience Platform] API，必須首先完成 [驗證教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份驗證教程將提供所有中每個必需標頭的值 [!DNL Platform] API調用，如下所示：

- Authorization: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

中的所有資源 [!DNL Experience Platform] 與特定虛擬沙箱隔離。 所有請求 [!DNL Platform] API需要一個標頭，該標頭指定操作將在其中進行的沙盒的名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有關使用沙箱的詳細資訊，請參閱 [!DNL Experience Platform]，請參見 [箱概述文檔](../../sandboxes/home.md)。

## 示例API調用

現在，您瞭解要使用哪些標頭後，就可以開始呼叫 [!DNL Query Service] API。 以下文檔可以通過 [!DNL Query Service] API。 每個示例調用包括一般API格式、顯示所需標頭的示例請求和示例響應。

- [查詢](queries.md)
- [連接參數](connection-parameters.md)
- [計畫查詢](scheduled-queries.md)
- [運行計畫查詢](runs-scheduled-queries.md)
- [查詢模板](query-templates.md)
- [加速查詢](./accelerated-queries.md)
- [警報訂閱](./alert-subscriptions.md)

## 後續步驟

現在您已經學會了如何使用 [!DNL Query Service] API，您可以建立自己的非交互查詢。 有關如何建立查詢的詳細資訊，請閱讀 [SQL參考指南](../sql/overview.md)。
