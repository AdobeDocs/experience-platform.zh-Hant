---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 標籤端點
topic: developer guide
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 3%

---


# 標籤端點

資料使用標籤可讓您根據可能套用至該資料的使用原則來分類資料。 中的 `/labels` 端點可讓您以 [!DNL Policy Service API] 程式設計方式管理體驗應用程式中的資料使用標籤。

>[!NOTE]
>
>端點 `/labels` 僅用於檢索、建立和更新資料使用標籤。 有關如何使用API呼叫將標籤新增至資料集和欄位的步驟，請參閱管理資料集標籤 [的指南](../labels/dataset-api.md)。

## 快速入門

本指南中使用的API端點是 [[!DNL策略服務API]的一部分](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)。 在繼續之前，請先閱讀快速入門 [指南](getting-started.md) ，以取得相關檔案的連結、閱讀本檔案中範例API呼叫的指南，以及成功呼叫任何 [!DNL Experience Platform] API所需之必要標題的重要資訊。

## 擷取標籤清單 {#list}

您可以分別 `core` 向或 `custom` 分別發出GET請求，以列 `/labels/core` 出所有或 `/labels/custom`標籤。

**API格式**

```http
GET /labels/core
GET /labels/custom
```

**請求**

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

成功的響應返回從系統檢索到的自定義標籤清單。 由於上述範例請求已提交至， `/labels/custom`下方的回應只會顯示自訂標籤。

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

您可以在GET請求到 `name` API [!DNL Policy Service] 的路徑中加入該標籤的屬性，以尋找特定標籤。

**API格式**

```http
GET /labels/core/{LABEL_NAME}
GET /labels/custom/{LABEL_NAME}
```

| 參數 | 說明 |
| --- | --- |
| `{LABEL_NAME}` | 您 `name` 要尋找的自訂標籤屬性。 |

**請求**

下列請求會擷取自訂標 `L2`簽，如路徑中所示。

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

若要建立或更新自訂標籤，您必須對 [!DNL Policy Service] API提出PUT要求。

**API格式**

```http
PUT /labels/custom/{LABEL_NAME}
```

| 參數 | 說明 |
| --- | --- |
| `{LABEL_NAME}` | 自 `name` 訂標籤的屬性。 如果沒有具有此名稱的自訂標籤，則會建立新標籤。 如果存在，則會更新該標籤。 |

**請求**

下列請求會建立新標籤， `L3`其目的在於說明包含客戶所選付款計畫相關資訊的資料。

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
| `category` | 標籤的類別。 雖然您可以為自訂標籤建立自己的類別，但強烈建議您使用， `Custom` 如果您要讓標籤顯示在UI中。 |
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

本指南涵蓋使用原則服 `/labels` 務API中的端點。 有關如何將標籤套用至資料集和欄位的步驟，請參閱資料集 [標籤API指南](../labels/dataset-api.md)。