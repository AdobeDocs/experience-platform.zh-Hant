---
description: 本頁說明了用於通過Adobe Experience Platform Destination SDK建立目標伺服器的API調用。
title: 建立目標伺服器配置
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '1623'
ht-degree: 9%

---


# 建立目標伺服器配置

建立目標伺服器是使用Destination SDK建立您自己的目標的第一步。 目標伺服器包括 [伺服器](../../functionality/destination-server/server-specs.md) 和 [模板](../../functionality/destination-server/templating-specs.md) 規格， [消息格式](../../functionality/destination-server/message-format.md)的 [檔案格式](../../functionality/destination-server/file-formatting.md) 選項（用於基於檔案的目標）。

本頁說明了API請求和負載，您可以使用 `/authoring/destination-servers` API終結點。

有關可以通過此端點配置的功能的詳細說明，請閱讀以下文章：

* [使用Destination SDK建立的目標的伺服器規格](../../../destination-sdk/functionality/destination-server/server-specs.md)
* [使用Destination SDK建立的目標的模板規格](../../../destination-sdk/functionality/destination-server/templating-specs.md)
* [訊息格式](../../../destination-sdk/functionality/destination-server/message-format.md)
* [檔案格式配置](../../../destination-sdk/functionality/destination-server/file-formatting.md)

>[!IMPORTANT]
>
>Destination SDK支援的所有參數名和值均 **區分大小寫**。 為避免區分大小寫錯誤，請完全按文檔所示使用參數名稱和值。

## 目標伺服器API操作入門 {#get-started}

在繼續之前，請查看 [入門指南](../../getting-started.md) 瞭解成功調用API所需的重要資訊，包括如何獲得所需的目標創作權限和所需的標題。

## 建立目標伺服器配置 {#create}

通過建立 `POST` 請求 `/authoring/destination-servers` 端點。

>[!TIP]
>
>**API終結點**: `platform.adobe.io/data/core/activation/authoring/destination-servers`

**API格式**

```http
POST /authoring/destination-servers
```

根據您建立的目標類型，您需要配置稍微不同的目標伺服器類型。 請參閱以下標籤中的目標伺服器示例，瞭解Destination SDK中支援的每種目標類型。

下面的示例負載包括每個目標伺服器類型支援的所有參數。 您不需要在請求中包括所有參數。 負載可根據您的需要定制。

選擇下面的每個頁籤以查看相應的API請求。

>[!BEGINTABS]

>[!TAB 即時（流）]

**建立即時（流）目標伺服器**

