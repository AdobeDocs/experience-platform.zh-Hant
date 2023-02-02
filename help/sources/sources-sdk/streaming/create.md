---
title: 使用流量服務API為串流SDK建立新的連線規格
description: 以下文檔提供了有關如何使用流服務API建立連接規範以及通過自助源整合新源的步驟。
hide: true
hidefromtoc: true
source-git-commit: f91ebcf8e27fd7d9019c5bb6d270b89fd08785ef
workflow-type: tm+mt
source-wordcount: '751'
ht-degree: 1%

---

# 使用 [!DNL Flow Service] API

連接規範表示源的結構。 它包含有關源的身份驗證要求的資訊，定義如何探索和檢查源資料，並提供有關給定源的屬性的資訊。 此 `/connectionSpecs` 端點 [!DNL Flow Service] API可讓您以程式設計方式管理組織內的連線規格。

以下文檔提供了如何使用 [!DNL Flow Service] API並透過自助來源（串流SDK）整合新來源。

## 快速入門

繼續之前，請檢閱 [快速入門手冊](./getting-started.md) 如需相關檔案的連結，請參閱本檔案中讀取範例API呼叫的指南，以及成功呼叫任何Experience PlatformAPI所需的必要標頭重要資訊。

## 收整合品

若要使用自助來源建立新的串流來源，您必須先與Adobe協調、請求私人Git存放庫，並與來源之標籤、說明、類別和圖示的詳細資訊Adobe一致。

提供後，您必須依此方式建構私人Git存放庫：

* 來源
   * {your_source}
      * 成品
         * {your_source}-category.txt
         * {your_source}-description.txt
         * {your_source}-icon.svg
         * {your_source}-label.txt
         * {your_source}-connectionSpec.json

| 對象（檔案名） | 說明 | 範例 |
| --- | --- | --- |
| {your_source} | 源的名稱。 此資料夾應會在您的私人Git存放庫中，包含與來源相關的所有成品。 | `medallia` |
| {your_source}-category.txt | 源所屬的類別，格式為文本檔案。 **附註**:如果您認為您的來源不符合上述任何類別，請連絡您的Adobe代表以討論。 | `medallia-category.txt` 在檔案內，請指定源的類別，如： `streaming`. |
| {your_source}-description.txt | 您的來源的簡短說明。 | [!DNL Medallia] 是行銷自動化來源，您可用來 [!DNL Medallia] 資料Experience Platform。 |
| {your_source}-icon.svg | 要在Experience Platform源目錄中表示源的影像。 此表徵圖必須是SVG檔案。 |
| {your_source}-label.txt | 源應顯示在Experience Platform源目錄中的名稱。 | 梅達利亞 |
| {your_source}-connectionSpec.json | 包含源的連接規範的JSON檔案。 此檔案最初不是必需的，因為您將在完成本指南時填充連接規範。 | `medallia-connectionSpec.json` |

{style=&quot;table-layout:auto&quot;}

>[!TIP]
>
>在連接規範的測試期間，您可以使用 `text` 在連接規範中。

將必要的檔案新增至私人Git存放庫後，您就必須建立提取請求(PR)，供Adobe檢閱。 核准並合併您的PR後，系統會提供ID，供連線規格參考來源的標籤、說明和圖示。

接下來，請按照以下步驟配置連接規範。 如需您可新增至來源的不同功能（例如進階排程、自訂結構或不同分頁類型）的其他指引，請參閱 [配置源規範](../config/sourcespec.md).

## 複製連接規範模板

收集到所需的成品後，將下面的連接規範模板複製並貼到所選的文本編輯器中，然後以方括弧更新屬性 `{}` 與特定來源相關的資訊。

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
  "authSpec": [

  ],
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
  }
}
```

## 建立連接規範 {#create}

獲得連接規範模板後，您現在可以通過填寫與源對應的適當值來開始創作新的連接規範。

連接規範可分為兩個不同的部分：源規範和探索規範。

有關連接規範各節的詳細資訊，請參閱以下文檔：

* [配置源規範](../config/sourcespec.md)
* [配置瀏覽規範](../config/explorespec.md)

更新規範資訊後，您可以通過向 `/connectionSpecs` 端點 [!DNL Flow Service] API。

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

成功的響應返回新建立的連接規範，包括其唯一性 `id`.

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

現在，您已建立了新的連接規範，必須將其對應的連接規範ID添加到現有流規範中。 請參閱 [更新流規範](./update-flow-specs.md) 以取得更多資訊。

若要修改您建立的連線規格，請參閱 [更新連接規範](./update-connection-specs.md).
