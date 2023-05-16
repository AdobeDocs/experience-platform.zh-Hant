---
description: 本頁面是透過Adobe Experience Platform Destination SDK建立目的地伺服器所使用的API呼叫的範例。
title: 建立目標伺服器配置
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '1623'
ht-degree: 9%

---


# 建立目標伺服器配置

建立目的地伺服器是使用Destination SDK建立您自己的目的地的第一步。 目標伺服器包括 [伺服器](../../functionality/destination-server/server-specs.md) 和 [模板](../../functionality/destination-server/templating-specs.md) 規格， [訊息格式](../../functionality/destination-server/message-format.md)，和 [檔案格式](../../functionality/destination-server/file-formatting.md) 選項（適用於檔案型目的地）。

此頁面是API要求和裝載的範例，您可以用來使用 `/authoring/destination-servers` API端點。

如需可透過此端點設定之功能的詳細說明，請參閱下列文章：

* [使用Destination SDK建立的目的地的伺服器規格](../../../destination-sdk/functionality/destination-server/server-specs.md)
* [使用Destination SDK建立的目的地的範本規格](../../../destination-sdk/functionality/destination-server/templating-specs.md)
* [訊息格式](../../../destination-sdk/functionality/destination-server/message-format.md)
* [檔案格式設定](../../../destination-sdk/functionality/destination-server/file-formatting.md)

>[!IMPORTANT]
>
>Destination SDK支援的所有參數名稱和值均為 **區分大小寫**. 為避免區分大小寫錯誤，請使用參數名稱和值，如說明檔案所示。

## 目標伺服器API操作快速入門 {#get-started}

繼續之前，請檢閱 [快速入門手冊](../../getting-started.md) 若要成功呼叫API，需知的重要資訊，包括如何取得必要的目的地編寫權限和必要的標題。

## 建立目標伺服器配置 {#create}

您可以建立新的目標伺服器配置，方法是 `POST` 請求 `/authoring/destination-servers` 端點。

>[!TIP]
>
>**API端點**: `platform.adobe.io/data/core/activation/authoring/destination-servers`

**API格式**

```http
POST /authoring/destination-servers
```

根據您建立的目標類型，您需要配置稍微不同的目標伺服器類型。 請參閱下方標籤中，Destination SDK支援之每種目的地類型的目的地伺服器範例。

以下示例負載包括每個目標伺服器類型支援的所有參數。 您不需要將所有參數納入請求中。 可根據您的需求自訂裝載。

選取下方的每個標籤，以檢視對應的API請求。

>[!BEGINTABS]

>[!TAB 即時（串流）]

**建立即時（串流）目的地伺服器**

設定即時（串流）API型整合時，您需要建立與下方所示類似的即時（串流）目的地伺服器。

