---
description: 此頁面是用來透過Adobe Experience Platform Destination SDK建立目的地伺服器的API呼叫的範例。
title: 建立目的地伺服器組態
exl-id: 5c6b6cf5-a9d9-4c8a-9fdc-f8a95ab2a971
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '2036'
ht-degree: 5%

---

# 建立目的地伺服器組態

使用Destination SDK建立自己的目的地時，第一步是建立目的地伺服器。 目的地伺服器包含[伺服器](../../functionality/destination-server/server-specs.md)和[範本](../../functionality/destination-server/templating-specs.md)規格的組態選項、[訊息格式](../../functionality/destination-server/message-format.md)以及[檔案格式](../../functionality/destination-server/file-formatting.md)選項（適用於檔案型目的地）。

此頁面是您可用來使用`/authoring/destination-servers` API端點建立自己的目的地伺服器的API要求與裝載範例。

如需可透過此端點設定的功能的詳細說明，請參閱以下文章：

* [以Destination SDK建立的目的地的伺服器規格](../../../destination-sdk/functionality/destination-server/server-specs.md)
* [使用Destination SDK建立之目的地的範本規格](../../../destination-sdk/functionality/destination-server/templating-specs.md)
* [訊息格式](../../../destination-sdk/functionality/destination-server/message-format.md)
* [檔案格式設定](../../../destination-sdk/functionality/destination-server/file-formatting.md)

>[!IMPORTANT]
>
>Destination SDK支援的所有引數名稱和值都區分大小寫&#x200B;****。 為避免區分大小寫錯誤，請完全依照檔案中所示使用引數名稱和值。

## 開始使用目的地伺服器API作業 {#get-started}

繼續之前，請檢閱[快速入門手冊](../../getting-started.md)以取得重要資訊，您必須瞭解這些資訊才能成功呼叫API，包括如何取得必要的目的地撰寫許可權和必要的標頭。

## 建立目的地伺服器組態 {#create}

您可以對`/authoring/destination-servers`端點發出`POST`要求，以建立新的目的地伺服器組態。

>[!TIP]
>
>**API端點**： `platform.adobe.io/data/core/activation/authoring/destination-servers`

**API格式**

```http
POST /authoring/destination-servers
```

視您建立的目的地型別而定，您需要設定稍有不同的目的地伺服器型別。

### 建立靜態綱要目的地伺服器 {#static-destination-servers}

