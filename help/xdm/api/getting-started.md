---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 架構註冊API開發人員指南
topic: developer guide
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '1207'
ht-degree: 0%

---


# [!DNL Schema Registry] API開發人員指南

此 [!DNL Schema Registry] 程式庫用於存取Adobe Experience Platform中的「架構庫」，提供使用者介面和RESTful API，讓所有可用的程式庫資源都可從中存取。

使用「架構註冊表API」，您可以執行基本的CRUD作業，以檢視並管理Adobe Experience Platform中所有可用的架構及相關資源。 這包括由您使用之應用程式的Adobe [!DNL Experience Platform] 、合作夥伴和廠商所定義的應用程式。 您也可以使用API呼叫為組織建立新的結構和資源，以及檢視和編輯已定義的資源。

本開發人員指南提供協助您開始使用 [!DNL Schema Registry] API的步驟。 然後，該指南提供使用執行鍵操作的示例API調用 [!DNL Schema Registry]。

## 必要條件

本指南需要有效瞭解Adobe Experience Platform的下列元件：

* [[!DNL體驗資料模型(XDM)系統]](../home.md):組織客戶體驗資料 [!DNL Experience Platform] 的標準化架構。
   * [架構構成基礎](../schema/composition.md):瞭解XDM架構的基本建置區塊。
