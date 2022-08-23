---
keywords: Experience Platform；首頁；熱門主題；流式服務；
title: (Beta)使用流服務API為按需接收建立流運行
description: 本教程介紹使用流服務API建立流運行以按需接收的步驟
source-git-commit: ab496c7a32c20487f47850c2c571976dff57704f
workflow-type: tm+mt
source-wordcount: '1147'
ht-degree: 1%

---

# (Beta)使用 [!DNL Flow Service] API

>[!IMPORTANT]
>
>按需攝取當前處於測試版，您的組織可能尚無訪問權。 本文檔中描述的功能可能會發生更改。

流運行表示流執行的實例。 例如，如果流計畫在上午9:00 、上午10:00和上午11:00每小時運行一次，則流運行的實例有三個。 流運行特定於您的特定組織。

按需接收功能使您能夠建立針對給定資料流運行的流。 這樣，您的用戶就可以根據給定參數建立流運行，並建立不帶服務令牌的接收週期。

本教程介紹如何使用按需接收和使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)。

## 快速入門

>[!NOTE]
>
>要建立流運行，必須首先具有計畫進行一次性接收的資料流的流ID。

本教程要求您對以下Adobe Experience Platform元件有一定的瞭解：

* [源](../../home.md): [!DNL Experience Platform] 允許從各種源接收資料，同時讓您能夠使用 [!DNL Platform] 服務。
* [沙箱](../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙箱，將單個沙箱 [!DNL Platform] 實例到獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

### 使用平台API

有關如何成功調用平台API的資訊，請參見上的指南 [平台API入門](../../../landing/api-guide.md)。

## 為基於表的源建立流運行

要為基於表的源建立流，請向 [!DNL Flow Service] API，同時提供要建立運行的流的ID以及開始時間、結束時間和增量列的值。

>[!TIP]
>
>基於表的源包括以下源類別：廣告、分析、同意和首選項、 CRM 、客戶成功、資料庫、營銷自動化、支付和協定。

**API格式**

```http
POST /runs/
```

**要求**

以下請求為流ID建立流運行 `3abea21c-7e36-4be1-bec1-d3bad0e3e0de`。

>[!NOTE]
>
>您只需提供 `deltaColumn` 建立第一個流運行時。 之後， `deltaColumn` 將作為 `copy` 流變，將作為真理的源泉。 更改 `deltaColumn` 值通過流運行參數將導致錯誤。

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
| `params.windowStartTime` | 一個整數，它定義要提取資料的窗口的開始時間。 該值以unix時間表示。 |
| `params.windowEndTime` | 一個整數，它定義要提取資料的窗口的結束時間。 該值以unix時間表示。 |
| `params.deltaColumn` | 需要增量列來對資料進行分區，並將新攝取的資料與歷史資料分離。 |
| `params.deltaColumn.name` | 增量列的名稱。 |

**回應**

成功的響應返回新建立的流運行的詳細資訊，包括其唯一運行 `id`。

```json
{
    "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
    "createdAt": 1651587212543,
    "updatedAt": 1651587223839,
    "createdBy": "{CREATED_BY}",
    "updatedBy": "{UPDATED_BY}",
    "createdClient": "{CREATED_CLIENT}",
    "updatedClient": "{UPDATED_CLIENT}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "imsOrgId": "{ORGANIZATION_ID}",
    "flowId": "3abea21c-7e36-4be1-bec1-d3bad0e3e0de",
    "params": {
        "windowStartTime": "1651584991",
        "windowEndTime": "16515859567",
        "deltaColumn": {
            "name": "DOB"
        }
    },
    "etag": "\"1100c53e-0000-0200-0000-627138980000\"",
    "metrics": {
        "statusSummary": {
            "status": "scheduled"
        }
    },
    "activities": []
}
```

| 屬性 | 說明 |
| --- | --- |
| `id` | 新建立的流運行的ID。 請參閱上的指南 [檢索流規範](../api/collect/database-nosql.md#specs) 的子菜單。 |
| `createdAt` | 指定建立流運行時間的unix時間戳。 |
| `updatedAt` | 指定上次更新流運行時間的unix時間戳。 |
| `createdBy` | 建立流運行的用戶的組織ID。 |
| `updatedBy` | 上次更新流運行的用戶的組織ID。 |
| `createdClient` | 建立流運行的應用程式客戶端。 |
| `updatedClient` | 上次更新流運行的應用程式客戶端。 |
| `sandboxId` | 包含流運行的沙盒的ID。 |
| `sandboxName` | 包含流運行的沙盒的名稱。 |
| `imsOrgId` | 組織ID。 |
| `flowId` | 為其建立流運行的流的ID。 |
| `params.windowStartTime` | 一個整數，它定義要提取資料的窗口的開始時間。 該值以unix時間表示。 |
| `params.windowEndTime` | 一個整數，它定義要提取資料的窗口的結束時間。 該值以unix時間表示。 |
| `params.deltaColumn` | 需要增量列來對資料進行分區，並將新攝取的資料與歷史資料分離。 **注釋**:的 `deltaColumn` 僅在建立第一個流運行時需要。 |
| `params.deltaColumn.name` | 增量列的名稱。 |
| `etag` | 流運行的資源版本。 |
| `metrics` | 此屬性顯示流運行的狀態摘要。 |

## 為基於檔案的源建立流運行

要為基於檔案的源建立流，請向 [!DNL Flow Service] API，同時提供要建立運行的流的ID以及開始時間和結束時間的值。

>[!TIP]
>
>基於檔案的源包括所有雲儲存源。

**API格式**

```http
POST /runs/
```

**要求**

以下請求為流ID建立流運行 `3abea21c-7e36-4be1-bec1-d3bad0e3e0de`。

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
          "windowStartTime": "1651584991",
          "windowEndTime": "16515859567"
      }
  }'
