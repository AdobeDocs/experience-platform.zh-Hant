---
keywords: Experience Platform；首頁；熱門主題；資料集api；管理資料使用；資料使用api
solution: Experience Platform
title: 使用API管理資料集的資料使用標籤
description: 資料集服務API可讓您套用及編輯資料集的使用標籤。 它是Adobe Experience Platform資料目錄功能的一部分，但與管理資料集中繼資料的目錄服務API不同。
exl-id: 24a8d870-eb81-4255-8e47-09ae7ad7a721
source-git-commit: 8db484e4a65516058d701ca972fcbcb6b73abb31
workflow-type: tm+mt
source-wordcount: '1318'
ht-degree: 1%

---

# 使用API管理資料集的資料使用標籤

此 [[!DNL Dataset Service API]](https://www.adobe.io/experience-platform-apis/references/dataset-service/) 可讓您套用及編輯資料集的使用標籤。 它是Adobe Experience Platform資料目錄功能的一部分，但與 [!DNL Catalog Service] 管理資料集中繼資料的API。

>[!IMPORTANT]
>
>僅資料控管使用案例支援在資料集層級套用標籤。 如果您嘗試建立資料的存取原則，您必須 [將標籤套用至結構描述](../../xdm/tutorials/labels.md) 資料集所根據的。 請參閱以下主題的概觀： [基於屬性的存取控制](../../access-control/abac/overview.md) 以取得詳細資訊。

本檔案說明如何使用 [!DNL Dataset Service API]. 如需如何使用API呼叫管理資料使用標籤本身的步驟，請參閱 [標籤端點指南](../api/labels.md) 針對 [!DNL Policy Service API].

## 快速入門

閱讀本指南前，請遵循以下說明的步驟 [快速入門區段](../../catalog/api/getting-started.md) 在目錄開發人員指南中，以收集必要的認證來呼叫 [!DNL Platform] API。

若要呼叫本檔案中概述的端點，您必須擁有 `id` 特定資料集的值。 如果您沒有此值，請參閱上的指南 [列出目錄物件](../../catalog/api/list-objects.md) 以尋找現有資料集的ID。

## 查詢資料集的標籤 {#look-up}

您可以透過向「 」發出GET請求，查詢已套用至現有資料集的資料使用標籤。 [!DNL Dataset Service] API。

**API格式**

```http
GET /datasets/{DATASET_ID}/labels
```

| 參數 | 說明 |
| --- | --- |
| `{DATASET_ID}` | 唯一的 `id` 您要查詢其標籤的資料集的值。 |

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

成功的回應會傳回已套用至資料集的資料使用標籤。

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
| `labels` | 已套用至資料集的資料使用標籤清單。 |
| `optionalLabels` | 資料集中已套用資料使用標籤的個別欄位清單。 |

## 將標籤套用至資料集 {#apply}

您可以在POST或PUT請求的裝載中提供一組標籤，將標籤套用至整個資料集。 [!DNL Dataset Service] API。 兩個呼叫的要求內文相同。 您無法將標籤新增至個別資料集欄位。

**API格式**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| 參數 | 說明 |
| --- | --- |
| `{DATASET_ID}` | 唯一的 `id` 您要建立標籤之資料集的值。 |

**要求**

以下範例POST請求會使用更新整個資料集 `C1` 標籤。 承載中提供的欄位與PUT請求所需的欄位相同。

進行API呼叫以更新資料集(PUT)的現有標籤時， `If-Match` 必須包含可指出資料集服務中資料集 — 標籤實體的目前版本的標頭。 為避免資料衝突，服務將僅更新資料集實體（如果包含） `If-Match` 字串符合系統為該資料集產生的最新版本標籤。

>[!NOTE]
>
>如果相關資料集目前存在標籤，則只能透過PUT請求新增新標籤，該請求需要 `If-Match` 標頭。 標籤新增至資料集後，最近一次 `etag` 稍後需要值才能更新或移除標籤<br>在執行PUT方法之前，您必須先對資料集標籤執行GET要求。 請確定您僅更新請求中要修改的特定欄位，其餘欄位保持不變。 此外，請確定PUT呼叫維護與GET呼叫相同的父項實體。 任何差異都會導致客戶發生錯誤。

若要擷取最新版本的資料集 — 標籤實體，請建立 [GET要求](#look-up) 至 `/datasets/{DATASET_ID}/labels` 端點。 目前的值會在回應中傳回，位於 `etag` 標頭。 更新現有的資料集標籤時，最佳實務是先執行資料集的查詢請求，以擷取其最新資料 `etag` 值之前，在中使用該 `If-Match` 後續PUT請求的標頭。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "entityId": {
          "namespace": "AEP",
          "id": "test-ds-id",
          "type": "dataset"
        },
        "labels": [
          "C1"
        ],
        "parents": []
      } '
