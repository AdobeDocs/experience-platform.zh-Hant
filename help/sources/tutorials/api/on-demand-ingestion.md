---
keywords: Experience Platform；首頁；熱門主題；流程服務；
title: 使用流程服務API建立隨選擷取的流程執行
description: 瞭解如何使用流程服務API建立隨選擷取的流程執行
exl-id: a7b20cd1-bb52-4b0a-aad0-796929555e4a
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '801'
ht-degree: 1%

---

# 使用[!DNL Flow Service] API建立隨選擷取的資料流執行

流程執行代表流程執行的例項。 例如，如果排程在早上9:00、上午10:00及上午11:00每小時執行流程，則您會有三個流程執行個體。 流程執行是您的特定組織所專屬。

隨選擷取可讓您建立針對指定資料流執行的流程。 這可讓您的使用者根據指定的引數建立流程執行，並建立擷取週期，而不使用服務權杖。 僅批次來源支援隨選擷取。

本教學課程涵蓋如何使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)隨選擷取和建立資料流執行的步驟。

## 快速入門

>[!NOTE]
>
>為了建立資料流執行，您必須先擁有排程為單次擷取的資料流的資料流ID。

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

* [來源](../../home.md)： [!DNL Experience Platform]允許從各種來源擷取資料，同時讓您能夠使用[!DNL Experience Platform]服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../sandboxes/home.md)： [!DNL Experience Platform]提供可將單一[!DNL Experience Platform]執行個體分割成個別虛擬環境的虛擬沙箱，以利開發及改進數位體驗應用程式。

### 使用Experience Platform API

如需如何成功呼叫Experience Platform API的詳細資訊，請參閱[Experience Platform API快速入門](../../../landing/api-guide.md)指南。

## 為以表格為基礎的來源建立資料流執行

若要為表格型來源建立流程，請對[!DNL Flow Service] API提出POST要求，同時提供您要建立執行之流程的識別碼，以及開始時間、結束時間和差異欄的值。

>[!TIP]
>
>表格型來源包括下列來源類別：廣告、分析、同意和偏好設定、CRM、客戶成功、資料庫、行銷自動化、付款和通訊協定。

**API格式**

```http
POST /runs/
```

**要求**

下列要求會建立流程識別碼`3abea21c-7e36-4be1-bec1-d3bad0e3e0de`的流程執行。

>[!NOTE]
>
>建立您的第一個資料流執行時，您只需要提供`deltaColumn`。 之後，`deltaColumn`將會修補為流程中`copy`轉換的一部分，並將視為真相來源。 任何透過資料流執行引數變更`deltaColumn`值的嘗試都會導致錯誤。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/runs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "flowId": "3abea21c-7e36-4be1-bec1-d3bad0e3e0de",
      "params": {
          "startTime": "1663735590",
          "windowStartTime": "1651584991",
          "windowEndTime": "16515859567",
          "deltaColumn": {
              "name": "DOB"
          }
      }
  }'
```

| 參數 | 說明 |
| --- | --- |
| `flowId` | 要針對其建立您的流程執行的流程ID。 |
| `params.startTime` | 隨選資料流執行的排定時間。 此值以unix時間表示。 |
| `params.windowStartTime` | 將會從中擷取資料的最早日期和時間。 此值以unix時間表示。 |
| `params.windowEndTime` | 擷取資料的日期和時間，截止日期為。 此值以unix時間表示。 |
| `params.deltaColumn` | 必須有delta欄才能分割資料，並將新擷取的資料與歷史資料分開。 **注意**：只有在建立您的第一個資料流執行時才需要`deltaColumn`。 |
| `params.deltaColumn.name` | 差異資料行的名稱。 |

**回應**

成功的回應傳回新建立的資料流執行的詳細資料，包括其唯一執行`id`。

```json
{
    "items": [
        {
            "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
            "etag": "\"1100c53e-0000-0200-0000-627138980000\""
        }
    ]
}
```

| 屬性 | 說明 |
| --- | --- |
| `id` | 新建立的資料流執行ID。 請參閱[擷取流程規格](../api/collect/database-nosql.md#specs)的指南，以取得資料表式執行規格的詳細資訊。 |
| `etag` | 流程執行的資源版本。 |

<!-- 
| `createdAt` | The unix timestamp that designates when the flow run was created. |
| `updatedAt` | The unix timestamp that designates when the flow run was last updated. |
| `createdBy` | The organization ID of the user who created the flow run. |
| `updatedBy` | The organization ID of the user who last updated the flow run. |
| `createdClient` | The application client that created the flow run. |
| `updatedClient` | The application client that last updated the flow run. |
| `sandboxId` | The ID of the sandbox that contains the flow run. |
| `sandboxName` | The name of the sandbox that contains the flow run. |
| `imsOrgId` | The organization ID. |
| `flowId` | The ID of the flow in which the flow run is created against. |
| `params.windowStartTime` | An integer that defines the start time of the window during which data is to be pulled. The value is represented in unix time. |
| `params.windowEndTime` | An integer that defines the end time of the window during which data is to be pulled. The value is represented in unix time. |
| `params.deltaColumn` | The delta column is required to partition the data and separate newly ingested data from historic data. **Note**: The `deltaColumn` is only needed when creating your firs flow run. |
| `params.deltaColumn.name` | The name of the delta column. |
| `etag` | The resource version of the flow run. |
| `metrics` | This property displays a status summary for the flow run. | -->

## 為檔案型來源建立資料流執行

若要建立檔案型來源的流程，請對[!DNL Flow Service] API提出POST要求，同時提供您要建立執行的流程識別碼，以及開始時間和結束時間的值。

>[!TIP]
>
>檔案型來源包含所有雲端儲存空間來源。

**API格式**

```http
POST /runs/
```

**要求**

下列要求會建立流程識別碼`3abea21c-7e36-4be1-bec1-d3bad0e3e0de`的流程執行。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/runs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json'
  -d '{
      "flowId": "3abea21c-7e36-4be1-bec1-d3bad0e3e0de",
      "params": {
          "startTime": "1663735590",
          "windowStartTime": "1651584991",
          "windowEndTime": "16515859567"
      }
  }'
```

| 參數 | 說明 |
| --- | --- |
| `flowId` | 要針對其建立您的流程執行的流程ID。 |
| `params.startTime` | 隨選資料流執行的排定時間。 此值以unix時間表示。 |
| `params.windowStartTime` | 將會從中擷取資料的最早日期和時間。 此值以unix時間表示。 |
| `params.windowEndTime` | 擷取資料的日期和時間，截止日期為。 此值以unix時間表示。 |

**回應**

成功的回應傳回新建立的資料流執行的詳細資料，包括其唯一執行`id`。


```json
{
    "items": [
        {
            "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
            "etag": "\"1100c53e-0000-0200-0000-627138980000\""
        }
    ]
}
```

| 屬性 | 說明 |
| --- | --- |
| `id` | 新建立的資料流執行ID。 請參閱[擷取流程規格](../api/collect/database-nosql.md#specs)的指南，以取得資料表式執行規格的詳細資訊。 |
| `etag` | 流程執行的資源版本。 |

## 監視您的流量執行

建立流程執行後，您可以監視透過它擷取的資料，以檢視有關流程執行、完成狀態和錯誤的資訊。 若要使用API監視您的資料流執行，請參閱有關[監視API中的資料流的教學課程](./monitor.md)。 若要使用Experience Platform UI監視您的資料流執行，請參閱[使用監視儀表板](../../../dataflows/ui/monitor-sources.md)監視來源資料流的指南。