在下列標籤中檢視使用[靜態結構描述](../../functionality/destination-configuration/schema-configuration.md#attributes-schema)之目的地的目的地伺服器範例。

以下範例裝載包含每種目的地伺服器型別支援的所有引數。 您不需要在請求中包含所有引數。 可根據您的需求自訂裝載。

選取底下的每個標籤以檢視對應的API請求。

>[!BEGINTABS]

>[!TAB 即時（串流）]

**建立即時（串流）目的地伺服器**

您需要建立類似於以下所示的即時（串流）目的地伺服器，以設定即時（串流） API型整合。

+++要求

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Moviestar destination server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{customerData.region}}/items"
      }
   },
   "httpTemplate":{
      "httpMethod":"POST",
      "requestBody":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{ \"attributes\": [ {% for ns in [\"external_id\", \"yourdestination_id\"] %} {% if input.profile.identityMap[ns] is not empty and first_namespace_encountered %} , {% endif %} {% set first_namespace_encountered = true %} {% for identity in input.profile.identityMap[ns]%} { \"{{ ns }}\": \"{{ identity.id }}\" {% if input.profile.segmentMembership.ups is not empty %} , \"AEPSegments\": { \"add\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"realized\" or segment.value.status == \"existing\" %} {% if added_segment_found %} , {% endif %} {% set added_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ], \"remove\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"exited\" %} {% if removed_segment_found %} , {% endif %} {% set removed_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ] } {% set removed_segment_found = false %} {% set added_segment_found = false %} {% endif %} {% if input.profile.attributes is not empty %} , {% endif %} {% for attribute in input.profile.attributes %} \"{{ attribute.key }}\": {% if attribute.value is empty %} null {% else %} \"{{ attribute.value.value }}\" {% endif %} {% if not loop.last%} , {% endif %} {% endfor %} } {% if not loop.last %} , {% endif %} {% endfor %} {% endfor %} ] }"
      },
      "contentType":"application/json"
   }
}
```

| 參數 | 類型 | 說明 |
| -------- | ----------- | ----------- |
| `name` | 字串 | *必要。*&#x200B;代表您伺服器的易記名稱，僅對Adobe可見。 合作夥伴或客戶看不到此名稱。 範例`Moviestar destination server`。 |
| `destinationServerType` | 字串 | *必要。針對即時（串流）目的地，*&#x200B;設為`URL_BASED`。 |
| `urlBasedDestination.url.templatingStrategy` | 字串 | *必要。* <ul><li>如果Adobe需要轉換下面`value`欄位中的URL，請使用`PEBBLE_V1`。 如果您有類似`https://api.moviestar.com/data/{{customerData.region}}/items`的端點，其中`region`部分可以因客戶而異，請使用此選項。 在此情況下，您也需要將`region`設定為[目的地設定](../destination-configuration/create-destination-configuration.md)中的[客戶資料欄位](../../functionality/destination-configuration/customer-data-fields.md)。 </li><li> 如果Adobe端不需要轉換，例如，如果您有類似`https://api.moviestar.com/data/items`的端點，請使用`NONE`。</li></ul> |
| `urlBasedDestination.url.value` | 字串 | *必要。*&#x200B;填入Experience Platform應連線的API端點位址。 |
| `httpTemplate.httpMethod` | 字串 | *必要。* Adobe將在伺服器呼叫中使用的方法。 選項為`GET`、`PUT`、`POST`、`DELETE`、`PATCH`。 |
| `httpTemplate.requestBody.templatingStrategy` | 字串 | *必要。*&#x200B;使用`PEBBLE_V1`。 |
| `httpTemplate.requestBody.value` | 字串 | *必要。*&#x200B;此字串是字元逸出版本，可將Platform客戶的資料轉換為您服務預期的格式。<br> <ul><li> 如需如何寫入範本的詳細資訊，請閱讀[使用範本區段](../../functionality/destination-server/message-format.md#using-templating)。 </li><li> 如需字元逸出的詳細資訊，請參閱[RFC JSON標準第7節](https://tools.ietf.org/html/rfc8259#section-7)。 </li><li> 如需簡單轉換的範例，請參閱[設定檔屬性](../../functionality/destination-server/message-format.md#attributes)轉換。 </li></ul> |
| `httpTemplate.contentType` | 字串 | *必要。*&#x200B;您的伺服器接受的內容型別。 此值很可能為`application/json`。 |

{style="table-layout:auto"}

+++

+++回應

成功的回應會傳回HTTP狀態200以及您新建立的目的地伺服器組態的詳細資料。

+++

>[!TAB Amazon S3]

**建立Amazon S3目的地伺服器**

您必須建立類似於下列設定檔案式[!DNL Amazon S3]目的地時所顯示的[!DNL Amazon S3]目的地伺服器。

