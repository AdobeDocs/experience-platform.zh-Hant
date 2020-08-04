---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: '使用API管理資料集的資料使用標籤 '
topic: developer guide
translation-type: tm+mt
source-git-commit: 3b6f46c5a81e1b6e8148bf4b78ae2560723f9d20
workflow-type: tm+mt
source-wordcount: '912'
ht-degree: 2%

---


# 使用API管理資料集的資料使用標籤

允許您 [!DNL Dataset Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dataset-service.yaml) 應用和編輯資料集的使用標籤。 它是Adobe Experience Platform資料目錄功能的一部分，但與管理資料集中繼資料的 [!DNL Catalog Service] API不同。

本文檔介紹如何使用管理資料集和欄位的標籤 [!DNL Dataset Service API]。 如需如何使用API呼叫自行管理資料使用標籤的步驟，請參 [閱標籤端點指南](../api/labels.md)[!DNL Policy Service API]。

## 快速入門

在閱讀本指南之前，請依照目錄開發人員指南 [中](../../catalog/api/getting-started.md) 「快速入門」一節中概述的步驟，收集必要的認證以呼叫 [!DNL Platform] API。

若要呼叫本檔案中概述的端點，您必須擁有特定資料集 `id` 的唯一值。 如果沒有此值，請參閱列出目錄對象 [以查找現有資料集的ID](../../catalog/api/list-objects.md) 的指南。

## 尋找資料集的標籤 {#look-up}

您可以對 [!DNL Dataset Service] API提出GET要求，以尋找已套用至現有資料集的資料使用標籤。

**API格式**

```http
GET /datasets/{DATASET_ID}/labels
```

| 參數 | 說明 |
| --- | --- |
| `{DATASET_ID}` | 您要 `id` 查找其標籤的資料集的唯一值。 |

**請求**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
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

## 將標籤套用至資料集 {#apply}

您可以在POST或PUT要求的裝載中提供標籤給 [!DNL Dataset Service] API，為資料集建立標籤集。 使用其中一種方法會覆寫任何現有的標籤，並以裝載中提供的標籤來取代標籤。

**API格式**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| 參數 | 說明 |
| --- | --- |
| `{DATASET_ID}` | 您正 `id` 在為其建立標籤的資料集的唯一值。 |

**請求**

下列PUT請求會更新資料集的現有標籤以及該資料集內的特定欄位。 裝載中提供的欄位與POST要求所需的欄位相同。

>[!IMPORTANT]
>
>對端點 `If-Match` 發出PUT請求時，必須提供有效的標 `/datasets/{DATASET_ID}/labels` 頭。 如需使 [用必要標題的詳細資訊](#if-match) ，請參閱附錄一節。

```shell
curl -X PUT \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `labels` | 您要新增至資料集的資料使用標籤清單。 |
| `optionalLabels` | 資料集中您想新增標籤的任何個別欄位清單。 此陣列中的每個項目都必須具有以下屬性： <br/><br/>`option`: 包含欄位 [!DNL Experience Data Model] (XDM)屬性的對象。 需要下列三個屬性：<ul><li>id</code>: 與欄位關聯的架構的URI</code> $id值。</li><li>contentType</code>: 架構的內容類型和版本號。 這應採用XDM查閱請求的有效「接 <a href="../../xdm/api/look-up-resource.md">受」標題</a> 之一的形式。</li><li>schemaPath</code>: 資料集結構中欄位的路徑。</li></ul>`labels`: 您要新增至欄位的資料使用標籤清單。 |

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

## 從資料集移除標籤 {#remove}

您可以對 [!DNL Dataset Service] API提出DELETE請求，移除套用至資料集的標籤。

**API格式**

```http
DELETE /datasets/{DATASET_ID}/labels
```

| 參數 | 說明 |
| --- | --- |
| `{DATASET_ID}` | 您要 `id` 移除其標籤的資料集的唯一值。 |

**請求**

下列請求會移除路徑中指定之資料集的標籤。

>[!IMPORTANT]
>
>向端點 `If-Match` 發出DELETE請求時，必須提供有效的 `/datasets/{DATASET_ID}/labels` 標頭。 如需使 [用必要標題的詳細資訊](#if-match) ，請參閱附錄一節。

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'If-Match: 8f00d38e-0000-0200-0000-5ef4fc6d0000'
```

**回應**

成功的回應HTTP狀態200（確定），表示標籤已移除。 您可 [以在個別呼叫中](#look-up) ，尋找資料集的現有標籤以確認此點。

## 後續步驟

閱讀本檔案後，您已學習如何使用 [!DNL Dataset Service] API管理資料集和欄位的資料使用標籤。

在資料集和欄位層級新增資料使用標籤後，您就可以開始將資料內嵌至 [!DNL Experience Platform]。 若要進一步瞭解，請先閱讀資料 [擷取檔案](../../ingestion/home.md)。

您現在也可以根據已套用的標籤來定義資料使用原則。 如需詳細資訊，請參閱資 [料使用政策概觀](../policies/overview.md)。

有關在中管理資料集的詳細信 [!DNL Experience Platform]息，請參 [見資料集概述](../../catalog/datasets/overview.md)。

## 附錄 {#appendix}

下節包含使用資料集服務API使用標籤的其他資訊。

### [!DNL If-Match] 標題 {#if-match}

在進行更新資料集（PUT和DELETE）現有標籤的API呼叫時，必須包含 `If-Match` 標題，指出資料集服務中資料集標籤實體的目前版本。 為避免資料衝突，只有當包含的字串符合系統為該資料集產生的最新版本標籤時， `If-Match` 服務才會更新資料集實體。

>[!NOTE]
>
>如果目前沒有相關資料集的標籤，則只能透過POST要求新增新標籤，而不需要標 `If-Match` 題。 將標籤新增至資料集後，會指 `etag` 派一個值，供稍後用來更新或移除標籤。

若要擷取最新版本的dataset-label實體，請向端點 [提出GET](#look-up)`/datasets/{DATASET_ID}/labels` 請求。 在回應中的標題下傳回目前 `etag` 值。 在更新現有資料集標籤時，最佳實務是先對資料集執行查閱請求，以便在後續PUT或DELETE請求的標題中使用該值之前，先擷取其最 `etag` 新 `If-Match` 值。