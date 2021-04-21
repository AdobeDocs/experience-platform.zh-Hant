---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: 標籤API端點
topic-legacy: developer guide
description: 瞭解如何使用Policy Service API管理Experience Platform中的資料使用標籤。
exl-id: 9a01f65c-01f1-4298-bdcf-b7e00ccfe9f2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 3%

---

# 標籤端點

資料使用標籤可讓您根據可能套用至該資料的使用原則來分類資料。 [!DNL Policy Service API]中的`/labels`端點可讓您以程式設計方式管理體驗應用程式中的資料使用標籤。

>[!NOTE]
>
>`/labels`端點僅用於檢索、建立和更新資料使用標籤。 有關如何使用API調用將標籤添加到資料集和欄位的步驟，請參閱[管理資料集標籤](../labels/dataset-api.md)上的指南。

## 快速入門

本指南中使用的API端點是[[!DNL Policy Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)的一部分。 在繼續之前，請先閱讀[快速入門手冊](getting-started.md)，以取得相關檔案的連結、閱讀本檔案中範例API呼叫的指南，以及成功呼叫任何[!DNL Experience Platform] API所需之必要標題的重要資訊。

## 檢索標籤清單{#list}

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

成功的響應返回從系統檢索到的自定義標籤清單。 由於上述範例要求是對`/labels/custom`所做，因此下方的回應只會顯示自訂標籤。

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

## 查找標籤{#look-up}

您可以在[!DNL Policy Service] API的GET請求路徑中加入該標籤的`name`屬性，以尋找特定標籤。

**API格式**

```http
GET /labels/core/{LABEL_NAME}
GET /labels/custom/{LABEL_NAME}
```

| 參數 | 說明 |
| --- | --- |
| `{LABEL_NAME}` | 您要查找的自訂標籤的`name`屬性。 |

**要求**

下列請求會擷取自訂標籤`L2`，如路徑所示。

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

## 建立或更新自訂標籤{#create-update}

若要建立或更新自訂標籤，您必須向[!DNL Policy Service] API提出PUT要求。

**API格式**

```http
PUT /labels/custom/{LABEL_NAME}
```

| 參數 | 說明 |
| --- | --- |
| `{LABEL_NAME}` | 自訂標籤的`name`屬性。 如果沒有具有此名稱的自訂標籤，則會建立新標籤。 如果存在，則會更新該標籤。 |

**要求**

下列請求會建立新標籤`L3`，其目的在於說明包含客戶所選付款計畫相關資訊的資料。

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
| `name` | 標籤的唯一字串識別碼。 此值用於查閱，並將標籤套用至資料集和欄位，因此建議使用它簡短且簡明。 |
| `category` | 標籤的類別。 雖然您可以為自訂標籤建立自己的類別，但強烈建議您使用`Custom`（如果您希望標籤顯示在UI中）。 |
| `friendlyName` | 標籤的好記名稱，用於顯示用途。 |
| `description` | （可選）標籤的說明，以提供更多內容。 |

**回應**

成功的回應會傳回自訂標籤的詳細資訊，如果已更新現有標籤，HTTP程式碼為200（確定）；如果已建立新標籤，則傳回201（已建立）。

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

本指南涵蓋在Policy Service API中使用`/labels`端點。 有關如何將標籤套用至資料集和欄位的步驟，請參閱[資料集標籤API指南](../labels/dataset-api.md)。
