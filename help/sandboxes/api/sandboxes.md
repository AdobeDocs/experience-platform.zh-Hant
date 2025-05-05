---
keywords: Experience Platform；首頁；熱門主題；沙箱開發人員指南
solution: Experience Platform
title: 沙箱管理API端點
description: 沙箱API中的/sandboxes端點可讓您以程式設計方式管理Adobe Experience Platform中的沙箱。
role: Developer
exl-id: 0ff653b4-3e31-4ea5-a22e-07e18795f73e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1477'
ht-degree: 3%

---

# 沙箱管理端點

Adobe Experience Platform中的沙箱提供獨立的開發環境，可讓您測試功能、執行實驗及進行自訂設定，而不會影響您的生產環境。 [!DNL Sandbox] API中的`/sandboxes`端點可讓您以程式設計方式管理Experience Platform中的沙箱。

## 快速入門

本指南中使用的API端點是[[!DNL Sandbox] API](https://www.adobe.io/experience-platform-apis/references/sandbox)的一部分。 在繼續之前，請先檢閱[快速入門手冊](./getting-started.md)，以取得相關檔案的連結、閱讀本檔案中範例API呼叫的手冊，以及有關成功呼叫任何Experience Platform API所需必要標題的重要資訊。

## 擷取沙箱清單 {#list}

您可以透過向`/sandboxes`端點發出GET請求，列出屬於您組織的所有沙箱（作用中或其他方式）。

**API格式**

```http
GET /sandboxes?{QUERY_PARAMS}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{QUERY_PARAMS}` | 篩選結果的選用查詢引數。 如需詳細資訊，請參閱[查詢引數](./appendix.md#query)的相關章節。 |

**要求**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes?&limit=4&offset=1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**回應**

成功的回應會傳回屬於您組織的沙箱清單，包括`name`、`title`、`state`和`type`等詳細資訊。

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
| `name` | 沙箱的名稱。 此屬性用於API呼叫中的查閱用途。 |
| `title` | 沙箱的顯示名稱。 |
| `state` | 沙箱的目前處理狀態。 沙箱的狀態可以是下列任一專案： <br/><ul><li>`creating`：沙箱已建立，但系統仍在布建中。</li><li>`active`：沙箱已建立且作用中。</li><li>`failed`：由於發生錯誤，沙箱無法由系統布建，因此已停用。</li><li>`deleted`：沙箱已手動停用。</li></ul> |
| `type` | 沙箱型別。 目前支援的沙箱型別包括`development`和`production`。 |
| `isDefault` | 表示此沙箱是否為組織的預設生產沙箱的布林值屬性。 |
| `eTag` | 特定版本沙箱的識別碼。 用於版本控制和快取效率，每次對沙箱進行變更時都會更新此值。 |

## 查詢沙箱 {#lookup}

您可以發出GET請求，在請求路徑中包含沙箱的`name`屬性，以查詢個別沙箱。

**API格式**

```http
GET /sandboxes/{SANDBOX_NAME}
```

| 參數 | 說明 |
| --- | --- |
| `{SANDBOX_NAME}` | 您要查詢之沙箱的`name`屬性。 |

**要求**

以下請求會擷取名為「dev-2」的沙箱。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**回應**

成功的回應傳回沙箱的詳細資料，包括其`name`、`title`、`state`和`type`。

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
| `name` | 沙箱的名稱。 此屬性用於API呼叫中的查閱用途。 |
| `title` | 沙箱的顯示名稱。 |
| `state` | 沙箱的目前處理狀態。 沙箱的狀態可以是下列任一專案： <ul><li>**正在建立**：沙箱已建立，但系統仍在布建中。</li><li>**使用中**：沙箱已建立且使用中。</li><li>**失敗**：由於發生錯誤，沙箱無法由系統布建，因此已停用。</li><li>**已刪除**：沙箱已手動停用。</li></ul> |
| `type` | 沙箱型別。 目前支援的沙箱型別包括： `development`和`production`。 |
| `isDefault` | 表示此沙箱是否為組織預設沙箱的布林值屬性。 通常這是生產沙箱。 |
| `eTag` | 特定版本沙箱的識別碼。 用於版本控制和快取效率，每次對沙箱進行變更時都會更新此值。 |

## 建立沙箱 {#create}

>[!NOTE]
>
>建立新沙箱時，您必須先在[Adobe Admin Console](https://adminconsole.adobe.com/)中將該新沙箱新增到您的產品設定檔中，然後才能開始使用新沙箱。 如需有關如何將沙箱布建至產品設定檔的資訊，請參閱有關[管理產品設定檔的許可權](../../access-control/ui/permissions.md)的檔案。

您可以對`/sandboxes`端點發出POST要求，以建立新的開發或生產沙箱。

### 建立開發沙箱

若要建立開發沙箱，您必須在要求裝載中提供值為`development`的`type`屬性。

**API格式**

```http
POST /sandboxes
```

**要求**

以下請求會建立名為「acme-dev」的新開發沙箱。

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
| `name` | 將在未來請求中用於存取沙箱的識別碼。 此值必須是唯一的，最佳做法是使其儘可能具描述性。 此值不能包含任何空格或特殊字元。 |
| `title` | 在Experience Platform使用者介面中用於顯示用途的人類可讀名稱。 |
| `type` | 要建立的沙箱型別。 對於非生產沙箱，此值必須是`development`。 |

**回應**

成功的回應會傳回新建立的沙箱的詳細資料，顯示其`state`正在「建立」。

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
>系統布建沙箱約需30秒鐘，之後的`state`會變成「作用中」或「失敗」。

### 建立生產沙箱

若要建立生產沙箱，您必須在要求裝載中提供值為`production`的`type`屬性。

**API格式**

```http
POST /sandboxes
```

**要求**

以下請求會建立名為「acme」的新生產沙箱。

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
| `name` | 將在未來請求中用於存取沙箱的識別碼。 此值必須是唯一的，最佳做法是使其儘可能具描述性。 此值不能包含任何空格或特殊字元。 |
| `title` | 在Experience Platform使用者介面中用於顯示用途的人類可讀名稱。 |
| `type` | 要建立的沙箱型別。 對於生產沙箱，此值必須是`production`。 |

**回應**

成功的回應會傳回新建立的沙箱的詳細資料，顯示其`state`正在「建立」。

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
>系統布建沙箱約需30秒鐘，之後的`state`會變成「作用中」或「失敗」。

## 更新沙箱 {#put}

您可以發出PATCH請求，在請求路徑中包含沙箱的`name`，並在請求承載中包含要更新的屬性，以更新沙箱中的一個或多個欄位。

>[!NOTE]
>
>目前只能更新沙箱的`title`屬性。

**API格式**

```http
PATCH /sandboxes/{SANDBOX_NAME}
```

| 參數 | 說明 |
| --- | --- |
| `{SANDBOX_NAME}` | 您要更新的沙箱的`name`屬性。 |

**要求**

以下請求會更新名為「acme」的沙箱的`title`屬性。

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

成功的回應會傳回HTTP狀態200 （確定）以及新更新沙箱的詳細資訊。

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

沙箱具有「原廠重設」功能，可從沙箱中刪除所有非預設資源。 您可以發出PUT請求，在請求路徑中包含沙箱的`name`，以重設沙箱。

**API格式**

```http
PUT /sandboxes/{SANDBOX_NAME}
```

| 參數 | 說明 |
| --- | --- |
| `{SANDBOX_NAME}` | 您要重設之沙箱的`name`屬性。 |
| `validationOnly` | 此選用引數可讓您對沙箱重設作業執行預檢作業，而不需提出實際請求。 將此引數設為`validationOnly=true`，以檢查您即將重設的沙箱是否包含任何Adobe Analytics、Adobe Audience Manager或區段共用資料。 |

**要求**

以下請求會重設名為「acme-dev」的沙箱。

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
| `action` | 您必須在請求承載中提供此引數，且引數值為「reset」，才能重設沙箱。 |

**回應**

>[!NOTE]
>
>沙箱重設後，系統布建約需要30秒。

成功的回應會傳回更新沙箱的詳細資料，顯示其`state`正在「重設」。

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

如果其中代管的身分圖表也被Adobe Analytics用於[跨裝置分析(CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html?lang=zh-Hant)功能，或其中代管的身分圖表也被Adobe Audience Manager用於[以人為基礎的目的地(PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=zh-Hant)功能，則無法重設預設生產沙箱和任何使用者建立的生產沙箱。

以下是可防止沙箱重設的可能例外清單：

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

您可以繼續重設用來與[!DNL Audience Manager]或[!DNL Audience Core Service]進行雙向區段共用的生產沙箱，方法是在您的要求中新增`ignoreWarnings`引數。

**API格式**

```http
PUT /sandboxes/{SANDBOX_NAME}?ignoreWarnings=true
```

| 參數 | 說明 |
| --- | --- |
| `{SANDBOX_NAME}` | 您要重設之沙箱的`name`屬性。 |
| `ignoreWarnings` | 選擇性引數可讓您略過驗證檢查，並強制重設用來與[!DNL Audience Manager]或[!DNL Audience Core Service]進行雙向區段共用的生產沙箱。 此引數無法套用至預設的生產沙箱。 |

**要求**

以下請求會重設名為「acme」的生產沙箱。

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

成功的回應會傳回更新沙箱的詳細資料，顯示其`state`正在「重設」。

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

您可以發出DELETE請求，在請求路徑中包含沙箱的`name`，藉此刪除沙箱。

>[!NOTE]
>
>發出此API呼叫會將沙箱的`status`屬性更新為「已刪除」並將其停用。 刪除沙箱後，GET請求仍可擷取沙箱的詳細資料。

**API格式**

```http
DELETE /sandboxes/{SANDBOX_NAME}
```

| 參數 | 說明 |
| --- | --- |
| `{SANDBOX_NAME}` | 您要刪除的沙箱的`name`。 |
| `validationOnly` | 此選用引數可讓您對沙箱刪除操作執行預先檢查而不會提出實際請求。 將此引數設為`validationOnly=true`，以檢查您即將重設的沙箱是否包含任何Adobe Analytics、Adobe Audience Manager或區段共用資料。 |
| `ignoreWarnings` | 此選用引數可讓您略過驗證檢查，並強制刪除使用者建立的生產沙箱（用於與[!DNL Audience Manager]或[!DNL Audience Core Service]的雙向區段共用）。 此引數無法套用至預設的生產沙箱。 |

**要求**

以下請求會刪除名為「acme」的生產沙箱。

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme?ignoreWarnings=true \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**回應**

成功的回應會傳回沙箱的更新詳細資料，顯示其`state`已「刪除」。

```json
{
    "name": "acme",
    "title": "Acme Business Group prod",
    "state": "deleted",
    "type": "development",
    "region": "VA7"
}
```
