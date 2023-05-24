---
keywords: Experience Platform；主題；熱門主題；批處理攝取；批處理攝取；部分攝取；檢索錯誤；檢索錯誤；部分批處理攝取；部分攝取；部分攝取；部分攝取；部分攝取；部分攝取；
solution: Experience Platform
title: 部分批接收概述
description: 本文檔提供了管理部分批處理接收的教程。
exl-id: 25a34da6-5b7c-4747-8ebd-52ba516b9dc3
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '945'
ht-degree: 0%

---

# 部分批量攝取

部分批處理接收是指能夠接收包含錯誤的資料，最高可達到某個閾值。 利用此功能，用戶可以成功將其所有正確資料接收到Adobe Experience Platform，同時將其所有不正確的資料分別進行批處理，並詳細瞭解其無效的原因。

本文檔提供了管理部分批處理接收的教程。

## 快速入門

本教程需要瞭解與部分批量接收有關的Adobe Experience Platform各服務的工作知識。 在開始本教程之前，請查看以下服務的文檔：

- [批量攝取](./overview.md):方法 [!DNL Platform] 從資料檔案（如CSV和Parket）中接收和儲存資料。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):標準化框架 [!DNL Platform] 組織客戶體驗資料。

以下各節提供了您需要瞭解的其他資訊，以便成功撥打 [!DNL Platform] API。

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

## 在API中為部分批接收啟用批 {#enable-api}

>[!NOTE]
>
>本節介紹使用API為部分批接收啟用批處理。 有關使用UI的說明，請閱讀 [在UI中啟用批處理部分接收](#enable-ui) 的子菜單。

您可以建立啟用部分攝取的新批。

要建立新批，請執行 [批量攝取顯影劑指南](./api-overview.md)。 一旦你到達 **[!UICONTROL 建立批]** 步驟，在請求正文中添加以下欄位：

```json
{
    "enableErrorDiagnostics": true,
    "partialIngestionPercent": 5
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `enableErrorDiagnostics` | 允許 [!DNL Platform] 生成有關批的詳細錯誤消息。 |
| `partialIngestionPercent` | 整個批失敗前可接受錯誤的百分比。 因此，在本示例中，最多5%的批可能是錯誤，然後才會失敗。 |


## 在UI中為部分批接收啟用批 {#enable-ui}

>[!NOTE]
>
>本節介紹使用UI啟用批處理以進行部分批處理接收。 如果已使用API為部分批接收啟用了批，則可以跳到下一節。

通過啟用批以進行部分攝取 [!DNL Platform] UI，您可以通過源連接建立新批、在現有資料集中建立新批或通過「 」建立新批[!UICONTROL 將CSV映射到XDM流]。

### 新建源連接 {#new-source}

要建立新源連接，請按照 [源概述](../../sources/home.md)。 一旦你到達 **[!UICONTROL 資料流詳細資訊]** 步驟，注意 **[!UICONTROL 部分攝取]** 和 **[!UICONTROL 錯誤診斷]** 的子菜單。

![](../images/batch-ingestion/partial-ingestion/configure-batch.png)

的 **[!UICONTROL 部分攝取]** 切換允許您啟用或禁用部分批接收。

的 **[!UICONTROL 錯誤診斷]** 僅當 **[!UICONTROL 部分攝取]** 切換關閉。 此功能允許 [!DNL Platform] 生成有關接收的批的詳細錯誤消息。 如果 **[!UICONTROL 部分攝取]** 開啟切換，自動強制執行增強的錯誤診斷。

![](../images/batch-ingestion/partial-ingestion/configure-batch-partial-ingestion-focus.png)

的 **[!UICONTROL 錯誤閾值]** 允許您在整個批失敗之前設定可接受錯誤的百分比。 預設情況下，此值設定為5%。

### 使用現有資料集 {#existing-dataset}

要使用現有資料集，請從選擇資料集開始。 右邊的提要欄將填充有關資料集的資訊。

![](../images/batch-ingestion/partial-ingestion/monitor-dataset.png)

的 **[!UICONTROL 部分攝取]** 切換允許您啟用或禁用部分批接收。

的 **[!UICONTROL 錯誤診斷]** 僅當 **[!UICONTROL 部分攝取]** 切換關閉。 此功能允許 [!DNL Platform] 生成有關接收的批的詳細錯誤消息。 如果 **[!UICONTROL 部分攝取]** 開啟切換，自動強制執行增強的錯誤診斷。

![](../images/batch-ingestion/partial-ingestion/monitor-dataset-partial-ingestion-focus.png)

的 **[!UICONTROL 錯誤閾值]** 允許您在整個批失敗之前設定可接受錯誤的百分比。 預設情況下，此值設定為5%。

現在，您可以使用 **添加資料** 按鈕，然後用部分攝入來攝取。

### 使用「」[!UICONTROL 將CSV映射到XDM架構]&quot;流&quot; {#map-flow}

使用「」[!UICONTROL 將CSV映射到XDM架構]「流」，按照 [映射CSV檔案教程](../tutorials/map-csv/overview.md)。 一旦你到達 **[!UICONTROL 添加資料]** 步驟，注意 **[!UICONTROL 部分攝取]** 和 **[!UICONTROL 錯誤診斷]** 的子菜單。

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow.png)

的 **[!UICONTROL 部分攝取]** 切換允許您啟用或禁用部分批接收。

的 **[!UICONTROL 錯誤診斷]** 僅當 **[!UICONTROL 部分攝取]** 切換關閉。 此功能允許 [!DNL Platform] 生成有關接收的批的詳細錯誤消息。 如果 **[!UICONTROL 部分攝取]** 開啟切換，自動強制執行增強的錯誤診斷。

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow-partial-ingestion-focus.png)

**[!UICONTROL 錯誤閾值]** 允許您在整個批失敗之前設定可接受錯誤的百分比。 預設情況下，此值設定為5%。

## 後續步驟 {#next-steps}

本教程介紹如何建立或修改資料集以啟用部分批處理接收。 有關批量攝取的詳細資訊，請閱讀 [批量攝取顯影劑指南](./api-overview.md)。

有關監視部分攝取錯誤的資訊，請閱讀 [批處理問題錯誤診斷指南](../quality/error-diagnostics.md)。
