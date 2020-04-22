---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: '使用API管理資料使用標籤 '
topic: developer guide
translation-type: tm+mt
source-git-commit: d685f1851badf54ce1d1ac3cbacd69d62894c33f

---


# 使用API管理資料使用標籤

本檔案提供如何使用Catalog Service API，在資料集和欄位層級管理資料使用標籤的步驟。

## 快速入門

在閱讀本指南之前，建議您閱讀目錄服務概觀 [](../../catalog/home.md) ，以取得更強穩的服務簡介。 此外，您也必須依照目錄開發人員指南中 [快速入門](../../catalog/api/getting-started.md) (Getting started)一節所述的步驟，收集必要的認證，以呼叫目錄API。

若要呼叫下列各節所述的端點，您必須擁有特定資料集 `id` 的唯一值。 如果您沒有此值，請參閱「開發人員指南」一節，其中列出 [目錄物件](../../catalog/api/list-objects.md) ，以尋找現有資料集的ID。

## 尋找資料集的標籤 {#lookup}

您可以透過提出GET請求，來尋找已套用至現有資料集的資料使用標籤。

**API格式**

```http
GET /dataSets/{DATASET_ID}/labels
```

| 參數 | 說明 |
| --- | --- |
| `{DATASET_ID}` | 您要 `id` 查找其標籤的資料集的唯一值。 |

**請求**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回已套用至資料集的資料使用標籤。

```json
{
  "AEP:dataset:5abd49645591445e1ba04f87": {
    "imsOrg": "{IMS_ORG}",
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
| `labels` | 已套用至資料集的資料使用標籤清單。 |
| `optionalLabels` | 資料集內已套用資料使用標籤的個別欄位清單。 |

## 將標籤套用至資料集

您可以在POST或PUT請求的裝載中提供資料集，以建立一組標籤。 使用其中一種方法會覆寫任何現有的標籤，並以裝載中提供的標籤來取代標籤。

**API格式**

```http
POST /dataSets/{DATASET_ID}/labels
PUT /dataSets/{DATASET_ID}/labels
```

| 參數 | 說明 |
| --- | --- |
| `{DATASET_ID}` | 您正 `id` 在為其建立標籤的資料集的唯一值。 |

**請求**

下列POST要求會將一系列標籤新增至資料集，以及該資料集內的特定欄位。 裝載中提供的欄位與PUT請求所需的欄位相同。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
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
| `labels` | 您要新增至資料集的資料使用標籤清單。 |
| `optionalLabels` | 資料集中您想新增標籤的任何個別欄位清單。 此陣列中的每個項目都必須具有以下屬性： <br/><br/>`option`:包含欄位「體驗資料模型」(XDM)屬性的物件。 需要下列三個屬性：<ul><li>id</code>:與欄位關聯的架構的URI</code> $id值。</li><li>contentType</code>:架構的內容類型和版本號。 這應採用XDM查閱請求的有效「接 <a href="../../xdm/api/look-up-resource.md">受」標題</a> 之一的形式。</li><li>schemaPath</code>:資料集結構中欄位的路徑。</li></ul>`labels`:您要新增至欄位的資料使用標籤清單。 |

**回應**

成功的回應會傳回已新增至資料集的標籤。

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

## 刪除資料集的標籤

您可以透過提出DELETE請求來刪除套用至資料集的標籤。

**API格式**

```http
DELETE /dataSets/{DATASET_ID}/labels
```

| 參數 | 說明 |
| --- | --- |
| `{DATASET_ID}` | 您要 `id` 刪除其標籤的資料集的唯一值。 |

**請求**

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/catalog/dataSets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功回應HTTP狀態200（確定），表示標籤已刪除。 您可 [以在個別呼叫中](#lookup) ，尋找資料集的現有標籤以確認此點。

## 後續步驟

現在您已在資料集和欄位層級新增資料使用標籤，您可以開始將資料收錄到Experience Platform。 若要進一步瞭解，請先閱讀資料 [擷取檔案](../../ingestion/home.md)。

您現在也可以根據已套用的標籤來定義資料使用原則。 如需詳細資訊，請參閱資 [料使用政策概觀](../policies/overview.md)。