+++要求

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "name": "S3 destination",
    "destinationServerType": "FILE_BASED_S3",
    "fileBasedS3Destination": {
        "bucket": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.bucket}}"
        },
        "path": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.path}}"
        }
    },
    "fileConfigurations": {
        "compression": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.compression}}"
        },
        "fileType": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.fileType}}"
        },
        "csvOptions": {
            "quote": {
                "templatingStrategy": "NONE",
                "value": "\""
            },
            "quoteAll": {
                "templatingStrategy": "NONE",
                "value": "false"
            },
            "escape": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "escapeQuotes": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "header": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreLeadingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreTrailingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "nullValue": {
                "templatingStrategy": "NONE",
                "value": ""
            },
            "dateFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd"
            },
            "timestampFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd'T':mm:ss[.SSS][XXX]"
            },
            "charToEscapeQuoteEscaping": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "emptyValue": {
                "templatingStrategy": "NONE",
                "value": ""
            }
        }
    }
}
```

| 參數 | 類型 | 說明 |
|---|---|---|
| `name` | 字串 | 目的地連線的名稱。 |
| `destinationServerType` | 字串 | 根據您的目的地平台設定此值。 針對[!DNL Amazon S3]，請將此項設為`FILE_BASED_S3`。 |
| `fileBasedS3Destination.bucket.templatingStrategy` | 字串 | *必要。*&#x200B;使用`PEBBLE_V1`。 |
| `fileBasedS3Destination.bucket.value` | 字串 | 此目的地要使用的[!DNL Amazon S3]儲存貯體的名稱。 |
| `fileBasedS3Destination.path.templatingStrategy` | 字串 | *必要。*&#x200B;使用`PEBBLE_V1`。 |
| `fileBasedS3Destination.path.value` | 字串 | 目的地資料夾的路徑，此資料夾將裝載匯出的檔案。 |
| `fileConfigurations` | 不適用 | 如需如何設定這些設定的詳細資訊，請參閱[檔案格式設定](../../functionality/destination-server/file-formatting.md)。 |

{style="table-layout:auto"}

+++

+++回應

成功的回應會傳回HTTP狀態200以及您新建立的目的地伺服器組態的詳細資料。

+++

>[!TAB SFTP]

**建立[!DNL SFTP]目的地伺服器**

您必須建立類似於下列設定檔案式[!DNL SFTP]目的地時所顯示的[!DNL SFTP]目的地伺服器。

+++要求

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"File-based SFTP destination server",
   "destinationServerType":"FILE_BASED_SFTP",
   "fileBasedSFTPDestination":{
      "rootDirectory":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.rootDirectory}}"
      }, 
      "port": 22,
      "encryptionMode" : "PGP"
   },
    "fileConfigurations": {
        "compression": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.compression}}"
        },
        "fileType": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.fileType}}"
        },
        "csvOptions": {
            "quote": {
                "templatingStrategy": "NONE",
                "value": "\""
            },
            "quoteAll": {
                "templatingStrategy": "NONE",
                "value": "false"
            },
            "escape": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "escapeQuotes": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "header": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreLeadingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreTrailingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "nullValue": {
                "templatingStrategy": "NONE",
                "value": ""
            },
            "dateFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd"
            },
            "timestampFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd'T':mm:ss[.SSS][XXX]"
            },
            "charToEscapeQuoteEscaping": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "emptyValue": {
                "templatingStrategy": "NONE",
                "value": ""
            }
        }
    }
}
```

| 參數 | 類型 | 說明 |
|---|---|---|
| `name` | 字串 | 目的地連線的名稱。 |
| `destinationServerType` | 字串 | 根據您的目的地平台設定此值。 針對[!DNL SFTP]目的地，請將此專案設為`FILE_BASED_SFTP`。 |
| `fileBasedSFTPDestination.rootDirectory.templatingStrategy` | 字串 | *必要。*&#x200B;使用`PEBBLE_V1`。 |
| `fileBasedSFTPDestination.rootDirectory.value` | 字串 | 目的地儲存體的根目錄。 |
| `fileBasedSFTPDestination.hostName.templatingStrategy` | 字串 | *必要。*&#x200B;使用`PEBBLE_V1`。 |
| `fileBasedSFTPDestination.hostName.value` | 字串 | 目的地儲存體的主機名稱。 |
| `port` | 整數 | SFTP檔案伺服器連線埠。 |
| `encryptionMode` | 字串 | 指示是否使用檔案加密。 支援的值： <ul><li>PGP</li><li>None</li></ul> |
| `fileConfigurations` | 不適用 | 如需如何設定這些設定的詳細資訊，請參閱[檔案格式設定](../../functionality/destination-server/file-formatting.md)。 |

