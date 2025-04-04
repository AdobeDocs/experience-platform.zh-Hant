---
description: 此頁面是用來透過Adobe Experience Platform Destination SDK更新現有目的地伺服器設定的API呼叫範例。
title: 更新目的地伺服器設定
exl-id: 579d2cc1-5110-4fba-9dcc-ff4b8d259827
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1103'
ht-degree: 7%

---

# 更新目的地伺服器設定

此頁面是您可用來使用`/authoring/destination-servers` API端點更新現有目的地伺服器設定的API要求與裝載範例。

>[!TIP]
>
>只有在您使用[發佈API](../../publishing-api/create-publishing-request.md)並提交更新以供Adobe檢閱後，才可看見對已生產/公開目的地執行的任何更新操作。

如需可透過此端點設定的功能的詳細說明，請參閱以下文章：

* [使用Destination SDK建立之目的地的伺服器規格](../../../destination-sdk/functionality/destination-server/server-specs.md)
* [使用Destination SDK建立之目的地的範本規格](../../../destination-sdk/functionality/destination-server/templating-specs.md)
* [訊息格式](../../../destination-sdk/functionality/destination-server/message-format.md)
* [檔案格式設定](../../../destination-sdk/functionality/destination-server/file-formatting.md)

>[!IMPORTANT]
>
>Destination SDK支援的所有引數名稱和值都會區分大小寫&#x200B;****。 為避免區分大小寫錯誤，請完全依照檔案中所示使用引數名稱和值。

## 開始使用目的地伺服器API作業 {#get-started}

繼續之前，請檢閱[快速入門手冊](../../getting-started.md)以取得重要資訊，您必須瞭解這些資訊才能成功呼叫API，包括如何取得必要的目的地撰寫許可權和必要的標頭。

## 更新目的地伺服器設定 {#update}

您可以藉由對具有更新承載的`/authoring/destination-servers`端點發出`PUT`要求，來更新[現有](create-destination-server.md)目的地伺服器設定。

>[!TIP]
>
>**API端點**： `platform.adobe.io/data/core/activation/authoring/destination-servers`

若要取得現有的目的地伺服器組態及其對應的`{INSTANCE_ID}`，請參閱有關[擷取目的地伺服器組態](retrieve-destination-server.md)的文章。

**API格式**

```http
PUT /authoring/destination-servers/{INSTANCE_ID}
```

| 參數 | 說明 |
| -------- | ----------- |
| `{INSTANCE_ID}` | 您要更新的目的地伺服器組態ID。 若要取得現有的目的地伺服器組態及其對應的`{INSTANCE_ID}`，請參閱[擷取目的地伺服器組態](retrieve-destination-server.md)。 |

以下要求會更新現有的目的地伺服器設定，此設定由承載中提供的引數所設定。

選取下方的每個索引標籤以檢視對應的裝載。

>[!BEGINTABS]

>[!TAB 即時（串流）]

+++要求

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
| `name` | 字串 | *必要。*&#x200B;代表您伺服器的易記名稱，僅對Adobe可見。 合作夥伴或客戶看不到此名稱。 範例`Moviestar destination server`。 |
| `destinationServerType` | 字串 | *必要。針對即時（串流）目的地，*&#x200B;設為`URL_BASED`。 |
| `urlBasedDestination.url.templatingStrategy` | 字串 | *必要。* <ul><li>如果Adobe需要轉換下面`value`欄位中的URL，請使用`PEBBLE_V1`。 如果您有類似以下的端點，請使用此選項： `https://api.moviestar.com/data/{{customerData.region}}/items`。 </li><li> 如果Adobe端不需要轉換，例如，如果您有類似`https://api.moviestar.com/data/items`的端點，請使用`NONE`。</li></ul> |
| `urlBasedDestination.url.value` | 字串 | *必要。*&#x200B;填入Experience Platform應連線的API端點位址。 |
| `httpTemplate.httpMethod` | 字串 | *必要。* Adobe將在呼叫伺服器時使用的方法。 選項為`GET`、`PUT`、`PUT`、`DELETE`、`PATCH`。 |
| `httpTemplate.requestBody.templatingStrategy` | 字串 | *必要。*&#x200B;使用`PEBBLE_V1`。 |
| `httpTemplate.requestBody.value` | 字串 | *必要。*&#x200B;此字串是字元逸出版本，會將Experience Platform客戶的資料轉換為您服務預期的格式。<br> <ul><li> 如需如何寫入範本的詳細資訊，請閱讀[使用範本區段](../../functionality/destination-server/message-format.md#using-templating)。 </li><li> 如需字元逸出的詳細資訊，請參閱[RFC JSON標準第7節](https://tools.ietf.org/html/rfc8259#section-7)。 </li><li> 如需簡單轉換的範例，請參閱[設定檔屬性](../../functionality/destination-server/message-format.md#attributes)轉換。 </li></ul> |
| `httpTemplate.contentType` | 字串 | *必要。*&#x200B;您的伺服器接受的內容型別。 此值很可能為`application/json`。 |

{style="table-layout:auto"}

+++

+++回應

成功的回應會傳回HTTP狀態200以及您更新的目的地伺服器組態的詳細資料。

+++

>[!TAB Amazon S3]

+++要求

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
| `destinationServerType` | 字串 | 根據您的目的地平台設定此值。 針對[!DNL Amazon S3]，請將此項設為`FILE_BASED_S3`。 |
| `fileBasedS3Destination.bucket.templatingStrategy` | 字串 | *必要。*&#x200B;使用`PEBBLE_V1`。 |
| `fileBasedS3Destination.bucket.value` | 字串 | 此目的地要使用的[!DNL Amazon S3]儲存貯體的名稱。 |
| `fileBasedS3Destination.path.templatingStrategy` | 字串 | *必要。*&#x200B;使用`PEBBLE_V1`。 |
| `fileBasedS3Destination.path.value` | 字串 | 目的地資料夾的路徑，此資料夾將裝載匯出的檔案。 |
| `fileConfigurations` | 不適用 | 如需如何設定這些設定的詳細資訊，請參閱[檔案格式設定](../../functionality/destination-server/file-formatting.md)。 |

