---
keywords: Experience Platform;home;popular topics;batch ingestion;Batch ingestion;partial ingestion;Partial ingestion;Retrieve error;retrieve error;Partial batch ingestion;partial batch ingestion;partial;ingestion;Ingestion;
solution: Experience Platform
title: 部分批次擷取概觀
topic: overview
description: 本檔案提供管理部分批次擷取的教學課程。
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '916'
ht-degree: 0%

---


# 部分批次擷取

部分批次擷取是指能夠擷取包含錯誤的資料，最高可達到特定臨界值。 透過這項功能，使用者可以成功將所有正確的資料內嵌至Adobe Experience Platform，而其所有不正確的資料都會個別批次處理，以及為何無效的詳細資訊。

本檔案提供管理部分批次擷取的教學課程。

## 快速入門

本教學課程需要對部分批次擷取所涉及的各種Adobe Experience Platform服務有相關的使用知識。 在開始本教學課程之前，請先閱讀下列服務的檔案：

- [批次擷取](./overview.md):從資料檔 [!DNL Platform] 案（例如CSV和Parce）擷取和儲存資料的方法。
- [[!DNL Experience Data Model] (XDM)](../../xdm/home.md):組織客戶體驗資料 [!DNL Platform] 的標準化架構。

以下章節提供您成功呼叫API所需的其他資訊 [!DNL Platform] 。

### 讀取範例API呼叫

本指南提供範例API呼叫，以示範如何格式化您的請求。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱疑難排解指 [南中有關如何讀取範例API呼叫的](../../landing/troubleshooting.md#how-do-i-format-an-api-request)[!DNL Experience Platform] 章節。

### 收集必要標題的值

若要呼叫API，您必 [!DNL Platform] 須先完成驗證教 [學課程](../../tutorials/authentication.md)。 完成驗證教學課程後，將提供所有 [!DNL Experience Platform] API呼叫中每個必要標題的值，如下所示：

- 授權：生產者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

中的所有資 [!DNL Experience Platform] 源都與特定虛擬沙盒隔離。 對API的所 [!DNL Platform] 有請求都需要一個標題，該標題會指定要在中執行的操作的沙盒名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>如需中沙盒的詳細資訊 [!DNL Platform]，請參閱沙 [盒概述檔案](../../sandboxes/home.md)。

## 在API中啟用批次以擷取部分批次 {#enable-api}

>[!NOTE]
>
>本節說明如何使用API啟用批次以擷取部分批次。 如需使用UI的指示，請閱讀UI步 [驟中啟用批次以擷取部分批次](#enable-ui) 。

您可以建立啟用部分擷取的新批次。

若要建立新批次，請依照批次擷取開發人員指 [南中的步驟進行](./api-overview.md)。 在您達到「建 **[!UICONTROL 立批次]** 」步驟後，在請求內文中新增下列欄位：

```json
{
    "enableErrorDiagnostics": true,
    "partialIngestionPercentage": 5
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `enableErrorDiagnostics` | 允許生成有關 [!DNL Platform] 批的詳細錯誤消息的標籤。 |
| `partialIngestionPercentage` | 整個批失敗前可接受錯誤的百分比。 因此，在此示例中，最多5%的批可能是錯誤，否則將失敗。 |


## 在UI中啟用批次以擷取部分批次 {#enable-ui}

>[!NOTE]
>
>本節說明如何使用UI啟用批處理以進行部分批處理。 如果您已使用API啟用批次以擷取部分批次，則可跳至下一節。

若要透過 [!DNL Platform] UI啟用批次以進行部分擷取，您可以透過來源連線建立新批次、在現有資料集中建立新批次，或透過「[!UICONTROL Map CSV to XDM flow]」建立新批次。

### 建立新源連接 {#new-source}

要建立新源連接，請遵循「源」概述中列出的 [步驟](../../sources/home.md)。 在到達「資料 **[!UICONTROL 流詳細資訊]** 」步驟後 **[!UICONTROL ，請注意「部分]** 提取 **[!UICONTROL 」和「]** 錯誤診斷」欄位。

![](../images/batch-ingestion/partial-ingestion/configure-batch.png)

「部 **[!UICONTROL 分擷取]** 」切換可讓您啟用或停用部分批次擷取的使用。

僅當 **[!UICONTROL Partial Ingestion（部分攝取）關]** 閉時，才會顯示 **** Error diagnostics（錯誤診斷）切換。 此功能可 [!DNL Platform] 產生有關您所擷取批次的詳細錯誤訊息。 如果已 **[!UICONTROL 開啟「部分擷取]** 」切換，則會自動強制執行增強的錯誤診斷。

![](../images/batch-ingestion/partial-ingestion/configure-batch-partial-ingestion-focus.png)

「錯 **[!UICONTROL 誤閾值]** 」(Error threshold)允許您在整個批失敗之前設定可接受錯誤的百分比。 依預設，此值會設為5%。

### 使用現有資料集 {#existing-dataset}

若要使用現有資料集，請從選取資料集開始。 右側的側欄會填入資料集的相關資訊。

![](../images/batch-ingestion/partial-ingestion/monitor-dataset.png)

「部 **[!UICONTROL 分擷取]** 」切換可讓您啟用或停用部分批次擷取的使用。

僅當 **[!UICONTROL Partial Ingestion（部分攝取）關]** 閉時，才會顯示 **** Error diagnostics（錯誤診斷）切換。 此功能可 [!DNL Platform] 產生有關您所擷取批次的詳細錯誤訊息。 如果已 **[!UICONTROL 開啟「部分擷取]** 」切換，則會自動強制執行增強的錯誤診斷。

![](../images/batch-ingestion/partial-ingestion/monitor-dataset-partial-ingestion-focus.png)

「錯 **[!UICONTROL 誤閾值]** 」(Error threshold)允許您在整個批失敗之前設定可接受錯誤的百分比。 依預設，此值會設為5%。

現在，您可以使用「新增資料」 **按鈕來上傳資料** ，而且會使用部分擷取來擷取資料。

### 使用「將[!UICONTROL CSV對應至XDM架構]」流程 {#map-flow}

若要使用「將[!UICONTROL CSV對應至XDM架構]」流程，請遵循「將CSV檔案對應」教學課程中 [所列的步驟](../tutorials/map-a-csv-file.md)。 一旦到達「添 **[!UICONTROL 加資料]** 」步驟 **[!UICONTROL ，請記下「部分提取」和「錯誤診斷」欄位]****** 。

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow.png)

「部 **[!UICONTROL 分擷取]** 」切換可讓您啟用或停用部分批次擷取的使用。

僅當 **[!UICONTROL Partial Ingestion（部分攝取）關]** 閉時，才會顯示 **** Error diagnostics（錯誤診斷）切換。 此功能可 [!DNL Platform] 產生有關您所擷取批次的詳細錯誤訊息。 如果已 **[!UICONTROL 開啟「部分擷取]** 」切換，則會自動強制執行增強的錯誤診斷。

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow-partial-ingestion-focus.png)

**[!UICONTROL 錯誤閾值]** ，允許您在整個批失敗之前設定可接受錯誤的百分比。 依預設，此值會設為5%。

## 下一步 {#next-steps}

本教學課程涵蓋如何建立或修改資料集以啟用部分批次擷取。 如需批次擷取的詳細資訊，請閱讀批次擷取開 [發人員指南](./api-overview.md)。

有關監視部分攝取錯誤的資訊，請閱讀批 [次攝取錯誤診斷指南](../quality/error-diagnostics.md)。