* [[!DNL即時客戶基本資料]](../../profile/home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。
* [[!DNL沙盒]](../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙盒，可將單一執行個體分 [!DNL Platform] 割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下章節提供您必須知道的其他資訊，才能成功呼叫 [!DNL Schema Registry] API。

## 讀取範例API呼叫

本指南提供範例API呼叫，以示範如何格式化您的請求。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱疑難排解指 [南中有關如何讀取範例API呼叫的](../../landing/troubleshooting.md#how-do-i-format-an-api-request)[!DNL Experience Platform] 章節。

## 收集必要標題的值

若要呼叫API，您必 [!DNL Platform] 須先完成驗證教 [學課程](../../tutorials/authentication.md)。 完成驗證教學課程後，將提供所有 [!DNL Experience Platform] API呼叫中每個必要標題的值，如下所示：

* 授權：生產者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

中的所有資 [!DNL Experience Platform]源（包括屬於的資源）都 [!DNL Schema Registry]被隔離到特定的虛擬沙盒中。 對API的所 [!DNL Platform] 有請求都需要一個標題，該標題會指定要在中執行的操作的沙盒名稱：

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>如需中沙盒的詳細資訊 [!DNL Platform]，請參閱沙 [盒概述檔案](../../sandboxes/home.md)。

對的所有查閱(GET)請 [!DNL Schema Registry] 求都需要額外的「接受」標題，其值會決定API傳回的資訊格式。 如需詳細 [資訊，請參閱下方](#accept) 「接受標題」一節。

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

* 內容類型：application/json

## 瞭解您的TENANT_ID {#know-your-tenant_id}

在本指南中，您將看到對的參考 `TENANT_ID`。 此ID可用來確保您建立的資源已正確命名並包含在IMS組織中。 如果您不知道您的ID，可以執行下列GET要求來存取它：

**API格式**

```http
GET /stats
```

**請求**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/stats \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回您組織使用的相關資訊 [!DNL Schema Registry]。 這包括 `tenantId` 屬性，其值為您的 `TENANT_ID`。

```JSON
{
  "imsOrg":"{IMS_ORG}",
  "tenantId":"{TENANT_ID}",
  "counts": {
    "schemas": 4,
    "mixins": 3,
    "datatypes": 1,
    "classes": 2,
    "unions": 0,
  },
  "recentlyCreatedResources": [ 
    {
      "title": "Sample Mixin",
      "description": "New Sample Mixin.",
      "meta:resourceType": "mixins",
      "meta:created": "Sat Feb 02 2019 00:24:30 GMT+0000 (UTC)",
      "version": "1.1"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/classes/5bdb5582be0c0f3ebfc1c603b705764f",
      "title": "Tenant Class",
      "description": "Tenant Defined Class",
      "meta:resourceType": "classes",
      "meta:created": "Fri Feb 01 2019 22:46:21 GMT+0000 (UTC)",
      "version": "1.0"
    } 
  ],
  "recentlyUpdatedResources": [
    {
      "title": "Sample Mixin",
      "description": "New Sample Mixin.",
      "meta:resourceType": "mixins",
      "meta:updated": "Sat Feb 02 2019 00:34:06 GMT+0000 (UTC)",
      "version": "1.1"
    },
    {
      "title": "Data Schema",
      "description": "Schema for Data Information",
      "meta:resourceType": "schemas",
      "meta:updated": "Fri Feb 01 2019 23:47:43 GMT+0000 (UTC)",
      "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/47b2189fc135e03c844b4f25139d10ab",
      "meta:classTitle": "Sample Class",
      "version": "1.1"
    }
 ],
 "classUsage": {
    "https://ns.adobe.com/{TENANT_ID}/classes/47b2189fc135e03c844b4f25139d10ab": [
      {
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
        "title": "Tenant Data Schema",
        "description": "Schema for tenant-specific data."
      }
    ],
    "https://ns.adobe.com/xdm/context/profile": [
      {
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/3ac6499f0a43618bba6b138226ae3542",
        "title": "Simple Profile",
        "description": "A simple profile schema."
      },
      {
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "title": "Program Schema",
        "description": "Schema for program-related data."
      },
      {
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/4025a705890c6d4a4a06b16f8cf6f4ca",
        "title": "Sample Schema",
        "description": "A sample schema."
      }
    ]
  }
 }
```

* `tenantId`:IMS `TENANT_ID` 組織的值。

## 瞭解 `CONTAINER_ID` {#container}

對 [!DNL Schema Registry] API的呼叫需要使用 `CONTAINER_ID`。 有兩個容器可對其進行API呼叫：全 **域容器** ，租 **戶容器**。

### 全域容器

全域容器包含所有標準Adobe及 [!DNL Experience Platform] 合作夥伴提供的類別、混合、資料類型和結構。 您只能對全域容器執行清單和查閱(GET)請求。

### 租用戶容器

不要與您的獨特性混淆，租 `TENANT_ID`用戶容器包含由IMS組織定義的所有類別、混合、資料類型、結構和描述子。 這是每個組織所獨有的，也就是說，其他IMS組織無法看到或管理。 您可以針對您在租用戶容器中建立的資源，執行所有CRUD作業(GET、POST、PUT、PATCH、DELETE)。

當您在租用戶容器中建立類別、混合、結構或資料類型時，會將其儲存至並指 [!DNL Schema Registry] 派包含您 `$id` 的URI `TENANT_ID`。 這 `$id` 會在整個API中用來參考特定資源。 值的范 `$id` 例會在下一節中提供。

## 模式識別 {#schema-identification}

方案以URI形 `$id` 式的屬性標識，如：
* `https://ns.adobe.com/xdm/context/profile`
* `https://ns.adobe.com/{TENANT_ID}/schemas/7442343-abs2343-21232421`

為了使URI更適合REST，架構在名為 `meta:altId`:
* `_xdm.context.profile`
* `_{TENANT_ID}.schemas.7442343-abs2343-21232421`

對架構註冊表API的呼叫將支援URL編碼 `$id` URI或 `meta:altId` （點符號格式）。 最佳實務是在對API進行REST呼叫時， `$id` 使用URL編碼的URI，例如：
* `https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile`
* `https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F7442343-abs2343-21232421`

## 接受標題 {#accept}

在 [!DNL Schema Registry] API中執行清單和查閱(GET)作業時，需要「接受」標題，以決定API傳回的資料格式。 查找特定資源時，「接受」標題中還必須包含版本號。

下表列出相容的「接受」標題值，包括具有版本號碼的值，以及使用API時傳回內容的說明。

| 接受 | 說明 |
| ------- | ------------ |
| `application/vnd.adobe.xed-id+json` | 僅傳回ID清單。 這最常用於列出資源。 |
| `application/vnd.adobe.xed+json` | 傳回包含原始和內含的完整JSON結 `$ref` 構 `allOf` 清單。 這可用來傳回完整資源清單。 |
| `application/vnd.adobe.xed+json; version={MAJOR_VERSION}` | Raw XDM `$ref` with和 `allOf`. 有標題和說明。 |
| `application/vnd.adobe.xed-full+json; version={MAJOR_VERSION}` | `$ref` 屬性和已解 `allOf` 決。 有標題和說明。 |
| `application/vnd.adobe.xed-notext+json; version={MAJOR_VERSION}` | Raw XDM `$ref` with和 `allOf`. 無標題或說明。 |
| `application/vnd.adobe.xed-full-notext+json; version={MAJOR_VERSION}` | `$ref` 屬性和已解 `allOf` 決。 無標題或說明。 |
| `application/vnd.adobe.xed-full-desc+json; version={MAJOR_VERSION}` | `$ref` 屬性和已解 `allOf` 決。 包括描述符。 |

>[!NOTE]
>
>如果僅提 `major` 供版本（例如1、2、3），則註冊表將返回最新 `minor` 版本(例如.1、.2、.3)。

## XDM現場限制和最佳做法

方案的欄位列在其對象中 `properties` 。 每個欄位本身都是物件，包含屬性以說明並限制欄位可包含的資料。

如需在API中定義欄位類型的詳細資訊，請參閱本指南的附 [錄](appendix.md) ，包括程式碼範例和常用資料類型的選用限制。

以下示例欄位說明了格式正確的XDM欄位，下面提供了有關命名約束和最佳做法的詳細資訊。 在定義包含類似屬性的其他資源時，也可套用這些做法。

```JSON
"fieldName": {
    "title": "Field Name",
    "type": "string",
    "format": "date-time",
    "examples": [
        "2004-10-23T12:00:00-06:00"
    ],
    "description": "Full sentence describing the field, using proper grammar and punctuation.",
}
```

* 欄位物件的名稱可能包含英數字元、破折號或底線字元，但 **不得以底線** 開頭。
   * **正確：**`fieldName`, `field_name2`, `Field-Name`, `field-name_3`
   * **錯誤：** `_fieldName`
* camelCase是欄位對象名稱的首選參數。 範例: `fieldName`
* 欄位應包含在「 `title`標題大小寫」中寫入的。 範例: `Field Name`
* 欄位需要 `type`。
   * 定義某些類型可能需要選擇 `format`。
   * 當需要特定格式化資料時， `examples` 可新增為陣列。
   * 也可以使用註冊表中的任何資料類型定義欄位類型。 如需詳細資訊， [請參閱本指南中](create-data-type.md) 「建立資料類型」一節。
* 說明 `description` 了有關現場資料的現場和相關資訊。 它應以完整的句子編寫，使用清楚的語言，讓任何存取架構的人都能瞭解欄位的意圖。

如需如 [何定義API中欄位類型的詳細資訊，請參閱附錄](appendix.md) 。

## 後續步驟

本檔案涵蓋對 [!DNL Schema Registry] API進行呼叫所需的先決條件知識，包括必要的驗證憑證。 您現在可以繼續閱讀本開發人員指南中提供的範例呼叫，並依照其指示進行。 有關如何在API中建立架構的完整逐步說明，請參閱下列教 [學課程](../tutorials/create-schema-api.md)。
