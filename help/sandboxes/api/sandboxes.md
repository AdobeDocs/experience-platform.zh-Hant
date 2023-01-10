---
keywords: Experience Platform；首頁；熱門主題；沙箱開發人員指南
solution: Experience Platform
title: 沙箱管理API端點
description: 沙箱API中的/沙箱端點可讓您以程式設計方式管理Adobe Experience Platform中的沙箱。
exl-id: 0ff653b4-3e31-4ea5-a22e-07e18795f73e
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1489'
ht-degree: 3%

---

# 沙箱管理端點

Adobe Experience Platform中的沙箱提供孤立的開發環境，可讓您測試功能、執行實驗及進行自訂設定，而不會影響您的生產環境。 此 `/sandboxes` 端點 [!DNL Sandbox] API可讓您以程式設計方式管理Platform中的沙箱。

## 快速入門

本指南中使用的API端點屬於 [[!DNL Sandbox] API](https://www.adobe.io/experience-platform-apis/references/sandbox). 繼續之前，請檢閱 [快速入門手冊](./getting-started.md) 如需相關檔案的連結，請參閱本檔案中讀取範例API呼叫的指南，以及成功呼叫任何Experience PlatformAPI所需的必要標頭重要資訊。

## 擷取沙箱清單 {#list}

您可以向 `/sandboxes` 端點。

**API格式**

```http
GET /sandboxes?{QUERY_PARAMS}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{QUERY_PARAMS}` | 可選的查詢參數，以依據篩選結果。 請參閱 [查詢參數](./appendix.md#query) 以取得更多資訊。 |

**要求**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes?&limit=4&offset=1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回屬於您組織的沙箱清單，包括 `name`, `title`, `state`，和 `type`.

```json
{
    "sandboxes": [
        {
            "name": "prod",
            "title": "Production",
            "state": "active",
            "type": "production",
            "region": "VA7",
            "isDefault": true,
            "eTag": 2,
            "createdDate": "2019-09-04 04:57:24",
            "lastModifiedDate": "2019-09-04 04:57:24",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        },
        {
            "name": "dev",
            "title": "Development",
            "state": "active",
            "type": "development",
            "region": "VA7",
            "isDefault": false,
            "eTag": 1,
            "createdDate": "2019-09-03 22:27:48",
            "lastModifiedDate": "2019-09-03 22:27:48",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        },
        {
            "name": "stage",
            "title": "Staging",
            "state": "active",
            "type": "development",
            "region": "VA7",
            "isDefault": false,
            "eTag": 1,
            "createdDate": "2019-09-03 22:27:48",
            "lastModifiedDate": "2019-09-03 22:27:48",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        },
        {
            "name": "dev-2",
            "title": "Development 2",
            "state": "creating",
            "type": "development",
            "region": "VA7",
            "isDefault": false,
            "eTag": 1,
            "createdDate": "2019-09-07 10:16:02",
            "lastModifiedDate": "2019-09-07 10:16:02",
            "createdBy": "{USER_ID}",
            "modifiedBy": "{USER_ID}"
        }
    ],
    "_page": {
        "limit": 4,
        "count": 4
    },
    "_links": {
        "next": {
            "href": "https://platform.adobe.io:443/data/foundation/sandbox-management/sandboxes/?limit={limit}&offset={offset}",
            "templated": true
        },
        "prev": {
            "href": "https://platform.adobe.io:443/data/foundation/sandbox-management/sandboxes?offset=0&limit=1",
            "templated": null
        },
        "page": {
            "href": "https://platform.adobe.io:443/data/foundation/sandbox-management/sandboxes?offset=1&limit=1",
            "templated": null
        }
    }
}
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 沙箱的名稱。 此屬性可用於API呼叫中的查詢用途。 |
| `title` | 沙箱的顯示名稱。 |
| `state` | 沙箱的目前處理狀態。 沙箱的狀態可以是下列任一項： <br/><ul><li>`creating`:沙箱已建立，但系統仍在布建。</li><li>`active`:沙箱已建立且作用中。</li><li>`failed`:由於錯誤，系統無法布建沙箱，且已停用。</li><li>`deleted`:沙箱已手動停用。</li></ul> |
| `type` | 沙箱類型。 目前支援的沙箱類型包括 `development` 和 `production`. |
| `isDefault` | 此布林值屬性可指出此沙箱是否為組織的預設生產沙箱。 |
| `eTag` | 沙箱特定版本的識別碼。 用於版本控制和快取效率，此值會在每次對沙箱進行變更時更新。 |

## 尋找沙箱 {#lookup}

您可以提出包含沙箱的GET要求，以查詢個別沙箱 `name` 屬性。

**API格式**

```http
GET /sandboxes/{SANDBOX_NAME}
```

| 參數 | 說明 |
| --- | --- |
| `{SANDBOX_NAME}` | 此 `name` 您要查詢的沙箱的屬性。 |

**要求**

下列要求會擷取名為「dev-2」的沙箱。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**回應**

成功的回應會傳回沙箱的詳細資訊，包括 `name`, `title`, `state`，和 `type`.

```json
{
    "name": "dev-2",
    "title": "Development 2",
    "state": "creating",
    "type": "development",
    "region": "VA7",
    "isDefault": false,
    "eTag": 1,
    "createdDate": "2019-09-07 10:16:02",
    "lastModifiedDate": "2019-09-07 10:16:02",
    "createdBy": "{USER_ID}",
    "modifiedBy": "{USER_ID}"
}
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 沙箱的名稱。 此屬性可用於API呼叫中的查詢用途。 |
| `title` | 沙箱的顯示名稱。 |
| `state` | 沙箱的目前處理狀態。 沙箱的狀態可以是下列任一項： <ul><li>**建立**:沙箱已建立，但系統仍在布建。</li><li>**活動**:沙箱已建立且作用中。</li><li>**失敗**:由於錯誤，系統無法布建沙箱，且已停用。</li><li>**已刪除**:沙箱已手動停用。</li></ul> |
| `type` | 沙箱類型。 目前支援的沙箱類型包括： `development` 和 `production`. |
| `isDefault` | 一個布林值屬性，用於指出此沙箱是否為組織的預設沙箱。 這通常是生產沙箱。 |
| `eTag` | 沙箱特定版本的識別碼。 用於版本控制和快取效率，此值會在每次對沙箱進行變更時更新。 |

## 建立沙箱 {#create}

>[!NOTE]
>
>建立新沙箱時，您必須先將該新沙箱新增至產品設定檔，位於 [Adobe Admin Console](https://adminconsole.adobe.com/) 開始使用新沙箱之前。 請參閱 [管理產品設定檔的權限](../../access-control/ui/permissions.md) 以取得如何將沙箱布建至產品設定檔的資訊。

您可以向發出POST要求，以建立新的開發或生產沙箱 `/sandboxes` 端點。

### 建立開發沙箱

若要建立開發沙箱，您必須提供 `type` 屬性，值為 `development` 在要求裝載中。

**API格式**

```http
POST /sandboxes
```

**要求**

下列請求會建立名為「acme-dev」的新開發沙箱。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "acme-dev",
    "title": "Acme Business Group dev",
    "type": "development"
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 未來要求中用來存取沙箱的識別碼。 此值必須是唯一的，最佳作法是盡可能提供描述性。 此值不能包含任何空格或特殊字元。 |
| `title` | 在Platform使用者介面中用於顯示目的的人類可讀名稱。 |
| `type` | 要建立的沙箱類型。 對於非生產沙箱，此值必須是 `development`. |

**回應**

成功的回應會傳回新建立沙箱的詳細資訊，顯示其 `state` 是「正在建立」。

```json
{
    "name": "acme-dev",
    "title": "Acme Business Group dev",
    "state": "creating",
    "type": "development",
    "region": "VA7"
}
```

>[!NOTE]
>
>沙箱需要約30秒的時間才能由系統布建，之後便會布建 `state` 會變為「作用中」或「失敗」。

### 建立生產沙箱

若要建立生產沙箱，您必須提供 `type` 屬性，值為 `production` 在要求裝載中。

**API格式**

```http
POST /sandboxes
```

**要求**

下列請求會建立名為「acme」的新生產沙箱。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H `Accept: application/json` \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "acme",
    "title": "Acme Business Group",
    "type": "production"
}'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 未來要求中用來存取沙箱的識別碼。 此值必須是唯一的，最佳作法是盡可能提供描述性。 此值不能包含任何空格或特殊字元。 |
| `title` | 在Platform使用者介面中用於顯示目的的人類可讀名稱。 |
| `type` | 要建立的沙箱類型。 對於生產沙箱，此值必須是 `production`. |

**回應**

成功的回應會傳回新建立沙箱的詳細資訊，顯示其 `state` 是「正在建立」。

```json
{
    "name": "acme",
    "title": "Acme Business Group",
    "state": "creating",
    "type": "production",
    "region": "VA7"
}
```

>[!NOTE]
>
>沙箱需要約30秒的時間才能由系統布建，之後便會布建 `state` 會變為「作用中」或「失敗」。

## 更新沙箱 {#put}

您可以提出包含沙箱的PATCH請求，以更新沙箱中的一或多個欄位 `name` ，以及要在請求裝載中更新的屬性。

>[!NOTE]
>
>目前僅有沙箱的 `title` 屬性可以更新。

**API格式**

```http
PATCH /sandboxes/{SANDBOX_NAME}
```

| 參數 | 說明 |
| --- | --- |
| `{SANDBOX_NAME}` | 此 `name` 您要更新之沙箱的屬性。 |

**要求**

下列請求會更新 `title` 名為「acme」的沙箱屬性。

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json'
  -d '{
    "title": "Acme Business Group prod"
  }'
```

**回應**

成功的回應會傳回HTTP狀態200(OK)，並附上新更新沙箱的詳細資訊。

```json
{
    "name": "acme",
    "title": "Acme Business Group prod",
    "state": "active",
    "type": "production",
    "region": "VA7"
}
```

## 重設沙箱 {#reset}

沙箱具有「工廠重設」功能，會從沙箱中刪除所有非預設資源。 您可以提出包含沙箱的PUT要求，以重設沙箱 `name` 在請求路徑中。

**API格式**

```http
PUT /sandboxes/{SANDBOX_NAME}
```

| 參數 | 說明 |
| --- | --- |
| `{SANDBOX_NAME}` | 此 `name` 您要重設之沙箱的屬性。 |
| `validationOnly` | 此選用參數可讓您對沙箱重設作業執行預檢檢查，而無須提出實際請求。 將此參數設為 `validationOnly=true` 來檢查您要重設的沙箱是否包含任何Adobe Analytics、Adobe Audience Manager或區段共用資料。 |

**要求**

下列請求會重設名為「acme-dev」的沙箱。

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme-dev?validationOnly=true \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json'
  -d '{
    "action": "reset"
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `action` | 必須在要求裝載中提供此參數，且值為「reset」，才能重設沙箱。 |

**回應**

>[!NOTE]
>
>重設沙箱後，系統需要大約30秒來布建。

成功的回應會傳回更新沙箱的詳細資訊，顯示其 `state` 為「正在重設」。

```json
{
    "id": "d8184350-dbf5-11e9-875f-6bf1873fec16",
    "name": "acme-dev",
    "title": "Acme Business Group dev",
    "state": "resetting",
    "type": "development",
    "region": "VA7"
}
```

如果Adobe Analytics也在將預設生產沙箱和使用者建立的生產沙箱用於 [跨裝置分析(CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html) 功能，或內部托管的身分圖表也正由Adobe Audience Manager用於 [以人物為基礎的目的地(PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html) 功能。

以下是可能導致沙箱無法重設的例外清單：

```json
{
    "status": 400,
    "title": "Sandbox `{SANDBOX_NAME}` cannot be reset. The identity graph hosted in this sandbox is also being used by Adobe Analytics for the Cross Device Analytics (CDA) feature.",
    "type": "http://ns.adobe.com/aep/errors/SMS-2074-400"
},
{
    "status": 400,
    "title": "Sandbox `{SANDBOX_NAME}` cannot be reset. The identity graph hosted in this sandbox is also being used by Adobe Audience Manager for the People Based Destinations (PBD) feature.",
    "type": "http://ns.adobe.com/aep/errors/SMS-2075-400"
},
{
    "status": 400,
    "title": "Sandbox `{SANDBOX_NAME}` cannot be reset. The identity graph hosted in this sandbox is also being used by Adobe Audience Manager for the People Based Destinations (PBD) feature, as well by Adobe Analytics for the Cross Device Analytics (CDA) feature.",
    "type": "http://ns.adobe.com/aep/errors/SMS-2076-400"
},
{
    "status": 400,
    "title": "Warning: Sandbox `{SANDBOX_NAME}` is used for bi-directional segment sharing with Adobe Audience Manager or Audience Core Service.",
    "type": "http://ns.adobe.com/aep/errors/SMS-2077-400"
}
```

您可以繼續重設用於與共用雙向區段的生產沙箱 [!DNL Audience Manager] 或 [!DNL Audience Core Service] 新增 `ignoreWarnings` 參數。

**API格式**

```http
PUT /sandboxes/{SANDBOX_NAME}?ignoreWarnings=true
```

| 參數 | 說明 |
| --- | --- |
| `{SANDBOX_NAME}` | 此 `name` 您要重設之沙箱的屬性。 |
| `ignoreWarnings` | 選用參數可讓您略過驗證檢查，並強制重設用於雙向區段共用的生產沙箱，與 [!DNL Audience Manager] 或 [!DNL Audience Core Service]. 此參數無法套用至預設的生產沙箱。 |

**要求**

下列請求會重設名為「acme」的生產沙箱。

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme?ignoreWarnings=true \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json'
  -d '{
    "action": "reset"
  }'
```

**回應**

成功的回應會傳回更新沙箱的詳細資訊，顯示其 `state` 為「正在重設」。

```json
{
    "id": "d8184350-dbf5-11e9-875f-6bf1873fec16",
    "name": "acme",
    "title": "Acme Business Group prod",
    "state": "resetting",
    "type": "production",
    "region": "VA7"
}
```

## 刪除沙箱 {#delete}

>[!IMPORTANT]
>
>無法刪除預設的生產沙箱。

您可以提出DELETE要求(包括沙箱的 `name` 在請求路徑中。

>[!NOTE]
>
>讓此API呼叫會更新沙箱的 `status` 屬性「已刪除」，並停用它。 GET請求刪除後，仍可擷取沙箱的詳細資料。

**API格式**

```http
DELETE /sandboxes/{SANDBOX_NAME}
```

| 參數 | 說明 |
| --- | --- |
| `{SANDBOX_NAME}` | 此 `name` 刪除的沙箱。 |
| `validationOnly` | 此選用參數可讓您對沙箱刪除作業執行預檢檢查，而無須提出實際請求。 將此參數設為 `validationOnly=true` 來檢查您要重設的沙箱是否包含任何Adobe Analytics、Adobe Audience Manager或區段共用資料。 |
| `ignoreWarnings` | 此選用參數可讓您略過驗證檢查，並強制刪除使用者建立的生產沙箱，以用於雙向區段共用，與 [!DNL Audience Manager] 或 [!DNL Audience Core Service]. 此參數無法套用至預設的生產沙箱。 |

**要求**

下列請求會刪除名為「acme」的生產沙箱。

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme?ignoreWarnings=true \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**回應**

成功的回應會傳回沙箱的更新詳細資料，顯示其 `state` 為「已刪除」。

```json
{
    "name": "acme",
    "title": "Acme Business Group prod",
    "state": "deleted",
    "type": "development",
    "region": "VA7"
}
```
