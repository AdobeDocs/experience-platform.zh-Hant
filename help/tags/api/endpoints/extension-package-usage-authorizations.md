---
title: 擴充功能套件使用授權端點
description: 瞭解如何在Reactor API中呼叫/extension_package_usage授權端點。
source-git-commit: fdf01451527e2fab8eb6e6f9d7b4901a85381450
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 4%

---


# 擴充功能套件使用授權端點

擴充功能套件表示擴充功能[由擴充功能開發人員所編寫。 ](./extensions.md)擴充功能套件會定義可提供給標籤使用者的其他功能。 這些功能可以包括主要模組和共用模組，不過它們最常作為[規則元件](./rule-components.md) （事件、條件和動作）和[資料元素](./data-elements.md)提供。

擴充功能套件屬於開發人員的[公司](./companies.md)。 擴充功能套件的擁有者可授權其他企業使用其私人版本的套件。 每個授權企業都會獲得單一擴充功能套件的使用授權，該套件適用於該套件所有未來和目前的私人版本。

## 快速入門

此指南中使用的端點是[Reactor API](https://www.adobe.io/experience-platform-apis/references/reactor/)的一部分。 在繼續之前，請檢閱[快速入門手冊](../getting-started.md)，以取得有關如何向API驗證的重要資訊。

## 擷取擴充功能套件的擴充功能套件使用授權 {#list}

若要擷取擴充功能套件的使用授權清單，請向下列端點發出GET要求。

**API格式**

```http
GET /extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations
```

| 參數 | 說明 |
| --- | --- |
| `{PROPERTY_ID}` | 您要列出其擴充套件使用授權之屬性的`ID`。 |

{style="table-layout:auto"}

**要求**

```shell
curl -X GET \
  https://reactor.adobe.io/extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**回應**

成功的回應會傳回擴充功能套件清單。

```json
{
  "data": [
    {
      "id": "EA722482c30fe44b54aa6a7317890b3bdb",
      "type": "extension_package_usage_authorizations",
      "attributes": {
        "created_at": "2024-06-05T23:17:35.776Z",
        "updated_at": "2024-06-05T23:17:35.776Z",
        "name": "Acme",
        "platform": "web",
        "owner_org_id": "{ORG_ID}",
        "owner_org_name": "Reactor QE",
        "authorized_org_id": "{ORG_ID}",
        "authorized_org_name": "Acme Inc'",
        "state": "pending_approval",
        "created_by_email": "example@adobe.com",
        "created_by_display_name": "john snow",
        "updated_by_email": "Restricted",
        "updated_by_display_name": "Restricted"
      },
      "relationships": {
        "extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extension_package_usage_authorizations/EA722482c30fe44b54aa6a7317890b3bdb/extension_package"
          },
          "data": {
            "id": "EPecefc8291ae346c3b3887d5b2da533b8",
            "type": "extension_packages"
          }
        }
      },
      "links": {
        "self": "https://reactor.adobe.io/extension_package_usage_authorizations/EA722482c30fe44b54aa6a7317890b3bdb"
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 1
    }
  }
}
```

## 建立擴充功能套件使用授權 {#create}

針對您想要授權的每個組織[擴充功能套件](./extension-packages.md)和`{ORG_ID}`，建立擴充功能套件使用授權。 若要建立新的擴充功能套件使用授權，請向下列端點發出POST請求。

**API格式**

```http
POST /extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations
```

| 參數 | 說明 |
| --- | --- |
| `EXTENSION_PACKAGE_ID` | 您要為其建立授權的延伸套件`ID`。」 |

{style="table-layout:auto"}

**要求**

```shell
curl -X POST \
  https://reactor.adobe.io/extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -d '{
        "data": {
          "attributes": {
            "authorized_org_id": "{ORG_ID}"
          },
          "type": "extension_package_usage_authorizations"
        }
      } 
