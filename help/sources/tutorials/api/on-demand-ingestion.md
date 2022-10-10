---
keywords: Experience Platform；首頁；熱門主題；流量服務；
title: （測試版）使用流程服務API建立隨需擷取的流程執行
description: 本教學課程涵蓋使用流程服務API建立隨需擷取的流程執行步驟
exl-id: a7b20cd1-bb52-4b0a-aad0-796929555e4a
source-git-commit: 795b1af6421c713f580829588f954856e0a88277
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 1%

---

# （測試版）使用建立隨需擷取的流程執行 [!DNL Flow Service] API

>[!IMPORTANT]
>
>隨需擷取目前處於測試階段，而您的組織可能尚無法存取。 本檔案所述的功能可能會有所變更。

流運行表示流執行的實例。 例如，如果排程在上午9:00、上午10:00和上午11:00每小時執行流量，則會有三個流量執行例項。 流量執行是特定組織專屬的。

按需獲取功能允許您建立針對給定資料流運行的流。 這可讓您的使用者根據指定參數建立流程執行，並建立擷取週期，而不需使用服務Token。 僅批源支援按需獲取。

本教學課程涵蓋如何使用隨需擷取，以及使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入門

>[!NOTE]
>
>要建立流運行，首先必須具有排程為一次性獲取的資料流的流ID。

本教學課程需要您妥善了解下列Adobe Experience Platform元件：

* [來源](../../home.md): [!DNL Experience Platform] 可讓您從各種來源擷取資料，同時使用來建構、加標籤及增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../sandboxes/home.md): [!DNL Experience Platform] 提供可分割單一沙箱的虛擬沙箱 [!DNL Platform] 例項放入個別的虛擬環境，以協助開發及改進數位體驗應用程式。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱 [Platform API快速入門](../../../landing/api-guide.md).

## 為基於表的源建立流運行

要為基於表的源建立流，請向 [!DNL Flow Service] API，同時提供您要建立執行之流程的ID，以及開始時間、結束時間和增量欄的值。

>[!TIP]
>
>基於表的源包括以下源類別：廣告、分析、同意和偏好、CRM、客戶成功、資料庫、行銷自動化、支付和通訊協定。

**API格式**

```http
POST /runs/
```

**要求**

以下請求會建立流ID的流運行 `3abea21c-7e36-4be1-bec1-d3bad0e3e0de`.

>[!NOTE]
>
>您只需提供 `deltaColumn` 建立第一個流時執行。 之後， `deltaColumn` 將作為的一部分進行修補 `copy` 轉換，將視為真理之源。 任何嘗試變更 `deltaColumn` 值會導致錯誤。

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
| `flowId` | 將針對其建立流運行的流的ID。 |
| `params.startTime` | 定義執行開始時間的整數。 值以unix紀元時間表示。 |
| `params.windowStartTime` | 一個整數，定義要提取資料的窗口的開始時間。 值以unix時間表示。 |
| `params.windowEndTime` | 一個整數，定義要提取資料的窗口的結束時間。 值以unix時間表示。 |
| `params.deltaColumn` | 需要差值欄來分割資料，並將新擷取的資料與歷史資料分開。 **附註**:此 `deltaColumn` 只有在建立第一個流運行時才需要。 |
| `params.deltaColumn.name` | 增量列的名稱。 |

**回應**

成功的回應會傳回新建立的流程執行的詳細資訊，包括其唯一執行 `id`.

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
| `id` | 新建立的流運行的ID。 請參閱 [檢索流規範](../api/collect/database-nosql.md#specs) 以了解有關基於表的運行規範的詳細資訊。 |
| `etag` | 流運行的資源版本。 |
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

## 為基於檔案的源建立流運行

若要為檔案型來源建立流程，請向 [!DNL Flow Service] API，同時提供您要建立執行之流程的ID，以及開始時間和結束時間的值。

>[!TIP]
>
>基於檔案的源包含所有雲儲存源。

**API格式**

```http
POST /runs/
```

**要求**

以下請求會建立流ID的流運行 `3abea21c-7e36-4be1-bec1-d3bad0e3e0de`.

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
| `flowId` | 將針對其建立流運行的流的ID。 |
| `params.startTime` | 定義執行開始時間的整數。 值以unix紀元時間表示。 |
| `params.windowStartTime` | 一個整數，定義要提取資料的窗口的開始時間。 值以unix時間表示。 |
| `params.windowEndTime` | 一個整數，定義要提取資料的窗口的結束時間。 值以unix時間表示。 |

**回應**

成功的回應會傳回新建立的流程執行的詳細資訊，包括其唯一執行 `id`.


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
| `id` | 新建立的流運行的ID。 請參閱 [檢索流規範](../api/collect/database-nosql.md#specs) 以了解有關基於表的運行規範的詳細資訊。 |
| `etag` | 流運行的資源版本。 |

## 監視流運行

建立流程執行後，您可以監控正在透過其擷取的資料，以查看有關流程執行、完成狀態和錯誤的資訊。 若要使用API監控您的流程執行，請參閱以下的教學課程： [監控API中的資料流 ](./monitor.md). 若要使用Platform UI監控您的流程執行，請參閱 [使用監視儀表板監視源資料流](../../../dataflows/ui/monitor-sources.md).