{style="table-layout:auto"}

+++

+++回應

成功的回應會傳回HTTP狀態200以及您新建立的目的地伺服器組態的詳細資料。

+++

>[!TAB Azure Data Lake儲存體]

**建立[!DNL Azure Data Lake Storage]目的地伺服器**

您必須建立類似於下列設定檔案式[!DNL Azure Data Lake Storage]目的地時所顯示的[!DNL Azure Data Lake Storage]目的地伺服器。

+++要求

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"ADLS destination server",
   "destinationServerType":"FILE_BASED_ADLS_GEN2",
   "fileBasedAdlsGen2Destination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   },
  "fileConfigurations": {
        "compression": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.compression}}"
        },
        "fileType": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.fileType}}"
        },
        "csvOptions": {
            "quote": {
                "templatingStrategy": "NONE",
                "value": "\""
            },
            "quoteAll": {
                "templatingStrategy": "NONE",
                "value": "false"
            },
            "escape": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "escapeQuotes": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "header": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreLeadingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreTrailingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "nullValue": {
                "templatingStrategy": "NONE",
                "value": ""
            },
            "dateFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd"
            },
            "timestampFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd'T':mm:ss[.SSS][XXX]"
            },
            "charToEscapeQuoteEscaping": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "emptyValue": {
                "templatingStrategy": "NONE",
                "value": ""
            }
        }
    }
}
```

| 參數 | 類型 | 說明 |
|---|---|---|
| `name` | 字串 | 目的地連線的名稱。 |
| `destinationServerType` | 字串 | 根據您的目的地平台設定此值。 針對[!DNL Azure Data Lake Storage]目的地，請將此專案設為`FILE_BASED_ADLS_GEN2`。 |
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | 字串 | *必要。*&#x200B;使用`PEBBLE_V1`。 |
| `fileBasedAdlsGen2Destination.path.value` | 字串 | 目的地資料夾的路徑，此資料夾將裝載匯出的檔案。 |
| `fileConfigurations` | 不適用 | 如需如何設定這些設定的詳細資訊，請參閱[檔案格式設定](../../functionality/destination-server/file-formatting.md)。 |

{style="table-layout:auto"}

+++

+++回應

成功的回應會傳回HTTP狀態200以及您新建立的目的地伺服器組態的詳細資料。

+++

>[!TAB Azure Blob儲存體]

**建立[!DNL Azure Blob Storage]目的地伺服器**

您必須建立類似於下列設定檔案式[!DNL Azure Blob Storage]目的地時所顯示的[!DNL Azure Blob Storage]目的地伺服器。

+++要求

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Blob destination server",
   "destinationServerType":"FILE_BASED_AZURE_BLOB",
   "fileBasedAzureBlobDestination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      },
      "container":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.container}}"
      }
   },
  "fileConfigurations": {
        "compression": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.compression}}"
        },
        "fileType": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.fileType}}"
        },
        "csvOptions": {
            "quote": {
                "templatingStrategy": "NONE",
                "value": "\""
            },
            "quoteAll": {
                "templatingStrategy": "NONE",
                "value": "false"
            },
            "escape": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "escapeQuotes": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "header": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreLeadingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreTrailingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "nullValue": {
                "templatingStrategy": "NONE",
                "value": ""
            },
            "dateFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd"
            },
            "timestampFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd'T':mm:ss[.SSS][XXX]"
            },
            "charToEscapeQuoteEscaping": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "emptyValue": {
                "templatingStrategy": "NONE",
                "value": ""
            }
        }
    }
}
```

