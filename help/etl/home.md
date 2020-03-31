---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 建立ETL整合
topic: overview
translation-type: tm+mt
source-git-commit: 4817162fe2b7cbf4ae4c1ed325db2af31da5b5d3

---


# 開發Adobe Experience Platform的ETL整合

ETL整合指南概述建立Experience Platform的高效能、安全連接器以及將資料匯入Platform的一般步驟。


- [目錄](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)
- [資料存取](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml)
- [資料擷取](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)
- [驗證與授權API](../tutorials/authentication.md)
- [架構註冊表](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)

本指南也包含設計ETL連接器時要使用的範例API呼叫，其中包含說明每個Experience Platform服務的檔案連結，以及其API的使用，有更詳細的說明。

GitHub上可透過 [ETL Cestium Integration Reference Code](https://github.com/adobe/acp-data-services-etl-reference) (Apache License Version 2.0)取得範例整合。

## 工作流程

以下工作流程圖提供整合Adobe Experience Platform元件與ETL應用程式和連接器的高階概觀。

![](images/etl.png)

## Adobe Experience Platform元件

ETL連接器整合涉及多個Experience Platform元件。 下列清單概述數個主要元件和功能：

- **Adobe Identity Management System(IMS)** —— 提供Adobe服務驗證的架構。
- **IMS組織** -可擁有或授權產品與服務並允許存取其會員的公司實體。
- **IMS使用者** - IMS組織的成員。 「組織與使用者」的關係是多對多的關係。
- **沙盒** -單一平台實例的虛擬分區，可協助開發和發展數位體驗應用程式。
- **資料發現** -在Experience Platform中記錄所擷取和轉換資料的中繼資料。
- **資料存取** -為使用者提供介面，以存取Experience Platform中的資料。
- **資料擷取** -使用資料擷取API將資料推送至Experience Platform。
- **架構註冊表** -定義並儲存描述Experience Platform中要使用之資料結構的架構。

## Experience Platform API快速入門

以下章節提供您必須知道或掌握的額外資訊，才能成功呼叫Experience Platform API。

### 讀取範例API呼叫

本指南提供範例API呼叫，以示範如何格式化您的請求。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱「Experience Platform疑難排解指 [南」中有關如何讀取範例API呼叫的章節](../landing/troubleshooting.md#how-do-i-format-an-api-request) 。

### 收集必要標題的值

若要呼叫平台API，您必須先完成驗證教 [學課程](../tutorials/authentication.md)。 完成驗證教學課程後，所有Experience Platform API呼叫中每個必要標題的值都會顯示在下方：

- 授權：生產者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有資源都隔離至特定的虛擬沙盒。 所有對平台API的請求都需要一個標題，該標題會指定要在中執行的操作的沙盒名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] 如需平台中沙盒的詳細資訊，請參閱沙盒 [概觀檔案](../sandboxes/home.md)。

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

- 內容類型：application/json

## 一般使用者流程

首先，ETL使用者會登入Experience Platform使用者介面(UI)，並使用標準連接器或推播服務連接器建立資料集以擷取。

在UI中，用戶通過選擇資料集模式建立輸出資料集。 方案的選擇取決於被引入平台的資料類型（記錄或時間序列）。 通過按一下UI中的「方案」頁籤，用戶將能夠查看所有可用的方案，包括方案支援的行為類型。

在ETL工具中，使用者將在設定適當的連線（使用其認證）後，開始設計其對應轉換。 假定ETL工具已安裝Experience Platform連接器（此整合指南中未定義的程式）。

ETL工作流程中已提供範例ETL工具和工作流程的 [模型](./workflow.md)。 雖然ETL工具的格式可能不同，但大部分都會公開類似的功能。

>[!NOTE] ETL連接器必須指定一個時間戳記篩選器，標籤要收錄資料和偏移的日期（即要讀取其資料的視窗）。 ETL工具應支援在此或其他相關UI中取用這兩個參數。 在Adobe Experience Platform中，這些參數會對應至資料集批次物件中的可用日期（如果存在）或擷取日期。

### 查看資料集清單

使用資料來源進行對應，可使用目錄API擷取所有可用資料集 [的清單](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)。

您可以發出單一API要求來檢視所有可用的資料集(例如 `GET /dataSets`)，最佳實務是包含限制回應大小的查詢參數。

在要求完整 _資料集資訊_ 時，回應負載可能會達到超過3GB的大小，進而降低整體效能。 因此，只使用查詢參數來過濾所需資訊將使目錄查詢更加有效。

#### 清單篩選

在篩選回應時，您可以在單一呼叫中使用多個篩選器，方法是使用&amp;符號(`&`)分隔參數。 有些查詢參數接受逗號分隔的值清單，例如下方範例請求中的「屬性」篩選。

目錄回應會根據設定的限制自動計量，但「限制」查詢參數可用來自訂限制並限制傳回的物件數。 預先設定的目錄回應限制為：

- 如果未指定限制參數，則每個回應裝載的物件數上限為20。
- 所有其他目錄查詢的全局限制是100個對象。
- 對於資料集查詢，如果使用屬性查詢參數請求evocableSchema，則返回的資料集的最大數量為20。
- 無效的限制參數( `limit=0`包括)會遇到HTTP 400錯誤，該錯誤會概述正確的範圍。
- 如果限制或偏移作為查詢參數傳遞，則其優先於作為標題傳遞的限制或偏移。

目錄服務概述中將更詳細地介紹 [查詢參數](../catalog/home.md)。

**API格式**

```http
GET /catalog/dataSets
GET /catalog/dataSets?{filter1}={value1},{value2}&{filter2}={value3}
```

**請求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets?limit=3&properties=name,description,schemaRef" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

請參閱目錄服 [務概觀](../catalog/home.md) ，以取得如何呼叫目錄API的詳細 [範例](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)。

**回應**

回應包含三(`limit=3`)個資料集，顯示查詢參數所指示的&quot;name&quot;、&quot;description&quot;和&quot;schemaRef&quot; `properties` 。

```json
{
    "5b95b155419ec801e6eee780": {
        "name": "Store Transactions",
        "description": "Retails Store Transactions",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
            "contentType": "application/vnd.adobe.xed+json;version=1"
        }
    },
    "5c351fa2f5fee300000fa9e8": {
        "name": "Loyalty Members",
        "description": "Loyalty Program Members",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
            "contentType": "application/vnd.adobe.xed+json;version=1"
        }
    },
    "5c1823b19e6f400000993885": {
        "name": "Web Traffic",
        "description": "Retail Web Traffic",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/2025a705890c6d4a4a06b16f8cf6f4ca",
            "contentType": "application/vnd.adobe.xed+json;version=1"
        }
    }
}
```

### 檢視資料集架構

資料集的&quot;schemaRef&quot;屬性包含引用資料集所基於的XDM模式的URI。 XDM架構(&quot;schemaRef&quot;)代表資料集可使用的所有潛在 _欄位_ ，而不一定是使用 _的欄位(請參閱下面的_ &quot;veocableSchema&quot;)。

XDM架構是您在需要向用戶顯示可寫入的所有可用欄位的清單時所使用的架構。

上一個響應對象(`https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18`)中的第一個&quot;schemaRef.id&quot;值是指向模式註冊表中特定XDM模式的URI。 可通過對方案註冊表API進行查找(GET)請求來檢索方案。

>[!NOTE] &quot;schemaRef&quot;屬性會取代現已過時的&quot;schema&quot;屬性。 如果資料集中沒有&quot;schemaRef&quot;或不包含值，則需要檢查是否存在&quot;schema&quot;屬性。 若要這麼做，請在先前呼叫的查詢參數中，將&quot;schemaRef&quot; `properties` 取代為&quot;schema&quot;。 下面的「資料集」「架構」屬性區段中提供了有關 [「架構」屬性的詳細資訊](#dataset-schema-property-deprecated---eol-2019-05-30) 。

**API格式**

```http
GET /schemaregistry/tenant/schemas/{url encoded schemaRef.id}
```

**請求**

請求使用架構的URL `id` 編碼URI（&quot;schemaRef.id&quot;屬性的值），並需要「接受」標題。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F274f17bc5807ff307a046bab1489fb18 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
```

回應格式取決於請求中傳送的「接受」標題類型。 查閱請求也需要 `version` 包含在「接受」標題中。 下表概述了可用的「接受」標題的查找：

| 接受 | 說明 |
| ------ | ----------- |
| `application/vnd.adobe.xed-id+json` | 清單(GET)要求、標題、ID和版本 |
| `application/vnd.adobe.xed-full+json; version={major version}` | $refs and allOf已解析，有標題和說明 |
| `application/vnd.adobe.xed+json; version={major version}` | Raw含$ref和allOf，有標題和說明 |
| `application/vnd.adobe.xed-notext+json; version={major version}` | Raw含$ref和allOf，無標題或說明 |
| `application/vnd.adobe.xed-full-notext+json; version={major version}` | $refs and allOf已解析，無標題或說明 |
| `application/vnd.adobe.xed-full-desc+json; version={major version}` | $refs and allOf已解析，包含描述符 |

>[!NOTE] 而且 `application/vnd.adobe.xed-id+json` 是 `application/vnd.adobe.xed-full+json; version={major version}` 最常使用的「接受」標題。 `application/vnd.adobe.xed-id+json` 優先於在架構註冊表中列出資源，因為它只返回&quot;title&quot;、&quot;id&quot;和&quot;version&quot;。 `application/vnd.adobe.xed-full+json; version={major version}` 偏好用於檢視特定資源（依其「id」），因為它會傳回所有欄位（巢狀內嵌於「屬性」下）以及標題和說明。

**回應**

傳回的JSON結構描述說明結構和欄位層級資訊（「類型」、「格式」、「最小」、「最大」等）資料的序號，序號為JSON。 如果使用JSON以外的序列化格式擷取（例如Parce或Scala）, [Schema Registry Guide](../xdm/tutorials/create-schema-api.md) （架構註冊表指南）會包含一個表格，其中顯示所要的JSON類型(「meta:xdmType」)及其他格式的對應表示法。

除了此表之外，《方案註冊開發人員指南》還包含使用「方案註冊表API」可進行的所有可能調用的深入示例。

### 資料集「架構」屬性（已過時- EOL 2019-05-30）

資料集可能包含「架構」屬性，該屬性現在已過時，並且暫時可用以向後相容。 例如，與先前所做的清單(GET)要求類似，其中查詢參數中的&quot;schema&quot;被取代為&quot;schemaRef&quot;的 `properties` 請求可能會傳回下列內容：

```json
{
  "5ba9452f7de80400007fc52a": {
    "name": "Sample Dataset 1",
    "description": "Description of Sample Dataset 1.",
    "schema": "@/xdms/context/person"
  }
}
```

如果填入資料集的「架構」屬性，這表示架構是已過時的架構，而且在支援的情況下，ETL連接器應使用「架構」屬性中的值與端點( `/xdms``/xdms`[](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)Catalog API中已過時的端點)來擷取舊式架構。

**API格式**

```http
GET /catalog/{"schema" property without the "@"}
```

**請求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/xdms/context/person?expansion=xdm" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

>[!NOTE] 選用的查詢參 `expansion=xdm`數會告訴API完全展開並內嵌任何參考的結構。 當向用戶顯示所有潛在欄位的清單時，可能希望執行此操作。

**回應**

與檢視資料集結 [構描述的步驟類似](#view-dataset-schema)，回應包含JSON結構描述資料的結構和欄位層級資訊，序列化為JSON。

>[!NOTE] 當&quot;schema&quot;欄位為空或完全不存在時，連接器應讀取&quot;schemaRef&quot;欄位，並使用 [Schema Registry API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) (如前面步驟中所 [示)查看資料集模式](#view-dataset-schema)。

### &quot;voocableSchema&quot;屬性

資料集的「可觀察結構」屬性具有與XDM結構JSON相符的JSON結構。 &quot;oveableSchema&quot;包含傳入輸入檔案中的欄位。 將資料寫入Experience Platform時，使用者不需要使用目標架構中的每個欄位。 而應僅提供正在使用的欄位。

可觀察模式是讀取資料或顯示可從中讀取／映射的欄位清單時要使用的模式。

```json
{
    "598d6e81b2745f000015edcb": {
        "observableSchema": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "name": {
                    "type": "string",
                },
                "age": {
                    "type": "string",
                }
            }
        }
    }
}
```

### 預覽資料

ETL應用程式可提供預覽資料的功能([「ETL工作流程」中的圖8](./workflow.md))。 資料存取API提供數種預覽資料的選項。

其他資訊，包括使用資料存取API預覽資料的逐步指引，請參閱資料存取教 [學課程](../data-access/tutorials/dataset-data.md)。

### 使用「屬性」查詢參數取得資料集詳細資料

如上述步驟所示，如 [果要檢視資料集清單](#view-list-of-datasets)，您可以使用「屬性」查詢參數來請求「檔案」。

有關查詢資料集和可用響 [應篩選器的詳細資訊](../catalog/home.md) ，請參閱目錄服務概述。

**API格式**

```http
GET /catalog/dataSets?limit={value}&properties={value}
```

**請求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets?limit=1&properties=files" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

**回應**

回應將包含一個顯示「檔`limit=1`案」屬性的資料集()。

```json
{
  "5bf479a6a8c862000050e3c7": {
    "files": "@/dataSets/5bf479a6a8c862000050e3c7/views/5bf479a654f52014cfffe7f1/files"
  }
}
```

### 使用「檔案」屬性列出資料集檔案

您也可以使用「檔案」屬性，使用GET請求來擷取檔案詳細資訊。

**API格式**

```http
GET /catalog/dataSets/{DATASET_ID}/views/{VIEW_ID}/files
```

**請求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets/5bf479a6a8c862000050e3c7/views/5bf479a654f52014cfffe7f1/files" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

**回應**

回應包含資料集檔案ID作為頂層屬性，而資料集檔案ID物件中包含檔案詳細資訊。

```json
{
    "194e89b976494c9c8113b968c27c1472-1": {
        "batchId": "194e89b976494c9c8113b968c27c1472",
        "dataSetViewId": "5bf479a654f52014cfffe7f1",
        "imsOrg": "{IMS_ORG}",
        "availableDates": {},
        "createdUser": "{USER_ID}",
        "createdClient": "{API_KEY}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1542749145828,
        "updated": 1542749145828
    },
    "14d5758c107443e1a83c714e56ca79d0-1": {
        "batchId": "14d5758c107443e1a83c714e56ca79d0",
        "dataSetViewId": "5bf479a654f52014cfffe7f1",
        "imsOrg": "{IMS_ORG}",
        "availableDates": {},
        "createdUser": "{USER_ID}",
        "createdClient": "{API_KEY}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1542752699111,
        "updated": 1542752699111
    },
    "ea40946ac03140ec8ac4f25da360620a-1": {
        "batchId": "ea40946ac03140ec8ac4f25da360620a",
        "dataSetViewId": "5bf479a654f52014cfffe7f1",
        "imsOrg": "{IMS_ORG}",
        "availableDates": {},
        "createdUser": "{USER_ID}",
        "createdClient": "{API_KEY}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1542756935535,
        "updated": 1542756935535
    }
}
```

### 擷取檔案詳細資訊

在先前響應中返回的資料集檔案ID可以用於GET請求中，以通過資料存取API獲取更多檔案詳細資訊。

資 [料存取概述](../data-access/home.md) ，包含如何使用資料存取API的詳細資訊。

**API格式**

```http
GET /export/files/{DATASET_FILE_ID}
```

**請求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/ea40946ac03140ec8ac4f25da360620a-1" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

**回應**

```json
[
    {
    "name": "{FILE_NAME}.parquet",
    "length": 2576,
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/export/files/ea40946ac03140ec8ac4f25da360620a-1?path=samplefile.parquet"
            }
        }
    }
]
```

### 預覽檔案資料

&quot;href&quot;屬性可用來透過資料存取API擷取預 [覽資料](../data-access/home.md)。

**API格式**

```http
GET /export/files/{FILE_ID}?path={FILE_NAME}.{FILE_FORMAT}
```

**請求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/ea40946ac03140ec8ac4f25da360620a-1?path=samplefile.parquet" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

對上述要求的回應將包含檔案內容的預覽。

資料存取概述中提供有關資料存取API的詳細資訊，包括詳細的請求 [和回應](../data-access/home.md)。

### 從資料集取得「fileDescription」

目標元件作為轉換資料的輸出，資料工程師將選擇輸出資料集([「ETL工作流」中的圖12](workflow.md))。 XDM模式與輸出資料集關聯。 要寫入的資料將由資料集實體的「fileDescription」屬性從Data Discovery API中標識。 此資訊可使用資料集ID(`{DATASET_ID}`)擷取。 JSON回應中的&quot;fileDescription&quot;屬性將提供所要求的資訊。

**API格式**

```shell
GET /catalog/dataSets/{DATASET_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{DATASET_ID}` | 您 `id` 嘗試存取的資料集值。 |

**請求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets/59c93f3da7d0c00000798f68" \
-H "accept: application/json" \
-H "x-gw-ims-org-id: {IMS_ORG}" \
-H "x-sandbox-name: {SANDBOX_NAME}" \
-H "Authorization: Bearer {ACCESS_TOKEN}" \
-H "x-api-key : {API_KEY}"
```

**回應**

```JSON
{
  "59c93f3da7d0c00000798f68": {
    "version": "1.0.4",
    "fileDescription": {
        "persisted": false,
        "format": "parquet"
    }
  }
}
```

資料將使用資料擷取API寫入 [Experience Platform](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)。  資料寫入是非同步的程式。 當資料寫入Adobe Experience Platform時，只有在資料完全寫入後，才會建立批次並標示為成功。

Experience Platform中的資料應以拼花檔案的形式寫入。

## 執行階段

當執行開始時，連接器（如來源元件中所定義）將使用資料存取API從Experience Platform讀取 [資料](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml)。 轉換過程將讀取特定時間範圍的資料。 內部查詢源資料集的批次。 查詢時，會使用參數化（滾動時間序列資料或增量資料）的開始日期和列出這些批的資料集檔案，並開始請求這些資料集檔案的資料。

### 範例轉換

范 [例ETL轉換檔案](./transformations.md) ，包含許多範例轉換，包括身分處理和資料類型映射。 請使用這些轉換以供參考。

### 從Experience Platform讀取資料

使用 [Catalog API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)，您可以擷取指定開始時間和結束時間之間的所有批次，並依其建立順序加以排序。

**請求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches?dataSet=DATASETID&createdAfter=START_TIMESTAMP&createdBefore=END_TIMESTAMP&sort=desc:created" \
  -H "Accept: application/json" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

有關篩選批次的詳細資訊，請參閱資料 [存取教學課程](../data-access/tutorials/dataset-data.md)。

### 從批次中取出檔案

在您擁有所尋找(`{BATCH_ID}`)批次的ID後，就可透過資料存取API擷取屬於特定批次的檔 [案清單](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml)。  資料存取教學課程中提供了相關 [的詳細資訊](../data-access/tutorials/dataset-data.md)。

**請求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/files" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

### 使用檔案ID存取檔案

使用檔案(`{FILE_ID`)的唯一ID，資料存取 [API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) 可用來存取檔案的特定詳細資訊，包括檔案名稱、大小（位元組），以及下載檔案的連結。

**請求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{FILE_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key : {API_KEY}"
```

響應可指向單個檔案或目錄。 資料存取教學課程中提供每項資 [料的詳細資訊](../data-access/tutorials/dataset-data.md)。

### 存取檔案內容

資 [料存取API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) ，可用來存取特定檔案的內容。 若要擷取內容，會使用使用檔案ID存取檔案時傳回 `_links.self.href` 的值來提出GET要求。

**請求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{DATASET_FILE_ID}?path=filename1.csv" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

對此請求的回應包含檔案的內容。 如需詳細資訊，包括回應分頁的詳細資訊，請參閱 [如何透過資料存取API教學課程來查詢資料](../data-access/tutorials/dataset-data.md) 。

### 驗證方案符合性記錄

在寫入資料時，使用者可以根據XDM架構中定義的驗證規則來驗證資料。 有關模式驗證的詳細資訊，請參閱GitHub上的 [ETL生態系統整合參考程式碼](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md#validation)。

如果您使用 [GitHub上的參考實作](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md)，則可使用系統屬性在此實作中開啟架構驗證 `-DenableSchemaValidation=true`。

可對邏輯XDM類型使用屬性（如字串）和 `minLength` 整數 `maxlength` 等， `minimum` 以 `maximum` 及更多屬性執行驗證。 Schema Registry [API開發人員指南包含](../xdm/api/getting-started.md) ，其中包含一個表，其中列出XDM類型和可用於驗證的屬性。

>[!NOTE] 為各種類型提供的最小值和最大值是 `integer` MIN和MAX值，這些值可進一步限制為您選擇的最小值和最大值。

### 建立批次

資料處理完成後，ETL工具會使用批次擷取API將資料寫回 [Experience Platform](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)。 資料必須連結至批次，之後才能上傳至特定資料集。

**請求**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -d '{
        "datasetId":"{DATASET_ID}"
      }'
```

有關建立批的詳細資訊，包括示例請求和響應，請參閱「批提取 [」概述](../ingestion/batch-ingestion/overview.md)。

### 寫入資料集

成功建立新批次後，檔案就可以上傳到特定資料集。 多個檔案可以在批次中張貼，直到升級為止。 檔案可以使用小型檔案 _上傳API上傳_;不過，如果您的檔案過大且已超出閘道限制，則可使用「大 _型檔案上傳API」_。 如需使用「大型和小型檔案上傳」的詳細資訊，請參閱「批次擷 [取」概觀](../ingestion/batch-ingestion/overview.md)。

**請求**

Experience Platform中的資料應以拼花檔案的形式寫入。

```shell
curl -X PUT "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/dataSets/{DATASET_ID}/files/{FILE_NAME}.parquet" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id:{IMS_ORG}" \
  -H "Authorization:Bearer ACCESS_TOKEN" \
  -H "x-api-key: API_KEY" \
  -H "content-type: application/octet-stream" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

### 標籤批次上傳完成

將所有檔案上傳到批後，可以向批發出完成信號。 通過執行此操作，將為已完成的檔案建立目錄「DataSetFile」條目，並與生成批關聯。 然後目錄批次會標示為成功，這會觸發下游流程，以擷取可用資料。

資料將先登入Adobe Experience Platform的測試位置，然後在編目及驗證後移至最終位置。 所有資料移至永久位置後，批次就會標示為成功。

**請求**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

如果成功，回應將傳回HTTP狀態200 OK，且回應內文為空。

ETL工具會確保在讀取資料時記下來源資料集的時間戳記。

在下次轉換執行中，ETL可能會透過排程或事件呼叫，開始從先前儲存的時間戳記和後續的所有資料請求資料。

### 取得上次批次狀態

在ETL工具中執行新任務之前，您必須確保已成功完成最後一批。 目 [錄服務API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) 提供批次特定選項，可提供相關批次的詳細資訊。

**請求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches?limit=1&sort=desc:created" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**回應**

如果上一批「狀態」值為「成功」，則可排程新任務，如下所示：

```json
"{BATCH_ID}": {
    "imsOrg": "{IMS_ORG}",
    "created": 1494349962314,
    "createdClient": "{API_KEY}",
    "createdUser": "CLIENT_USER_ID@AdobeID",
    "updatedUser": "CLIENT_USER_ID@AdobeID",
    "updated": 1494349963467,
    "status": "success",
    "errors": [],
    "version": "1.0.1",
    "availableDates": {}
}
```

### 依ID取得上次批次狀態

您可以透過目錄服務API [來擷取個別的批次狀態](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) ，方法是使用 `{BATCH_ID}`。 使 `{BATCH_ID}` 用的值與建立批次時傳回的ID相同。

**請求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID}" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**回應——成功**

下列回應顯示「成功」:

```json
"{BATCH_ID}": {
    "imsOrg": "{IMS_ORG}",
    "created": 1494349962314,
    "createdClient": "{API_KEY}",
    "createdUser": "{CREATED_USER}",
    "updatedUser": "{UPDATED_USER}",
    "updated": 1494349962314,
    "status": "success",
    "errors": [],
    "version": "1.0.1",
    "availableDates": {}
}
```

**響應——失敗**

如果失敗，可從回應中擷取「錯誤」，並在ETL工具上呈現為錯誤訊息。

```json
"{BATCH_ID}": {
    "imsOrg": "{IMS_ORG}",
    "created": 1494349962314,
    "createdClient": "{API_KEY}",
    "createdUser": "{CREATED_USER}",
    "updatedUser": "{UPDATED_USER}",
    "updated": 1494349962314,
    "status": "failure",
    "errors": [
        {
            "code": "200",
            "description": "Error in validating schema for file: 'adl://dataLake.azuredatalakestore.net/connectors-dev/stage/BATCHID/dataSetId/contact.csv' with errorMessage=adl://dataLake.azuredatalakestore.net/connectors-dev/stage/BATCHID/dataSetId/contact.csv is not a Parquet file. expected magic number at tail [80, 65, 82, 49] but found [57, 98, 55, 10] and errorType=java.lang.RuntimeException",
            "rows": []
        }
    ],
    "version": "1.0.1",
    "availableDates": {}
}
```

## 增量與快照資料、事件與配置檔案

資料可以用二乘二的矩陣表示，如下所示：

| 增量事件 | 增量配置檔案 |
|-------------------------------|----------------------|
| 快照事件（不太可能） | 快照配置檔案 |

事件資料通常在每行都有索引時間戳列時顯示。

描述檔資料通常是在資料中沒有時間戳記，且每一列都可由主／複合索引鍵識別時。

增量資料是只有新的／更新的資料才會進入系統並附加到資料集中的當前資料的位置。

快照資料是指所有資料進入系統並替換資料集中的部分或全部先前資料時。

對於增量事件，ETL工具應使用批次實體的可用日期／建立日期。 若是推播服務，則不會顯示可用日期，因此工具會使用批次建立／更新日期來標籤增量。 需要處理每批增量事件。

對於增量配置檔案，ETL工具將使用批次實體的建立／更新日期。 通常每批增量配置檔案資料都需要處理。

快照事件由於資料的龐大規模而極不可能發生。 但是，如果需要這個工具，ETL工具只能挑選最後一個批次進行處理。

使用快照配置檔案時，ETL工具將必須選擇到達系統的最後一批資料。 但如果要求追蹤變更版本，則所有批次都必須處理。 在ETL過程中執行重複資料消除處理將有助於控制儲存成本。

## 批次重播和資料重新處理

當客戶發現在過去的n天中，ETL處理的資料未如預期發生或來源資料本身可能不正確時，可能需要進行批次重播和資料重新處理。

為此，客戶端的資料管理員將使用平台UI刪除包含損壞資料的批。 然後，ETL可能需要重新執行，因此會重新填入正確的資料。 如果來源本身有損壞的資料，資料工程師／管理員將需要更正來源批次並重新收錄資料（可以是透過Adobe Experience Platform或ETL連接器）。

根據所生成的資料類型，資料工程師可以選擇從某些資料集中刪除單個批或所有批。 資料將依據「體驗平台」方針移除／封存。

清除資料的ETL功能很可能很重要。

清除完成後，用戶端管理員必須重新設定Adobe Experience Platform，才能從刪除批次時開始重新處理核心服務。

## 並行批處理

根據客戶的決定，資料管理員／工程師可以根據特定資料集的特性，以順序或並行方式來決定提取、轉換和載入資料。 這也將以用戶端使用轉換後的資料來定位的使用案例為基礎。

例如，如果客戶端持續存在可更新的持久性儲存，並且事件的順序或順序很重要，則客戶端可能需要使用循序ETL轉換嚴格處理作業。

在其他情況下，下游應用程式／進程可以使用指定的時間戳在內部排序時，可以處理順序錯誤的資料。 在這些情況下，並行ETL轉換可能可以改善處理時間。

對於源批，它將再次依賴於客戶機首選項和消費者約束。 如果源資料可以並行提取而不考慮行的攝政／排序，則轉換過程可以建立具有較高並行度的處理批（基於亂序處理的優化）。 但是，如果轉換必須遵循時間戳記或變更優先順序，資料存取API或ETL工具排程器／呼叫將必須確保批次不會在可能的情況下順序錯誤處理。

## 遞延

遞延是指輸入資料尚未完整到可傳送至下遊程式的程式，但日後可能可用的程式。 客戶將確定他們對資料窗口的個別容限，以便將來匹配和處理成本，以便通知他們決定在下次轉換執行中保留資料並重新處理資料，希望在保留窗口內的某個將來時間豐富和協調／銜接資料。 此週期一直持續，直到行被充分處理或認為過時，才能繼續投資。 每個迭代都將生成延遲資料，這是以前迭代中所有延遲資料的超集。

Adobe Experience Platform目前不會識別延遲資料，因此用戶端實作必須仰賴ETL和資料集手動組態，才能在平台中建立另一個資料集，以鏡像可用來保留延遲資料的來源資料集。 在這種情況下，延遲的資料將類似於快照資料。 在ETL轉換的每次執行中，源資料將與延遲資料相結合，並被發送以進行處理。

## 更改日誌

| 日期 | 動作 | 說明 |
| ---- | ------ | ----------- |
| 2019-01-19 | 已從資料集移除「欄位」屬性 | 資料集以前包含「欄位」屬性，該屬性包含模式的副本。 不應再使用此功能。 如果找到&quot;fields&quot;屬性，則應忽略它，並改用&quot;oscementedSchema&quot;或&quot;schemaRef&quot;。 |
| 2019-03-15 | &quot;schemaRef&quot;屬性添加到資料集 | 資料集的&quot;schemaRef&quot;屬性包含參照資料集所依據之XDM架構的URI，並代表資料集可使用的所有潛在欄位。 |
| 2019-03-15 | 所有使用者識別碼都對應至&quot;identityMap&quot;屬性 | 「identityMap」是主體所有唯一識別碼的封裝，例如CRM ID、ECID或忠誠度方案ID。 此地圖由 [Identity Service使用](../identity-service/home.md) ，以解析主體的所有已知和匿名身份，為每位使用者建立單一身分圖。 |
| 2019-05-30 | EOL和從資料集中刪除「模式」屬性 | 資料集「架構」屬性使用目錄API中已過時的端點，提供 `/xdms` 架構的參考連結。 這已由&quot;schemaRef&quot;取代，該&quot;schemaRef&quot;提供新架構註冊表API中引用的架構的&quot;id&quot;、&quot;version&quot;和&quot;contentType&quot;。 |