```

| 屬性 | 說明 |
| --- | --- |
| `entityId` | 這會識別要更新的特定資料集實體。 |
| `entityId.namespace` | 這是用於避免ID衝突。 此 `namespace` 是 `AEP`. |
| `entityId.id` | 正在更新的資源ID。 這是指 `datasetId`. |
| `entityId.type` | 正在更新的資源型別。 永遠是 `dataset`. |
| `labels` | 您要新增至整個資料集的資料使用標籤清單。 |
| `parents` | 此 `parents` 陣列包含清單 `entityId`此資料集將繼承其標籤的位置。 資料集可以從結構描述和/或資料集繼承標籤。 |

**回應**

成功的回應會傳回資料集的更新標籤集。

>[!IMPORTANT]
>
>此 `optionalLabels` 屬性已棄用，不適用於POST請求。 無法再將資料標籤新增至資料集欄位。 POST如果 `optionalLabel` 值存在。 不過，您可以使用PUT請求和 `optionalLabels` 屬性。 如需詳細資訊，請參閱以下章節： [從資料集中移除標籤](#remove).

```json
{
  "parents": [
      {
        "id": "_ddgduleint.schemas.4a95cdba7d560e3bca7d8c5c7b58f00ca543e2bb1e4137d6",
        "type": "schema",
        "namespace": "AEP"
      }
  ],
  "optionalLabels": [],
  "labels": [
      "C1"
  ],
  "code": "PES-201",
  "message": "POST Successful"
} 
```

## 從資料集中移除標籤 {#remove}

您可以更新現有的欄位標籤，以移除任何先前套用的欄位標籤 `optionalLabels` 具有現有欄位標籤子集的值，或是要完全移除它們的空白清單。 向發出PUT請求 [!DNL Dataset Service] 更新或移除先前套用標籤的API。

**API格式**

```http
PUT /datasets/{DATASET_ID}/labels
```

| 參數 | 說明 |
| --- | --- |
| `{DATASET_ID}` | 唯一的 `id` 您要建立標籤之資料集的值。 |

**要求**

套用PUT操作的以下資料集在properties/person/properties/address欄位上有C1 optionalLabel，在/properties/person/properties/name/properties/fullName欄位上有C1， C2 optionalLabels。 put作業之後，第一個欄位將沒有標籤（移除C1標籤），而第二個欄位將只有C1標籤（移除C2標籤）

在以下範例案例中，PUT請求用於移除新增至個別欄位的標籤。 在提出要求之前， `fullName` 欄位具有 `C1` 和 `C2` 標籤已套用，而且 `address` 欄位已有 `C1` 標籤已套用。 PUT請求會覆寫現有標籤 `C1, C2` 標籤來自 `fullName` 欄位包含 `C1` 標籤使用 `optionalLabels.labels` 引數。 請求也會覆寫 `C1` 標籤來自 `address` 具有空白欄位標籤集的欄位。

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
        "entityId": {
          "namespace": "AEP",
          "id": "646b814d52e1691c07b41032",
          "type": "dataset"
        },
        "labels": [
          "C1"
        ],
        "parents": [
          {
            "id": "_xdm.context.identity-graph-flattened-export",
            "type": "schema",
            "namespace": "AEP"
          }
        ],
        "optionalLabels": [
          {
            "option": {
              "id": "https://ns.adobe.com/xdm/context/identity-graph-flattened-export",
              "contentType": "application/vnd.adobe.xed-full+json;version=1",
              "schemaPath": "/properties/person/properties/name/properties/fullName"
            },
            "labels": [
              "C1"
            ]
          },
          {
            "option": {
              "id": "https://ns.adobe.com/xdm/context/identity-graph-flattened-export",
              "contentType": "application/vnd.adobe.xed-full+json;version=1",
              "schemaPath": "/properties/person/properties/address"
            },
            "labels": []
          }
        ]
      }'
```

| 參數 | 說明 |
| --- | --- |
| `entityId` | 這會識別要更新的特定資料集實體。 此 `entityId` 必須包括下列三個值：<br/><br/>`namespace`：這是用於避免ID衝突。 此 `namespace` 是 `AEP`.<br/>`id`：正在更新之資源的ID。 這是指 `datasetId`.<br/>`type`：正在更新的資源型別。 永遠是 `dataset`. |
| `labels` | 您要新增至整個資料集的資料使用標籤清單。 |
| `parents` | 此 `parents` 陣列包含清單 `entityId`此資料集將繼承其標籤的位置。 資料集可以從結構描述和/或資料集繼承標籤。 |
| `optionalLabels` | 此引數用於移除先前套用至資料集欄位的標籤。 資料集中您要移除其標籤的任何個別欄位清單。 此陣列中的每個專案都必須具備下列屬性： <br/><br/>`option`：包含 [!DNL Experience Data Model] (XDM)欄位的屬性。 需要下列三個屬性：<ul><li><code>id</code>：URI <code>$id</code> 與欄位關聯之結構描述的值。</li><li><code>contentType</code>：結構描述的內容型別和版本號碼。 這應該採用有效的其中一種形式 <a href="../../xdm/api/getting-started.md#accept">接受標頭</a> XDM查詢請求的變數。</li><li><code>schemanpath</code>：資料集結構內欄位的路徑。</li></ul>`labels`：此值必須包含套用的現有欄位標籤的子集，或為空白以移除所有現有欄位標籤。 PUT或POST方法現在會在下列情況下傳回錯誤： `optionalLabels` 欄位具有任何新標籤或修改的標籤。 |

**回應**

成功的回應會傳回資料集的更新標籤集。

```json
{
  "parents": [
      {
        "id": "_xdm.context.identity-graph-flattened-export",
        "type": "schema",
        "namespace": "AEP"
      }
  ],
  "optionalLabels": [],
  "labels": [
      "C1"
  ],
  "code": "PES-200",
  "message": "PUT Successful"
} 
```

## 後續步驟

閱讀本檔案後，您已瞭解如何使用 [!DNL Dataset Service] API。 您現在可以定義 [資料使用原則](../policies/overview.md) 和 [存取控制原則](../../access-control/abac/ui/policies.md) 根據您已套用的標籤。

有關管理資料集的詳細資訊，請參閱 [!DNL Experience Platform]，請參閱 [資料集總覽](../../catalog/datasets/overview.md).
