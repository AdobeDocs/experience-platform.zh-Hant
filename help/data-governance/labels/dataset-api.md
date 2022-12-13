---
keywords: Experience Platform；首頁；熱門主題；資料集api；管理資料使用情況；資料使用api
solution: Experience Platform
title: 使用API管理資料集的資料使用量標籤
topic-legacy: developer guide
description: 資料集服務API可讓您套用及編輯資料集的使用量標籤。 此API是Adobe Experience Platform資料目錄功能的一部分，但與管理資料集中繼資料的目錄服務API不同。
exl-id: 24a8d870-eb81-4255-8e47-09ae7ad7a721
source-git-commit: 7e4c2ef8089276829604c9d8a8dd20a122b18c7a
workflow-type: tm+mt
source-wordcount: '816'
ht-degree: 1%

---

# 使用API管理資料集的資料使用量標籤

此 [[!DNL Dataset Service API]](https://www.adobe.io/experience-platform-apis/references/dataset-service/) 可讓您套用和編輯資料集的使用量標籤。 這是Adobe Experience Platform資料目錄功能的一部分，但與 [!DNL Catalog Service] 管理資料集中繼資料的API。

>[!IMPORTANT]
>
>只有資料控管使用案例才支援在資料集層級套用標籤。 如果您嘗試為資料建立訪問策略，則必須 [將標籤應用於方案](../../xdm/tutorials/labels.md) 資料集所依據之資料集。 請參閱 [基於屬性的訪問控制](../../access-control/abac/overview.md) 以取得更多資訊。

本檔案說明如何使用 [!DNL Dataset Service API]. 如需如何使用API呼叫自行管理資料使用量標籤的步驟，請參閱 [標籤端點指南](../api/labels.md) 針對 [!DNL Policy Service API].

## 快速入門

閱讀本指南之前，請遵循 [快速入門部分](../../catalog/api/getting-started.md) ，以收集進行呼叫所需的憑證 [!DNL Platform] API。

若要呼叫本檔案中概述的端點，您必須具有唯一 `id` 值。 如果您沒有此值，請參閱 [清單目錄對象](../../catalog/api/list-objects.md) 尋找現有資料集的ID。

## 查找資料集的標籤 {#look-up}

您可以向 [!DNL Dataset Service] API。

**API格式**

```http
GET /datasets/{DATASET_ID}/labels
```

| 參數 | 說明 |
| --- | --- |
| `{DATASET_ID}` | 唯一 `id` 您要查詢其標籤的資料集值。 |

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

成功的回應會傳回已套用至資料集的資料使用量標籤。

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
| `labels` | 已套用至資料集的資料使用量標籤清單。 |
| `optionalLabels` | 資料集內已套用資料使用標籤的個別欄位清單。 |

## 將標籤套用至資料集 {#apply}

您可以在POST或PUT請求的裝載中提供標籤給 [!DNL Dataset Service] API。 使用其中一種方法會覆寫任何現有標籤，並以裝載中提供的標籤取代這些標籤。

**API格式**

```http
POST /datasets/{DATASET_ID}/labels
PUT /datasets/{DATASET_ID}/labels
```

| 參數 | 說明 |
| --- | --- |
| `{DATASET_ID}` | 唯一 `id` 為其建立標籤的資料集值。 |

**要求**

以下的範例PUT請求會更新資料集的現有標籤，以及該資料集內的特定欄位。 有效負載中提供的欄位與POST要求所需的欄位相同。

發出API呼叫以更新資料集(PUT)的現有標籤時， `If-Match` 指出資料集服務中資料集標籤實體目前版本的標題。 為避免資料衝突，服務只會在包含的 `If-Match` 字串會比對系統為該資料集產生的最新版本標籤。

>[!NOTE]
>
>如果相關資料集目前沒有標籤，則只能透過POST請求新增標籤，這不需要 `If-Match` 頁首。 將標籤新增至資料集後， `etag` 會指派值，以便稍後更新或移除標籤。

若要擷取最新版本的資料集標籤實體，請建立 [GET要求](#look-up) 到 `/datasets/{DATASET_ID}/labels` 端點。 目前值會在回應中的 `etag` 頁首。 更新現有資料集標籤時，最佳作法是先對資料集執行查詢請求，以擷取其最新資料集 `etag` 值，然後在 `If-Match` 後續PUT請求的標題。

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
| `labels` | 您要新增至資料集的資料使用量標籤清單。 |
| `optionalLabels` | 資料集內您要新增標籤的任何個別欄位清單。 此陣列中的每個項目必須具有下列屬性： <br/><br/>`option`:包含 [!DNL Experience Data Model] (XDM)欄位的屬性。 需要下列三個屬性：<ul><li>id</code>:URI $id</code> 與欄位相關聯的架構的值。</li><li>contentType</code>:結構的內容類型和版本號。 這應採用有效 <a href="../../xdm/api/getting-started.md#accept">接受標題</a> XDM查詢請求。</li><li>schemaPath</code>:資料集結構內欄位的路徑。</li></ul>`labels`:您要新增至欄位的資料使用量標籤清單。 |

**回應**

成功的回應會傳回資料集的更新標籤集。

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

閱讀本檔案後，您已了解如何使用 [!DNL Dataset Service] API。 您現在可以定義 [資料使用原則](../policies/overview.md) 和 [訪問控制策略](../../access-control/abac/ui/policies.md) 根據您已套用的標籤。

如需管理資料集的詳細資訊，請參閱 [!DNL Experience Platform]，請參閱 [資料集概述](../../catalog/datasets/overview.md).