```

| 參數 | 說明 |
| --- | --- |
| `flowId` | 將針對其建立流運行的流的ID。 |
| `params.windowStartTime` | 一個整數，它定義要提取資料的窗口的開始時間。 該值以unix時間表示。 |
| `params.windowEndTime` | 一個整數，它定義要提取資料的窗口的結束時間。 該值以unix時間表示。 |

**回應**

成功的響應返回新建立的流運行的詳細資訊，包括其唯一運行 `id`。


```json
{
    "id": "3fb0418e-1804-45d6-8d56-dd51f05c0baf",
    "createdAt": 1651587212543,
    "updatedAt": 1651587223839,
    "createdBy": "{CREATED_BY}",
    "updatedBy": "{UPDATED_BY}",
    "createdClient": "{CREATED_CLIENT}",
    "updatedClient": "{UPDATED_CLIENT}",
    "sandboxId": "{SANDBOX_ID}",
    "sandboxName": "prod",
    "imsOrgId": "{ORGANIZATION_ID}",
    "flowId": "3abea21c-7e36-4be1-bec1-d3bad0e3e0de",
    "params": {
        "windowStartTime": "1651584991",
        "windowEndTime": "16515859567"
    },
    "etag": "\"1100c53e-0000-0200-0000-627138980000\"",
    "metrics": {
        "statusSummary": {
            "status": "scheduled"
        }
    },
    "activities": []
}
```

| 屬性 | 說明 |
| --- | --- |
| `id` | 新建立的流運行的ID。 請參閱上的指南 [檢索流規範](../api/collect/cloud-storage.md#specs) 的子菜單。 |
| `createdAt` | 指定建立流運行時間的unix時間戳。 |
| `updatedAt` | 指定上次更新流運行時間的unix時間戳。 |
| `createdBy` | 建立流運行的用戶的組織ID。 |
| `updatedBy` | 上次更新流運行的用戶的組織ID。 |
| `createdClient` | 建立流運行的應用程式客戶端。 |
| `updatedClient` | 上次更新流運行的應用程式客戶端。 |
| `sandboxId` | 包含流運行的沙盒的ID。 |
| `sandboxName` | 包含流運行的沙盒的名稱。 |
| `imsOrgId` | 組織ID。 |
| `flowId` | 為其建立流運行的流的ID。 |
| `params.windowStartTime` | 一個整數，它定義要提取資料的窗口的開始時間。 該值以unix時間表示。 |
| `params.windowEndTime` | 一個整數，它定義要提取資料的窗口的結束時間。 該值以unix時間表示。 |
| `etag` | 流運行的資源版本。 |
| `metrics` | 此屬性顯示流運行的狀態摘要。 |


## 監視流運行

建立流運行後，您可以監視正在通過它接收的資料，以查看有關流運行、完成狀態和錯誤的資訊。 要使用API監視流運行，請參閱上的教程 [監視API中的資料流 ](./monitor.md)。 要使用平台UI監視流運行，請參閱上的指南 [使用監視儀表板監視源資料流](../../../dataflows/ui/monitor-sources.md)。