| 參數 | 類型 | 說明 |
|---|---|---|
| `name` | 字串 | 目的地連線的名稱。 |
| `destinationServerType` | 字串 | 根據您的目的地平台設定此值。 針對[!DNL Azure Blob Storage]目的地，請將此專案設為`FILE_BASED_AZURE_BLOB`。 |
| `fileBasedAzureBlobDestination.path.templatingStrategy` | 字串 | *必要。*&#x200B;使用`PEBBLE_V1`。 |
| `fileBasedAzureBlobDestination.path.value` | 字串 | 目的地資料夾的路徑，此資料夾將裝載匯出的檔案。 |
| `fileBasedAzureBlobDestination.container.templatingStrategy` | 字串 | *必要。*&#x200B;使用`PEBBLE_V1`。 |
| `fileBasedAzureBlobDestination.container.value` | 字串 | 此目的地要使用的[!DNL Azure Blob Storage]容器的名稱。 |
| `fileConfigurations` | 不適用 | 如需如何設定這些設定的詳細資訊，請參閱[檔案格式設定](../../functionality/destination-server/file-formatting.md)。 |

{style="table-layout:auto"}

+++

+++回應

成功的回應會傳回HTTP狀態200以及您新建立的目的地伺服器組態的詳細資料。

+++

>[!TAB 資料登陸區域(DLZ)]

**建立[!DNL Data Landing Zone (DLZ)]目的地伺服器**

您必須建立類似於下列設定檔案式[!DNL Data Landing Zone (DLZ)]目的地時所顯示的[!DNL Data Landing Zone (DLZ)]目的地伺服器。

+++要求

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"DLZ destination server",
   "destinationServerType":"FILE_BASED_DLZ",
   "fileBasedDlzDestination":{
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      },
      "useCase": "Your use case"
   },
   "fileConfigurations": {
        "compression": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.compression}}"
        },
        "fileType": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.fileType}}"
        },
        "csvOptions": {
            "quote": {
                "templatingStrategy": "NONE",
                "value": "\""
            },
            "quoteAll": {
                "templatingStrategy": "NONE",
                "value": "false"
            },
            "escape": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "escapeQuotes": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "header": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreLeadingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreTrailingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "nullValue": {
                "templatingStrategy": "NONE",
                "value": ""
            },
            "dateFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd"
            },
            "timestampFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd'T':mm:ss[.SSS][XXX]"
            },
            "charToEscapeQuoteEscaping": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "emptyValue": {
                "templatingStrategy": "NONE",
                "value": ""
            }
        }
    }
}
```

| 參數 | 類型 | 說明 |
|---|---|---|
| `name` | 字串 | 目的地連線的名稱。 |
| `destinationServerType` | 字串 | 根據您的目的地平台設定此值。 針對[!DNL Data Landing Zone]目的地，請將此專案設為`FILE_BASED_DLZ`。 |
| `fileBasedDlzDestination.path.templatingStrategy` | 字串 | *必要。*&#x200B;使用`PEBBLE_V1`。 |
| `fileBasedDlzDestination.path.value` | 字串 | 目的地資料夾的路徑，此資料夾將裝載匯出的檔案。 |
| `fileConfigurations` | 不適用 | 如需如何設定這些設定的詳細資訊，請參閱[檔案格式設定](../../functionality/destination-server/file-formatting.md)。 |

{style="table-layout:auto"}

+++

+++回應

成功的回應會傳回HTTP狀態200以及您新建立的目的地伺服器組態的詳細資料。

+++

>[!TAB Google雲端儲存空間]

**建立[!DNL Google Cloud Storage]目的地伺服器**

您必須建立類似於下列設定檔案式[!DNL Google Cloud Storage]目的地時所顯示的[!DNL Google Cloud Storage]目的地伺服器。

+++要求

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Google Cloud Storage Server",
   "destinationServerType":"FILE_BASED_GOOGLE_CLOUD",
   "fileBasedGoogleCloudStorageDestination":{
      "bucket":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.bucket}}"
      },
      "path":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{{customerData.path}}"
      }
   },
  "fileConfigurations": {
        "compression": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.compression}}"
        },
        "fileType": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.fileType}}"
        },
        "csvOptions": {
            "quote": {
                "templatingStrategy": "NONE",
                "value": "\""
            },
            "quoteAll": {
                "templatingStrategy": "NONE",
                "value": "false"
            },
            "escape": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "escapeQuotes": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "header": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreLeadingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreTrailingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "nullValue": {
                "templatingStrategy": "NONE",
                "value": ""
            },
            "dateFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd"
            },
            "timestampFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd'T':mm:ss[.SSS][XXX]"
            },
            "charToEscapeQuoteEscaping": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "emptyValue": {
                "templatingStrategy": "NONE",
                "value": ""
            }
        }
    }
}
```

