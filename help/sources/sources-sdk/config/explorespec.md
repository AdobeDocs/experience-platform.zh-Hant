---
keywords: Experience Platform；首頁；熱門主題；來源；連接器；來源連接器；來源sdk;sdk; SDK
title: 配置自助源(Batch SDK)的瀏覽規格
description: 本檔案概述使用自助來源（批次SDK）所需準備的設定。
exl-id: 423a7e56-9dd1-4071-bd26-ee4f9f206122
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 2%

---

# 配置自助源(Batch SDK)的瀏覽規格

「瀏覽」規範定義了瀏覽和檢查源中包含的對象所需的參數。 「瀏覽」規範還定義在探索和檢查對象時返回的響應格式。

>[!TIP]
>
>探索規格是硬式編碼，您只需將下方的裝載複製並貼到連線規格中即可。

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

| 了解規格 | 說明 | 範例 |
| --- | --- | --- |
| `name` | 定義瀏覽規範的名稱或標識符。 | `Resource` |
| `type` | 定義瀏覽規範的類型。 | `Resource` |
| `requestSpec` | 包含瀏覽連接中的對象所需的參數。 |
| `requestSpec.type` | 定義請求規格的資料類型。 | `object` |
| `responseSpec` | 包含定義根據探索呼叫傳回之回應訊息格式的參數。 |
| `responseSpec.type` | 定義響應規範的資料類型。 | `object` |
| `responseSpec.properties` | 包含與回應訊息的格式化相關的資訊。 |
| `responseSpec.properties.format` | 定義回應架構的格式。 | `object` |
| `responseSpec.properties.format.type` | 定義屬性的資料類型。 | `string` |
| `responseSpec.schema` | 包含與如何格式化回應架構相關的資訊。 |
| `responseSpec.schema.type` | 定義架構的資料類型。 | `object` |
| `responseSpec.schema.properties` | 包含有關架構中保留的列、類型和項的資訊。 |
| `responseSpec.schema.properties.columns.items.properties.name` | 顯示檔案的名稱。 |
| `responseSpec.schema.properties.columns.items.properties.name.type` | 定義檔案名的資料類型。 | `string` |

{style=&quot;table-layout:auto&quot;}

## 後續步驟

填入瀏覽規格後，您可以繼續使用 [!DNL Flow Service] API。 請參閱 [自助來源（批次SDK）API指南](../api/api-overview.md) 以取得更多資訊。
