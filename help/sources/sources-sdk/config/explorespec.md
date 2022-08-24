---
keywords: Experience Platform；首頁；熱門主題；源；連接器；源連接器；源sdk;sdk;SDK
title: 配置自助源的瀏覽規範（批處理SDK）
topic-legacy: overview
description: 本文檔概述了使用自助源（批處理SDK）所需準備的配置。
exl-id: 423a7e56-9dd1-4071-bd26-ee4f9f206122
source-git-commit: 4d7799b01c34f4b9e4a33c130583eadcfdc3af69
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 2%

---

# 配置自助源的瀏覽規範（批處理SDK）

「瀏覽」規範定義了瀏覽和檢查源中包含的對象所需的參數。 瀏覽規範還定義在瀏覽和檢查對象時返回的響應格式。

>[!TIP]
>
>瀏覽規範是硬編碼的，您只需將負載複製並貼上到連接規範下。

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

| 瀏覽規格 | 說明 | 範例 |
| --- | --- | --- |
| `name` | 定義瀏覽規範的名稱或標識符。 | `Resource` |
| `type` | 定義瀏覽規範的類型。 | `Resource` |
| `requestSpec` | 包含瀏覽連接中的對象所需的參數。 |
| `requestSpec.type` | 定義請求規範的資料類型。 | `object` |
| `responseSpec` | 包含定義針對瀏覽調用返回的響應消息格式的參數。 |
| `responseSpec.type` | 定義響應規範的資料類型。 | `object` |
| `responseSpec.properties` | 包含有關如何格式化響應消息的資訊。 |
| `responseSpec.properties.format` | 定義響應架構的格式。 | `object` |
| `responseSpec.properties.format.type` | 定義屬性的資料類型。 | `string` |
| `responseSpec.schema` | 包含有關如何格式化響應架構的資訊。 |
| `responseSpec.schema.type` | 定義架構的資料類型。 | `object` |
| `responseSpec.schema.properties` | 包含有關架構中保留的列、類型和項的資訊。 |
| `responseSpec.schema.properties.columns.items.properties.name` | 顯示檔案的名稱。 |
| `responseSpec.schema.properties.columns.items.properties.name.type` | 定義檔案名的資料類型。 | `string` |

{style=&quot;table-layout:auto&quot;}

## 後續步驟

在填充了瀏覽規範後，您可以使用 [!DNL Flow Service] API。 查看 [自助源（批處理SDK）API指南](../api/api-overview.md) 的子菜單。
