---
keywords: Experience Platform；首頁；熱門主題；批次內嵌；批次內嵌；部分內嵌；部分擷取；擷取錯誤；擷取錯誤；部分批次內嵌；部分批次內嵌；部分擷取；內嵌；
solution: Experience Platform
title: 部分批次擷取概觀
description: 本檔案提供管理部分批次內嵌的教學課程。
exl-id: 25a34da6-5b7c-4747-8ebd-52ba516b9dc3
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '945'
ht-degree: 0%

---

# 部分批次內嵌

部分批次內嵌是指內嵌包含錯誤的資料的功能，最多可達特定臨界值。 透過此功能，使用者可以將其所有正確資料成功內嵌至Adobe Experience Platform，同時將其所有不正確的資料分別批次處理，並提供其無效原因的詳細資訊。

本檔案提供管理部分批次內嵌的教學課程。

## 快速入門

本教學課程需要具備部分批次內嵌所涉及各種Adobe Experience Platform服務的實用知識。 開始本教學課程之前，請先檢閱下列服務的檔案：

- [批次內嵌](./overview.md):方法 [!DNL Platform] 擷取並儲存資料檔案（例如CSV和Parquet）中的資料。
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md):標準化框架 [!DNL Platform] 組織客戶體驗資料。

以下小節提供您需要知道的其他資訊，以便成功對 [!DNL Platform] API。

### 讀取範例API呼叫

本指南提供範例API呼叫，以示範如何設定請求格式。 這些功能包括路徑、必要標題和格式正確的請求裝載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所使用慣例的相關資訊，請參閱 [如何閱讀API呼叫範例](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑難排解指南。

### 收集必要標題的值

若要對 [!DNL Platform] API，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程會提供所有 [!DNL Experience Platform] API呼叫，如下所示：

- 授權：承載 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

中的所有資源 [!DNL Experience Platform] 與特定虛擬沙箱隔離。 所有請求 [!DNL Platform] API需要標頭，以指定要在中執行操作的沙箱名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>如需中沙箱的詳細資訊，請參閱 [!DNL Platform]，請參閱 [沙箱概述檔案](../../sandboxes/home.md).

## 在API中啟用批次以進行部分批次內嵌 {#enable-api}

>[!NOTE]
>
>本節說明如何使用API啟用批次以進行部分批次內嵌。 有關使用UI的說明，請閱讀 [在UI中啟用批次以進行部分批次內嵌](#enable-ui) 步驟。

您可以建立已啟用部分擷取的新批次。

要建立新批，請按照 [批次匯入開發人員指南](./api-overview.md). 一旦您到達 **[!UICONTROL 建立批次]** 步驟中，在請求內文中新增下列欄位：

```json
{
    "enableErrorDiagnostics": true,
    "partialIngestionPercent": 5
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `enableErrorDiagnostics` | 允許 [!DNL Platform] 生成有關批的詳細錯誤消息。 |
| `partialIngestionPercent` | 整個批處理失敗前可接受的錯誤百分比。 因此，在本示例中，最多5%的批可能是錯誤，然後它才會失敗。 |


## 在UI中啟用批次以進行部分批次內嵌 {#enable-ui}

>[!NOTE]
>
>本節說明如何使用UI啟用批次以進行部分批次內嵌。 如果您已使用API為部分批次內嵌啟用批次，可跳至下一節。

若要透過啟用批次以進行部分擷取，請 [!DNL Platform] UI中，您可以透過來源連線建立新批次、在現有資料集中建立新批次，或透過「[!UICONTROL 將CSV對應至XDM流量]」。

### 建立新源連接 {#new-source}

要建立新源連接，請遵循 [來源概觀](../../sources/home.md). 一旦您到達 **[!UICONTROL 資料流詳細資訊]** 步驟，請注意 **[!UICONTROL 部分擷取]** 和 **[!UICONTROL 錯誤診斷]** 欄位。

![](../images/batch-ingestion/partial-ingestion/configure-batch.png)

此 **[!UICONTROL 部分擷取]** 切換可讓您啟用或停用部分批次內嵌的使用。

此 **[!UICONTROL 錯誤診斷]** 切換時，僅會在 **[!UICONTROL 部分擷取]** 切換為關閉。 此功能可讓 [!DNL Platform] 生成有關所接收批的詳細錯誤消息。 若 **[!UICONTROL 部分擷取]** 開啟切換開關，自動強制執行增強錯誤診斷。

![](../images/batch-ingestion/partial-ingestion/configure-batch-partial-ingestion-focus.png)

此 **[!UICONTROL 錯誤閾值]** 可讓您在整個批次失敗前設定可接受錯誤的百分比。 此值預設為5%。

### 使用現有資料集 {#existing-dataset}

若要使用現有資料集，請先選取資料集。 右側的側欄會填入資料集的相關資訊。

![](../images/batch-ingestion/partial-ingestion/monitor-dataset.png)

此 **[!UICONTROL 部分擷取]** 切換可讓您啟用或停用部分批次內嵌的使用。

此 **[!UICONTROL 錯誤診斷]** 切換時，僅會在 **[!UICONTROL 部分擷取]** 切換為關閉。 此功能可讓 [!DNL Platform] 生成有關所接收批的詳細錯誤消息。 若 **[!UICONTROL 部分擷取]** 開啟切換開關，自動強制執行增強錯誤診斷。

![](../images/batch-ingestion/partial-ingestion/monitor-dataset-partial-ingestion-focus.png)

此 **[!UICONTROL 錯誤閾值]** 可讓您在整個批次失敗前設定可接受錯誤的百分比。 此值預設為5%。

現在，您可以使用 **新增資料** 按鈕，則會使用部分擷取來擷取。

### 使用「[!UICONTROL 將CSV對應至XDM結構]「流」 {#map-flow}

若要使用「[!UICONTROL 將CSV對應至XDM結構]」流程，請遵循 [對應CSV檔案教學課程](../tutorials/map-csv/overview.md). 一旦您到達 **[!UICONTROL 新增資料]** 步驟，請注意 **[!UICONTROL 部分擷取]** 和 **[!UICONTROL 錯誤診斷]** 欄位。

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow.png)

此 **[!UICONTROL 部分擷取]** 切換可讓您啟用或停用部分批次內嵌的使用。

此 **[!UICONTROL 錯誤診斷]** 切換時，僅會在 **[!UICONTROL 部分擷取]** 切換為關閉。 此功能可讓 [!DNL Platform] 生成有關所接收批的詳細錯誤消息。 若 **[!UICONTROL 部分擷取]** 開啟切換開關，自動強制執行增強錯誤診斷。

![](../images/batch-ingestion/partial-ingestion/xdm-csv-workflow-partial-ingestion-focus.png)

**[!UICONTROL 錯誤閾值]** 可讓您在整個批次失敗前設定可接受錯誤的百分比。 此值預設為5%。

## 後續步驟 {#next-steps}

本教學課程說明如何建立或修改資料集以啟用部分批次內嵌。 如需批次內嵌的詳細資訊，請參閱 [批次匯入開發人員指南](./api-overview.md).

如需監控部分擷取錯誤的資訊，請參閱 [批次匯入錯誤診斷指南](../quality/error-diagnostics.md).