```

| 屬性 | 說明 |
| --- | --- |
| `attributes.authorized_org_id` | 您要授權的組織`ID`。 |

**回應**

成功的回應會傳回新建立的擴充功能套件使用授權詳細資料。

```json
{
  "data": {
    "id": "EA35d0e731f73645e6972df9fcac101434",
    "type": "extension_package_usage_authorizations",
    "attributes": {
      "created_at": "2024-06-05T23:17:30.308Z",
      "updated_at": "2024-06-05T23:17:30.308Z",
      "name": "Acme",
      "platform": "web",
      "owner_org_id": "{ORG_ID}",
      "owner_org_name": "Reactor QE",
      "authorized_org_id": "{ORG_ID}",
      "authorized_org_name": "Acme Inc'",
      "state": "pending_approval",
      "created_by_email": "example@adobe.com",
      "created_by_display_name": "john snow",
      "updated_by_email": "Restricted",
      "updated_by_display_name": "Restricted"
    },
    "relationships": {
      "extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extension_package_usage_authorizations/EA35d0e731f73645e6972df9fcac101434/extension_package"
        },
        "data": {
          "id": "EP43649cc8856d4f09a7c2a21a4b1e449d",
          "type": "extension_packages"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/extension_package_usage_authorizations/EA35d0e731f73645e6972df9fcac101434"
    }
  }
}
```

>[!NOTE]
>
>在上述範例回應中，授權目前處於`pending_approval`階段。 在使用擴充功能套件之前，組織必須核准授權。 當授權處於未決核准狀態時，組織的使用者可以瀏覽私人擴充功能套件，但他們無法安裝該套件，且無法在擴充功能目錄中找到。

## 擷取擴充功能套件使用授權清單 {#list_authorizations}

您可以發出GET要求，擷取擴充功能套件使用授權的清單。

**API格式**

```http
GET /extension_package_usage_authorizations
```

**要求**

```shell
curl -X GET \
  https://reactor.adobe.io/extension_package_usage_authorizations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**回應**

成功的回應會傳回擴充功能套件清單。

```json
{
  "data": [
    {
      "id": "EA35d0e731f73645e6972df9fcac101434",
      "type": "extension_package_usage_authorizations",
      "attributes": {
        "created_at": "2024-06-05T23:17:30.308Z",
        "updated_at": "2024-06-05T23:17:30.308Z",
        "name": "Acme",
        "platform": "web",
        "owner_org_id": "{ORG_ID}",
        "owner_org_name": "Reactor QE",
        "authorized_org_id": "{ORG_ID}",
        "authorized_org_name": "Acme Inc'",
        "state": "pending_approval",
        "created_by_email": "Restricted",
        "created_by_display_name": "Restricted",
        "updated_by_email": "example@adobe.com",
        "updated_by_display_name": "john snow"
      },
      "relationships": {
        "extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extension_package_usage_authorizations/EA35d0e731f73645e6972df9fcac101434/extension_package"
          },
          "data": null
        }
      },
      "links": {
        "self": "https://reactor.adobe.io/extension_package_usage_authorizations/EA35d0e731f73645e6972df9fcac101434"
      }
    }
  ],
  "links": {
    "self": "https://reactor.adobe.io/extension_package_usage_authorizations?page%5Bnumber%5D=1&page%5Bsize%5D=25",
    "next": "https://reactor.adobe.io/extension_package_usage_authorizations?page%5Bnumber%5D=2&page%5Bsize%5D=25",
    "last": "https://reactor.adobe.io/extension_package_usage_authorizations?page%5Bnumber%5D=3&page%5Bsize%5D=25"
  },
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": 2,
      "prev_page": null,
      "total_pages": 3,
      "total_count": 57
    }
  }
}
```

## 刪除擴充功能套件使用授權 {#delete}

若要刪除擴充套件使用授權，請在DELETE要求的路徑中包含其`ID`。 這可防止授權組織檢視目錄中擴充功能套件的私人版本，以及在其屬性上安裝該套件。

>[!NOTE]
>
>先前安裝的任何私人版本將可繼續如預期運作。

**API格式**

```http
DELETE /extension_package_usage_authorizations/{ID}
```

| 參數 | 說明 |
| --- | --- |
| `ID` | 您要刪除之擴充套件使用授權的`ID`。 |

{style="table-layout:auto"}

**要求**

