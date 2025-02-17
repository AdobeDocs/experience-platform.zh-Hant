---
title: 使用流量服務API建立Microsoft Dynamics基本連線
description: 瞭解如何使用流量服務API將Platform連線至Microsoft Dynamics帳戶。
exl-id: 423c6047-f183-4d92-8d2f-cc8cc26647ef
source-git-commit: bda26fa4ecf4f54cb36ffbedf6a9aa13faf7a09d
workflow-type: tm+mt
source-wordcount: '1102'
ht-degree: 3%

---

# 使用[!DNL Flow Service] API連線[!DNL Microsoft Dynamics]至Experience Platform

閱讀本指南，瞭解如何使用[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/)將您的[!DNL Microsoft Dynamics]來源連結至Adobe Experience Platform。

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

* [來源](../../../../home.md)： Experience Platform允許從各種來源擷取資料，同時讓您能夠使用Platform服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)： Experience Platform提供的虛擬沙箱可將單一Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱[Platform API快速入門](../../../../../landing/api-guide.md)的指南。

下列章節提供您需瞭解的其他資訊，才能使用[!DNL Flow Service] API成功連線Platform至Dynamics帳戶。

### 收集必要的認證

為了讓[!DNL Flow Service]連線到[!DNL Dynamics]，您必須提供下列連線屬性的值：

>[!BEGINTABS]

>[!TAB 基本驗證]

| 認證 | 說明 |
| --- | --- |
| `serviceUri` | [!DNL Dynamics]執行個體的服務URL。 |
| `username` | 您的[!DNL Dynamics]使用者帳戶的使用者名稱。 |
| `password` | 您的[!DNL Dynamics]帳戶密碼。 |

>[!TAB 服務主體和金鑰驗證]

| 認證 | 說明 |
| --- | --- |
| `servicePrincipalId` | 您[!DNL Dynamics]帳戶的使用者端識別碼。 使用服務主體和金鑰式驗證時，需要此ID。 |
| `servicePrincipalKey` | 服務主體秘密金鑰。 使用服務主體和金鑰式驗證時，需要此認證。 |

>[!ENDTABS]

如需開始使用的詳細資訊，請參閱[此 [!DNL Dynamics] 檔案](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth)。

## 建立基礎連線

>[!TIP]
>
>建立後，您無法變更[!DNL Dynamics]基本連線的驗證型別。 若要變更驗證型別，您必須建立新的基礎連線。

基本連線會保留來源與Experience Platform之間的資訊，包括來源的驗證認證、連線的目前狀態，以及唯一的基本連線ID。 基礎連線ID可讓您從來源內部探索及導覽檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

若要建立基底連線ID，請在提供您的[!DNL Dynamics]驗證認證作為要求引數的一部分時，對`/connections`端點提出POST要求。

**API格式**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB 基本驗證]

若要使用基本驗證建立[!DNL Dynamics]基本連線，請在提供連線的`serviceUri`、`username`和`password`的值時，對[!DNL Flow Service] API提出POST要求。

**要求**

下列要求使用基本驗證建立[!DNL Dynamics]來源的基本連線。

+++選取以檢視請求範例

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Dynamics connection",
      "description": "Dynamics connection using basic auth",
      "auth": {
          "specName": "Basic Authentication for Dynamics-Online",
          "params": {
              "serviceUri": "{SERVICE_URI}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}"
          }
      },
      "connectionSpec": {
          "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
          "version": "1.0"
      }
  }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `auth.params.serviceUri` | 與您的[!DNL Dynamics]執行個體關聯的服務URI。 |
