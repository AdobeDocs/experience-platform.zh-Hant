---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用Flow Service API探索資料庫或NoSQL系統
topic: overview
translation-type: tm+mt
source-git-commit: 4c34ecdaeb4a0df1faf2dd54e8a264b9126f20b4

---


# 使用Flow Service API探索資料庫或NoSQL系統

Flow Service用於收集和集中Adobe Experience Platform內不同來源的客戶資料。 該服務提供用戶介面和REST風格的API，所有支援的源都可從中連接。

本教程使用Flow Service API來探索資料庫或NoSQL系統。

## 快速入門

本指南需要有效瞭解Adobe Experience Platform的下列元件：

* [來源](../../../home.md):Experience Platform可讓您從各種來源擷取資料，同時讓您能夠使用平台服務來建構、標示和增強傳入資料。
* [沙盒](../../../../sandboxes/home.md):Experience Platform提供虛擬沙盒，可將單一Platform實例分割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您需要知道的其他資訊，以便使用流服務API成功連接到資料庫或NoSQL系統。

### 獲得基本連接

要使用平台API來探索資料庫或NoSQL系統，您必須擁有有效的基本連接ID。 如果您尚未建立資料庫或NoSQL系統的基本連接，則可以通過以下教程建立一個：

* [Amazon Redshift](../create/databases/redshift.md)
* [Apache Spark on Azure HDInsights ](../create/databases/spark.md)
* [Azure突觸分析](../create/databases/synapse-analytics.md)
* [Azure表格儲存](../create/databases/ats.md)
* [Google BigQuery](../create/databases/bigquery.md)
* [Hive](../create/databases/hive.md)
* [MariaDB](../create/databases/mariadb.md)
* [MySQL](../create/databases/mysql.md)
* [鳳凰城](../create/databases/phoenix.md)
* [PostgreSQL](../create/databases/postgres.md)
* [SQL Server](../create/databases/sql-server.md)

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱「Experience Platform疑難排解指 [南」中有關如何讀取範例API呼叫的章節](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 。

### 收集必要標題的值

若要呼叫平台API，您必須先完成驗證教 [學課程](../../../../tutorials/authentication.md)。 完成驗證教學課程後，所有Experience Platform API呼叫中每個必要標題的值都會顯示在下方：

* 授權：生產者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有資源（包括屬於Flow Service的資源）都隔離至特定的虛擬沙盒。 所有對平台API的請求都需要一個標題，該標題會指定要在中執行的操作的沙盒名稱：

* x-sandbox-name: `{SANDBOX_NAME}`

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的媒體類型標題：

* 內容類型： `application/json`

## 探索您的資料表格

使用資料庫或NoSQL系統的基本連接，可以通過執行GET請求來瀏覽資料表。 使用以下調用查找要檢查或裝入平台的表的路徑。

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| 參數 | 說明 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 資料庫或NoSQL基連接的ID。 |

**請求**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/54c22133-3a01-4d3b-8221-333a01bd3b03/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應從資料庫或NoSQL系統返回表陣列。 尋找您要帶入Platform的表格，並記下其屬性，因為您必須在下一 `path` 步驟中提供表格以檢查其結構。

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

## 檢查表格結構

要從資料庫或NoSQL系統檢查表的結構，請在將表的路徑指定為查詢參數時執行GET請求。

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| 參數 | 說明 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 資料庫或NoSQL基連接的ID。 |
| `{TABLE_PATH}` | 表的路徑。 |

**請求**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/54c22133-3a01-4d3b-8221-333a01bd3b03/explore?objectType=table&object=test1.Mytable' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回指定表的結構。 有關每個表列的詳細資訊位於陣列的元 `columns` 素中。

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

通過本教程，您已探索了資料庫或NoSQL系統，找到了要添加到平台中的表的路徑，並獲取了有關其結構的資訊。 您可以在下一個教程中使用此信 [息從資料庫或NoSQL系統收集資料並將其導入平台](../collect/database-nosql.md)。