```shell
curl -X DELETE \
  https://reactor.adobe.io/extension_package_usage_authorizations/{ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**回應**

成功的回應會傳回HTTP狀態204 （無內容），但沒有回應內文。 這表示擴充功能已刪除。

## 更新擴充功能套件使用授權 {#update}

若要核准或拒絕擴充套件使用授權，請在PATCH要求的路徑中包含其`ID`。

>[!NOTE]
>
>若要核准或拒絕貴公司的擴充功能套件使用授權，您必須擁有`manage_properties`許可權。

**API格式**

```http
PATCH /extension_package_usage_authorizations/{ID}
```

| 參數 | 說明 |
| --- | --- |
| `ID` | 您要刪除之擴充套件使用授權的`ID`。 |

{style="table-layout:auto"}

**要求**

```shell
curl -X PATCH \
  https://reactor.adobe.io/extension_package_usage_authorizations/{ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -d '{
        "data": {
          "attributes": {
            "state": "approved"
          },
          "type": "extension_package_usage_authorizations",
          "id": "EA86f54b48dd7042a68686508e03be8ba9"
        }
      } 
```

| 屬性 | 說明 |
| --- | --- |
| `attributes` | 您想要修訂的屬性。 針對擴充功能套件使用授權，您可以修訂其`state`。 |

**回應**

成功的回應會傳回修訂後擴充功能套件使用授權的詳細資料。

```json
{
  "data": {
    "id": "EA86f54b48dd7042a68686508e03be8ba9",
    "type": "extension_package_usage_authorizations",
    "attributes": {
      "created_at": "2024-06-05T23:17:59.480Z",
      "updated_at": "2024-06-05T23:18:00.115Z",
      "name": "Acme",
      "platform": "web",
      "owner_org_id": "{ORG_ID}",
      "owner_org_name": "Reactor QE",
      "authorized_org_id": "{ORG_ID}",
      "authorized_org_name": "Acme Inc'",
      "state": "approved",
      "created_by_email": "Restricted",
      "created_by_display_name": "Restricted",
      "updated_by_email": "example@adobe.com",
      "updated_by_display_name": "john snow"
    },
    "relationships": {
      "extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extension_package_usage_authorizations/EA86f54b48dd7042a68686508e03be8ba9/extension_package"
        },
        "data": {
          "id": "EPb91d54cad9f749dba4e5566459f84c9c",
          "type": "extension_packages"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/extension_package_usage_authorizations/EA86f54b48dd7042a68686508e03be8ba9"
    }
  }
}
```

>[!NOTE]
>
>在授權核准後，您的組織可以在您的屬性上安裝擴充功能套件。

## 擷取擴充功能套件的資料，以取得擴充功能套件使用授權 {#retrieve_data}

您可以提出GET要求，擷取擴充功能套件資料，以取得擴充功能套件使用授權。

**API格式**

```http
GET /extension_package_usage_authorizations/{ID}/extension_package
```

| 參數 | 說明 |
| --- | --- |
| `ID` | 您要擷取的擴充套件使用授權的`ID`。 |

{style="table-layout:auto"}

**要求**

```shell
curl -X GET \
  https://reactor.adobe.io/extension_package_usage_authorizations/{ID}/extension_package \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**回應**

成功的回應會傳回擴充功能套件授權的資料。

```json
{
  "data": {
    "id": "EP45ae063fd75c4c22936d3d456c858cfa",
    "type": "extension_packages",
    "attributes": {
      "actions": [],
      "author": {
        "url": "http://adobe.com",
        "name": "Acme",
        "email": "acme@adobe.com"
      },
      "availability": "private",
      "cdn_path": "https://assets.adobedtm.com/staging/extensions/EP45ae063fd75c4c22936d3d456c858cfa",
      "conditions": [],
      "configuration": null,
      "created_at": "2024-06-05T23:17:48.607Z",
      "data_elements": [],
      "description": "Provides nothing.",
      "discontinued": false,
      "display_name": "Acme Template Test",
      "ecma_version": null,
      "events": [],
      "exchange_url": null,
      "hosted_lib_files": null,
      "icon_path": "resources/icons/core.svg",
      "main": "null",
      "name": "Acme",
      "owner_org_id": "{ORG_ID}",
      "resources": null,
      "shared_modules": null,
      "status": "succeeded",
      "platform": "web",
      "updated_at": "2024-06-05T23:17:53.806Z",
      "version": "1.0.0",
      "view_base_path": "dist/",
      "created_by_email": "example@adobe.com",
      "created_by_display_name": "john snow",
      "updated_by_email": "example@adobe.com",
      "updated_by_display_name": "john snow"
    },
    "relationships": {
      "extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extension_packages/EP45ae063fd75c4c22936d3d456c858cfa/extension_package_usage_authorizations"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/extension_packages/EP45ae063fd75c4c22936d3d456c858cfa"
    }
  }
}
```