| 參數 | 類型 | 說明 |
|---|---|---|
| `name` | 字串 | 目的地連線的名稱。 |
| `destinationServerType` | 字串 | 根據您的目的地平台設定此值。 針對[!DNL Google Cloud Storage]目的地，請將此專案設為`FILE_BASED_GOOGLE_CLOUD`。 |
| `fileBasedGoogleCloudStorageDestination.bucket.templatingStrategy` | 字串 | *必要。*&#x200B;使用`PEBBLE_V1`。 |
| `fileBasedGoogleCloudStorageDestination.bucket.value` | 字串 | 此目的地要使用的[!DNL Google Cloud Storage]儲存貯體的名稱。 |
| `fileBasedGoogleCloudStorageDestination.path.templatingStrategy` | 字串 | *必要。*&#x200B;使用`PEBBLE_V1`。 |
| `fileBasedGoogleCloudStorageDestination.path.value` | 字串 | 目的地資料夾的路徑，此資料夾將裝載匯出的檔案。 |
| `fileConfigurations` | 不適用 | 如需如何設定這些設定的詳細資訊，請參閱[檔案格式設定](../../functionality/destination-server/file-formatting.md)。 |

{style="table-layout:auto"}

+++

+++回應

成功的回應會傳回HTTP狀態200以及您新建立的目的地伺服器組態的詳細資料。

+++

>[!ENDTABS]

### 建立動態結構描述目的地伺服器 {#dynamic-schema-servers}

動態方案可讓您動態擷取支援的目標屬性，並根據您自己的API產生方案。 您必須先設定動態綱要的目的地伺服器，才能設定綱要。

