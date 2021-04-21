---
keywords: Experience Platform;home；熱門主題；資料集api；管理資料使用；資料使用api
solution: Experience Platform
title: '使用API管理資料集的資料使用標籤 '
topic-legacy: developer guide
description: 資料集服務API可讓您套用和編輯資料集的使用標籤。 它是Adobe Experience Platform資料目錄功能的一部分，但與管理資料集元資料的目錄服務API不同。
exl-id: 24a8d870-eb81-4255-8e47-09ae7ad7a721
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 2%

---

# 使用API管理資料集的資料使用標籤

[[!DNL Dataset Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dataset-service.yaml)允許您應用和編輯資料集的使用標籤。 它是Adobe Experience Platform資料目錄功能的一部分，但與管理資料集元資料的[!DNL Catalog Service] API不同。

本文檔介紹如何使用[!DNL Dataset Service API]管理資料集和欄位的標籤。 如需如何使用API呼叫自行管理資料使用標籤的步驟，請參閱[!DNL Policy Service API]的[標籤端點指南](../api/labels.md)。

## 快速入門

在閱讀本指南之前，請依照目錄開發人員指南中[快速入門章節](../../catalog/api/getting-started.md)中概述的步驟，收集必要的認證以呼叫[!DNL Platform] API。

為了對本文檔中概述的端點進行調用，您必須具有特定資料集的唯一`id`值。 如果沒有此值，請參見[上列出目錄對象](../../catalog/api/list-objects.md)的指南，以查找現有資料集的ID。

## 查找資料集{#look-up}的標籤

您可以向[!DNL Dataset Service] API提出GET請求，以查找已應用到現有資料集的資料使用標籤。

**API格式**

```http
GET /datasets/{DATASET_ID}/labels
```

| 參數 | 說明 |
| --- | --- |
| `{DATASET_ID}` | 您要尋找其標籤的資料集的唯一`id`值。 |

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

## 將標籤套用至資料集{#apply}

您可以在POST或PUT請求的裝載中提供標籤給[!DNL Dataset Service] API，為資料集建立標籤集。 使用其中一種方法會覆寫任何現有的標籤，並以裝載中提供的標籤來取代標籤。

**API格式**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| 參數 | 說明 |
| --- | --- |
| `{DATASET_ID}` | 您正在為其建立標籤的資料集的唯一`id`值。 |

**要求**

下列PUT請求會更新資料集的現有標籤，以及該資料集內的特定欄位。 裝載中提供的欄位與POST要求所需的欄位相同。

>[!IMPORTANT]
>
>向`/datasets/{DATASET_ID}/labels`端點發出PUT請求時，必須提供有效的`If-Match`標頭。 有關使用所需標題的詳細資訊，請參閱[附錄部分](#if-match)。

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
| `optionalLabels` | 資料集中您想新增標籤的任何個別欄位清單。 此陣列中的每個項目都必須具有以下屬性：<br/><br/>`option`:包含欄位[!DNL Experience Data Model](XDM)屬性的對象。 需要下列三個屬性：<ul><li>id</code>:與欄位關聯的架構的URI $id</code>值。</li><li>contentType</code>:架構的內容類型和版本號。 這應採用有效<a href="../../xdm/api/getting-started.md#accept">Accept headers</a>的其中一種形式，用於XDM查閱請求。</li><li>schemaPath</code>:資料集結構中欄位的路徑。</li></ul>`labels`:您要新增至欄位的資料使用標籤清單。 |

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

## 從資料集{#remove}移除標籤

您可以對[!DNL Dataset Service] API提出DELETE請求，以移除套用至資料集的標籤。

**API格式**

```http
DELETE /datasets/{DATASET_ID}/labels
```

| 參數 | 說明 |
| --- | --- |
| `{DATASET_ID}` | 您要移除其標籤的資料集的唯一`id`值。 |

**要求**

下列請求會移除路徑中指定之資料集的標籤。

>[!IMPORTANT]
>
>向`/datasets/{DATASET_ID}/labels`端點發出DELETE請求時，必須提供有效的`If-Match`標頭。 有關使用所需標題的詳細資訊，請參閱[附錄部分](#if-match)。

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

成功的回應HTTP狀態200（確定），表示標籤已移除。 您可以在個別呼叫中，[尋找資料集的現有標籤](#look-up)以確認此點。

## 後續步驟

閱讀本檔案後，您已學習如何使用[!DNL Dataset Service] API管理資料集和欄位的資料使用標籤。

在資料集和欄位層級新增資料使用標籤後，您就可以開始將資料內嵌至[!DNL Experience Platform]。 若要進一步瞭解，請先閱讀[資料擷取檔案](../../ingestion/home.md)。

您現在也可以根據已套用的標籤來定義資料使用原則。 如需詳細資訊，請參閱[資料使用政策概述](../policies/overview.md)。

有關在[!DNL Experience Platform]中管理資料集的詳細資訊，請參見[資料集概述](../../catalog/datasets/overview.md)。

## 附錄 {#appendix}

下節包含使用資料集服務API使用標籤的其他資訊。

### [!DNL If-Match] 標題  {#if-match}

在進行更新資料集(PUT和DELETE)現有標籤的API呼叫時，必須包含`If-Match`標題，指出資料集服務中資料集標籤實體的目前版本。 為避免資料衝突，只有當包含的`If-Match`字串與系統為該資料集產生的最新版本標籤相符時，服務才會更新資料集實體。

>[!NOTE]
>
>如果目前沒有相關資料集的標籤，則只能透過POST請求新增新標籤，而不需要`If-Match`標題。 將標籤新增至資料集後，會指派`etag`值，供日後更新或移除標籤。

要檢索dataset-label實體的最新版本，請向`/datasets/{DATASET_ID}/labels`端點發出[GET請求](#look-up)。 在`etag`標題下的回應中傳回目前值。 更新現有資料集標籤時，最佳實務是先對資料集執行查閱請求，以便在後續PUT或DELETE請求的`If-Match`標題中使用該值前，先擷取其最新`etag`值。
