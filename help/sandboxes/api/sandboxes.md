---
keywords: Experience Platform；首頁；熱門主題；沙盒開發人員指南
solution: Experience Platform
title: 沙盒管理API終結點
description: 沙盒API中的/sandboxes端點允許您以寫程式方式管理Adobe Experience Platform的沙盒。
exl-id: 0ff653b4-3e31-4ea5-a22e-07e18795f73e
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1488'
ht-degree: 3%

---

# 沙盒管理終結點

Adobe Experience Platform的沙箱提供獨立的開發環境，使您能夠test功能、運行實驗和進行定制配置，而不會影響您的生產環境。 的 `/sandboxes` 端點 [!DNL Sandbox] API允許您以寫程式方式管理平台中的沙箱。

## 快速入門

本指南中使用的API終結點是 [[!DNL Sandbox] API](https://www.adobe.io/experience-platform-apis/references/sandbox)。 在繼續之前，請查看 [入門指南](./getting-started.md) 有關相關文檔的連結、閱讀本文檔中示例API調用的指南，以及有關成功調用任何Experience PlatformAPI所需標頭的重要資訊。

## 檢索沙箱清單 {#list}

通過向組織發出GET請求，您可以列出屬於您的組織（活動或其他）的所有沙箱 `/sandboxes` 端點。

**API格式**

```http
GET /sandboxes?{QUERY_PARAMS}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{QUERY_PARAMS}` | 用於篩選結果的可選查詢參數。 請參閱 [查詢參數](./appendix.md#query) 的子菜單。 |

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

成功的響應將返回屬於您組織的沙箱清單，包括詳細資訊，如 `name`。 `title`。 `state`, `type`。

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
| `name` | 沙盒的名稱。 此屬性用於API調用中的查找目的。 |
| `title` | 沙盒的顯示名稱。 |
| `state` | 沙盒的當前處理狀態。 沙盒的狀態可以是下列任何一種： <br/><ul><li>`creating`:沙盒已建立，但系統仍在設定。</li><li>`active`:沙盒已建立並處於活動狀態。</li><li>`failed`:由於錯誤，系統無法設定沙盒並且已禁用。</li><li>`deleted`:已手動禁用沙盒。</li></ul> |
| `type` | 沙盒類型。 當前支援的沙盒類型包括 `development` 和 `production`。 |
| `isDefault` | 一個布爾屬性，用於指示此沙盒是否是組織的預設生產沙盒。 |
| `eTag` | 沙盒的特定版本的標識符。 用於版本控制和快取效率，每次更改沙盒時都會更新此值。 |

## 查找沙盒 {#lookup}

通過發出包含沙盒的GET請求，您可以查找單個沙盒 `name` 請求路徑中的屬性。

**API格式**

```http
GET /sandboxes/{SANDBOX_NAME}
```

| 參數 | 說明 |
| --- | --- |
| `{SANDBOX_NAME}` | 的 `name` 要查找的沙盒的屬性。 |

**要求**

以下請求檢索名為「dev-2」的沙盒。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**回應**

成功的響應返回沙盒的詳細資訊，包括其 `name`。 `title`。 `state`, `type`。

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
| `name` | 沙盒的名稱。 此屬性用於API調用中的查找目的。 |
| `title` | 沙盒的顯示名稱。 |
| `state` | 沙盒的當前處理狀態。 沙盒的狀態可以是下列任何一種： <ul><li>**建立**:沙盒已建立，但系統仍在設定。</li><li>**活動**:沙盒已建立並處於活動狀態。</li><li>**失敗**:由於錯誤，系統無法設定沙盒並且已禁用。</li><li>**已刪除**:已手動禁用沙盒。</li></ul> |
| `type` | 沙盒類型。 當前支援的沙盒類型包括： `development` 和 `production`。 |
| `isDefault` | 指示此沙盒是否是組織的預設沙盒的布爾屬性。 通常，這是生產沙箱。 |
| `eTag` | 沙盒的特定版本的標識符。 用於版本控制和快取效率，每次更改沙盒時都會更新此值。 |

## 建立沙盒 {#create}

>[!NOTE]
>
>建立新沙盒時，必須先將新沙盒添加到產品配置檔案中 [Adobe Admin Console](https://adminconsole.adobe.com/) 才能開始使用新沙盒。 請參閱 [管理產品配置檔案的權限](../../access-control/ui/permissions.md) 有關如何將沙盒設定到產品配置檔案的資訊。

您可以通過向以下站點發出POST請求來建立新的開發或生產沙箱 `/sandboxes` 端點。

### 建立開發沙盒

要建立開發沙盒，必須提供 `type` 值為 `development` 在請求負載中。

**API格式**

```http
POST /sandboxes
```

**要求**

以下請求將建立一個名為「acme-dev」的新開發沙箱。

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
| `name` | 將用於在將來請求中訪問沙盒的標識符。 此值必須唯一，最佳做法是使其盡可能具有描述性。 此值不能包含任何空格或特殊字元。 |
| `title` | 用於在平台用戶介面中顯示目的的可讀名稱。 |
| `type` | 要建立的沙盒類型。 對於非生產沙箱，此值必須為 `development`。 |

**回應**

成功的響應將返回新建立的沙盒的詳細資訊，並顯示其 `state` 是「建立」。

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
>沙箱需要大約30秒才能由系統配置，之後系統會設定沙箱 `state` 將變為「活動」或「失敗」。

### 建立生產沙盒

要建立生產沙盒，必須提供 `type` 值為 `production` 在請求負載中。

**API格式**

```http
POST /sandboxes
```

**要求**

以下請求將建立一個名為「acme」的新生產沙箱。

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
| `name` | 將用於在將來請求中訪問沙盒的標識符。 此值必須唯一，最佳做法是使其盡可能具有描述性。 此值不能包含任何空格或特殊字元。 |
| `title` | 用於在平台用戶介面中顯示目的的可讀名稱。 |
| `type` | 要建立的沙盒類型。 對於生產沙箱，此值必須是 `production`。 |

**回應**

成功的響應將返回新建立的沙盒的詳細資訊，並顯示其 `state` 是「建立」。

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
>沙箱需要大約30秒才能由系統配置，之後系統會設定沙箱 `state` 將變為「活動」或「失敗」。

## 更新沙盒 {#put}

您可以通過發出包含沙盒的PATCH請求來更新沙盒中的一個或多個欄位 `name` 在請求路徑和請求負載中要更新的屬性中。

>[!NOTE]
>
>當前僅沙盒 `title` 可以更新屬性。

**API格式**

```http
PATCH /sandboxes/{SANDBOX_NAME}
```

| 參數 | 說明 |
| --- | --- |
| `{SANDBOX_NAME}` | 的 `name` 要更新的沙盒的屬性。 |

**要求**

以下請求更新 `title` 名為&quot;acme&quot;的沙盒的屬性。

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

成功的響應返回HTTP狀態200(OK)以及新更新沙盒的詳細資訊。

```json
{
    "name": "acme",
    "title": "Acme Business Group prod",
    "state": "active",
    "type": "production",
    "region": "VA7"
}
```

## 重置沙盒 {#reset}

沙箱具有「工廠重置」功能，該功能從沙箱中刪除所有非預設資源。 通過發出包含沙盒的PUT請求，可以重置沙盒 `name` 的子菜單。

**API格式**

```http
PUT /sandboxes/{SANDBOX_NAME}
```

| 參數 | 說明 |
| --- | --- |
| `{SANDBOX_NAME}` | 的 `name` 要重置的沙盒的屬性。 |
| `validationOnly` | 允許您對沙盒重置操作執行飛行前檢查而不發出實際請求的可選參數。 將此參數設定為 `validationOnly=true` 檢查您要重置的沙盒是否包含任何Adobe Analytics、Adobe Audience Manager或段共用資料。 |

**要求**

以下請求重置名為「acme-dev」的沙箱。

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
| `action` | 為了重置沙盒，必須在請求負載中提供此參數，其值必須為「reset」。 |

**回應**

>[!NOTE]
>
>重置沙盒後，系統需要大約30秒才能配置沙盒。

成功的響應將返回更新沙盒的詳細資訊，顯示其 `state` 是「重置」。

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

如果Adobe Analytics也在使用預設生產沙箱和用戶建立的任何生產沙箱中承載的標識圖形，則無法重置 [跨設備分析(CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html) 功能，或者，如果其中承載的標識圖也由Adobe Audience Manager用於 [基於人員的目的地(PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html) 的子菜單。

以下是可能阻止重置沙盒的異常清單：

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

您可以繼續重置用於雙向段共用的生產沙盒 [!DNL Audience Manager] 或 [!DNL Audience Core Service] 通過添加 `ignoreWarnings` 參數。

**API格式**

```http
PUT /sandboxes/{SANDBOX_NAME}?ignoreWarnings=true
```

| 參數 | 說明 |
| --- | --- |
| `{SANDBOX_NAME}` | 的 `name` 要重置的沙盒的屬性。 |
| `ignoreWarnings` | 允許您跳過驗證檢查並強制重置用於雙向段共用的生產沙盒的可選參數 [!DNL Audience Manager] 或 [!DNL Audience Core Service]。 此參數不能應用於預設的生產沙盒。 |

**要求**

以下請求重置名為「acme」的生產沙箱。

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

成功的響應將返回更新沙盒的詳細資訊，顯示其 `state` 是「重置」。

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

## 刪除沙盒 {#delete}

>[!IMPORTANT]
>
>無法刪除預設生產沙盒。

通過發出包含沙盒的DELETE請求，可以刪除沙盒 `name` 的子菜單。

>[!NOTE]
>
>使此API調用更新沙盒 `status` 「已刪除」並取消激活它。 GET請求在刪除沙盒詳細資訊後仍可檢索沙盒的詳細資訊。

**API格式**

```http
DELETE /sandboxes/{SANDBOX_NAME}
```

| 參數 | 說明 |
| --- | --- |
| `{SANDBOX_NAME}` | 的 `name` 您想要刪除的沙盒。 |
| `validationOnly` | 允許您對沙盒刪除操作執行印前檢查而不發出實際請求的可選參數。 將此參數設定為 `validationOnly=true` 檢查您要重置的沙盒是否包含任何Adobe Analytics、Adobe Audience Manager或段共用資料。 |
| `ignoreWarnings` | 允許您跳過驗證檢查並強制刪除用戶建立的生產沙盒的可選參數，該沙盒用於與 [!DNL Audience Manager] 或 [!DNL Audience Core Service]。 此參數不能應用於預設的生產沙盒。 |

**要求**

以下請求刪除名為「acme」的生產沙箱。

```shell
curl -X DELETE \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/acme?ignoreWarnings=true \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**回應**

成功的響應返回沙盒的更新詳細資訊，顯示其 `state` 為「已刪除」。

```json
{
    "name": "acme",
    "title": "Acme Business Group prod",
    "state": "deleted",
    "type": "development",
    "region": "VA7"
}
```