在下方標籤中，檢視使用[動態結構描述](../../functionality/destination-configuration/schema-configuration.md#dynamic-schema-configuration)之目的地的目的地伺服器範例。

以下範例裝載包含動態結構描述伺服器所需的所有引數。

>[!BEGINTABS]

>[!TAB 動態結構描述伺服器]

**建立動態結構描述伺服器**

設定從您自己的API端點擷取設定檔方案的目的地時，您需要建立類似於以下顯示的動態方案伺服器。 相對於靜態結構描述，動態結構描述不會使用`profileFields`陣列。 動態方案會改用動態方案伺服器，此伺服器會連線至您自己的API，從其中擷取方案設定。

+++要求

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Dynamic Schema Server",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://YOUR_API_ENDPOINT/"
      }
   },
   "httpTemplate":{
      "httpMethod":"GET"
   },
   "responseFields":[
      {
         "templatingStrategy":"PEBBLE_V1",
         "value":"{\n    \"type\":\"object\",\n    \"title\": \"Contact Schema\",\n    \"properties\": {\n        {% for setDefinition in response.body.items %}\n            \"{{setDefinition.key}}\": {\n                \"title\" : \"{{setDefinition.name.value}}\",\n                \"type\" : \"object\",\n                \"properties\": {\n                    {% for attribute in setDefinition.attributes %}\n                        \"{{attribute.key}}\": {\n                            \"title\" : \"{{attribute.name.value}}\",\n                            \"type\" : \"string\"\n                        }\n                        {% if not loop.last %},{%endif%}\n                    {% endfor %}\n                }\n            }\n            {% if not loop.last %},{%endif%}\n        {% endfor %}\n    }\n}",
         "name":"schema"
      }
   ]
}
```

| 參數 | 類型 | 說明 |
| -------- | ----------- | ----------- |
| `name` | 字串 | *必要。*&#x200B;代表動態結構描述伺服器的易記名稱，僅對Adobe可見。 |
| `destinationServerType` | 字串 | *必要。動態結構描述伺服器的*&#x200B;設定為`URL_BASED`。 |
| `urlBasedDestination.url.templatingStrategy` | 字串 | *必要。* <ul><li>如果Adobe需要轉換下面`value`欄位中的URL，請使用`PEBBLE_V1`。 如果您有類似以下的端點，請使用此選項： `https://api.moviestar.com/data/{{customerData.region}}/items`。 </li><li> 如果Adobe端不需要轉換，例如，如果您有類似`https://api.moviestar.com/data/items`的端點，請使用`NONE`。</li></ul> |
| `urlBasedDestination.url.value` | 字串 | *必要。*&#x200B;填入Experience Platform應連線的API端點位址，並擷取結構描述欄位，以填入為啟動工作流程對應步驟中的目標欄位。 |
| `httpTemplate.httpMethod` | 字串 | *必要。* Adobe將在伺服器呼叫中使用的方法。 對於動態結構描述伺服器，請使用`GET`。 |
| `responseFields.templatingStrategy` | 字串 | *必要。*&#x200B;使用`PEBBLE_V1`。 |
| `responseFields.value` | 字串 | *必要。*&#x200B;此字串是字元逸出轉換範本，可將從合作夥伴API收到的回應轉換為將顯示在平台UI中的合作夥伴結構描述。<br> <ul><li> 如需如何寫入範本的詳細資訊，請閱讀[使用範本區段](../../functionality/destination-server/message-format.md#using-templating)。 </li><li> 如需字元逸出的詳細資訊，請參閱[RFC JSON標準第7節](https://tools.ietf.org/html/rfc8259#section-7)。 </li><li> 如需簡單轉換的範例，請參閱[設定檔屬性](../../functionality/destination-server/message-format.md#attributes)轉換。 </li></ul> |

{style="table-layout:auto"}

+++

+++回應

成功的回應會傳回HTTP狀態200以及您新建立的目的地伺服器組態的詳細資料。

+++


>[!ENDTABS]


### 建立動態下拉式清單目的地伺服器 {#dynamic-dropdown-servers}

