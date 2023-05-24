---
title: 使用流服務API為流式SDK建立新連接規範
description: 以下文檔提供了有關如何使用流服務API建立連接規範並通過自助源整合新源的步驟。
hide: true
hidefromtoc: true
exl-id: ad8f6004-4e82-49b5-aede-413d72a1482d
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 1%

---

# 使用 [!DNL Flow Service] API

連接規範表示源的結構。 它包含有關源的驗證要求的資訊，定義如何瀏覽和檢查源資料，並提供有關給定源的屬性的資訊。 的 `/connectionSpecs` 端點 [!DNL Flow Service] API允許您以寫程式方式管理組織內的連接規範。

以下文檔提供了有關如何使用 [!DNL Flow Service] API，並通過Self-Serve Sources(Streaming SDK)整合新源。

## 快速入門

在繼續之前，請查看 [入門指南](./getting-started.md) 有關相關文檔的連結、閱讀本文檔中示例API調用的指南，以及有關成功調用任何Experience PlatformAPI所需標頭的重要資訊。

## 收集對象

要使用Self-Serve源建立新的流源，必須首先與Adobe協調，請求專用Git儲存庫，並與Adobe對齊有關源的標籤、說明、類別和表徵圖的詳細資訊。

提供後，您必須按如下方式構建私有Git儲存庫：

* 來源
   * {your_source}
      * 工件
         * {your_source.txt}-category.txt
         * {your_source}-description.txt
         * {your_source}-icon.svg
         * {your_source}-label.txt
         * {your_source}-connectionSpec.json

| 對象（檔案名） | 說明 | 範例 |
| --- | --- | --- |
| {your_source} | 源的名稱。 此資料夾應包含與您的源相關的所有對象，位於您的專用Git儲存庫中。 | `medallia` |
| {your_source.txt}-category.txt | 源所屬的類別，格式為文本檔案。 **注釋**:如果您認為您的來源不適合上述任何類別，請與Adobe代表聯繫以進行討論。 | `medallia-category.txt` 在檔案內，請指定源的類別，如： `streaming`。 |
| {your_source}-description.txt | 來源的簡要描述。 | [!DNL Medallia] 是市場營銷自動化的來源 [!DNL Medallia] 資料到Experience Platform。 |
| {your_source}-icon.svg | 用於在Experience Platform源目錄中表示源的影像。 此表徵圖必須是SVG檔案。 |
| {your_source}-label.txt | 源應出現在Experience Platform源目錄中的名稱。 | 梅達利亞 |
| {your_source}-connectionSpec.json | 包含源的連接規範的JSON檔案。 在完成本指南時，您將填充連接規範，因此最初不需要此檔案。 | `medallia-connectionSpec.json` |

{style="table-layout:auto"}

>[!TIP]
>
>在連接規範的測試期間，您可以使用 `text` 在連接規範中。

在將必要檔案添加到專用Git儲存庫後，必須建立拉入請求(PR)以供Adobe審閱。 在批准和合併您的PR後，將為您提供一個ID，該ID可用於連接規範以參考源的標籤、說明和表徵圖。

接下來，按照下面介紹的步驟配置連接規範。 有關可添加到源中的不同功能（如高級計畫、自定義架構或不同分頁類型）的其他指導，請參閱上的指南 [配置源規範](../config/sourcespec.md)。

## 複製連接規範模板

收集所需對象後，將下面的連接規範模板複製並貼上到所選文本編輯器中，然後更新方括弧中的屬性 `{}` 與特定來源相關的資訊。

```json
{
  "name": "generic-streaming",
  "type": "generic-streaming",
  "description": "{DESCRIPTION}",
  "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
  "version": "1.0",
  "attributes": {
    "category": "Streaming",
    "isSource": true,
    "documentationLink": "https://docs.adobe.com/content/help/en/platform-learn/tutorials/data-ingestion/understanding-streaming-ingestion.html",
    "uiAttributes": {
      "apiFeatures": {
        "updateSupported": false
      }
    }
  },
  "authSpec": [],
  "name": "generic-streaming",
  "permissionsInfo": {
    "view": [
      {
        "name": "StreamingSource",
        "@type": "lowLevel",
        "permissions": [
          "read"
        ]
      }
    ],
    "manage": [
      {
        "name": "StreamingSource",
        "@type": "lowLevel",
        "permissions": [
          "write"
        ]
      }
    ]
  },
  "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
  "sourceSpec": {
    "attributes": {
      "authRequired": false,
      "uiAttributes": {
        "documentationLink": "http://www.adobe.com/go/understanding-data-streaming-ingestion-en",
        "isSource": true,
        "monitoringSupported": false,
        "category": {
          "key": "streaming"
        },
        "icon": {
          "key": "generic"
        },
        "description": {
          "text": "Generic Streaming For Authentication Testing 2"
        },
        "label": {
          "text": "Generic Streaming For Authentication Testing 2"
        },
        "frequency": {
          "text": "Generic Streaming"
        }
      }
    }
  },
  "exploreSpec": {
    "type": "StreamingConnection"
  }
}
```