+++請求

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
| `name` | 字串 | *必填。* 代表您伺服器的好記名稱，只顯示給Adobe。 合作夥伴或客戶看不到此名稱。 範例 `Moviestar destination server`. |
| `destinationServerType` | 字串 | *必填。* 設為 `URL_BASED` 用於即時（串流）目的地。 |
| `urlBasedDestination.url.templatingStrategy` | 字串 | *必填.* <ul><li>使用 `PEBBLE_V1` 如果Adobe需要轉換 `value` 欄位。 如果您有這樣的端點，請使用此選項 `https://api.moviestar.com/data/{{customerData.region}}/items`，其中 `region` 部件可能因客戶而異。 在此情況下，您也需要設定 `region` as a [客戶資料欄位](../../functionality/destination-configuration/customer-data-fields.md) 在 [目的地配置](../destination-configuration/create-destination-configuration.md)。 </li><li> 使用 `NONE` 如果Adobe端不需要轉換，例如，如果您有如下的端點： `https://api.moviestar.com/data/items`.</li></ul> |
| `urlBasedDestination.url.value` | 字串 | *必填。* 填入Experience Platform應連線之API端點的位址。 |
| `httpTemplate.httpMethod` | 字串 | *必填。* Adobe將用於呼叫伺服器的方法。 選項包括 `GET`, `PUT`, `POST`, `DELETE`, `PATCH`. |
| `httpTemplate.requestBody.templatingStrategy` | 字串 | *必填。* 使用 `PEBBLE_V1`. |
| `httpTemplate.requestBody.value` | 字串 | *必填。* 此字串是字元逸出版本，可將Platform客戶的資料轉換為服務預期的格式。 <br> <ul><li> 如需如何編寫範本的資訊，請閱讀 [使用模板部分](../../functionality/destination-server/message-format.md#using-templating). </li><li> 如需字元逸出的詳細資訊，請參閱 [RFC JSON標準，第七節](https://tools.ietf.org/html/rfc8259#section-7). </li><li> 如需簡單轉換的範例，請參閱 [設定檔屬性](../../functionality/destination-server/message-format.md#attributes) 轉換。 </li></ul> |
| `httpTemplate.contentType` | 字串 | *必填。* 伺服器接受的內容類型。 此值很可能 `application/json`. |

{style="table-layout:auto"}

+++

+++回應

成功的回應會傳回HTTP狀態200，並包含您新建立之目標伺服器組態的詳細資訊。

+++

>[!TAB Amazon S3]

**建立Amazon S3目的地伺服器**

您需要建立 [!DNL Amazon S3] 目標伺服器類似於配置基於檔案的伺服器時顯示的伺服器 [!DNL Amazon S3] 目的地。

+++請求

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
| `destinationServerType` | 字串 | 根據您的目的地平台設定此值。 針對 [!DNL Amazon S3]將此項設為 `FILE_BASED_S3`. |
| `fileBasedS3Destination.bucket.templatingStrategy` | 字串 | *必填。* 使用 `PEBBLE_V1`. |
| `fileBasedS3Destination.bucket.value` | 字串 | 的名稱 [!DNL Amazon S3] 此目的地所使用的貯體。 |
| `fileBasedS3Destination.path.templatingStrategy` | 字串 | *必填。* 使用 `PEBBLE_V1`. |
| `fileBasedS3Destination.path.value` | 字串 | 將承載導出檔案的目標資料夾的路徑。 |
| `fileConfigurations` | 不適用 | 請參閱 [檔案格式設定](../../functionality/destination-server/file-formatting.md) 以取得如何設定這些設定的詳細資訊。 |

{style="table-layout:auto"}

+++

+++回應

成功的回應會傳回HTTP狀態200，並包含您新建立之目標伺服器組態的詳細資訊。

+++

>[!TAB SFTP]

**建立 [!DNL SFTP] 目的地伺服器**

您需要建立 [!DNL SFTP] 目標伺服器類似於配置基於檔案的伺服器時顯示的伺服器 [!DNL SFTP] 目的地。

+++請求

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
   "fileBasedSftpDestination":{
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
| `destinationServerType` | 字串 | 根據您的目的地平台設定此值。 針對 [!DNL SFTP] 目的地，請將此設為 `FILE_BASED_SFTP`. |
| `fileBasedSftpDestination.rootDirectory.templatingStrategy` | 字串 | *必填。* 使用 `PEBBLE_V1`. |
| `fileBasedSftpDestination.rootDirectory.value` | 字串 | 目標儲存的根目錄。 |
| `fileBasedSftpDestination.hostName.templatingStrategy` | 字串 | *必填。* 使用 `PEBBLE_V1`. |
| `fileBasedSftpDestination.hostName.value` | 字串 | 目標儲存的主機名。 |
| `port` | 整數 | SFTP檔案伺服器埠。 |
| `encryptionMode` | 字串 | 指示是否使用檔案加密。 支援的值： <ul><li>PGP</li><li>None</li></ul> |
| `fileConfigurations` | 不適用 | 請參閱 [檔案格式設定](../../functionality/destination-server/file-formatting.md) 以取得如何設定這些設定的詳細資訊。 |

{style="table-layout:auto"}

+++

+++回應

成功的回應會傳回HTTP狀態200，並包含您新建立之目標伺服器組態的詳細資訊。

+++

>[!TAB Azure資料湖儲存]

**建立 [!DNL Azure Data Lake Storage] 目的地伺服器**

您需要建立 [!DNL Azure Data Lake Storage] 目標伺服器類似於配置基於檔案的伺服器時顯示的伺服器 [!DNL Azure Data Lake Storage] 目的地。

+++請求

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
| `destinationServerType` | 字串 | 根據您的目的地平台設定此值。 針對 [!DNL Azure Data Lake Storage] 目的地，請將此設為 `FILE_BASED_ADLS_GEN2`. |
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | 字串 | *必填。* 使用 `PEBBLE_V1`. |
| `fileBasedAdlsGen2Destination.path.value` | 字串 | 將承載導出檔案的目標資料夾的路徑。 |
| `fileConfigurations` | 不適用 | 請參閱 [檔案格式設定](../../functionality/destination-server/file-formatting.md) 以取得如何設定這些設定的詳細資訊。 |

{style="table-layout:auto"}

+++

+++回應

成功的回應會傳回HTTP狀態200，並包含您新建立之目標伺服器組態的詳細資訊。

+++

>[!TAB Azure Blob 儲存體]

**建立 [!DNL Azure Blob Storage] 目的地伺服器**

您需要建立 [!DNL Azure Blob Storage] 目標伺服器類似於配置基於檔案的伺服器時顯示的伺服器 [!DNL Azure Blob Storage] 目的地。

+++請求

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
| `destinationServerType` | 字串 | 根據您的目的地平台設定此值。 針對 [!DNL Azure Blob Storage] 目的地，請將此設為 `FILE_BASED_AZURE_BLOB`. |
| `fileBasedAzureBlobDestination.path.templatingStrategy` | 字串 | *必填。* 使用 `PEBBLE_V1`. |
| `fileBasedAzureBlobDestination.path.value` | 字串 | 將承載導出檔案的目標資料夾的路徑。 |
| `fileBasedAzureBlobDestination.container.templatingStrategy` | 字串 | *必填。* 使用 `PEBBLE_V1`. |
| `fileBasedAzureBlobDestination.container.value` | 字串 | 的名稱 [!DNL Azure Blob Storage] 供此目的地使用的容器。 |
| `fileConfigurations` | 不適用 | 請參閱 [檔案格式設定](../../functionality/destination-server/file-formatting.md) 以取得如何設定這些設定的詳細資訊。 |

{style="table-layout:auto"}

+++

+++回應

成功的回應會傳回HTTP狀態200，並包含您新建立之目標伺服器組態的詳細資訊。

+++

>[!TAB 資料登錄區(DLZ)]

**建立 [!DNL Data Landing Zone (DLZ)] 目的地伺服器**

您需要建立 [!DNL Data Landing Zone (DLZ)] 目標伺服器類似於配置基於檔案的伺服器時顯示的伺服器 [!DNL Data Landing Zone (DLZ)] 目的地。

+++請求

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
| `destinationServerType` | 字串 | 根據您的目的地平台設定此值。 針對 [!DNL Data Landing Zone] 目的地，請將此設為 `FILE_BASED_DLZ`. |
| `fileBasedDlzDestination.path.templatingStrategy` | 字串 | *必填。*  使用 `PEBBLE_V1`. |
| `fileBasedDlzDestination.path.value` | 字串 | 將承載導出檔案的目標資料夾的路徑。 |
| `fileConfigurations` | 不適用 | 請參閱 [檔案格式設定](../../functionality/destination-server/file-formatting.md) 以取得如何設定這些設定的詳細資訊。 |

{style="table-layout:auto"}

+++

+++回應

成功的回應會傳回HTTP狀態200，並包含您新建立之目標伺服器組態的詳細資訊。

+++

>[!TAB Google雲端儲存空間]

**建立 [!DNL Google Cloud Storage] 目的地伺服器**

您需要建立 [!DNL Google Cloud Storage] 目標伺服器類似於配置基於檔案的伺服器時顯示的伺服器 [!DNL Google Cloud Storage] 目的地。

+++請求

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
| `destinationServerType` | 字串 | 根據您的目的地平台設定此值。 針對 [!DNL Google Cloud Storage] 目的地，請將此設為 `FILE_BASED_GOOGLE_CLOUD`. |
| `fileBasedGoogleCloudStorageDestination.bucket.templatingStrategy` | 字串 | *必填。*  使用 `PEBBLE_V1`. |
| `fileBasedGoogleCloudStorageDestination.bucket.value` | 字串 | 的名稱 [!DNL Google Cloud Storage] 此目的地所使用的貯體。 |
| `fileBasedGoogleCloudStorageDestination.path.templatingStrategy` | 字串 | *必填。* 使用 `PEBBLE_V1`. |
| `fileBasedGoogleCloudStorageDestination.path.value` | 字串 | 將承載導出檔案的目標資料夾的路徑。 |
| `fileConfigurations` | 不適用 | 請參閱 [檔案格式設定](../../functionality/destination-server/file-formatting.md) 以取得如何設定這些設定的詳細資訊。 |

{style="table-layout:auto"}

+++

+++回應

成功的回應會傳回HTTP狀態200，並包含您新建立之目標伺服器組態的詳細資訊。

+++

>[!TAB 動態架構伺服器]

**建立動態架構伺服器**

當您設定要從自己的API端點擷取其設定檔架構的目的地時，需要建立類似下方所示的動態架構伺服器。 與靜態結構相反，動態結構不使用 `profileFields` 陣列。 動態結構會使用動態結構伺服器，從中連線至您自己的API，以擷取結構配置。

+++請求

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
| `name` | 字串 | *必填。* 代表動態結構伺服器的好記名稱，只顯示給Adobe。 |
| `destinationServerType` | 字串 | *必填。* 設為 `URL_BASED` 動態架構伺服器。 |
| `urlBasedDestination.url.templatingStrategy` | 字串 | *必填.* <ul><li>使用 `PEBBLE_V1` 如果Adobe需要轉換 `value` 欄位。 如果您的端點如下所示，請使用此選項： `https://api.moviestar.com/data/{{customerData.region}}/items`. </li><li> 使用 `NONE` 如果Adobe端不需要轉換，例如，如果您有如下的端點： `https://api.moviestar.com/data/items`.</li></ul> |
| `urlBasedDestination.url.value` | 字串 | *必填。* 填入Experience Platform應連線之API端點的位址，並擷取結構欄位，以在啟動工作流程的對應步驟中作為目標欄位填入。 |
| `httpTemplate.httpMethod` | 字串 | *必填。* Adobe將用於呼叫伺服器的方法。 若為動態結構伺服器，請使用 `GET`. |
| `responseFields.templatingStrategy` | 字串 | *必填。* 使用 `PEBBLE_V1`. |
| `responseFields.value` | 字串 | *必填。* 此字串是字元逸出轉換範本，可將從合作夥伴API收到的回應轉換為將顯示在Platform UI中的合作夥伴架構。 <br> <ul><li> 如需如何編寫範本的資訊，請閱讀 [使用模板部分](../../functionality/destination-server/message-format.md#using-templating). </li><li> 如需字元逸出的詳細資訊，請參閱 [RFC JSON標準，第七節](https://tools.ietf.org/html/rfc8259#section-7). </li><li> 如需簡單轉換的範例，請參閱 [設定檔屬性](../../functionality/destination-server/message-format.md#attributes) 轉換。 </li></ul> |

{style="table-layout:auto"}

+++

+++回應

成功的回應會傳回HTTP狀態200，並包含您新建立之目標伺服器組態的詳細資訊。

+++

>[!ENDTABS]

## API錯誤處理 {#error-handling}

Destination SDKAPI端點遵循一般Experience PlatformAPI錯誤訊息原則。 請參閱 [API狀態代碼](../../../../landing/troubleshooting.md#api-status-codes) 和 [請求標題錯誤](../../../../landing/troubleshooting.md#request-header-errors) （位於平台疑難排解指南中）。

## 後續步驟 {#next-steps}

閱讀本檔案後，您現在知道如何透過Destination SDK建立新的目標伺服器 `/authoring/destination-servers` API端點。

若要進一步了解您可以使用此端點執行的操作，請參閱下列文章：

* [檢索目標伺服器配置](retrieve-destination-server.md)
* [更新目標伺服器配置](update-destination-server.md)
* [刪除目標伺服器配置](delete-destination-server.md)

若要了解此端點在目標製作程式中的適用位置，請參閱下列文章：

* [使用Destination SDK來設定串流目的地](../../guides/configure-destination-instructions.md#create-server-template-configuration)
* [使用Destination SDK配置基於檔案的目標](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration)