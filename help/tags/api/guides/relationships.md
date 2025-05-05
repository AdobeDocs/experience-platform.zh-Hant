---
title: Reactor API中的關係
description: 瞭解如何在Reactor API中建立資源關係，包括每個資源的關係需求。
exl-id: 23976978-a639-4eef-91b6-380a29ec1c14
source-git-commit: 7e4bc716e61b33563e0cb8059cb9f1332af7fd36
workflow-type: tm+mt
source-wordcount: '809'
ht-degree: 6%

---

# Reactor API中的關係

Reactor API中的資源通常彼此相關。 本檔案概述如何在API中建立資源關係，以及每種資源型別的關係需求。

根據相關資源的型別，需要一些關係。 必要的關聯性表示父資源不能沒有關聯性存在。 所有其他關係都是選擇性的。

無論關聯性是必要還是選擇性的，系統都會在建立相關資源時自動建立，或者必須手動建立。 在手動建立關係的情況下，根據相關資源有兩種可能的方法：

* [依承載建立](#payload)
* [依URL建立](#url) （僅適用於資料庫）

請參閱[關係需求](#requirements)一節，以取得每個資源型別的相容關係清單，以及建立這些關係所需的方法（如適用）。

## 依承載建立關係 {#payload}

當您最初建立資源時，必須手動建立某些關係。 若要完成此操作，您必須在第一次建立父資源時，在要求裝載中提供`relationship`物件。 這些關係的範例包括：

* [正在建立具有必要副檔名的資料元素](../endpoints/data-elements.md#create)
* [正在建立具有所需主機關聯性的環境](../endpoints/environments.md#create)

**API格式**

```http
POST /properties/{PROPERTY_ID}/{RESOURCE_TYPE}
```

| 參數 | 說明 |
| --- | --- |
| `{PROPERTY_ID}` | 資源所屬屬性的ID。 |
| `{RESOURCE_TYPE}` | 要建立的資源型別。 |

{style="table-layout:auto"}

**要求**

下列要求會建立新的`rule_component`，與`rules`和`extension`建立關係。

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
| `relationships` | 依承載建立關係時必須提供的物件。 此物件中的每個索引鍵代表特定的關聯性型別。 在上述範例中，已建立`extension`和`rules`關係，這些關係是`rule_components`所特有的。 如需不同資源的相容關聯性型別的詳細資訊，請參閱資源[&#128279;](#relationship-requirements-by-resource)的關聯性需求一節。 |
| `data` | 在`relationship`物件下提供的每個關聯性型別都必須包含`data`屬性，該屬性會參考關聯性建立時所使用之資源的`id`和`type`。 您可以將`data`屬性格式化為物件陣列，讓每個物件包含適用資源的`id`和`type`，藉此與相同型別的多個資源建立關係。 |
| `id` | 資源的唯一ID。 每個`id`都必須隨附同層級`type`屬性，以表示相關資源的型別。 |
| `type` | 同層級`id`欄位參考的資源型別。 接受的值包括`data_elements`、`rules`、`extensions`和`environments`。 |

{style="table-layout:auto"}

## 依URL建立關係 {#url}

與其他資源不同，程式庫會透過自己的專用`/relationship`端點建立關係。 例如：

* [將擴充功能、資料元素和規則新增至程式庫](../endpoints/libraries.md#add-resources)
* [將程式庫指派給環境](../endpoints/libraries.md#environment)

**API格式**

```http
POST /properties/{PROPERTY_ID}/libraries/{LIBRARY_ID}/relationships/{RESOURCE_TYPE}
```

| 參數 | 說明 |
| --- | --- |
| `{PROPERTY_ID}` | 程式庫所屬屬性的ID。 |
| `{LIBRARY_ID}` | 您要建立關聯性的資料庫ID。 |
| `{RESOURCE_TYPE}` | 關係所定位的資源型別。 可用的值包括`environment`、`data_elements`、`extensions`和`rules`。 |

**要求**

下列要求使用程式庫的`/relationships/environment`端點來建立與環境的關係。

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
| `data` | 參考關聯性之目標資源的`id`和`type`的物件。 如果您要與相同型別的多個資源（例如`extensions`和`rules`）建立關聯性，`data`屬性必須格式化為物件陣列，每個物件包含適用資源的`id`和`type`。 |
| `id` | 資源的唯一ID。 每個`id`都必須隨附同層級`type`屬性，以表示相關資源的型別。 |
| `type` | 同層級`id`欄位參考的資源型別。 接受的值包括`data_elements`、`rules`、`extensions`和`environments`。 |

{style="table-layout:auto"}

## 依資源的關係需求 {#requirements}

下表概述每種資源型別的可用關係（無論這些關係是否必要），以及手動建立關係的可接受方法（如適用）。

>[!NOTE]
>
>如果關係未列為由承載或URL建立，則由系統自動指派。

### 稽核事件

| 關係 | 必要 | 依承載建立 | 依URL建立 |
| :--- | :---: | :---: | :---: |
| `property` | ✓ (A) | | |
| `entity` | ✓ (A) | | |

{style="table-layout:auto"}

### 組建

| 關係 | 必要 | 依承載建立 | 依URL建立 |
| :--- | :---: | :---: | :---: |
| `data_elements` | | | |
| `extensions` | | | |
| `rules` | | | |
| `environment` | ✓ (A) | | |
| `library` | ✓ (A) | | |
| `property` | ✓ (A) | | |

{style="table-layout:auto"}

### 回呼

| 關係 | 必要 | 依承載建立 | 依URL建立 |
| :--- | :---: | :---: | :---: |
| `property` | ✓ (A) | | |

{style="table-layout:auto"}

### 公司

| 關係 | 必要 | 依承載建立 | 依URL建立 |
| :--- | :---: | :---: | :---: |
| `properties` | | | |

{style="table-layout:auto"}

### 資料元素

| 關係 | 必要 | 依承載建立 | 依URL建立 |
| :--- | :---: | :---: | :---: |
| `libraries` | | | |
| `revisions` | ✓ (A) | | |
| `notes` | | | |
| `property` | ✓ (A) | | |
| `origin` | ✓ (A) | | |
| `extension` | ✓ (A) | ✓ (A) | |
| `updated_with_extension` | ✓ (A) | | |
| `updated_with_extension_package` | ✓ (A) | | |

{style="table-layout:auto"}

### 環境

| 關係 | 必要 | 依承載建立 | 依URL建立 |
| :--- | :---: | :---: | :---: |
| `library` | | | |
| `builds` | | | |
| `host` | ✓ (A) | ✓ (A) | |
| `property` | ✓ (A) | | |

{style="table-layout:auto"}

### 擴充功能

| 關係 | 必要 | 依承載建立 | 依URL建立 |
| :--- | :---: | :---: | :---: |
| `libraries` | | | |
| `revisions` | ✓ (A) | | |
| `notes` | | | |
| `property` | ✓ (A) | | |
| `origin` | ✓ (A) | | |
| `extension_package` | ✓ (A) | ✓ (A) | |
| `updated_with_extension_package` | ✓ (A) | | |

{style="table-layout:auto"}

### 主機

| 關係 | 必要 | 依承載建立 | 依URL建立 |
| :--- | :---: | :---: | :---: |
| `property` | ✓ (A) | | |

{style="table-layout:auto"}

### 程式庫

| 關係 | 必要 | 依承載建立 | 依URL建立 |
| :--- | :---: | :---: | :---: |
| `builds` | | | |
| `environment` | | | ✓ (A) |
| `data_elements` | | | ✓ (A) |
| `extensions` | | | ✓ (A) |
| `rules` | | | ✓ (A) |
| `notes` | | | |
| `upstream_library` | ✓ (A) | | |
| `property` | ✓ (A) | | |
| `last_build` | | | |

{style="table-layout:auto"}

### 附註

| 關係 | 必要 | 依承載建立 | 依URL建立 |
| :--- | :---: | :---: | :---: |
| `resource` | ✓ (A) | | |

{style="table-layout:auto"}

### 屬性

| 關係 | 必要 | 依承載建立 | 依URL建立 |
| :--- | :---: | :---: | :---: |
| `company` | ✓ (A) | | |
| `callbacks` | | | |
| `environments` | | | |
| `libraries` | | | |
| `data_elements` | | | |
| `extensions` | | | |
| `extensions` | | | |

{style="table-layout:auto"}

### 規則元件

| 關係 | 必要 | 依承載建立 | 依URL建立 |
| :--- | :---: | :---: | :---: |
| `updated_with_extensions_package` | ✓ (A) | | |
| `updated_with_extension` | ✓ (A) | | |
| `extension` | ✓ (A) | ✓ (A) | |
| `notes` | | | |
| `origin` | ✓ (A) | | |
| `property` | ✓ (A) | | |
| `rules` | ✓ (A) | ✓ (A) | |
| `revisions` | ✓ (A) | | |

{style="table-layout:auto"}

### 規則

| 關係 | 必要 | 依承載建立 | 依URL建立 |
| :--- | :---: | :---: | :---: |
| `libraries` | | | |
| `revisions` | ✓ (A) | | |
| `notes` | | | |
| `property` | ✓ (A) | | |
| `origin` | ✓ (A) | | |
| `rule_components` | | | |

### 秘密

| 關係 | 必要 | 依承載建立 | 依URL建立 |
| :--- | :---: | :---: | :---: |
| `property` | ✓ (A) | | ✓ (A) |
| `environment` | ✓ (A) | ✓ (A) | |

