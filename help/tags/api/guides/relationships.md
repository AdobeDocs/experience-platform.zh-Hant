---
title: Reactor API中的關係
description: 了解如何在Reactor API中建立資源關係，包括每個資源的關係需求。
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 10%

---

# Reactor API中的關係

Reactor API中的資源通常彼此相關。 本檔案概略說明如何在API中建立資源關係，以及每種資源類型的關係需求。

根據相關資源的類型，需要一些關係。 必要的關係表示沒有該關係父資源不能存在。 所有其他關係均為可選關係。

無論關係是必需的還是可選的，在建立相關資源時系統都會自動建立關係，或者必須手動建立關係。 在手動建立關係的情況下，有兩種可能的方法取決於相關資源：

* [由裝載建立](#payload)
* [依URL建立](#url) （僅適用於程式庫）

有關每種資源類型的相容關係清單，以及在適用情況下建立這些關係所需的方法，請參閱[relationship requirements](#requirements)上的部分。

## 依裝載建立關係 {#payload}

在最初建立資源時，必須手動建立某些關係。 若要完成此操作，您必須先建立上層資源時，在請求裝載中提供`relationship`物件。 這些關係的範例包括：

* [使用必要的擴](../endpoints/data-elements.md#create) 充功能建立資料元素
* [建立具](../endpoints/environments.md#create) 有所需主機關係的環境

**API格式**

```http
POST /properties/{PROPERTY_ID}/{RESOURCE_TYPE}
```

| 參數 | 說明 |
| --- | --- |
| `{PROPERTY_ID}` | 資源所屬屬性的ID。 |
| `{RESOURCE_TYPE}` | 要建立的資源類型。 |

{style=&quot;table-layout:auto&quot;}

**要求**

以下請求建立新的`rule_component`，與`rules`和`extension`建立關係。

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PRf606dbddfbdc44f580fc6f342b5ff9be/rule_components \
  -H 'Authorization: Bearer [TOKEN]' \
  -H 'x-api-key: [KEY]' \
  -H 'x-gw-ims-org-id: [ORG_ID]' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json' \
  -d '{
        "data": {
          "attributes": {
            "delegate_descriptor_id": "kessel-test::events::click",
            "name": "My Example Click Event",
            "settings": "{\"elementSelector\":\".accordion\",\"bubbleFireIfChildFired\":true}"
          },
          "relationships": {
            "extension": {
              "data": {
                "id": "EXa2865f4d14204fa094f247406424371b",
                "type": "extensions"
              }
            },
            "rules": {
              "data": [
                {
                  "id": "RLd53598e3f1884e63bbc8e9c95e463dcf",
                  "type": "rules"
                }
              ]
            }
          },
          "type": "rule_components"
        }
      }'
```

| 屬性 | 說明 |
| --- | --- |
| `relationships` | 依裝載建立關係時必須提供的物件。 此對象中的每個鍵表示特定的關係類型。 在上例中，建立了`extension`和`rules`關係，這些關係對`rule_components`是特別的。 有關不同資源的相容關係類型的詳細資訊，請參閱[關係需求上按資源](#relationship-requirements-by-resource)的一節。 |
| `data` | `relationship`對象下提供的每個關係類型都必須包含`data`屬性，該屬性引用正在建立關係的資源的`id`和`type`。 通過將`data`屬性格式化為對象陣列，每個對象都包含適用資源的`id`和`type`，您可以建立與多個相同類型的資源的關係。 |
| `id` | 資源的唯一ID。 每個`id`都必須與同級`type`屬性一起，以指示有關的資源類型。 |
| `type` | 由同級`id`欄位引用的資源類型。 接受的值包括`data_elements`、`rules`、`extensions`和`environments`。 |

{style=&quot;table-layout:auto&quot;}

## 按URL建立關係 {#url}

與其他資源不同，程式庫會透過其自己的專用`/relationship`端點來建立關係。 例如：

* [新增擴充功能、資料元素和規則至程式庫](../endpoints/libraries.md#add-resources)
* [指派程式庫至環境](../endpoints/libraries.md#environment)

**API格式**

```http
POST /properties/{PROPERTY_ID}/libraries/{LIBRARY_ID}/relationships/{RESOURCE_TYPE}
```

| 參數 | 說明 |
| --- | --- |
| `{PROPERTY_ID}` | 程式庫所屬屬性的ID。 |
| `{LIBRARY_ID}` | 您要建立關係的程式庫ID。 |
| `{RESOURCE_TYPE}` | 關係所定位的資源類型。 可用值包括`environment`、`data_elements`、`extensions`和`rules`。 |

**要求**

以下請求使用`/relationships/environment`端點讓程式庫建立與環境的關係。

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PRf606dbddfbdc44f580fc6f342b5ff9be/libraries/LB10c1fd171cd347f19fcb8659a8d679ef/relationships/environment \
  -H 'Authorization: Bearer [TOKEN]' \
  -H 'x-api-key: [KEY]' \
  -H 'x-gw-ims-org-id: [ORG_ID]' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json' \
  -d '{
        "data": {
          "id": "ENf395a477d2b24ad696d65b901055b9dc",
          "type": "environments",
        }
      }'
```

| 屬性 | 說明 |
| --- | --- |
| `data` | 為關係引用目標資源的`id`和`type`的對象。 如果要與同一類型的多個資源建立關係（如`extensions`和`rules`）,`data`屬性必須格式化為對象陣列，每個對象都包含適用資源的`id`和`type`。 |
| `id` | 資源的唯一ID。 每個`id`都必須與同級`type`屬性一起，以指示有關的資源類型。 |
| `type` | 由同級`id`欄位引用的資源類型。 接受的值包括`data_elements`、`rules`、`extensions`和`environments`。 |

{style=&quot;table-layout:auto&quot;}

## 按資源分列的關係需求 {#requirements}

下表概述了每種資源類型的可用關係（無論這些關係是否需要），以及在適用時手動建立關係的接受方法。

>[!NOTE]
>
>如果關係未列為由裝載或URL建立，則系統會自動指派它。

### 稽核事件

| 關係 | 必填 | 由裝載建立 | 按URL建立 |
| :--- | :---: | :---: | :---: |
| `property` | ✓ |  |  |
| `entity` | ✓ |  |  |

{style=&quot;table-layout:auto&quot;}

### 組建

| 關係 | 必填 | 由裝載建立 | 按URL建立 |
| :--- | :---: | :---: | :---: |
| `data_elements` |  |  |  |
| `extensions` |  |  |  |
| `rules` |  |  |  |
| `environment` | ✓ |  |  |
| `library` | ✓ |  |  |
| `property` | ✓ |  |  |

{style=&quot;table-layout:auto&quot;}

### 回呼

| 關係 | 必填 | 由裝載建立 | 按URL建立 |
| :--- | :---: | :---: | :---: |
| `property` | ✓ |  |  |

{style=&quot;table-layout:auto&quot;}

### 公司

| 關係 | 必填 | 由裝載建立 | 按URL建立 |
| :--- | :---: | :---: | :---: |
| `properties` |  |  |  |

{style=&quot;table-layout:auto&quot;}

### 資料元素

| 關係 | 必填 | 由裝載建立 | 按URL建立 |
| :--- | :---: | :---: | :---: |
| `libraries` |  |  |  |
| `revisions` | ✓ |  |  |
| `notes` |  |  |  |
| `property` | ✓ |  |  |
| `origin` | ✓ |  |  |
| `extension` | ✓ | ✓ |  |
| `updated_with_extension` | ✓ |  |  |
| `updated_with_extension_package` | ✓ |  |  |

{style=&quot;table-layout:auto&quot;}

### 環境

| 關係 | 必填 | 由裝載建立 | 按URL建立 |
| :--- | :---: | :---: | :---: |
| `library` |  |  |  |
| `builds` |  |  |  |
| `host` | ✓ | ✓ |  |
| `property` | ✓ |  |  |

{style=&quot;table-layout:auto&quot;}

### 擴充功能

| 關係 | 必填 | 由裝載建立 | 按URL建立 |
| :--- | :---: | :---: | :---: |
| `libraries` |  |  |  |
| `revisions` | ✓ |  |  |
| `notes` |  |  |  |
| `property` | ✓ |  |  |
| `origin` | ✓ |  |  |
| `extension_package` | ✓ | ✓ |  |
| `updated_with_extension_package` | ✓ |  |  |

{style=&quot;table-layout:auto&quot;}

### 主機

| 關係 | 必填 | 由裝載建立 | 按URL建立 |
| :--- | :---: | :---: | :---: |
| `property` | ✓ |  |  |

{style=&quot;table-layout:auto&quot;}

### 程式庫

| 關係 | 必填 | 由裝載建立 | 按URL建立 |
| :--- | :---: | :---: | :---: |
| `builds` |  |  |  |
| `environment` |  |  | ✓ |
| `data_elements` |  |  | ✓ |
| `extensions` |  |  | ✓ |
| `rules` |  |  | ✓ |
| `notes` |  |  |  |
| `upstream_library` | ✓ |  |  |
| `property` | ✓ |  |  |
| `last_build` |  |  |  |

{style=&quot;table-layout:auto&quot;}

### 附註

| 關係 | 必填 | 由裝載建立 | 按URL建立 |
| :--- | :---: | :---: | :---: |
| `resource` | ✓ |  |  |

{style=&quot;table-layout:auto&quot;}

### 屬性

| 關係 | 必填 | 由裝載建立 | 按URL建立 |
| :--- | :---: | :---: | :---: |
| `company` | ✓ |  |  |
| `callbacks` |  |  |  |
| `environments` |  |  |  |
| `libraries` |  |  |  |
| `data_elements` |  |  |  |
| `extensions` |  |  |  |
| `extensions` |  |  |  |

{style=&quot;table-layout:auto&quot;}

### 規則元件

| 關係 | 必填 | 由裝載建立 | 按URL建立 |
| :--- | :---: | :---: | :---: |
| `updated_with_extensions_package` | ✓ |  |  |
| `updated_with_extension` | ✓ |  |  |
| `extension` | ✓ | ✓ |  |
| `notes` |  |  |  |
| `origin` | ✓ |  |  |
| `property` | ✓ |  |  |
| `rules` | ✓ | ✓ |  |
| `revisions` | ✓ |  |  |

{style=&quot;table-layout:auto&quot;}

### 規則

| 關係 | 必填 | 由裝載建立 | 按URL建立 |
| :--- | :---: | :---: | :---: |
| `libraries` |  |  |  |
| `revisions` | ✓ |  |  |
| `notes` |  |  |  |
| `property` | ✓ |  |  |
| `origin` | ✓ |  |  |
| `rule_components` |  |  |  |
