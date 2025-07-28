---
title: 使用流程服務API探索資料庫
description: 本教學課程使用流程服務API來探索協力廠商資料庫的內容和檔案結構。
exl-id: 94935492-a7be-48dc-8089-18476590bf98
source-git-commit: 46e1a62e558a209ffed4a693cfd71ad5e76d7d98
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 6%

---

# 使用[!DNL Flow Service] API探索資料庫

此教學課程使用[!DNL Flow Service] API來探索協力廠商資料庫的內容和檔案結構。

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

* [來源](../../../home.md)： Experience Platform允許從各種來源擷取資料，同時讓您能夠使用Experience Platform服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../sandboxes/home.md)： Experience Platform提供的虛擬沙箱可將單一Experience Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

下列章節提供您需瞭解的其他資訊，才能使用[!DNL Flow Service] API成功連線至協力廠商資料庫。

### 使用Experience Platform API

如需如何成功呼叫Experience Platform API的詳細資訊，請參閱[Experience Platform API快速入門](../../../../landing/api-guide.md)指南。

## 探索您的資料表

使用資料庫的連線ID，您可以執行GET請求來探索資料表格。 使用以下呼叫來尋找您要檢查或擷取至Experience Platform的表格路徑。

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| 參數 | 說明 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 資料庫來源的連線ID。 |

**要求**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/6990abad-977d-41b9-a85d-17ea8cf1c0e4/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會從資料庫傳回資料表陣列。 尋找您要帶入Experience Platform的表格並記下其`path`屬性，因為您必須在下一個步驟中提供它以檢查其結構。

```json
[
    {
        "type": "table",
        "name": "test1.Mytable",
        "path": "test1.Mytable",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "test1.austin_demo",
        "path": "test1.austin_demo",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## 檢查表格的結構

若要從資料庫檢查表格結構，請在將表格路徑指定為查詢引數時執行GET要求。

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| 參數 | 說明 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 資料庫連線的識別碼。 |
| `{TABLE_PATH}` | 表格的路徑。 |

**要求**

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connections/6990abad-977d-41b9-a85d-17ea8cf1c0e4/explore?objectType=table&object=test1.Mytable' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回指定資料表的結構。 有關每個資料表資料行的詳細資料位於`columns`陣列的元素中。

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "TestID",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Name",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            }
        ]
    },
    "data": [],
    "cdcMetadata": {
      "columnDetected": true
    }
}
```

## 後續步驟

按照本教學課程，您已探索您的資料庫、找到您要擷取至Experience Platform的表格路徑，並取得有關其結構的資訊。 您可以在下一個教學課程中使用此資訊，從資料庫[收集資料並將其帶入Experience Platform](../collect/database-nosql.md)。