在配置基於即時（流）API的整合時，需要建立與下面所示類似的即時（流）目標伺服器。

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
| `name` | 字串 | *必填。* 表示伺服器的友好名稱，僅對Adobe可見。 合作夥伴或客戶看不到此名稱。 範例 `Moviestar destination server`. |
| `destinationServerType` | 字串 | *必填。* 設定為 `URL_BASED` 用於即時（流）目標。 |
| `urlBasedDestination.url.templatingStrategy` | 字串 | *必填.* <ul><li>使用 `PEBBLE_V1` 如果Adobe需要轉換 `value` 的下界。 如果您具有類似 `https://api.moviestar.com/data/{{customerData.region}}/items`的子菜單。 `region` 部件可能因客戶而異。 在這種情況下，您還需要配置 `region` 作為 [客戶資料欄位](../../functionality/destination-configuration/customer-data-fields.md) 的 [目標配置](../destination-configuration/create-destination-configuration.md)。 </li><li> 使用 `NONE` 如果Adobe端不需要轉換，例如，如果您有一個端點，如： `https://api.moviestar.com/data/items`。</li></ul> |
| `urlBasedDestination.url.value` | 字串 | *必填。* 填寫Experience Platform應連接到的API終結點的地址。 |
| `httpTemplate.httpMethod` | 字串 | *必填。* Adobe在對伺服器的調用中使用的方法。 選項為 `GET`。 `PUT`。 `POST`。 `DELETE`。 `PATCH`。 |
| `httpTemplate.requestBody.templatingStrategy` | 字串 | *必填。* 使用 `PEBBLE_V1`. |
| `httpTemplate.requestBody.value` | 字串 | *必填。* 此字串是字元轉義版本，它將平台客戶的資料轉換為服務所需的格式。 <br> <ul><li> 有關如何編寫模板的資訊，請閱讀 [使用模板部](../../functionality/destination-server/message-format.md#using-templating)。 </li><li> 有關字元轉義的詳細資訊，請參閱 [RFC JSON標準，第7節](https://tools.ietf.org/html/rfc8259#section-7)。 </li><li> 有關簡單轉換的示例，請參閱 [配置檔案屬性](../../functionality/destination-server/message-format.md#attributes) 轉換。 </li></ul> |
| `httpTemplate.contentType` | 字串 | *必填。* 伺服器接受的內容類型。 此值極有可能 `application/json`。 |

{style="table-layout:auto"}

+++

+++回應

成功的響應返回HTTP狀態200，其中包含新建立的目標伺服器配置的詳細資訊。

+++

>[!TAB Amazon S3]

**建立AmazonS3目標伺服器**

您需要建立 [!DNL Amazon S3] 與配置基於檔案的伺服器時如下所示的目標伺服器類似 [!DNL Amazon S3] 目標。

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
| `name` | 字串 | 目標連接的名稱。 |
| `destinationServerType` | 字串 | 根據目標平台設定此值。 對於 [!DNL Amazon S3]，將其設定為 `FILE_BASED_S3`。 |
| `fileBasedS3Destination.bucket.templatingStrategy` | 字串 | *必填。* 使用 `PEBBLE_V1`. |
| `fileBasedS3Destination.bucket.value` | 字串 | 名稱 [!DNL Amazon S3] 該目標使用的儲存桶。 |
| `fileBasedS3Destination.path.templatingStrategy` | 字串 | *必填。* 使用 `PEBBLE_V1`. |
| `fileBasedS3Destination.path.value` | 字串 | 將承載導出檔案的目標資料夾的路徑。 |
| `fileConfigurations` | 不適用 | 請參閱 [檔案格式配置](../../functionality/destination-server/file-formatting.md) 的子菜單。 |

{style="table-layout:auto"}

+++

+++回應

成功的響應返回HTTP狀態200，其中包含新建立的目標伺服器配置的詳細資訊。

+++

>[!TAB SFTP]

**建立 [!DNL SFTP] 目標伺服器**

您需要建立 [!DNL SFTP] 與配置基於檔案的伺服器時如下所示的目標伺服器類似 [!DNL SFTP] 目標。

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
| `name` | 字串 | 目標連接的名稱。 |
| `destinationServerType` | 字串 | 根據目標平台設定此值。 對於 [!DNL SFTP] 目標，將其設定為 `FILE_BASED_SFTP`。 |
| `fileBasedSftpDestination.rootDirectory.templatingStrategy` | 字串 | *必填。* 使用 `PEBBLE_V1`. |
| `fileBasedSftpDestination.rootDirectory.value` | 字串 | 目標儲存的根目錄。 |
| `fileBasedSftpDestination.hostName.templatingStrategy` | 字串 | *必填。* 使用 `PEBBLE_V1`. |
| `fileBasedSftpDestination.hostName.value` | 字串 | 目標儲存的主機名。 |
| `port` | 整數 | SFTP檔案伺服器埠。 |
| `encryptionMode` | 字串 | 指示是否使用檔案加密。 支援的值： <ul><li>PGP</li><li>None</li></ul> |
| `fileConfigurations` | 不適用 | 請參閱 [檔案格式配置](../../functionality/destination-server/file-formatting.md) 的子菜單。 |

{style="table-layout:auto"}

+++

+++回應

成功的響應返回HTTP狀態200，其中包含新建立的目標伺服器配置的詳細資訊。

+++

>[!TAB Azure資料湖儲存]

**建立 [!DNL Azure Data Lake Storage] 目標伺服器**

您需要建立 [!DNL Azure Data Lake Storage] 與配置基於檔案的伺服器時如下所示的目標伺服器類似 [!DNL Azure Data Lake Storage] 目標。

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
| `name` | 字串 | 目標連接的名稱。 |
| `destinationServerType` | 字串 | 根據目標平台設定此值。 對於 [!DNL Azure Data Lake Storage] 目標，將其設定為 `FILE_BASED_ADLS_GEN2`。 |
| `fileBasedAdlsGen2Destination.path.templatingStrategy` | 字串 | *必填。* 使用 `PEBBLE_V1`. |
| `fileBasedAdlsGen2Destination.path.value` | 字串 | 將承載導出檔案的目標資料夾的路徑。 |
| `fileConfigurations` | 不適用 | 請參閱 [檔案格式配置](../../functionality/destination-server/file-formatting.md) 的子菜單。 |

{style="table-layout:auto"}

+++

+++回應

成功的響應返回HTTP狀態200，其中包含新建立的目標伺服器配置的詳細資訊。

+++

>[!TAB Azure Blob 儲存體]

**建立 [!DNL Azure Blob Storage] 目標伺服器**

您需要建立 [!DNL Azure Blob Storage] 與配置基於檔案的伺服器時如下所示的目標伺服器類似 [!DNL Azure Blob Storage] 目標。

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
| `name` | 字串 | 目標連接的名稱。 |
| `destinationServerType` | 字串 | 根據目標平台設定此值。 對於 [!DNL Azure Blob Storage] 目標，將其設定為 `FILE_BASED_AZURE_BLOB`。 |
| `fileBasedAzureBlobDestination.path.templatingStrategy` | 字串 | *必填。* 使用 `PEBBLE_V1`. |
| `fileBasedAzureBlobDestination.path.value` | 字串 | 將承載導出檔案的目標資料夾的路徑。 |
| `fileBasedAzureBlobDestination.container.templatingStrategy` | 字串 | *必填。* 使用 `PEBBLE_V1`. |
| `fileBasedAzureBlobDestination.container.value` | 字串 | 名稱 [!DNL Azure Blob Storage] 要由此目標使用的容器。 |
| `fileConfigurations` | 不適用 | 請參閱 [檔案格式配置](../../functionality/destination-server/file-formatting.md) 的子菜單。 |

{style="table-layout:auto"}

+++

+++回應

成功的響應返回HTTP狀態200，其中包含新建立的目標伺服器配置的詳細資訊。

+++

>[!TAB 資料登錄區(DLZ)]

**建立 [!DNL Data Landing Zone (DLZ)] 目標伺服器**

您需要建立 [!DNL Data Landing Zone (DLZ)] 與配置基於檔案的伺服器時如下所示的目標伺服器類似 [!DNL Data Landing Zone (DLZ)] 目標。

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
| `name` | 字串 | 目標連接的名稱。 |
| `destinationServerType` | 字串 | 根據目標平台設定此值。 對於 [!DNL Data Landing Zone] 目標，將其設定為 `FILE_BASED_DLZ`。 |
| `fileBasedDlzDestination.path.templatingStrategy` | 字串 | *必填。*  使用 `PEBBLE_V1`. |
| `fileBasedDlzDestination.path.value` | 字串 | 將承載導出檔案的目標資料夾的路徑。 |
| `fileConfigurations` | 不適用 | 請參閱 [檔案格式配置](../../functionality/destination-server/file-formatting.md) 的子菜單。 |

{style="table-layout:auto"}

+++

+++回應

成功的響應返回HTTP狀態200，其中包含新建立的目標伺服器配置的詳細資訊。

+++

>[!TAB Google雲儲存]

**建立 [!DNL Google Cloud Storage] 目標伺服器**

您需要建立 [!DNL Google Cloud Storage] 與配置基於檔案的伺服器時如下所示的目標伺服器類似 [!DNL Google Cloud Storage] 目標。

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
| `name` | 字串 | 目標連接的名稱。 |
| `destinationServerType` | 字串 | 根據目標平台設定此值。 對於 [!DNL Google Cloud Storage] 目標，將其設定為 `FILE_BASED_GOOGLE_CLOUD`。 |
| `fileBasedGoogleCloudStorageDestination.bucket.templatingStrategy` | 字串 | *必填。*  使用 `PEBBLE_V1`. |
| `fileBasedGoogleCloudStorageDestination.bucket.value` | 字串 | 名稱 [!DNL Google Cloud Storage] 該目標使用的儲存桶。 |
| `fileBasedGoogleCloudStorageDestination.path.templatingStrategy` | 字串 | *必填。* 使用 `PEBBLE_V1`. |
| `fileBasedGoogleCloudStorageDestination.path.value` | 字串 | 將承載導出檔案的目標資料夾的路徑。 |
| `fileConfigurations` | 不適用 | 請參閱 [檔案格式配置](../../functionality/destination-server/file-formatting.md) 的子菜單。 |

{style="table-layout:auto"}

+++

+++回應

成功的響應返回HTTP狀態200，其中包含新建立的目標伺服器配置的詳細資訊。

+++

>[!TAB 動態架構伺服器]

**建立動態架構伺服器**

在配置從自己的API終結點檢索其配置檔案架構的目標時，需要建立與下面所示的動態架構伺服器類似的動態架構伺服器。 與靜態模式不同，動態模式不使用 `profileFields` 陣列。 相反，動態架構使用動態架構伺服器，該伺服器連接到您自己的API，從中檢索架構配置。

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
| `name` | 字串 | *必填。* 表示動態架構伺服器的友好名稱，僅對Adobe可見。 |
| `destinationServerType` | 字串 | *必填。* 設定為 `URL_BASED` 動態架構伺服器。 |
| `urlBasedDestination.url.templatingStrategy` | 字串 | *必填.* <ul><li>使用 `PEBBLE_V1` 如果Adobe需要轉換 `value` 的下界。 如果您具有端點，如： `https://api.moviestar.com/data/{{customerData.region}}/items`。 </li><li> 使用 `NONE` 如果Adobe端不需要轉換，例如，如果您有一個端點，如： `https://api.moviestar.com/data/items`。</li></ul> |
| `urlBasedDestination.url.value` | 字串 | *必填。* 填寫Experience Platform應連接到的API終結點的地址並檢索要作為激活工作流映射步驟中的目標欄位填充的架構欄位。 |
| `httpTemplate.httpMethod` | 字串 | *必填。* Adobe在對伺服器的調用中使用的方法。 對於動態架構伺服器，使用 `GET`。 |
| `responseFields.templatingStrategy` | 字串 | *必填。* 使用 `PEBBLE_V1`. |
| `responseFields.value` | 字串 | *必填。* 此字串是字元轉義轉換模板，用於將從夥伴API接收的響應轉換為將在平台UI中顯示的夥伴架構。 <br> <ul><li> 有關如何編寫模板的資訊，請閱讀 [使用模板部](../../functionality/destination-server/message-format.md#using-templating)。 </li><li> 有關字元轉義的詳細資訊，請參閱 [RFC JSON標準，第7節](https://tools.ietf.org/html/rfc8259#section-7)。 </li><li> 有關簡單轉換的示例，請參閱 [配置檔案屬性](../../functionality/destination-server/message-format.md#attributes) 轉換。 </li></ul> |

{style="table-layout:auto"}

+++

+++回應

成功的響應返回HTTP狀態200，其中包含新建立的目標伺服器配置的詳細資訊。

+++

>[!ENDTABS]

## API錯誤處理 {#error-handling}

Destination SDKAPI端點遵循常規Experience PlatformAPI錯誤消息原則。 請參閱 [API狀態代碼](../../../../landing/troubleshooting.md#api-status-codes) 和 [請求標頭錯誤](../../../../landing/troubleshooting.md#request-header-errors) 中。

## 後續步驟 {#next-steps}

閱讀此文檔後，您現在知道如何通過Destination SDK建立新的目標伺服器 `/authoring/destination-servers` API終結點。

要瞭解有關可以使用此端點執行什麼操作的詳細資訊，請參閱以下文章：

* [檢索目標伺服器配置](retrieve-destination-server.md)
* [更新目標伺服器配置](update-destination-server.md)
* [刪除目標伺服器配置](delete-destination-server.md)

要瞭解此端點在目標創作流程中的位置，請參閱以下文章：

* [使用Destination SDK配置流目標](../../guides/configure-destination-instructions.md#create-server-template-configuration)
* [使用Destination SDK配置基於檔案的目標](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration)