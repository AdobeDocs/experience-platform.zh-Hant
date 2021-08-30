---
keywords: Experience Platform；首頁；熱門主題；資料集api；管理資料使用情況；資料使用api
solution: Experience Platform
title: '使用API管理資料集的資料使用量標籤 '
topic-legacy: developer guide
description: 資料集服務API可讓您套用及編輯資料集的使用量標籤。 此API是Adobe Experience Platform資料目錄功能的一部分，但與管理資料集中繼資料的目錄服務API不同。
exl-id: 24a8d870-eb81-4255-8e47-09ae7ad7a721
source-git-commit: 937225ff08e2e02c5840f86d6ed50644e05bdfe5
workflow-type: tm+mt
source-wordcount: '957'
ht-degree: 2%

---

# 使用API管理資料集的資料使用量標籤

[[!DNL Dataset Service API]](https://www.adobe.io/experience-platform-apis/references/dataset-service/)可讓您套用及編輯資料集的使用量標籤。 這是Adobe Experience Platform資料目錄功能的一部分，但與管理資料集中繼資料的[!DNL Catalog Service] API不同。

本檔案說明如何使用[!DNL Dataset Service API]管理資料集和欄位的標籤。 有關如何使用API呼叫自行管理資料使用量標籤的步驟，請參閱[標籤端點指南](../api/labels.md)以取得[!DNL Policy Service API]。

## 快速入門

閱讀本指南之前，請依照目錄開發人員指南中[快速入門小節](../../catalog/api/getting-started.md)中概述的步驟，收集必要憑證，以呼叫[!DNL Platform] API。

若要呼叫本檔案中概述的端點，特定資料集必須具有唯一的`id`值。 如果您沒有此值，請參閱[列出目錄物件](../../catalog/api/list-objects.md)的指南，以尋找現有資料集的ID。

## 查找資料集的標籤 {#look-up}

您可以向[!DNL Dataset Service] API提出GET要求，以查找已套用至現有資料集的資料使用量標籤。

**API格式**

```http
GET /datasets/{DATASET_ID}/labels
```

| 參數 | 說明 |
| --- | --- |
| `{DATASET_ID}` | 您要查詢其標籤的資料集的唯一`id`值。 |

**要求**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dataset/datasets/5abd49645591445e1ba04f87/labels' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回已套用至資料集的資料使用量標籤。

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
| `labels` | 已套用至資料集的資料使用量標籤清單。 |
| `optionalLabels` | 資料集內已套用資料使用標籤的個別欄位清單。 |

## 將標籤套用至資料集 {#apply}

您可以在[!DNL Dataset Service] API的POST或PUT請求的裝載中提供資料集，以建立資料集的標籤集。 使用其中一種方法會覆寫任何現有標籤，並以裝載中提供的標籤取代這些標籤。

**API格式**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| 參數 | 說明 |
| --- | --- |
| `{DATASET_ID}` | 為建立標籤的資料集的唯一`id`值。 |

**要求**

下列PUT請求會更新資料集的現有標籤，以及該資料集內的特定欄位。 有效負載中提供的欄位與POST要求所需的欄位相同。

>[!IMPORTANT]
>
>向`/datasets/{DATASET_ID}/labels`端點發出PUT請求時，必須提供有效的`If-Match`標題。 有關使用所需標題的詳細資訊，請參閱[附錄部分](#if-match)。

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
| `labels` | 您要新增至資料集的資料使用量標籤清單。 |
| `optionalLabels` | 資料集內您要新增標籤的任何個別欄位清單。 此陣列中的每個項目必須具有下列屬性：<br/><br/>`option`:包含欄位[!DNL Experience Data Model](XDM)屬性的物件。 需要下列三個屬性：<ul><li>id</code>:與欄位關聯的架構的URI $id</code>值。</li><li>contentType</code>:結構的內容類型和版本號。 此格式應為XDM查詢請求的有效<a href="../../xdm/api/getting-started.md#accept">接受標題</a>之一。</li><li>schemaPath</code>:資料集結構內欄位的路徑。</li></ul>`labels`:您要新增至欄位的資料使用量標籤清單。 |

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

## 從資料集中移除標籤 {#remove}

您可以向[!DNL Dataset Service] API提出DELETE請求，移除套用至資料集的標籤。

**API格式**

```http
DELETE /datasets/{DATASET_ID}/labels
```

| 參數 | 說明 |
| --- | --- |
| `{DATASET_ID}` | 您要移除其標籤之資料集的唯一`id`值。 |

**要求**

下列請求會移除路徑中指定之資料集的標籤。

>[!IMPORTANT]
>
>向`/datasets/{DATASET_ID}/labels`端點發出DELETE請求時，必須提供有效的`If-Match`標題。 有關使用所需標題的詳細資訊，請參閱[附錄部分](#if-match)。

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

成功的回應HTTP狀態200（確定），表示標籤已移除。 您可以透過個別呼叫[查找資料集的現有標籤](#look-up)以確認此情況。

## 後續步驟

閱讀本檔案後，您就學習了如何使用[!DNL Dataset Service] API管理資料集和欄位的資料使用量標籤。

在資料集和欄位層級新增資料使用量標籤後，您就可以開始將資料內嵌至[!DNL Experience Platform]。 若要深入了解，請先閱讀[資料擷取檔案](../../ingestion/home.md)。

您現在也可以根據已套用的標籤來定義資料使用原則。 如需詳細資訊，請參閱[資料使用原則概述](../policies/overview.md)。

如需在[!DNL Experience Platform]中管理資料集的詳細資訊，請參閱[資料集概述](../../catalog/datasets/overview.md)。

## 附錄 {#appendix}

以下章節包含使用資料集服務API使用標籤的其他資訊。

### [!DNL If-Match] 標題 {#if-match}

發出API呼叫以更新資料集(PUT和DELETE)的現有標籤時，必須加上`If-Match`標題，指出資料集服務中資料集標籤實體的目前版本。 為避免資料衝突，只有當包含的`If-Match`字串符合系統為該資料集產生的最新版本標籤時，服務才會更新資料集實體。

>[!NOTE]
>
>如果相關資料集目前沒有標籤，則只能透過POST請求新增新標籤，而此請求不需要`If-Match`標題。 將標籤新增至資料集後，會指派`etag`值，以便稍後更新或移除標籤。

若要擷取最新版本的dataset-label實體，請向`/datasets/{DATASET_ID}/labels`端點發出[GET要求](#look-up)。 回應中`etag`標題下會傳回目前值。 更新現有資料集標籤時，最佳作法是先對資料集執行查詢請求，以在後續PUT或DELETE請求的`If-Match`標題中使用該值前擷取其最新`etag`值。