| `auth.params.username` | 與您的[!DNL Dynamics]帳戶相關聯的使用者名稱。 |
| `auth.params.password` | 與您的[!DNL Dynamics]帳戶關聯的密碼。 |
| `connectionSpec.id` | [!DNL Dynamics]連線規格識別碼： `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

+++

**回應**

成功的回應會傳回新建立的基礎連線，包括其唯一識別碼(`id`)。

+++選取以檢視回應範例

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

+++

>[!TAB 服務主要金鑰式驗證]

若要使用服務主體金鑰式驗證來建立[!DNL Dynamics]基底連線，請對[!DNL Flow Service] API提出POST要求，同時為您連線的`serviceUri`、`servicePrincipalId`和`servicePrincipalKey`提供值。

**要求**

下列要求會使用基本服務主要金鑰式驗證，為[!DNL Dynamics]來源建立基礎連線。

+++選取以檢視請求範例

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Dynamics connection",
      "description": "Dynamics connection using key-based authentication",
      "auth": {
          "specName": "Service Principal Key Based Authentication",
          "params": {
              "serviceUri": "{SERVICE_URI}",
              "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
              "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}"
          }
      },
      "connectionSpec": {
          "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
          "version": "1.0"
      }
  }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `auth.params.serviceUri` | 與您的[!DNL Dynamics]執行個體關聯的服務URI。 |
| `auth.params.servicePrincipalId` | 您[!DNL Dynamics]帳戶的使用者端識別碼。 使用服務主體和金鑰式驗證時，需要此ID。 |
| `auth.params.servicePrincipalKey` | 服務主體秘密金鑰。 使用服務主體和金鑰式驗證時，需要此認證。 |
| `connectionSpec.id` | [!DNL Dynamics]連線規格識別碼： `38ad80fe-8b06-4938-94f4-d4ee80266b07` |

+++

**回應**

成功的回應會傳回新建立的連線，包括其唯一識別碼(`id`)。

+++選取以檢視回應範例

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

+++

>[!ENDTABS]

## 探索您的資料表

若要探索您的[!DNL Dynamics]資料表，請向`/connections/{BASE_CONNECTION_ID}/explore`端點發出GET請求，並提供您的基本連線ID作為查詢引數的一部分。

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| 查詢參數 | 說明 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 基礎連線的ID。 使用此ID來探索來源的內容和結構。 |

**要求**

下列要求會擷取基底連線識別碼為`dd668808-25da-493f-8782-f3433b976d1e`之[!DNL Dynamics]來源的可用資料表和檢視清單。

+++選取以檢視請求範例

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/dd668808-25da-493f-8782-f3433b976d1e/explore?objectType=root' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**回應**

成功的回應傳回根層級的[!DNL Dynamics]資料表和檢視目錄。

+++選取以檢視回應範例

```json
[
    {
        "type": "table",
        "name": "systemuserlicenses",
        "path": "systemuserlicenses",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Process Dependency",
        "path": "workflowdependency",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "view",
        "name": "accountView1",
        "path": "accountView1",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "view",
        "name": "Inactive_ACC_custom",
        "path": "Inactive_ACC_custom",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

+++


## 檢查表格的結構

若要檢查特定表格的結構，請向`/connections/{BASE_CONNECTION_ID}/explore`發出GET請求，並提供特定表格的路徑作為查詢引數。

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?object={TABLE_PATH}&objectType=table
```

| 查詢引數 | 說明 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 基礎連線的ID。 使用此ID來探索來源的內容和結構。 |
| `{TABLE_PATH}` | 您要探索的特定表格的路徑。 |

**要求**

下列要求會擷取路徑為`workflowdependency`之[!DNL Dynamics]表格的結構和內容。

+++選取以檢視請求範例

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/dd668808-25da-493f-8782-f3433b976d1e/explore?object=workflowdependency&objectType=table' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**回應**

成功的回應傳迴路徑`workflowdependency`的內容。

+++選取以檢視回應範例

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "first_name",
                "type": "string",
                "meta": {
                    "originalType": "String"
                }
            },
            {
                "name": "last_name",
                "type": "string",
                "meta": {
                    "originalType": "String"
                }
            },
            {
                "name": "email",
                "type": "string",
                "meta": {
                    "originalType": "String"
                }
            }
        ]
    }
}
```

+++

## 檢查檢視的結構

在[!DNL Dynamics]中，檢視是指要顯示的欄、每欄的寬度、記錄清單排序的預設系統，以及套用的預設篩選器，以限制清單中出現的記錄。

若要檢查檢視的結構，請向`/connections/{BASE_CONNECTION_ID}/explore`發出GET要求，並在您的查詢引數中指定檢視路徑。 此外，您必須指定`objectType`為`view`。

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?object={VIEW_PATH}&objectType=view
```

| 查詢引數 | 說明 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 基礎連線的ID。 使用此ID來探索來源的內容和結構。 |
| `{VIEW_PATH}` | 您要檢查的檢視的路徑。 |

**要求**

下列要求會擷取`accountView1`。

+++選取以檢視請求範例

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/dd668808-25da-493f-8782-f3433b976d1e/explore?object=accountView1&objectType=view' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**回應**

成功的回應傳回`accountView1`的結構。

+++選取以檢視回應範例

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "name",
                "type": "string",
                "meta": {
                    "originalType": "string"
                },
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "fetchxml",
                "type": "string",
                "meta": {
                    "originalType": "string"
                },
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "querytype",
                "type": "integer",
                "meta": {
                    "originalType": "int"
                },
                "xdm": {
                    "type": "integer",
                    "minimum": -2147483648,
                    "maximum": 2147483647
                }
            },
            {
                "name": "userqueryid",
                "type": "string",
                "meta": {
                    "originalType": "guid"
                },
                "xdm": {
                    "type": "string"
                }
            }
        ]
    }
}
```

+++

## 預覽實體型別檢視

若要預覽檢視的內容，請向`/connections/{BASE_CONNECTION_ID}/explore`發出GET請求，並在您的查詢引數中包含檢視路徑以及`preview=true`。

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?object={VIEW_PATH}&preview=true&objectType=view
```

| 查詢引數 | 說明 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 基礎連線的ID。 使用此ID來探索來源的內容和結構。 |
| `{VIEW_PATH}` | 您要檢查的檢視的路徑。 |


**要求**

下列要求會預覽`accountView1`的內容。

+++選取以檢視請求範例

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/dd668808-25da-493f-8782-f3433b976d1e/explore?object=accountView1&preview=true&objectType=view' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**回應**

成功的回應傳回`accountView1`的內容。

+++選取以檢視回應範例

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "emailaddress1",
                "type": "string",
                "meta": {
                    "originalType": "string"
                },
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "contactid",
                "type": "string",
                "meta": {
                    "originalType": "guid"
                },
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "fullname",
                "type": "string",
                "meta": {
                    "originalType": "string"
                },
                "xdm": {
                    "type": "string"
                }
            }
        ]
    },
    "data": [
        {
            "contactid": "396e19de-0852-ec11-8c62-00224808a1df",
            "fullname": "Tim Barr",
            "emailaddress1": "barrtim@googlemedia.com"
        }
    ]
}
```

+++

## 建立來源連線以擷取檢視

若要建立來源連線並擷取檢視，請對`/sourceConnections`端點提出POST要求、提供資料表名稱，並在要求內文中將`entityType`指定為`view`。

**API格式**

```http
POST /sourceConnections
```

**要求**

下列要求會建立[!DNL Dynamics]來源連線並擷取檢視。

+++選取以檢視請求範例

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Dynamics Source Connection",
      "description": "Dynamics Source Connection",
      "baseConnectionId": "dd668808-25da-493f-8782-f3433b976d1e",
      "data": {
          "format": "tabular",
          "schema": null,
          "properties": null
      },
      "params": {
          "tableName": "Contacts with name TIM",
          "entityType": "view"
      },
      "connectionSpec": {
          "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
          "version": "1.0"
      }
  }'
```

+++

**回應**

成功的回應會傳回新產生的來源連線ID及其對應的電子標籤。

+++選取以檢視回應範例

```json
{
    "id": "e566bab3-1b58-428c-b751-86b8cc79a3b4",
    "etag": "\"82009592-0000-0200-0000-678121030000\""
}
```

+++

## 後續步驟

依照此教學課程，您已使用[!DNL Flow Service] API建立[!DNL Microsoft Dynamics]基礎連線。 您可以在下列教學課程中使用此基本連線ID：

* [使用 [!DNL Flow Service] API探索資料表的結構和內容](../../explore/tabular.md)
* [使用 [!DNL Flow Service] API建立資料流以將CRM資料帶入Platform](../../collect/crm.md)
