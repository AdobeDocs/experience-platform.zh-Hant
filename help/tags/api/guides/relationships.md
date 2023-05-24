---
title: 反應堆API中的關係
description: 瞭解如何在Reactor API中建立資源關係，包括每個資源的關係要求。
exl-id: 23976978-a639-4eef-91b6-380a29ec1c14
source-git-commit: 7e4bc716e61b33563e0cb8059cb9f1332af7fd36
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 6%

---

# 反應堆API中的關係

反應堆API中的資源通常彼此相關。 本文檔概述了如何在API中建立資源關係以及每種資源類型的關係要求。

根據所涉資源的類型，需要一些關係。 必需的關係意味著沒有關係就無法存在父資源。 所有其他關係都是可選的。

無論是必需的還是可選的，在建立相關資源時，系統會自動建立關係，或者必須手動建立關係。 在手動建立關係時，根據所涉資源有兩種可能的方法：

* [按負載建立](#payload)
* [按URL建立](#url) （僅適用於庫）

請參閱上 [關係需求](#requirements) 的子目錄。

## 按負載建立關係 {#payload}

初始建立資源時必須手動建立某些關係。 要完成此操作，必須提供 `relationship` 首次建立父資源時請求負載中的對象。 這些關係的示例包括：

* [建立資料元素](../endpoints/data-elements.md#create) 帶有所需副檔名
* [建立環境](../endpoints/environments.md#create) 具有所需的主機關係

**API格式**

```http
POST /properties/{PROPERTY_ID}/{RESOURCE_TYPE}
```

| 參數 | 說明 |
| --- | --- |
| `{PROPERTY_ID}` | 資源所屬屬性的ID。 |
| `{RESOURCE_TYPE}` | 要建立的資源類型。 |

{style="table-layout:auto"}

**要求**

以下請求將建立新 `rule_component`，建立關係 `rules` 和 `extension`。

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
| `relationships` | 按負載建立關係時必須提供的對象。 此對象中的每個鍵都表示特定的關係類型。 在上例中， `extension` 和 `rules` 建立關係，這是 `rule_components`。 有關不同資源的相容關係類型的詳細資訊，請參閱上的 [按資源列出的關係需求](#relationship-requirements-by-resource)。 |
| `data` | 在 `relationship` 對象必須包含 `data` 屬性，引用 `id` 和 `type` 與之建立關係的資源。 您可以通過格式化 `data` 屬性，每個對象都包含 `id` 和 `type` 的下界。 |
| `id` | 資源的唯一ID。 每個 `id` 必須和兄弟姐妹一起 `type` 屬性，指明所涉資源的類型。 |
| `type` | 同級引用的資源類型 `id` 的子菜單。 接受的值包括 `data_elements`。 `rules`。 `extensions`, `environments`。 |

{style="table-layout:auto"}

## 按URL建立關係 {#url}

與其他資源不同，圖書館通過自己的專用資源建立關係 `/relationship` 端點。 例如：

* [向庫添加擴展、資料元素和規則](../endpoints/libraries.md#add-resources)
* [將庫分配給環境](../endpoints/libraries.md#environment)

**API格式**

```http
POST /properties/{PROPERTY_ID}/libraries/{LIBRARY_ID}/relationships/{RESOURCE_TYPE}
```

| 參數 | 說明 |
| --- | --- |
| `{PROPERTY_ID}` | 庫所屬的屬性的ID。 |
| `{LIBRARY_ID}` | 要為其建立關係的庫的ID。 |
| `{RESOURCE_TYPE}` | 關係所針對的資源類型。 可用值包括 `environment`。 `data_elements`。 `extensions`, `rules`。 |

**要求**

以下請求使用 `/relationships/environment` 用於庫建立與環境關係的端點。

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
| `data` | 引用的對象 `id` 和 `type` 關係的目標資源。 如果要建立與同一類型的多個資源的關係(如 `extensions` 和 `rules`) `data` 屬性必須格式化為對象陣列，每個對象都包含 `id` 和 `type` 的下界。 |
| `id` | 資源的唯一ID。 每個 `id` 必須和兄弟姐妹一起 `type` 屬性，指明所涉資源的類型。 |
| `type` | 同級引用的資源類型 `id` 的子菜單。 接受的值包括 `data_elements`。 `rules`。 `extensions`, `environments`。 |

{style="table-layout:auto"}

## 按資源劃分的關係需求 {#requirements}

下表概述了每種資源類型的可用關係，以及在適用時手動建立關係的接受方法。

>[!NOTE]
>
>如果關係未列為由負載或URL建立，則系統會自動分配它。

### 審計事件

| 關係 | 必填 | 按負載建立 | 按URL建立 |
| :--- | :---: | :---: | :---: |
| `property` | ✓ |  |  |
| `entity` | ✓ |  |  |

{style="table-layout:auto"}

### 組建

| 關係 | 必填 | 按負載建立 | 按URL建立 |
| :--- | :---: | :---: | :---: |
| `data_elements` |  |  |  |
| `extensions` |  |  |  |
| `rules` |  |  |  |
| `environment` | ✓ |  |  |
| `library` | ✓ |  |  |
| `property` | ✓ |  |  |

{style="table-layout:auto"}

### 回調

| 關係 | 必填 | 按負載建立 | 按URL建立 |
| :--- | :---: | :---: | :---: |
| `property` | ✓ |  |  |

{style="table-layout:auto"}

### 公司

| 關係 | 必填 | 按負載建立 | 按URL建立 |
| :--- | :---: | :---: | :---: |
| `properties` |  |  |  |

{style="table-layout:auto"}

### 資料元素

| 關係 | 必填 | 按負載建立 | 按URL建立 |
| :--- | :---: | :---: | :---: |
| `libraries` |  |  |  |
| `revisions` | ✓ |  |  |
| `notes` |  |  |  |
| `property` | ✓ |  |  |
| `origin` | ✓ |  |  |
| `extension` | ✓ | ✓ |  |
| `updated_with_extension` | ✓ |  |  |
| `updated_with_extension_package` | ✓ |  |  |

{style="table-layout:auto"}

### 環境

| 關係 | 必填 | 按負載建立 | 按URL建立 |
| :--- | :---: | :---: | :---: |
| `library` |  |  |  |
| `builds` |  |  |  |
| `host` | ✓ | ✓ |  |
| `property` | ✓ |  |  |

{style="table-layout:auto"}

### 擴充功能

| 關係 | 必填 | 按負載建立 | 按URL建立 |
| :--- | :---: | :---: | :---: |
| `libraries` |  |  |  |
| `revisions` | ✓ |  |  |
| `notes` |  |  |  |
| `property` | ✓ |  |  |
| `origin` | ✓ |  |  |
| `extension_package` | ✓ | ✓ |  |
| `updated_with_extension_package` | ✓ |  |  |

{style="table-layout:auto"}

### 主機

| 關係 | 必填 | 按負載建立 | 按URL建立 |
| :--- | :---: | :---: | :---: |
| `property` | ✓ |  |  |

{style="table-layout:auto"}

### 程式庫

| 關係 | 必填 | 按負載建立 | 按URL建立 |
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

{style="table-layout:auto"}

### 附註

| 關係 | 必填 | 按負載建立 | 按URL建立 |
| :--- | :---: | :---: | :---: |
| `resource` | ✓ |  |  |

{style="table-layout:auto"}

### 屬性

| 關係 | 必填 | 按負載建立 | 按URL建立 |
| :--- | :---: | :---: | :---: |
| `company` | ✓ |  |  |
| `callbacks` |  |  |  |
| `environments` |  |  |  |
| `libraries` |  |  |  |
| `data_elements` |  |  |  |
| `extensions` |  |  |  |
| `extensions` |  |  |  |

{style="table-layout:auto"}

### 規則元件

| 關係 | 必填 | 按負載建立 | 按URL建立 |
| :--- | :---: | :---: | :---: |
| `updated_with_extensions_package` | ✓ |  |  |
| `updated_with_extension` | ✓ |  |  |
| `extension` | ✓ | ✓ |  |
| `notes` |  |  |  |
| `origin` | ✓ |  |  |
| `property` | ✓ |  |  |
| `rules` | ✓ | ✓ |  |
| `revisions` | ✓ |  |  |

{style="table-layout:auto"}

### 規則

| 關係 | 必填 | 按負載建立 | 按URL建立 |
| :--- | :---: | :---: | :---: |
| `libraries` |  |  |  |
| `revisions` | ✓ |  |  |
| `notes` |  |  |  |
| `property` | ✓ |  |  |
| `origin` | ✓ |  |  |
| `rule_components` |  |  |  |

### 秘密

| 關係 | 必填 | 按負載建立 | 按URL建立 |
| :--- | :---: | :---: | :---: |
| `property` | ✓ |  | ✓ |
| `environment` | ✓ | ✓ |  |