{style="table-layout:auto"}

+++

+++回應

成功的回應會傳回HTTP狀態200以及您更新的目的地伺服器組態的詳細資料。

+++

>[!TAB SFTP]

+++要求

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

成功的回應會傳回HTTP狀態200以及您更新的目的地伺服器組態的詳細資料。

+++

>[!TAB Azure Data Lake儲存體]

+++要求

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
| `destinationServerType` | 字串 | 根據您的目的地平台設定此值。 針對[!DNL Azure Data Lake Storage]目的地，請將此專案設為`FILE_BASED_ADLS_GEN2`。 |
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | 字串 | *必要。*&#x200B;使用`PEBBLE_V1`。 |
| `fileBasedAdlsGen2Destination.path.value` | 字串 | 目的地資料夾的路徑，此資料夾將裝載匯出的檔案。 |
| `fileConfigurations` | 不適用 | 如需如何設定這些設定的詳細資訊，請參閱[檔案格式設定](../../functionality/destination-server/file-formatting.md)。 |

{style="table-layout:auto"}

+++

+++回應

成功的回應會傳回HTTP狀態200以及您更新的目的地伺服器組態的詳細資料。

+++

>[!TAB Azure Blob儲存體]

+++要求

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
| `destinationServerType` | 字串 | 根據您的目的地平台設定此值。 針對[!DNL Azure Blob Storage]目的地，請將此專案設為`FILE_BASED_AZURE_BLOB`。 |
| `fileBasedAzureBlobDestination.path.templatingStrategy` | 字串 | *必要。*&#x200B;使用`PEBBLE_V1`。 |
| `fileBasedAzureBlobDestination.path.value` | 字串 | 目的地資料夾的路徑，此資料夾將裝載匯出的檔案。 |
| `fileBasedAzureBlobDestination.container.templatingStrategy` | 字串 | *必要。*&#x200B;使用`PEBBLE_V1`。 |
| `fileBasedAzureBlobDestination.container.value` | 字串 | 此目的地要使用的[!DNL Azure Blob Storage]容器的名稱。 |
| `fileConfigurations` | 不適用 | 如需如何設定這些設定的詳細資訊，請參閱[檔案格式設定](../../functionality/destination-server/file-formatting.md)。 |

{style="table-layout:auto"}

+++

+++回應

成功的回應會傳回HTTP狀態200以及您更新的目的地伺服器組態的詳細資料。

+++

>[!TAB 資料登陸區域(DLZ)]

+++要求

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
| `destinationServerType` | 字串 | 根據您的目的地平台設定此值。 針對[!DNL Data Landing Zone]目的地，請將此專案設為`FILE_BASED_DLZ`。 |
| `fileBasedDlzDestination.path.templatingStrategy` | 字串 | *必要。*&#x200B;使用`PEBBLE_V1`。 |
| `fileBasedDlzDestination.path.value` | 字串 | 目的地資料夾的路徑，此資料夾將裝載匯出的檔案。 |
| `fileConfigurations` | 不適用 | 如需如何設定這些設定的詳細資訊，請參閱[檔案格式設定](../../functionality/destination-server/file-formatting.md)。 |

{style="table-layout:auto"}

+++

+++回應

成功的回應會傳回HTTP狀態200以及您更新的目的地伺服器組態的詳細資料。

+++

>[!TAB Google雲端儲存空間]

+++要求

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
| `destinationServerType` | 字串 | 根據您的目的地平台設定此值。 針對[!DNL Google Cloud Storage]目的地，請將此專案設為`FILE_BASED_GOOGLE_CLOUD`。 |
| `fileBasedGoogleCloudStorageDestination.bucket.templatingStrategy` | 字串 | *必要。*&#x200B;使用`PEBBLE_V1`。 |
| `fileBasedGoogleCloudStorageDestination.bucket.value` | 字串 | 此目的地要使用的[!DNL Google Cloud Storage]儲存貯體的名稱。 |
| `fileBasedGoogleCloudStorageDestination.path.templatingStrategy` | 字串 | *必要。*&#x200B;使用`PEBBLE_V1`。 |
| `fileBasedGoogleCloudStorageDestination.path.value` | 字串 | 目的地資料夾的路徑，此資料夾將裝載匯出的檔案。 |
| `fileConfigurations` | 不適用 | 如需如何設定這些設定的詳細資訊，請參閱[檔案格式設定](../../functionality/destination-server/file-formatting.md)。 |

{style="table-layout:auto"}

+++

+++回應

成功的回應會傳回HTTP狀態200以及您更新的目的地伺服器組態的詳細資料。

+++

>[!ENDTABS]

## API錯誤處理 {#error-handling}

Destination SDK API端點遵循一般Experience Platform API錯誤訊息原則。 請參閱Experience Platform疑難排解指南中的[API狀態碼](../../../../landing/troubleshooting.md#api-status-codes)和[請求標頭錯誤](../../../../landing/troubleshooting.md#request-header-errors)。

## 後續步驟 {#next-steps}

閱讀本檔案後，您現在知道如何透過Destination SDK `/authoring/destination-servers` API端點更新目的地伺服器設定。

若要深入瞭解您可以使用此端點的功能，請參閱下列文章：

* [建立目的地伺服器組態](create-destination-server.md)
* [擷取目的地伺服器設定](retrieve-destination-server.md)
* [更新目的地伺服器設定](update-destination-server.md)
