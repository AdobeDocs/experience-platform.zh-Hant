---
keywords: Experience Platform；首頁；熱門主題；來源；聯結器；來源聯結器；來源sdk；sdk；SDK
title: 設定自助式來源的探索規格(批次SDK)
description: 本檔案提供使用自助來源(批次SDK)所需準備的設定概述。
exl-id: 423a7e56-9dd1-4071-bd26-ee4f9f206122
source-git-commit: 16cc811a545414021b8686ae303d6112bcf6cebb
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 1%

---

# 設定自助式來源的探索規格(批次SDK)

瀏覽規格定義瀏覽和檢查來源中所含物件所需的引數。 探索規格也會定義探索及檢查物件時傳回的回應格式。

>[!TIP]
>
>探索規格採用硬式編碼，您只需將下方的裝載複製並貼到您的連線規格即可。

```json
"exploreSpec": {
  "name": "Resource",
  "type": "Resource",
  "requestSpec": {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "type": "object"
  },
  "responseSpec": {
    "$schema": "http: //json-schema.org/draft-07/schema#",
    "type": "object",
    "properties": {
      "format": {
        "type": "string"
      },
      "schema": {
        "type": "object",
        "properties": {
          "columns": {
            "type": "array",
            "items": {
              "type": "object",
              "properties": {
                "name": {
                  "type": "string"
                },
                "type": {
                  "type": "string"
                }
              }
            }
          }
        }
      },
      "data": {
        "type": "array",
        "items": {
          "type": "object"
        }
      }
    }
  }
}
```

| 探索規格 | 說明 | 範例 |
| --- | --- | --- |
| `name` | 定義瀏覽規格的名稱或識別碼。 | `Resource` |
| `type` | 定義瀏覽規格的型別。 | `Resource` |
| `requestSpec` | 包含探索連線中物件所需的引數。 |  |
| `requestSpec.type` | 定義要求規格的資料型別。 | `object` |
| `responseSpec` | 包含定義回應訊息（針對探索呼叫傳回）格式的引數。 |  |
| `responseSpec.type` | 定義回應規格的資料型別。 | `object` |
| `responseSpec.properties` | 包含與回應訊息格式相關之資訊。 |  |
| `responseSpec.properties.format` | 定義回應結構的格式。 | `object` |
| `responseSpec.properties.format.type` | 定義屬性的資料型別。 | `string` |
| `responseSpec.schema` | 包含與回應結構描述格式相關之資訊。 |  |
| `responseSpec.schema.type` | 定義結構描述的資料型別。 | `object` |
| `responseSpec.schema.properties` | 包含有關資料行、型別和結構描述內儲存專案的資訊。 |  |
| `responseSpec.schema.properties.columns.items.properties.name` | 顯示檔案的名稱。 |  |
| `responseSpec.schema.properties.columns.items.properties.name.type` | 定義檔案名稱的資料型別。 | `string` |

{style="table-layout:auto"}

## 後續步驟

填入您的瀏覽規格後，您就可以繼續使用[!DNL Flow Service] API建立完整的連線規格。 如需詳細資訊，請參閱[自助式來源(批次SDK) API指南](../api/api-overview.md)。
