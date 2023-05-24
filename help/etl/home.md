---
keywords: Experience Platform；首頁；熱門主題；ETL;etl整合；ETL整合
solution: Experience Platform
title: 開發Adobe Experience PlatformETL整合
description: ETL整合指南概述了建立高效能、安全連接器以將資料Experience Platform和插入平台的一般步驟。
exl-id: 7d29b61c-a061-46f8-a31f-f20e4d725655
source-git-commit: 76ef5638316a89aee1c6fb33370af943228b75e1
workflow-type: tm+mt
source-wordcount: '4081'
ht-degree: 1%

---

# 開發Adobe Experience PlatformETL整合

ETL整合指南概述了建立高效能、安全連接器的一般步驟 [!DNL Experience Platform] 將資料導入 [!DNL Platform]。


- [[!DNL Catalog]](https://www.adobe.io/experience-platform-apis/references/catalog/)
- [[!DNL Data Access]](https://www.adobe.io/experience-platform-apis/references/data-access/)
- [[!DNL Batch Ingestion]](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/)
- [[!DNL Streaming Ingestion]](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/)
- [Experience PlatformAPI的驗證和授權](https://www.adobe.com/go/platform-api-authentication-en)
- [[!DNL Schema Registry]](https://www.adobe.io/experience-platform-apis/references/schema-registry/)

本指南還包括設計ETL連接器時使用的示例API調用，其中包含指向描述每個連接器的文檔的連結 [!DNL Experience Platform] 以及API的使用。

整合示例 [!DNL GitHub] 通過 [ETL生態系統整合參考代碼](https://github.com/adobe/acp-data-services-etl-reference) 下 [!DNL Apache] 許可證版本2.0。

## 工作流程

以下工作流圖提供了將Adobe Experience Platform元件與ETL應用程式和連接器整合的高級概述。

![](images/etl.png)

## Adobe Experience Platform元件

ETL連接器整合中涉及多個Experience Platform元件。 以下清單概述了幾個關鍵元件和功能：

- **AdobeIdentity Management系統**  — 提供Adobe服務驗證框架。
- **IMS組織**  — 擁有或許可產品和服務並允許其成員訪問的公司實體。
- **IMS用戶**  — 國際監測系統組織成員。 「組織與用戶」關係是多對多的關係。
- **[!DNL Sandbox]**  — 單個虛擬分區 [!DNL Platform] 例如，幫助開發和發展數字型驗應用。
- **資料發現**  — 將所攝取和轉換的資料的元資料記錄在 [!DNL Experience Platform]。
- **[!DNL Data Access]**  — 為用戶提供訪問其資料的介面 [!DNL Experience Platform]。
- **[!DNL Data Ingestion]**  — 將資料推送到 [!DNL Experience Platform] 與 [!DNL Data Ingestion] API。
- **[!DNL Schema Registry]**  — 定義和儲存描述要在中使用的資料結構的架構 [!DNL Experience Platform]。

## 入門 [!DNL Experience Platform] API

以下各節提供了您需要瞭解或掌握的其他資訊，以便成功撥打 [!DNL Experience Platform] API。

### 讀取示例API調用

本指南提供了示例API調用，以演示如何格式化請求。 這些包括路徑、必需的標頭和正確格式化的請求負載。 還提供了API響應中返回的示例JSON。 有關示例API調用文檔中使用的約定的資訊，請參見上的 [如何讀取示例API調用](../landing/troubleshooting.md#how-do-i-format-an-api-request) 的 [!DNL Experience Platform] 疑難解答指南。

### 收集所需標題的值

為了呼叫 [!DNL Platform] API，必須首先完成 [驗證教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份驗證教程將提供所有中每個必需標頭的值 [!DNL Experience Platform] API調用，如下所示：

- 授權：持 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

中的所有資源 [!DNL Experience Platform] 與特定虛擬沙箱隔離。 所有請求 [!DNL Platform] API需要一個標頭，該標頭指定操作將在以下位置進行的沙盒的名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有關中的沙箱的詳細資訊 [!DNL Platform]，請參見 [沙盒概述文檔](../sandboxes/home.md)。

包含負載(POST、PUT、PATCH)的所有請求都需要附加的標頭：

- 內容類型：應用程式/json

## 一般用戶流

要開始，ETL用戶將登錄到 [!DNL Experience Platform] 用戶介面(UI)，並使用標準連接器或推送服務連接器建立用於接收的資料集。

在UI中，用戶通過選擇資料集模式建立輸出資料集。 架構的選擇取決於所接收到的資料（記錄或時間序列）的類型 [!DNL Platform]。 通過按一下UI中的「方案」頁籤，用戶將能夠查看所有可用的方案，包括方案支援的行為類型。

在ETL工具中，用戶將在配置適當的連接（使用其憑據）後開始設計其映射轉換。 假定ETL工具已具有 [!DNL Experience Platform] 已安裝連接器（本《整合指南》中未定義進程）。

中提供了示例ETL工具和工作流的Mockups [ETL工作流](./workflow.md)。 雖然ETL工具的格式可能不同，但大多數都會公開類似的功能。

>[!NOTE]
>
>ETL連接器必須指定時間戳篩選器，以標籤要接收資料和偏移的日期（即要讀取資料的窗口）。 ETL工具應支援在此或另一個相關UI中獲取這兩個參數。 在Adobe Experience Platform，這些參數將映射到資料集的批處理對象中存在的可用日期（如果存在）或捕獲日期。

### 查看資料集清單

使用資料源進行映射，可以使用 [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/)。

您可以發出單個API請求以查看所有可用資料集(例如， `GET /dataSets`)，最佳做法是包括限制響應大小的查詢參數。

在請求完整資料集資訊的情況下，響應負載的大小可能超過3GB，這會降低整體效能。 因此，使用查詢參數只過濾所需資訊將產生 [!DNL Catalog] 查詢效率更高。

#### 清單篩選

篩選響應時，可以通過用「和」分隔參數(`&`)。 某些查詢參數接受以逗號分隔的值清單，如下面示例請求中的「屬性」篩選器。

[!DNL Catalog] 響應根據配置的限制自動計量，但「limit」查詢參數可用於定制約束並限制返回的對象數。 預配置 [!DNL Catalog] 響應限制：

- 如果未指定限制參數，則每個響應負載的最大對象數為20。
- 所有其他項的全局限制 [!DNL Catalog] 查詢是100個對象。
- 對於資料集查詢，如果使用屬性查詢參數請求可觀察模式，則返回的最大資料集數為20。
- 無效的限制參數(包括 `limit=0`)時遇到一個HTTP 400錯誤，該錯誤會列出正確的範圍。
- 如果限制或偏移作為查詢參數傳遞，則它們優先於作為標題傳遞的限制或偏移。

查詢參數在 [目錄服務概述](../catalog/home.md)。

**API格式**

```http
GET /catalog/dataSets
GET /catalog/dataSets?{filter1}={value1},{value2}&{filter2}={value3}
```

**要求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets?limit=3&properties=name,description,schemaRef" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

請參閱 [目錄服務概述](../catalog/home.md) 有關如何調用的詳細示例 [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/)。

**回應**

響應包括三個(`limit=3`)資料集，如 `properties` 查詢參數。

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

### 查看資料集架構

資料集的&quot;schemaRef&quot;屬性包含引用資料集所基於的XDM架構的URI。 XDM架構(「schemaRef」)表示資料集可以使用的所有潛在欄位，而不一定是正在使用的欄位（請參見下面的「可觀察的架構」）。

XDM模式是您在需要向用戶顯示可寫入的所有可用欄位的清單時使用的模式。

上一個響應對象中的第一個&quot;schemaRef.id&quot;值(`https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18`)是指向中的特定XDM架構的URI [!DNL Schema Registry]。 可通過對進行查找(GET)請求來檢索該模式 [!DNL Schema Registry] API。

>[!NOTE]
>
>&quot;schemaRef&quot;屬性替換現在不建議使用的&quot;schema&quot;屬性。 如果資料集中缺少&quot;schemaRef&quot;或者不包含值，則需要檢查是否存在&quot;schema&quot;屬性。 可以通過將「schemaRef」替換為「schema」 `properties` 查詢參數。 有關「架構」屬性的詳細資訊，請參見 [資料集「架構」屬性](#dataset-schema-property-deprecated---eol-2019-05-30) 的下界。

**API格式**

```http
GET /schemaregistry/tenant/schemas/{url encoded schemaRef.id}
```

**要求**

請求使用URL編碼 `id` 架構的URI（&quot;schemaRef.id&quot;屬性的值），並需要Accept標頭。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F274f17bc5807ff307a046bab1489fb18 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
```

響應格式取決於請求中發送的接受標頭的類型。 查找請求還需要 `version` 包含在「接受」標題中。 下表概述了可用於查找的接受標頭：

| Accept | 說明 |
| ------ | ----------- |
| `application/vnd.adobe.xed-id+json` | 列出(GET)請求、標題、ID和版本 |
| `application/vnd.adobe.xed-full+json; version={major version}` | $refs和allOf已解析，具有標題和說明 |
| `application/vnd.adobe.xed+json; version={major version}` | 帶有$ref和allOf的原始，有標題和說明 |
| `application/vnd.adobe.xed-notext+json; version={major version}` | 帶有$ref和allOf的原始，無標題或說明 |
| `application/vnd.adobe.xed-full-notext+json; version={major version}` | $refs和allOf已解析，無標題或說明 |
| `application/vnd.adobe.xed-full-desc+json; version={major version}` | 包含$refs和allOf已解析描述符 |

>[!NOTE]
>
>`application/vnd.adobe.xed-id+json` 和 `application/vnd.adobe.xed-full+json; version={major version}` 是最常用的「接受」標頭。 `application/vnd.adobe.xed-id+json` 在中列出資源 [!DNL Schema Registry] 因為它只返回&quot;title&quot;、&quot;id&quot;和&quot;version&quot;。 `application/vnd.adobe.xed-full+json; version={major version}` 首選於查看特定資源（按其「id」），因為它返回所有欄位（嵌套在「屬性」下）以及標題和說明。

**回應**

返回的JSON架構描述了結構和欄位級資訊（「type」、「format」、「minimum」、「maximum」等） 序列化為JSON。 如果使用JSON以外的序列化格式進行接收（如Parce或Scala），則 [架構註冊表指南](../xdm/tutorials/create-schema-api.md) 包含一個表，該表顯示所需的JSON類型(&quot;meta:xdmType&quot;)及其以其他格式表示的對應形式。

和這張桌子一樣， [!DNL Schema Registry] 《開發人員指南》包含使用 [!DNL Schema Registry] API。

### 資料集「架構」屬性（不建議使用 — EOL 2019-05-30）

資料集可能包含「架構」屬性，該屬性現在已棄用，並且暫時可用，以便向後相容。 例如，清單(GET)請求與先前所做的請求類似，其中，將「schema」替換 `properties` 查詢參數，可能返回以下內容：

```json
{
  "5ba9452f7de80400007fc52a": {
    "name": "Sample Dataset 1",
    "description": "Description of Sample Dataset 1.",
    "schema": "@/xdms/context/person"
  }
}
```

如果填充了資料集的&quot;schema&quot;屬性，則表明該模式已被棄用 `/xdms` schema和（如果支援）,ETL連接器應將「schema」屬性中的值與 `/xdms` 終結點（不建議使用的終結點） [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/))以檢索舊架構。

**API格式**

```http
GET /catalog/{"schema" property without the "@"}
```

**要求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/xdms/context/person?expansion=xdm" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

>[!NOTE]
>
>可選查詢參數， `expansion=xdm`，指示API完全展開和串聯所有引用的架構。 當向用戶顯示所有潛在欄位的清單時，您可能希望執行此操作。

**回應**

與 [查看資料集模式](#view-dataset-schema)，響應包含描述資料的結構和欄位級資訊的JSON架構，序列化為JSON。

>[!NOTE]
>
>當&quot;schema&quot;欄位為空或完全不存在時，連接器應讀取&quot;schemaRef&quot;欄位，並使用 [架構註冊表API](https://www.adobe.io/experience-platform-apis/references/schema-registry/) 如前面的步驟所示 [查看資料集模式](#view-dataset-schema)。

### &quot;ovebaibleSchema&quot;屬性

資料集的&quot;ovebableSchema&quot;屬性具有與XDM架構JSON相匹配的JSON結構。 &quot;ovebailableSchema&quot;包含傳入輸入檔案中存在的欄位。 將資料寫入 [!DNL Experience Platform]，用戶不需要使用目標架構中的每個欄位。 相反，它們應僅提供正在使用的欄位。

可觀察模式是讀取資料或顯示可用於讀取/映射的欄位清單時使用的模式。

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

ETL應用程式可提供預覽資料([ETL工作流中的「圖8」](./workflow.md))。 資料存取API提供了多個預覽資料的選項。

其他資訊，包括使用資料存取API預覽資料的逐步指導，可在 [資料存取教程](../data-access/tutorials/dataset-data.md)。

### 使用「屬性」查詢參數獲取資料集詳細資訊

如上面的步驟所示： [查看資料集清單](#view-list-of-datasets)，可以使用「屬性」查詢參數請求「檔案」。

您可以參考 [目錄服務概述](../catalog/home.md) 的子菜單。

**API格式**

```http
GET /catalog/dataSets?limit={value}&properties={value}
```

**要求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets?limit=1&properties=files" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

**回應**

響應將包括一個資料集(`limit=1`)顯示「files」屬性。

```json
{
  "5bf479a6a8c862000050e3c7": {
    "files": "@/dataSets/5bf479a6a8c862000050e3c7/views/5bf479a654f52014cfffe7f1/files"
  }
}
```

### 使用「files」屬性列出資料集檔案

您還可以使用「檔案」屬性使用GET請求獲取檔案詳細資訊。

**API格式**

```http
GET /catalog/dataSets/{DATASET_ID}/views/{VIEW_ID}/files
```

**要求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets/5bf479a6a8c862000050e3c7/views/5bf479a654f52014cfffe7f1/files" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**回應**

響應將資料集檔案ID作為頂級屬性，檔案詳細資訊包含在資料集檔案ID對象中。

```json
{
    "194e89b976494c9c8113b968c27c1472-1": {
        "batchId": "194e89b976494c9c8113b968c27c1472",
        "dataSetViewId": "5bf479a654f52014cfffe7f1",
        "imsOrg": "{ORG_ID}",
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
        "imsOrg": "{ORG_ID}",
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
        "imsOrg": "{ORG_ID}",
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

### 獲取檔案詳細資訊

在先前響應中返回的資料集檔案ID可以用在GET請求中，以通過 [!DNL Data Access] API。

的 [資料存取概述](../data-access/home.md) 包含有關如何使用的詳細資訊 [!DNL Data Access] API。

**API格式**

```http
GET /export/files/{DATASET_FILE_ID}
```

**要求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/ea40946ac03140ec8ac4f25da360620a-1" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
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

「href」屬性可用於通過 [[!DNL Data Access API]](../data-access/home.md)。

**API格式**

```http
GET /export/files/{FILE_ID}?path={FILE_NAME}.{FILE_FORMAT}
```

**要求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/ea40946ac03140ec8ac4f25da360620a-1?path=samplefile.parquet" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

對上述請求的響應將包含檔案內容的預覽。

有關 [!DNL Data Access] API（包括詳細的請求和響應）可在 [資料存取概述](../data-access/home.md)。

### 從資料集獲取&quot;fileDescription&quot;

目標元件作為已轉換資料的輸出，資料工程師將選擇輸出資料集([ETL工作流中的「圖12」](workflow.md))。 XDM模式與輸出資料集關聯。 要寫入的資料將由資料集實體的「fileDescription」屬性從資料發現API中標識。 可以使用資料集ID(`{DATASET_ID}`)。 JSON響應中的&quot;fileDescription&quot;屬性將提供請求的資訊。

**API格式**

```shell
GET /catalog/dataSets/{DATASET_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{DATASET_ID}` | 的 `id` 您嘗試訪問的資料集的值。 |

**要求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets/59c93f3da7d0c00000798f68" \
-H "accept: application/json" \
-H "x-gw-ims-org-id: {ORG_ID}" \
-H "x-sandbox-name: {SANDBOX_NAME}" \
-H "Authorization: Bearer {ACCESS_TOKEN}" \
-H "x-api-key: {API_KEY}"
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

資料將寫入 [!DNL Experience Platform] 使用 [批處理接收API](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/)。  資料寫入是一個非同步過程。 將資料寫入Adobe Experience Platform時，只有在完全寫入資料後，才會建立批處理並標籤為成功。

資料 [!DNL Experience Platform] 應該以鑲木檔案的形式寫。

## 執行階段

當執行開始時，連接器（如源元件中定義）將從中讀取資料 [!DNL Experience Platform] 使用 [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/)。 轉換過程將讀取特定時間範圍內的資料。 在內部，它將查詢成批的源資料集。 在查詢時，它將使用參數化（對時間系列資料或增量資料滾動）開始日期和列出這些批的資料集檔案，並開始對這些資料集檔案請求資料。

### 示例轉換

的 [示例ETL轉換](./transformations.md) 文檔包含許多示例轉換，包括身份處理和資料類型映射。 請使用這些轉換以供參考。

### 從中讀取資料 [!DNL Experience Platform]

使用 [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/)，您可以提取指定開始時間和結束時間之間的所有批，並按建立順序對它們進行排序。

**要求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches?dataSet=DATASETID&createdAfter=START_TIMESTAMP&createdBefore=END_TIMESTAMP&sort=desc:created" \
  -H "Accept: application/json" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

有關篩選批的詳細資訊，請參閱 [資料存取教程](../data-access/tutorials/dataset-data.md)。

### 從批中獲取檔案

一旦您獲得要查找的批的ID(`{BATCH_ID}`)，可以通過 [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/)。  有關執行此操作的詳細資訊，請參閱 [[!DNL Data Access] 教程](../data-access/tutorials/dataset-data.md)。

**要求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/files" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

### 使用檔案ID訪問檔案

使用檔案的唯一ID(`{FILE_ID`) [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) 可用於訪問檔案的特定詳細資訊，包括其名稱、大小（以位元組為單位）以及下載該檔案的連結。

**要求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{FILE_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

響應可指向單個檔案或目錄。 有關每項的詳細資訊，請參見 [[!DNL Data Access] 教程](../data-access/tutorials/dataset-data.md)。

### 訪問檔案內容

的 [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) 可用於訪問特定檔案的內容。 要獲取內容，請使用返回的值進行GET請求 `_links.self.href` 使用檔案ID訪問檔案時。

**要求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{DATASET_FILE_ID}?path=filename1.csv" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

對此請求的響應包含檔案的內容。 有關詳細資訊（包括有關響應分頁的詳細資訊），請參閱 [如何通過資料存取API查詢資料](../data-access/tutorials/dataset-data.md) 教程。

### 驗證方案符合性記錄

當寫入資料時，用戶可以選擇根據XDM架構中定義的驗證規則來驗證資料。 有關架構驗證的詳細資訊，請參閱 [ETL生態系統整合參考代碼 [!DNL GitHub]](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md#validation)。

如果您使用的是上 [[!DNL GitHub]](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md)，可以使用此系統屬性在此實現中啟用模式驗證 `-DenableSchemaValidation=true`。

可以使用屬性(如 `minLength` 和 `maxlength` 對於弦， `minimum` 和 `maximum` 為整數等。 的 [架構註冊API開發人員指南](../xdm/api/getting-started.md) 包含一個表，該表概述了XDM類型和可用於驗證的屬性。

>[!NOTE]
>
>為各種 `integer` 類型是類型可支援的MIN和MAX值，但這些值可以進一步限制為所選的最小值和最大值。

### 建立批

一旦處理資料，ETL工具將將資料寫回 [!DNL Experience Platform] 使用 [批處理接收API](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/)。 在將資料添加到資料集之前，必須將其連結到批處理，該批處理稍後將上載到特定資料集。

**要求**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -d '{
        "datasetId":"{DATASET_ID}"
      }'
```

有關建立批的詳細資訊，包括示例請求和響應，請參見 [批處理接收概述](../ingestion/batch-ingestion/overview.md)。

### 寫入資料集

成功建立新批後，檔案可以上載到特定資料集。 可以在批處理中過帳多個檔案，直到其升級。 檔案可以使用Small File Upload API上傳；但是，如果檔案太大且超出了網關限制，則可以使用「大檔案上載API」。 有關使用大檔案和小檔案上載的詳細資訊，請參閱 [批處理接收概述](../ingestion/batch-ingestion/overview.md)。

**要求**

資料 [!DNL Experience Platform] 應該以鑲木檔案的形式寫。

```shell
curl -X PUT "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/dataSets/{DATASET_ID}/files/{FILE_NAME}.parquet" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id:{ORG_ID}" \
  -H "Authorization:Bearer ACCESS_TOKEN" \
  -H "x-api-key: API_KEY" \
  -H "content-type: application/octet-stream" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

### 標籤批上載完成

在所有檔案都上載到批後，可以發出批完成的信號。 通過這樣， [!DNL Catalog] 為已完成的檔案建立「DataSetFile」條目，並與生成批關聯。 的 [!DNL Catalog] 然後將批處理標籤為成功，這將觸發下游流以接收可用資料。

資料將首先降落在Adobe Experience Platform的登台位置，然後在編目和驗證後移至最終位置。 所有資料移到永久位置後，批將標籤為成功。

**要求**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

如果成功，響應將返回HTTP狀態200 OK ，且響應正文為空。

ETL工具將確保在讀取資料時記錄源資料集的時間戳。

在下次轉換執行中，ETL將開始請求先前保存的時間戳和所有向前的資料。

### 獲取上一批狀態

在ETL工具中運行新任務之前，必須確保已成功完成上一批。 的 [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) 提供了批特定選項，該選項提供了相關批的詳細資訊。

**要求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches?limit=1&sort=desc:created" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**回應**

如果上一批「狀態」值為「成功」，則可以計畫新任務，如下所示：

```json
"{BATCH_ID}": {
    "imsOrg": "{ORG_ID}",
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

### 按ID獲取上次批處理狀態

可通過 [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) 通過發出GET請求 `{BATCH_ID}`。 的 `{BATCH_ID}` 使用與建立批時返回的ID相同。

**要求**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID}" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**響應 — 成功**

以下響應顯示「成功」：

```json
"{BATCH_ID}": {
    "imsOrg": "{ORG_ID}",
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

**響應 — 失敗**

如果失敗，可以從響應中提取「錯誤」，並作為錯誤消息在ETL工具上顯示。

```json
"{BATCH_ID}": {
    "imsOrg": "{ORG_ID}",
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

## 增量與快照資料和事件與配置檔案

資料可以用兩個矩陣表示，如下所示：

| 增量事件 | 增量配置檔案 |
|-------------------------------|----------------------|
| 快照事件（不太可能） | 快照配置檔案 |

事件資料通常是在每行都有索引時間戳列時。

配置檔案資料通常在資料中沒有時間戳且每行都可由主/複合鍵標識時使用。

增量資料是指只有新/更新的資料才進入系統並附加到資料集中的當前資料。

快照資料是指所有資料進入系統並替換資料集中部分或全部以前的資料。

對於增量事件，ETL工具應使用批實體的可用日期/建立日期。 在推送服務中，可用日期將不存在，因此工具將使用批建立/更新日期來標籤增量。 需要處理每批增量事件。

對於增量配置檔案，ETL工具將使用批實體的建立/更新日期。 通常需要處理每批增量配置檔案資料。

由於資料的巨大規模，快照事件發生的可能性很小。 但是，如果需要此操作，則ETL工具只能選擇最後一個批處理。

使用快照配置檔案時，ETL工具將必須選擇到達系統中的最後一批資料。 但是，如果要求跟蹤更改的版本，則將要求處理所有批。 ETL進程內的重複資料消除處理將有助於控制儲存成本。

## 批重放和資料重新處理

如果客戶端發現在過去「n」天中，ETL處理的資料未按預期發生或源資料本身可能不正確，則可能需要進行批重放和資料重新處理。

為此，客戶端的資料管理員將使用 [!DNL Platform] UI：刪除包含損壞資料的批。 然後，可能需要重新運行ETL，從而重新填充正確的資料。 如果源本身有損壞的資料，則資料工程師/管理員需要更正源批處理並重新接收資料(可以是Adobe Experience Platform或通過ETL連接器)。

根據正在生成的資料類型，資料工程師可以選擇從某些資料集中刪除單個批或所有批。 資料將按照 [!DNL Experience Platform] 准則。

清除資料的ETL功能很可能很重要。

清除完成後，客戶端管理員將必須重新配置Adobe Experience Platform，以從刪除批次時開始重新開始核心服務的處理。

## 併發批處理

根據客戶機的決定，資料管理員/工程師可以根據特定資料集的特徵決定以順序或併發方式提取、轉換和載入資料。 這還將基於客戶端針對已轉換資料的使用情形。

例如，如果客戶端正在永續到可更新持久性儲存，並且事件的順序或順序很重要，則客戶端可能需要嚴格處理具有連續ETL轉換的作業。

在其他情況下，下游應用程式/進程可以使用指定的時間戳對順序錯誤的資料進行內部排序。 在這些情況下，並行ETL轉換可能可以改進處理時間。

對於源批，它將再次依賴於客戶端首選項和用戶約束。 如果源資料可以並行地拾取而不考慮行的攝政/排序，則轉換過程可以建立具有較高並行度的處理批（基於無序處理的優化）。 但是，如果轉換必須執行時間戳或更改優先順序，則資料存取API或ETL工具調度器/調用必須確保批處理不會在可能的情況下無序進行。

## 遞延

延遲是指輸入資料尚未足夠完整地發送到下游進程，但將來可能可用的過程。 客戶將確定其針對未來匹配的資料窗口的單個容差與處理成本，以通知他們在下次轉換執行中保留資料並重新處理資料的決定，希望在保留窗口內的將來某個時間對資料進行豐富和協調/縫合。 此週期一直持續，直到行得到充分處理或被視為過於陳舊而無法繼續投資。 每個迭代都將生成延遲資料，該資料是先前迭代中所有延遲資料的超集。

Adobe Experience Platform當前不標識延遲資料，因此客戶端實現必須依賴ETL和資料集手動配置在中建立另一個資料集 [!DNL Platform] 鏡像可用於保留延遲資料的源資料集。 在這種情況下，延遲資料將與快照資料類似。 在ETL轉換的每次執行中，源資料將與延遲資料相統一並發送以供處理。

## 更改日誌

| 日期 | 動作 | 說明 |
| ---- | ------ | ----------- |
| 2019-01-19 | 已從資料集中刪除&quot;fields&quot;屬性 | 資料集以前包含包含架構副本的「欄位」屬性。 不應再使用此功能。 如果找到&quot;fields&quot;屬性，則應忽略該屬性，改用&quot;overedSchema&quot;或&quot;schemaRef&quot;。 |
| 2019-03-15 | &quot;schemaRef&quot;屬性已添加到資料集 | 資料集的&quot;schemaRef&quot;屬性包含引用資料集所基於的XDM架構的URI，並表示資料集可以使用的所有潛在欄位。 |
| 2019-03-15 | 所有最終用戶標識符都映射到&quot;identityMap&quot;屬性 | 「identityMap」是主題的所有唯一標識符的封裝，如CRM ID、ECID或會員計畫ID。 此地圖由 [[!DNL Identity Service]](../identity-service/home.md) 解析主題的所有已知和匿名身份，為每個最終用戶形成單個身份圖。 |
| 2019-05-30 | EOL和從資料集中刪除&quot;schema&quot;屬性 | 資料集「schema」屬性使用不建議使用的 `/xdms` 端點 [!DNL Catalog] API。 已用「schemaRef」替換，該「schemaRef」提供新中引用的架構的「id」、「version」和「contentType」 [!DNL Schema Registry] API。 |
