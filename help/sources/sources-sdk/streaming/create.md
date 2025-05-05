---
title: 使用流量服務API建立串流SDK的新連線規格
description: 以下檔案提供如何使用「流程服務API」建立連線規格，以及透過「自助式來源」整合新來源的步驟。
exl-id: ad8f6004-4e82-49b5-aede-413d72a1482d
badge: Beta
source-git-commit: 256857103b4037b2cd7b5b52d6c5385121af5a9f
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 1%

---

# 使用[!DNL Flow Service] API建立新的連線規格

>[!NOTE]
>
>自助來源串流SDK為測試版。 如需使用Beta版標籤來源的相關資訊，請參閱[來源概觀](../../home.md#terms-and-conditions)。

連線對規格代表來源的結構。 它包含有關來源驗證需求的資訊，定義如何探索和檢查來源資料，並提供有關給定來源屬性的資訊。 [!DNL Flow Service] API中的`/connectionSpecs`端點可讓您以程式設計方式管理組織內的連線規格。

以下檔案提供如何使用[!DNL Flow Service] API建立連線規格，以及透過自助來源（串流SDK）整合新來源的步驟。

## 快速入門

繼續之前，請先檢閱[快速入門手冊](./getting-started.md)，以取得相關檔案的連結、閱讀本檔案中範例API呼叫的手冊，以及有關成功呼叫任何Experience PlatformAPI所需必要標題的重要資訊。

## 收整合品

若要使用自助來源建立新的串流來源，您必須先協調Adobe、請求私人Git存放庫，並對齊有關來源標籤、說明、類別和圖示詳細資訊的Adobe。

提供後，您必須建構您的私人Git存放庫，如下所示：

* 來源
   * {your_source}
      * 成品
         * {your_source}-category.txt
         * {your_source}-description.txt
         * {your_source}-icon.svg
         * {your_source}-label.txt
         * {your_source}-connectionSpec.json

| 成品（檔案名稱） | 說明 | 範例 |
| --- | --- | --- |
| {your_source} | 來源的名稱。 此資料夾應在您的私人Git存放庫中包含與您的來源相關的所有成品。 | `medallia` |
| {your_source}-category.txt | 來源所屬的類別，格式為文字檔。 **注意**：如果您認為您的來源不符合上述任何類別，請聯絡您的Adobe代表進行討論。 | `medallia-category.txt`在檔案內，請指定您來源的類別，例如： `streaming`。 |
| {your_source}-description.txt | 來源的簡短說明。 | [!DNL Medallia]是行銷自動化來源，可用來將[!DNL Medallia]資料帶入Experience Platform。 |
| {your_source}-icon.svg | 用來在Experience Platform來源目錄中表示來源的影像。 此圖示必須是SVG檔案。 |
| {your_source}-label.txt | 您應顯示在Experience Platform來源目錄中的來源名稱。 | 梅迪亞文 |
| {your_source}-connectionSpec.json | 包含您來源之連線規格的JSON檔案。 一開始不需要這個檔案，因為當您完成本指南時，會填入您的連線規格。 | `medallia-connectionSpec.json` |

{style="table-layout:auto"}

>[!TIP]
>
>在連線規格的測試期間，您可以在連線規格中使用`text`取代索引鍵值。

將必要的檔案新增至私人Git存放庫後，您必須建立提取請求(PR)以供Adobe檢閱。 您的PR獲得核准並合併後，系統就會提供您的ID，供連線規格參考來源的標籤、說明和圖示。

接下來，請依照下列步驟設定您的連線規格。 如需可新增至來源的不同功能（例如進階排程、自訂結構描述或不同分頁型別）的其他指引，請檢閱[設定來源規格](../config/sourcespec.md)的指南。

## 複製連線規格範本

收集到必要的成品後，請將下方的連線規格範本複製並貼到您選擇的文字編輯器中，然後使用與特定來源相關的資訊更新括弧`{}`中的屬性。

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
    "documentationLink": "https://docs.adobe.com/content/help/zh-Hant/platform-learn/tutorials/data-ingestion/understanding-streaming-ingestion.html",
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

## 建立連線規格 {#create}

取得連線規格範本後，您現在可以開始撰寫新的連線規格，方法是填寫與來源對應的適當值。

連線規格可以分成兩個不同的部分：來源規格和探索規格。

請參閱下列檔案，以取得有關連線規格區段的詳細資訊：

* [設定您的來源規格](../config/sourcespec.md)
* [設定您的瀏覽規格](../config/explorespec.md)

更新您的規格資訊後，您可以透過向[!DNL Flow Service] API的`/connectionSpecs`端點發出POST請求來提交新的連線規格。

**API格式**

```http
POST /connectionSpecs
```

**要求**

以下請求是串流來源的完整編寫連線規格範例：

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
          "documentationLink": "https://docs.adobe.com/content/help/zh-Hant/platform-learn/tutorials/data-ingestion/understanding-streaming-ingestion.html",
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

成功的回應會傳回新建立的連線規格，包括其唯一的`id`。

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
        "documentationLink": "https://docs.adobe.com/content/help/zh-Hant/platform-learn/tutorials/data-ingestion/understanding-streaming-ingestion.html",
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

現在您已經建立了新的連線規格，您必須將其對應的連線規格ID加入現有的流程規格。 如需詳細資訊，請參閱[更新流程規格](./update-flow-specs.md)的教學課程。

若要修改您建立的連線規格，請參閱有關[更新連線規格](./update-connection-specs.md)的教學課程。
