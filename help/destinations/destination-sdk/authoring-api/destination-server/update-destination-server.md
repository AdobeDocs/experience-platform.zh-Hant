---
description: 本頁說明透過Adobe Experience Platform Destination SDK更新現有目標伺服器設定所使用的API呼叫。
title: 更新目標伺服器配置
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '1098'
ht-degree: 12%

---


# 更新目標伺服器配置

此頁面是API要求和裝載的範例，您可使用來更新現有的目的地伺服器設定 `/authoring/destination-servers` API端點。

>[!TIP]
>
>產品化/公用目的地上的任何更新操作，只有在您使用 [發佈API](../../publishing-api/create-publishing-request.md) 並提交更新以供Adobe審核。

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

## 更新目標伺服器配置 {#update}

您可以更新 [現有](create-destination-server.md) 目標伺服器配置，方法是： `PUT` 請求 `/authoring/destination-servers` 以更新的裝載結束點。

>[!TIP]
>
>**API端點**: `platform.adobe.io/data/core/activation/authoring/destination-servers`

獲取現有目標伺服器配置及其相應配置 `{INSTANCE_ID}`，請參閱關於 [檢索目標伺服器配置](retrieve-destination-server.md).

**API格式**

```http
PUT /authoring/destination-servers/{INSTANCE_ID}
```

| 參數 | 說明 |
| -------- | ----------- |
| `{INSTANCE_ID}` | 要更新的目標伺服器配置ID。 獲取現有目標伺服器配置及其相應配置 `{INSTANCE_ID}`，請參閱 [檢索目標伺服器配置](retrieve-destination-server.md). |

下列請求會更新現有的目的地伺服器設定，由裝載中提供的參數所設定。

選取下方的每個標籤，以檢視對應的裝載。

>[!BEGINTABS]

>[!TAB 即時（串流）]

+++請求

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers\{INSTANCE_ID} \
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
      "httpMethod":"PUT",
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
| `urlBasedDestination.url.templatingStrategy` | 字串 | *必填.* <ul><li>使用 `PEBBLE_V1` 如果Adobe需要轉換 `value` 欄位。 如果您的端點如下所示，請使用此選項： `https://api.moviestar.com/data/{{customerData.region}}/items`. </li><li> 使用 `NONE` 如果Adobe端不需要轉換，例如，如果您有如下的端點： `https://api.moviestar.com/data/items`.</li></ul> |
| `urlBasedDestination.url.value` | 字串 | *必填。* 填入Experience Platform應連線之API端點的位址。 |
| `httpTemplate.httpMethod` | 字串 | *必填。* Adobe將用於呼叫伺服器的方法。 選項包括 `GET`, `PUT`, `PUT`, `DELETE`, `PATCH`. |
| `httpTemplate.requestBody.templatingStrategy` | 字串 | *必填。* 使用 `PEBBLE_V1`. |
| `httpTemplate.requestBody.value` | 字串 | *必填。* 此字串是字元逸出版本，可將Platform客戶的資料轉換為服務預期的格式。 <br> <ul><li> 如需如何編寫範本的資訊，請閱讀 [使用模板部分](../../functionality/destination-server/message-format.md#using-templating). </li><li> 如需字元逸出的詳細資訊，請參閱 [RFC JSON標準，第七節](https://tools.ietf.org/html/rfc8259#section-7). </li><li> 如需簡單轉換的範例，請參閱 [設定檔屬性](../../functionality/destination-server/message-format.md#attributes) 轉換。 </li></ul> |
| `httpTemplate.contentType` | 字串 | *必填。* 伺服器接受的內容類型。 此值很可能 `application/json`. |

{style="table-layout:auto"}

+++

+++回應

成功的回應會傳回HTTP狀態200，並包含更新目的地伺服器設定的詳細資訊。

+++

>[!TAB Amazon S3]

+++請求

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers\{INSTANCE_ID} \
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

成功的回應會傳回HTTP狀態200，並包含更新目的地伺服器設定的詳細資訊。

+++

>[!TAB SFTP]

+++請求

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_ID} \
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

成功的回應會傳回HTTP狀態200，並包含更新目的地伺服器設定的詳細資訊。

+++

>[!TAB Azure資料湖儲存]

+++請求

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_ID} \
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

成功的回應會傳回HTTP狀態200，並包含更新目的地伺服器設定的詳細資訊。

+++

>[!TAB Azure Blob 儲存體]

+++請求

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_D} \
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

成功的回應會傳回HTTP狀態200，並包含更新目的地伺服器設定的詳細資訊。

+++

>[!TAB 資料登錄區(DLZ)]

+++請求

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_ID} \
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

成功的回應會傳回HTTP狀態200，並包含更新目的地伺服器設定的詳細資訊。

+++

>[!TAB Google雲端儲存空間]

+++請求

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/destination-servers/{INSTANCE_ID} \
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

成功的回應會傳回HTTP狀態200，並包含更新目的地伺服器設定的詳細資訊。

+++

>[!ENDTABS]

## API錯誤處理 {#error-handling}

Destination SDKAPI端點遵循一般Experience PlatformAPI錯誤訊息原則。 請參閱 [API狀態代碼](../../../../landing/troubleshooting.md#api-status-codes) 和 [請求標題錯誤](../../../../landing/troubleshooting.md#request-header-errors) （位於平台疑難排解指南中）。

## 後續步驟 {#next-steps}

閱讀本檔案後，您現在知道如何透過Destination SDK更新目標伺服器設定 `/authoring/destination-servers` API端點。

若要進一步了解您可以使用此端點執行的操作，請參閱下列文章：

* [建立目標伺服器配置](create-destination-server.md)
* [檢索目標伺服器配置](retrieve-destination-server.md)
* [更新目標伺服器配置](update-destination-server.md)