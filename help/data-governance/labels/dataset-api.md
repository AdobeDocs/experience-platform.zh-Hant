---
keywords: Experience Platform；首頁；熱門主題；資料集api；管理資料使用；資料使用api
solution: Experience Platform
title: 使用API管理資料集的資料使用標籤
description: 資料集服務API允許您應用和編輯資料集的使用標籤。 它是Adobe Experience Platform資料目錄功能的一部分，但與管理資料集元資料的目錄服務API是分開的。
exl-id: 24a8d870-eb81-4255-8e47-09ae7ad7a721
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '816'
ht-degree: 1%

---

# 使用API管理資料集的資料使用標籤

的 [[!DNL Dataset Service API]](https://www.adobe.io/experience-platform-apis/references/dataset-service/) 允許您應用和編輯資料集的用法標籤。 它是Adobe Experience Platform資料目錄功能的一部分，但與 [!DNL Catalog Service] 管理資料集元資料的API。

>[!IMPORTANT]
>
>僅在資料治理使用案例中支援在資料集級別應用標籤。 如果嘗試為資料建立訪問策略，則必須 [將標籤應用於架構](../../xdm/tutorials/labels.md) 資料集所基於。 請參閱 [基於屬性的訪問控制](../../access-control/abac/overview.md) 的子菜單。

本文檔介紹如何使用 [!DNL Dataset Service API]。 有關如何使用API調用管理資料使用標籤本身的步驟，請參見 [標籤端點指南](../api/labels.md) 為 [!DNL Policy Service API]。

## 快速入門

在閱讀本指南之前，請遵循中概述的步驟 [入門部分](../../catalog/api/getting-started.md) 在目錄開發人員指南中，收集調用所需的憑據 [!DNL Platform] API。

要調用本文檔中概述的端點，必須具有 `id` 特定資料集的值。 如果沒有此值，請參閱上的指南 [列出目錄對象](../../catalog/api/list-objects.md) 查找現有資料集的ID。

## 查找資料集的標籤 {#look-up}

通過向Web站點發出GET請求，您可以查找已應用到現有資料集的資料使用標籤 [!DNL Dataset Service] API。

**API格式**

```http
GET /datasets/{DATASET_ID}/labels
```

| 參數 | 說明 |
| --- | --- |
| `{DATASET_ID}` | 獨特 `id` 要查找其標籤的資料集的值。 |

**要求**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回已應用到資料集的資料使用標籤。

```json
{
  "AEP:dataset:5abd49645591445e1ba04f87": {
    "imsOrg": "{ORG_ID}",
    "labels": [ "C1", "C2", "C3", "I1", "I2" ],
    "optionalLabels": [
      {
        "option": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/c6b1b09bc3f2ad2627c1ecc719826836",
          "contentType": "application/vnd.adobe.xed-full+json;version=1",
          "schemaPath": "/properties/repositoryCreatedBy"
        },
        "labels": [ "S1", "S2" ]
      }
    ]
  }
}
```

| 屬性 | 說明 |
| --- | --- |
| `labels` | 已應用到資料集的資料使用標籤清單。 |
| `optionalLabels` | 資料集中具有應用資料使用標籤的各個欄位的清單。 |

## 將標籤應用於資料集 {#apply}

通過將標籤提供到POST或PUT請求的負載中，可以為資料集建立一組標籤 [!DNL Dataset Service] API。 使用這些方法中的任一方法覆蓋任何現有標籤，並用負載中提供的標籤替換它們。

**API格式**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| 參數 | 說明 |
| --- | --- |
| `{DATASET_ID}` | 獨特 `id` 要為其建立標籤的資料集的值。 |

**要求**

下面的示例PUT請求將更新資料集的現有標籤以及該資料集中的特定欄位。 負載中提供的欄位與POST請求所需的欄位相同。

當進行更新資料集(PUT)的現有標籤的API調用時， `If-Match` 必須包括指示資料集服務中資料集標籤實體的當前版本的標頭。 為防止資料衝突，服務將僅在包含 `If-Match` 字串與系統為該資料集生成的最新版本標籤匹配。

>[!NOTE]
>
>如果當前不存在有關資料集的標籤，則只能通過POST請求添加新標籤，這不需要 `If-Match` 標題。 將標籤添加到資料集後， `etag` 值已分配，可用於以後更新或刪除標籤。

要檢索資料集標籤實體的最新版本，請 [GET請求](#look-up) 到 `/datasets/{DATASET_ID}/labels` 端點。 當前值在響應中返回， `etag` 標題。 在更新現有資料集標籤時，最佳做法是首先對資料集執行查找請求以獲取其最新的資料集 `etag` 值，然後在 `If-Match` 後續PUT請求的標頭。

```shell
curl -X PUT \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -H 'If-Match: 8f00d38e-0000-0200-0000-5ef4fc6d0000' \
  -d '{
        "labels": [ "C1", "C2", "C3", "I1", "I2" ],
        "optionalLabels": [
          {
            "option": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/c6b1b09bc3f2ad2627c1ecc719826836",
              "contentType": "application/vnd.adobe.xed-full+json;version=1",
              "schemaPath": "/properties/repositoryCreatedBy"
            },
            "labels": [ "S1", "S2" ]
          }
        ]
      }'
```

| 屬性 | 說明 |
| --- | --- |
| `labels` | 要添加到資料集的資料使用標籤清單。 |
| `optionalLabels` | 資料集中要向其添加標籤的任何單個欄位的清單。 此陣列中的每個項都必須具有以下屬性： <br/><br/>`option`:包含 [!DNL Experience Data Model] (XDM)欄位的屬性。 需要以下三個屬性：<ul><li>ID</code>:URI $id</code> 與欄位關聯的架構的值。</li><li>內容類型</code>:架構的內容類型和版本號。 這應採用有效 <a href="../../xdm/api/getting-started.md#accept">接受標頭</a> 查找請求。</li><li>架構路徑</code>:資料集架構中欄位的路徑。</li></ul>`labels`:要添加到欄位的資料使用標籤清單。 |

**回應**

成功的響應返回資料集的更新標籤集。

```json
{
  "labels": [ "C1", "C2", "C3", "I1", "I2" ],
  "optionalLabels": [
    {
      "option": {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/c6b1b09bc3f2ad2627c1ecc719826836",
        "contentType": "application/vnd.adobe.xed-full+json;version=1",
        "schemaPath": "/properties/repositoryCreatedBy"
      },
      "labels": [ "S1", "S2" ]
    }
  ]
}
```

## 後續步驟

通過閱讀此文檔，您已學會了如何使用 [!DNL Dataset Service] API。 現在可以定義 [資料使用策略](../policies/overview.md) 和 [訪問控制策略](../../access-control/abac/ui/policies.md) 根據您所應用的標籤。

有關在中管理資料集的詳細資訊 [!DNL Experience Platform]，請參見 [資料集概述](../../catalog/datasets/overview.md)。
