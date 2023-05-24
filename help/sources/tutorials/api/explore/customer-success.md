---
keywords: Experience Platform；家庭；熱門主題；cs;CS；客戶成功系統
solution: Experience Platform
title: 使用流服務API探索客戶成功系統
description: 本教程使用流服務API來探索客戶成功(CS)系統。
exl-id: 453be69d-3d72-4987-81cd-67fa3be7ee59
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 2%

---

# 使用 [!DNL Flow Service] API

[!DNL Flow Service] 用於收集和集中Adobe Experience Platform內不同來源的客戶資料。 該服務提供了用戶介面和REST風格的API，所有支援的源都可從中連接。

本教程使用 [!DNL Flow Service] API，用於探索客戶成功(CS)系統。

## 快速入門

本指南要求對Adobe Experience Platform的下列組成部分有工作上的理解：

* [源](../../../home.md): [!DNL Experience Platform] 允許從各種源接收資料，同時讓您能夠使用 [!DNL Platform] 服務。
* [沙箱](../../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙箱，將單個沙箱 [!DNL Platform] 實例到獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

以下各節提供了您需要瞭解的其他資訊，以便使用 [!DNL Flow Service] API。

### 獲取基連接

為了使用 [!DNL Platform] API，必須具有有效的基連接ID。 如果尚未為要使用的CS系統建立基本連接，則可以通過以下教程建立一個基本連接：

* [Salesforce服務雲](../create/customer-success/salesforce-service-cloud.md)
* [立即服務](../create/customer-success/servicenow.md)

### 讀取示例API調用

本教程提供了示例API調用，以演示如何格式化請求。 這些包括路徑、必需的標頭和正確格式化的請求負載。 還提供了API響應中返回的示例JSON。 有關示例API調用文檔中使用的約定的資訊，請參見上的 [如何讀取示例API調用](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 的 [!DNL Experience Platform] 疑難解答指南。

### 收集所需標題的值

為了呼叫 [!DNL Platform] API，必須首先完成 [驗證教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份驗證教程將提供所有中每個必需標頭的值 [!DNL Experience Platform] API調用，如下所示：

* 授權：持 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

中的所有資源 [!DNL Experience Platform]包括那些 [!DNL Flow Service]，與特定虛擬沙箱隔離。 所有請求 [!DNL Platform] API需要一個標頭，該標頭指定操作將在以下位置進行的沙盒的名稱：

* x-sandbox-name: `{SANDBOX_NAME}`

所有包含負載(POST、PUT、PATCH)的請求都需要附加的媒體類型報頭：

* Content-Type: `application/json`

## 瀏覽資料表

使用CS系統的基本連接，可以通過執行GET請求來瀏覽資料表。 使用以下調用查找要檢查或插入的表的路徑 [!DNL Platform]。

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| 參數 | 說明 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | CS基連接的ID。 |

**要求**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/60a5c8b9-3c30-43ba-a5c8-b93c3093ba66/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應從CS系統返回表陣列。 查找要放入的表 [!DNL Platform] 並注意到 `path` 屬性，因為在下一步中需要提供該屬性來檢查其結構。

```json
[
    {
        "type": "table",
        "name": "Accepted Event Relation",
        "path": "AcceptedEventRelation",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Account",
        "path": "Account",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Account Change Event",
        "path": "AccountChangeEvent",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Account Clean Info",
        "path": "AccountCleanInfo",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## Inspect桌子的結構

要從CS系統檢查表的結構，請在將表的路徑指定為查詢參數時執行GET請求。

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| 參數 | 說明 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | CS基連接的ID。 |
| `{TABLE_PATH}` | 表的路徑。 |

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/60a5c8b9-3c30-43ba-a5c8-b93c3093ba66/explore?objectType=table&object=test1.Mytable' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回指定表的結構。 有關每個表列的詳細資訊位於 `columns` 陣列。

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "Id",
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
            },
            {
                "name": "Phone",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
        ]
    }
}
```

## 後續步驟

按照本教程，您已探索了CS系統，找到了要插入的表的路徑 [!DNL Platform]並獲取了有關其結構的資訊。 您可以在下一教程中使用此資訊 [從您的CS系統收集資料並將其引入平台](../collect/customer-success.md)。
