---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: 標籤API端點
topic-legacy: developer guide
description: 了解如何使用原則服務API管理Experience Platform中的資料使用量標籤。
exl-id: 9a01f65c-01f1-4298-bdcf-b7e00ccfe9f2
source-git-commit: 8133804076b1c0adf2eae5b748e86a35f3186d14
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 3%

---

# 標籤端點

資料使用量標籤可讓您根據可能套用至該資料的使用量原則來分類資料。 [!DNL Policy Service API]中的`/labels`端點可讓您以程式設計方式管理體驗應用程式中的資料使用量標籤。

>[!NOTE]
>
>`/labels`端點僅用於擷取、建立和更新資料使用量標籤。 有關如何使用API呼叫將標籤新增至資料集和欄位的步驟，請參閱[管理資料集標籤](../labels/dataset-api.md)的指南。

## 快速入門

本指南中使用的API端點是[[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/)的一部分。 繼續之前，請檢閱[快速入門手冊](getting-started.md)，取得相關檔案的連結、閱讀本檔案中範例API呼叫的指南，以及成功呼叫任何[!DNL Experience Platform] API所需的重要標題資訊。

## 擷取標籤清單 {#list}

您可以分別向`/labels/core`或`/labels/custom`發出GET請求，以列出所有`core`或`custom`標籤。

**API格式**

```http
GET /labels/core
GET /labels/custom
```

**要求**

下列請求會列出您組織下建立的所有自訂標籤。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回從系統擷取的自訂標籤清單。 由於對`/labels/custom`提出了上述範例要求，因此下方的回應只會顯示自訂標籤。

```json
{
    "_page": {
        "count": 2
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom?{?limit,start,property}",
            "templated": true
        }
    },
    "children": [
        {
            "name": "L1",
            "category": "Custom",
            "friendlyName": "Banking Information",
            "description": "Data containing banking information for a customer.",
            "imsOrg": "{IMS_ORG}",
            "sandboxName": "{SANDBOX_NAME}",
            "created": 1594396718731,
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1594396718731,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L1"
                }
            }
        },
        {
            "name": "L2",
            "category": "Custom",
            "friendlyName": "Purchase History Data",
            "description": "Data containing information on past transactions",
            "imsOrg": "{IMS_ORG}",
            "sandboxName": "{SANDBOX_NAME}",
            "created": 1594397415663,
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1594397728708,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L2"
                }
            }
        }
    ]
}
```

## 查找標籤 {#look-up}

您可以在[!DNL Policy Service] API的GET請求路徑中加入該標籤的`name`屬性，以查找特定標籤。

**API格式**

```http
GET /labels/core/{LABEL_NAME}
GET /labels/custom/{LABEL_NAME}
```

| 參數 | 說明 |
| --- | --- |
| `{LABEL_NAME}` | 您要查詢的自訂標籤的`name`屬性。 |

**要求**

如路徑所示，下列請求會擷取自訂標籤`L2`。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L2' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回自訂標籤的詳細資訊。

```json
{
    "name": "L2",
    "category": "Custom",
    "friendlyName": "Purchase History Data",
    "description": "Data containing information on past transactions",
    "imsOrg": "{IMS_ORG}",
    "sandboxName": "{SANDBOX_NAME}",
    "created": 1594397415663,
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1594397728708,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L2"
        }
    }
}
```

## 建立或更新自訂標籤 {#create-update}

若要建立或更新自訂標籤，您必須向[!DNL Policy Service] API提出PUT要求。

**API格式**

```http
PUT /labels/custom/{LABEL_NAME}
```

| 參數 | 說明 |
| --- | --- |
| `{LABEL_NAME}` | 自訂標籤的`name`屬性。 如果具有此名稱的自訂標籤不存在，則會建立新標籤。 如果確實存在，則會更新該標籤。 |

**要求**

以下請求建立新標籤`L3`，該標籤旨在描述包含與客戶選定付款計畫相關資訊的資料。

```shell
curl -X PUT \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "L3",
        "category": "Custom",
        "friendlyName": "Payment Plan",
        "description": "Data containing information on selected payment plans."
      }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 標籤的唯一字串識別碼。 此值可用於查詢，並將標籤套用至資料集和欄位，因此建議使用它簡短明瞭。 |
| `category` | 標籤的類別。 雖然您可以為自訂標籤建立自己的類別，但如果您希望標籤顯示在UI中，則強烈建議您使用`Custom`。 |
| `friendlyName` | 標籤的好記名稱，用於顯示用途。 |
| `description` | （選用）提供進一步內容之標籤的說明。 |

**回應**

成功的回應會傳回自訂標籤的詳細資訊，如果現有標籤更新，則會傳回HTTP代碼200(OK)，如果建立新標籤，則會傳回201(Created)。

```json
{
  "name": "L3",
  "category": "Custom",
  "friendlyName": "Payment Plan",
  "description": "Data containing information on selected payment plans.",
  "imsOrg": "{IMS_ORG}",
  "sandboxName": "{SANDBOX_NAME}",
  "created": 1529696681413,
  "createdClient": "{CLIENT_ID}",
  "createdUser": "{USER_ID}",
  "updated": 1529697651972,
  "updatedClient": "{CLIENT_ID}",
  "updatedUser": "{USER_ID}",
  "_links": {
    "self": {
      "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L3"
    }
  }
}
```

## 後續步驟

本指南介紹了策略服務API中`/labels`端點的使用。 如需如何將標籤套用至資料集和欄位的步驟，請參閱資料集標籤API指南](../labels/dataset-api.md)。[