根據您自己的API，使用[動態下拉式清單](../../functionality/destination-configuration/customer-data-fields.md#dynamic-dropdown-selectors)來動態擷取及填入下拉式清單客戶資料欄位。 例如，您可以擷取要用於目的地連線的現有使用者帳戶清單。

您必須先設定動態下拉式清單的目的地伺服器，才能設定動態下拉式清單客戶資料欄位。

請參閱下方標籤中的目的地伺服器範例，此範例是用來從API動態擷取要在下拉式選取器中顯示的值。

以下範例裝載包含動態結構描述伺服器所需的所有引數。

>[!BEGINTABS]

>[!TAB 動態下拉式伺服器]

**建立動態下拉式伺服器**

設定從您自己的API端點擷取下拉式客戶資料欄位值的目的地時，您需要建立類似於以下顯示的動態下拉式清單伺服器。

+++要求

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-servers \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"Server for dynamic dropdown",
   "destinationServerType":"URL_BASED",
   "urlBasedDestination":{
      "url":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"https://api.moviestar.com/data/{{customerData.users}}/items"
      }
   },
   "httpTemplate":{
      "httpMethod":"GET",
      "headers":[
         {
            "header":"Authorization",
            "value":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"My Bearer Token"
            }
         },
         {
            "header":"x-integration",
            "value":{
               "templatingStrategy":"PEBBLE_V1",
               "value":"{{customerData.integrationId}}"
            }
         },
         {
            "header":"Accept",
            "value":{
               "templatingStrategy":"NONE",
               "value":"application/json"
            }
         }
      ]
   },
   "responseFields":[
      {
         "templatingStrategy":"PEBBLE_V1",
         "value":"{% set list = [] %} {% for record in response.body %} {% set list = list|merge([{'name' : record.name, 'value' : record.id }]) %} {% endfor %}{{ {'list': list} | toJson | raw }}",
         "name":"list"
      }
   ]
}
```

| 參數 | 類型 | 說明 |
| -------- | ----------- | ----------- |
| `name` | 字串 | *必要。*&#x200B;代表您動態下拉式伺服器的易記名稱，僅對Adobe可見。 |
| `destinationServerType` | 字串 | *必要。動態下拉式伺服器的*&#x200B;設定為`URL_BASED`。 |
| `urlBasedDestination.url.templatingStrategy` | 字串 | *必要。* <ul><li>如果Adobe需要轉換下面`value`欄位中的URL，請使用`PEBBLE_V1`。 如果您有類似以下的端點，請使用此選項： `https://api.moviestar.com/data/{{customerData.region}}/items`。 </li><li> 如果Adobe端不需要轉換，例如，如果您有類似`https://api.moviestar.com/data/items`的端點，請使用`NONE`。</li></ul> |
| `urlBasedDestination.url.value` | 字串 | *必要。*&#x200B;填入Experience Platform應連線的API端點位址並擷取下拉式清單值。 |
| `httpTemplate.httpMethod` | 字串 | *必要。* Adobe將在伺服器呼叫中使用的方法。 對於動態下拉式伺服器，請使用`GET`。 |
| `httpTemplate.headers` | 物件 | *Optiona.l*&#x200B;包含連線至動態下拉式伺服器所需的任何標頭。 |
| `responseFields.templatingStrategy` | 字串 | *必要。*&#x200B;使用`PEBBLE_V1`。 |
| `responseFields.value` | 字串 | *必要。*&#x200B;此字串是字元逸出轉換範本，可將從API收到的回應轉換為將顯示在平台UI中的值。<br> <ul><li> 如需如何寫入範本的詳細資訊，請閱讀[使用範本區段](../../functionality/destination-server/message-format.md#using-templating)。 </li><li> 如需字元逸出的詳細資訊，請參閱[RFC JSON標準第7節](https://tools.ietf.org/html/rfc8259#section-7)。 |

{style="table-layout:auto"}

+++

+++回應

成功的回應會傳回HTTP狀態200以及您新建立的目的地伺服器組態的詳細資料。

+++

>[!ENDTABS]

## API錯誤處理 {#error-handling}

Destination SDK API端點遵循一般Experience Platform API錯誤訊息原則。 請參閱Platform疑難排解指南中的[API狀態碼](../../../../landing/troubleshooting.md#api-status-codes)和[請求標頭錯誤](../../../../landing/troubleshooting.md#request-header-errors)。

## 後續步驟 {#next-steps}

閱讀此檔案後，您現在知道如何透過Destination SDK`/authoring/destination-servers` API端點建立新的目的地伺服器。

若要深入瞭解您可以使用此端點的功能，請參閱下列文章：

* [擷取目的地伺服器設定](retrieve-destination-server.md)
* [更新目的地伺服器設定](update-destination-server.md)
* [刪除目的地伺服器設定](delete-destination-server.md)

若要瞭解此端點適用於目標製作程式的位置，請參閱下列文章：

* [使用Destination SDK設定串流目的地](../../guides/configure-destination-instructions.md#create-server-template-configuration)
* [使用Destination SDK來設定以檔案為基礎的目的地](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration)
