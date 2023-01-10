---
keywords: Experience Platform；首頁；熱門主題；第三方資料庫；資料庫流服務
solution: Experience Platform
title: 使用流服務API探索資料庫
description: 本教學課程使用流量服務API來探索協力廠商資料庫的內容和檔案結構。
exl-id: 94935492-a7be-48dc-8089-18476590bf98
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 2%

---

# 使用 [!DNL Flow Service] API

本教學課程使用 [!DNL Flow Service] 探索協力廠商資料庫的內容和檔案結構的API。

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../../home.md): [!DNL Experience Platform] 可讓您從各種來源擷取資料，同時使用來建構、加標籤及增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../../sandboxes/home.md): [!DNL Experience Platform] 提供可分割單一沙箱的虛擬沙箱 [!DNL Platform] 例項放入個別的虛擬環境，以協助開發及改進數位體驗應用程式。

以下章節提供您需要知道的其他資訊，以便使用 [!DNL Flow Service] API。

### 收集所需憑據

本教學課程要求您與要從中內嵌資料的第三方資料庫建立有效連線。 有效的連接涉及資料庫的連接規範ID和連接ID。 有關建立資料庫連接和檢索這些值的詳細資訊，請參見 [來源連接器概觀](./../../../home.md#database).

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定要求格式。 這些功能包括路徑、必要標題和格式正確的請求裝載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所使用慣例的相關資訊，請參閱 [如何閱讀API呼叫範例](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 在 [!DNL Experience Platform] 疑難排解指南。

### 收集必要標題的值

若要對 [!DNL Platform] API，您必須先完成 [驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en). 完成驗證教學課程可提供所有E中每個必要標題的值[!DNL xperience Platform] API呼叫，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

中的所有資源 [!DNL Experience Platform]，包括 [!DNL Flow Service]，會與特定虛擬沙箱隔離。 所有請求 [!DNL Platform] API需要標頭，以指定要在中執行操作的沙箱名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含裝載(POST、PUT、PATCH)的請求都需要其他媒體類型標題：

* `Content-Type: application/json`

## 探索資料表

使用資料庫的連接ID，可以通過執行GET請求來瀏覽資料表。 使用以下調用查找要檢查或將其嵌入的表的路徑 [!DNL Platform].

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| 參數 | 說明 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 資料庫源的連接ID。 |

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

成功的響應從資料庫返回表陣列。 找到要放進的桌子 [!DNL Platform] 並注意 `path` 屬性，因為您必須在下一個步驟中提供屬性，以檢查其結構。

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

## Inspect表的結構

要從資料庫檢查表的結構，請執行GET請求，同時將表的路徑指定為查詢參數。

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| 參數 | 說明 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 資料庫連接的ID。 |
| `{TABLE_PATH}` | 表的路徑。 |

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

成功的響應返回指定表的結構。 有關表格各欄的詳細資訊位於 `columns` 陣列。

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
    }
}
```

## 後續步驟

按照本教程，您已探索了資料庫，找到了要嵌入的表的路徑 [!DNL Platform]，並取得其結構的相關資訊。 您可以在下一個教學課程中使用此資訊，以 [從資料庫收集資料並匯入Platform](../collect/database-nosql.md).