## 建立連接規範 {#create}

獲取連接規範模板後，現在可以通過填寫與源對應的相應值開始創作新的連接規範。

連接規範可以分為兩個不同的部分：源規範和瀏覽規範。

有關連接規範各節的詳細資訊，請參閱以下文檔：

* [配置源規範](../config/sourcespec.md)
* [配置瀏覽規範](../config/explorespec.md)

在更新規範資訊後，您可以通過向POST `/connectionSpecs` 端點 [!DNL Flow Service] API。

**API格式**

```http
POST /connectionSpecs
```

**要求**

以下請求是流源完全創作的連接規範的示例：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "generic-streaming",
      "type": "generic-streaming",
      "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
      "version": "1.0",
      "attributes": {
          "category": "Streaming",
          "isSource": true,
          "documentationLink": "https://docs.adobe.com/content/help/en/platform-learn/tutorials/data-ingestion/understanding-streaming-ingestion.html",
          "uiAttributes": {
            "apiFeatures": {
              "updateSupported": false
            }
          }
        },
        "authSpec": [],
        "name": "generic-streaming",
        "permissionsInfo": {
          "view": [
            {
              "name": "StreamingSource",
              "@type": "lowLevel",
              "permissions": [
                "read"
              ]
            }
          ],
          "manage": [
            {
              "name": "StreamingSource",
              "@type": "lowLevel",
              "permissions": [
                "write"
              ]
            }
          ]
        },
        "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
        "sourceSpec": {
          "attributes": {
            "uiAttributes": {
              "documentationLink": "http://www.adobe.com/go/understanding-data-streaming-ingestion-en",
              "isSource": true,
              "monitoringSupported": false,
              "category": {
                "key": "streaming"
              },
              "icon": {
                "key": "Generic-Streaming"
              },
              "description": {
                "text": "Generic Streaming Connector"
              },
              "label": {
                "text": "Generic"
              },
              "frequency": {
                "text": "streaming"
              }
            }
          }
        },
        "exploreSpec": {
          "type": "StreamingConnection"
          },
        "type": "generic-streaming",
        "version": "1.0"
      }'
```

**回應**

成功的響應返回新建立的連接規範，包括其唯一性 `id`。

```json
{
  "items": [
    {
      "id": "bdb5b792-451b-42de-acf8-15f3195821de",
      "createdAt": 1667536504101,
      "updatedAt": 1667536504101,
      "createdBy": "{CREATED_BY}",
      "updatedBy": "{UPDATED_BY}",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{CREATED_CLIENT}",
      "sandboxId": "d537df80-c5d7-11e9-aafb-87c71c35cac8",
      "sandboxName": "prod",
      "imsOrgId": "{ORG_ID}",
      "name": "generic-streaming",
      "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
      "version": "1.0",
      "type": "generic-streaming",
      "sourceSpec": {
        "attributes": {
          "authRequired": false,
          "uiAttributes": {
            "documentationLink": "http://www.adobe.com/go/understanding-data-streaming-ingestion-en",
            "isSource": true,
            "monitoringSupported": false,
            "category": {
              "key": "streaming"
            },
            "icon": {
              "key": "Generic-Streaming"
            },
            "description": {
              "text": "Generic Streaming Connector"
            },
            "label": {
              "text": "Generic"
            },
            "frequency": {
              "text": "streaming"
            }
          }
        }
      },
      "exploreSpec": {
        "type": "StreamingConnection"
      },
      "attributes": {
        "category": "Streaming",
        "isSource": true,
        "documentationLink": "https://docs.adobe.com/content/help/en/platform-learn/tutorials/data-ingestion/understanding-streaming-ingestion.html",
        "uiAttributes": {
          "apiFeatures": {
            "updateSupported": false
          }
        }
      },
      "permissionsInfo": {
        "view": [
          {
            "@type": "lowLevel",
            "name": "StreamingSource",
            "permissions": [
              "read"
            ]
          }
        ],
        "manage": [
          {
            "@type": "lowLevel",
            "name": "StreamingSource",
            "permissions": [
              "write"
            ]
          }
        ]
      }
    }
  ]
}
```

## 後續步驟

現在，您已建立了新的連接規範，必須將其相應的連接規範ID添加到現有的流規範中。 請參閱上的教程 [更新流規範](./update-flow-specs.md) 的子菜單。

要修改所建立的連接規範，請參閱上的教程 [更新連接規範](./update-connection-specs.md)。
