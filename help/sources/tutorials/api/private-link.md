---
title: 來源中的私人連結支援
description: 瞭解如何建立並使用Adobe Experience Platform來源的私人連結
badge: Beta
hide: true
hidefromtoc: true
source-git-commit: 4c91ffc60a2537fcc76ce935bf3b163984fdc5e4
workflow-type: tm+mt
source-wordcount: '1326'
ht-degree: 5%

---

# 來源中的私人連結支援

>[!AVAILABILITY]
>
>此功能處於「有限可用性」，目前僅受以下來源支援：
>
>* [[!DNL Azure Blob]](../../connectors/cloud-storage/blob.md)
>* [[!DNL Azure Data Lake Gen2]](../../connectors/cloud-storage/adls-gen2.md)
>* [[!DNL Azure File Storage]](../../connectors/cloud-storage/azure-file-storage.md)
>* [[!DNL Snowflake]](../../connectors/databases/snowflake.md)

閱讀本指南，瞭解如何透過私人連結建立與Azure型來源的私人端點連線，並為您的資料提供更安全的傳輸機制。

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

* [來源](../../home.md)： Experience Platform允許從各種來源擷取資料，同時讓您能夠使用[!DNL Platform]服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../sandboxes/home.md)： Experience Platform提供的虛擬沙箱可將單一[!DNL Platform]執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱[Platform API快速入門](../../../landing/api-guide.md)的指南。

## 建立私人端點 {#create-private-endpoint}

若要建立私用端點，請向`/privateEndpoints`發出POST要求。

**API格式**

```http
POST /privateEndpoints
```

**要求**

以下請求會建立私有端點：

+++選取以檢視請求範例

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints/' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "ACME Private Endpoint",
      "subscriptionId": "4281a16a-696f-4993-a7d3-a3da32b846f3",
      "resourceGroupName": "acme-sources-experience-platform",
      "resourceName": "acmeexperienceplatform",
      "fqdns": [],
      "connectionSpec": {
          "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
          "version": "1.0"
    }
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 您的私人端點的名稱。 |
| `subscriptionId` | 與您的[!DNL Azure]訂閱相關聯的識別碼。 如需詳細資訊，請參閱[的[!DNL Azure]指南，從 [!DNL Azure Portal]](https://learn.microsoft.com/en-us/azure/azure-portal/get-subscription-tenant-id)擷取您的訂閱和租使用者ID。 |
| `resourceGroupName` | [!DNL Azure]上資源群組的名稱。 資源群組包含[!DNL Azure]解決方案的相關資源。 如需詳細資訊，請閱讀[管理資源群組](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/manage-resource-groups-portal)的[!DNL Azure]指南。 |
| `resourceName` | 資源的名稱。 在[!DNL Azure]中，資源是指虛擬機器器、網頁應用程式和資料庫等執行個體。 如需詳細資訊，請閱讀[上的[!DNL Azure]指南，瞭解 [!DNL Azure] 資源管理員](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/overview)。 |
| `fqdns` | 您來源的完整網域名稱。 只有在使用[!DNL Snowflake]來源時，才需要此屬性。 |
| `connectionSpec.id` | 您使用之來源的連線規格ID。 |
| `connectionSpec.version` | 您正在使用的連線規格ID版本。 |

+++

**回應**

成功的回應會傳回以下內容：

+++選取以檢視回應範例

```json
{
  "id": "2c7f6574-299a-4832-aec5-886e875872e2",
  "name": "ACME Private Endpoint",
  "subscriptionId": "4281a16a-696f-4993-a7d3-a3da32b846f3",
  "resourceGroupName": "acme-sources-experience-platform",
  "resourceName": "acmeexperienceplatform",
  "fqdns": [],
  "connectionSpec": {
      "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
      "version": "1.0"
  },
  "state": "Pending"
}
```

| 屬性 | 說明 |
| --- | --- |
| `id` | 您新建立的私人端點的識別碼。 |
| `name` | 您的私人端點的名稱。 |
| `subscriptionId` | 與您的[!DNL Azure]訂閱相關聯的識別碼。 如需詳細資訊，請參閱[的[!DNL Azure]指南，從 [!DNL Azure Portal]](https://learn.microsoft.com/en-us/azure/azure-portal/get-subscription-tenant-id)擷取您的訂閱和租使用者ID。 |
| `resourceGroupName` | [!DNL Azure]上資源群組的名稱。 資源群組包含[!DNL Azure]解決方案的相關資源。 如需詳細資訊，請閱讀[管理資源群組](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/manage-resource-groups-portal)的[!DNL Azure]指南。 |
| `resourceName` | 資源的名稱。 在[!DNL Azure]中，資源是指虛擬機器器、網頁應用程式和資料庫等執行個體。 如需詳細資訊，請閱讀[上的[!DNL Azure]指南，瞭解 [!DNL Azure] 資源管理員](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/overview)。 |
| `fqdns` | 您來源的完整網域名稱。 只有在使用[!DNL Snowflake]來源時，才需要此屬性。 |
| `connectionSpec.id` | 您使用之來源的連線規格ID。 |
| `connectionSpec.version` | 您正在使用的連線規格ID版本。 |
| `state` | 您的私人端點的目前狀態。 有效狀態包括： <ul><li>`Pending`</li><li>`Failed`</li><li>`Approved`</li><li>`Rejected`</li></ul> |

+++

## 擷取私人端點的清單 {#retrieve-private-endpoints}

若要從您組織中的指定沙箱擷取私人端點清單，請向`/privateEndpoints`發出GET請求。

**API格式**

```http
GET /privateEndpoints
```

**要求**

下列請求會擷取貴組織中所有私人端點的清單。

+++選取以檢視請求範例

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**回應**

成功的回應會傳回組織中私人端點的清單。

+++選取以檢視回應範例

```json
{
  "items": [
       {
      "id": "ac9eb695-0d1a-42d4-bc45-0842aeaa1eff",
      "name": "TEST_E2E_29_Jan",
      "subscriptionId": "4281a16a-696f-4993-a7d3-a3da32b846f3",
      "resourceGroupName": "acme-noid-experience-platform",
      "resourceName": "acmeprivatelinking",
      "fqdns": [
         
      ],
      "state": "Approved",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      }
    },
          {
      "id": "4c9eb695-0d1a-42d4-bc45-0842aeaa1efr",
      "name": "TEST_E2E_29_Jan",
      "subscriptionId": "5a0ff2f3-53d6-47e4-abb5-10a18bd3fff0",
      "resourceGroupName": "acme-sources-experience-platform",
      "resourceName": "acmeexperienceplatform",
      "fqdns": [
         
      ],
      "state": "Pending",
      "connectionSpec": {
        "id": "b3ba5556-48be-44b7-8b85-ff2b69b46dc4",
        "version": "1.0"
      }
    } 
  ]
}
```

+++

## 擷取指定來源的私人端點清單 {#retrieve-private-endpoints-by-source}

若要擷取與特定來源對應的私人端點清單，請向`/privateEndpoints`端點發出GET要求並提供來源的`connectionSpec.id`。

**API格式**

```http
GET /privateEndpoints?property=connectionSpec.id=={CONNECTION_SPEC_ID}
```

| 查詢參數 | 說明 |
| --- | --- |
| `{CONNECTION_SPEC_ID}` | 您要搜尋私人端點的來源之連線規格ID。 |

**要求**

下列要求會擷取與具有連線規格ID之來源對應的所有私人端點的清單： `4c10e202-c428-4796-9208-5f1f5732b1cf`。

+++選取以檢視請求範例

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints?property=connectionSpec.id==4c10e202-c428-4796-9208-5f1f5732b1cf' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**回應**

成功的回應會傳回所有私人端點的清單，這些端點對應到連線規格ID為`4c10e202-c428-4796-9208-5f1f5732b1cf`的來源。

+++選取以檢視回應範例

```json
{
  "items": [
       {
      "id": "ac9eb695-0d1a-42d4-bc45-0842aeaa1eff",
      "name": "TEST_E2E_29_Jan",
      "subscriptionId": "4281a16a-696f-4993-a7d3-a3da32b846f3",
      "resourceGroupName": "acme-noid-experience-platform",
      "resourceName": "acmeprivatelinkhg",
      "fqdns": [
         
      ],
      "state": "Approved",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      }
    },
    {
      "id": "4c9eb695-0d1a-42d4-bc45-0842aeaa1efr",
      "name": "TEST_E2E_29_Jan",
      "subscriptionId": "5a0ff2f3-53d6-47e4-abb5-10a18bd3fff0",
      "resourceGroupName": "acme-sources-experience-platform",
      "resourceName": "acmeexperienceplatform",
      "fqdns": [
         
      ],
      "state": "Pending",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      }
    } 
  ]
}
```

+++

## 擷取私人端點 {#retrieve-specific-private-endpoint}

若要擷取特定的私用端點，請向`/privateEndpoints`發出GET請求，並提供您要擷取的私用端點識別碼。

**API格式**

```http
GET /privateEndpoints/{PRIVATE_ENDPOINT_ID}
```

| 查詢參數 | 說明 |
| --- | --- |
| `{PRIVATE_ENDPOINT_ID}` | 您要擷取的私人端點ID。 |

**要求**

下列要求會擷取識別碼為`2c5699b0-b9b6-486f-8877-ee5e21fe9a9d`的私用端點。

+++選取以檢視請求範例

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints/2c5699b0-b9b6-486f-8877-ee5e21fe9a9d' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**回應**

成功的回應傳回識別碼為`2c5699b0-b9b6-486f-8877-ee5e21fe9a9d`的私人端點

+++選取以檢視回應範例

```json
{
  "items": [
       {
      "id": "2c5699b0-b9b6-486f-8877-ee5e21fe9a9d",
      "name": "TEST_E2E_29_Jan",
      "subscriptionId": "5a0ff2f3-53d6-47e4-abb5-10a18bd3fff0",
      "resourceGroupName": "acme-noid-experience-platform",
      "resourceName": "acmeprivatelinkhg",
      "fqdns": [
         
      ],
      "state": "Approved",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      }
    }
  ]
}
```

+++

## 解析私人端點 {#resolve-private-endpoint}

**API格式**

```http
GET /privateEndpoints?op=autoResolve
```

**要求**

+++選取以檢視請求範例

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints?op=autoResolve' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "auth": {
          "specName": "ConnectionString",
          "params": {
              "usePrivateLink": true,
              "connectionString": "{CONNECTION_STRING}"
          }
      },
      "connectionSpec": {
          "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
          "version": "1.0"
      }
  }'
```

+++

**回應**

+++選取以檢視回應範例

```json
{
  "items": [
        {
      "id": "4c9eb695-0d1a-42d4-bc45-0842aeaa1efr",
      "name": "TEST_E2E_29_Jan",
      "subscriptionId": "5a0ff2f3-53d6-47e4-abb5-10a18bd3fff0",
      "resourceGroupName": "acme-sources-experience-platform",
      "resourceName": "acmeexperienceplatform",
      "fqdns": [
         
      ],
      "state": "Pending",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      } 
    }
  ]
}
```

+++

## 啟用互動式撰寫 {#enable-interactive-authoring}

互動式製作可用於探索連線或帳戶及預覽資料等功能。 若要啟用互動式撰寫，請向`/privateEndpoints/interactiveAuthoring`發出POST要求，並在查詢引數中將`enable`指定為運運算元。

**API格式**

```http
POST /privateEndpoints/interactiveAuthoring?op=enable
```

| 查詢參數 | 說明 |
| --- | --- |
| `op` | 您要執行的作業。 若要啟用互動式撰寫，請將`op`值設為`enable`。 |

**要求**

以下請求會啟用私人端點的互動式製作，並將TTL設為60分鐘。

+++選取以檢視請求範例

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints/interactiveAuthoring?op=enable' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "autoTerminationMinutes": 60
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `autoTerminationMinutes` | 互動式製作TTL （存留時間）只需幾分鐘即可完成。 互動式製作可用於探索連線或帳戶及預覽資料等功能。 您最多可以設定120分鐘的TTL。 預設TTL為60分鐘。 |

+++

**回應**

成功的回應會傳回HTTP狀態202 （已接受）。

## 擷取互動式撰寫狀態 {#retrieve-interactive-authoring-status}

若要檢視您私人端點的目前互動式撰寫狀態，請向`/privateEndpoints/interactiveAuthoring`發出GET請求。

**API格式**

```http
GET /privateEndpoints/interactiveAuthoring
```

**要求**

下列請求會擷取互動式編寫的狀態：

+++選取以檢視請求範例

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints/interactiveAuthoring' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**回應**

+++選取以檢視回應範例

```json
{
    "status": "Disabled"
}
```

| 屬性 | 說明 |
| --- | --- |
| `status` | 互動式撰寫的狀態。 有效值包括： `disabled`、`enabling`、`enabled`。 |

+++

## 刪除私人端點 {#delete-private-endpoint}

若要刪除您的私人端點，請向`/privateEndpoints`發出DELETE請求，並提供您要刪除的端點識別碼。

**API格式**

```http
DELETE /privateEndpoints/{PRIVATE_ENDPOINT_ID}
```

| 查詢參數 | 說明 |
| --- | --- |
| `{PRIVATE_ENDPOINT_ID}` | 您要刪除的私人端點ID。 |

**要求**

下列要求會刪除識別碼為`02a74b31-a566-4a86-9cea-309b101a7f24`的私人端點。

+++選取以檢視請求範例

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints/02a74b31-a566-4a86-9cea-309b101a7f24' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**回應**

成功的回應會傳回HTTP狀態200 （成功）。 您可以發出GET要求並向`/privateEndpoints`提供已刪除的ID作為查詢引數，以驗證刪除。

## 流程服務 {#flow-service}

請閱讀下列章節，以瞭解如何結合[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/)使用私人端點。

### 建立與私人端點的連線 {#create-base-connection}

若要在Experience Platform中建立與私人端點的連線，請對[!DNL Flow Service] API的`/connections`端點提出POST要求。

**API格式**

```http
POST /connections/
```

**要求**

下列要求會建立[!DNL Snowflake]的已驗證基底連線，同時使用私用端點。

+++選取以檢視請求範例

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections/' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Snowflake base connection",
      "description": "A base connection for a Snowflake source that uses a private link.",
      "auth": {
          "specName": "ConnectionString",
          "params": {
              "connectionString": "{CONNECTION_STRING}",
              "usePrivateLink" : true
          }
      },
      "connectionSpec": {
          "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
          "version": "1.0"
      }
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 基礎連線的名稱。 |
| `description` | （選用）提供連線其他資訊的說明。 |
| `auth.specName` | 用來將您的來源連線至Experience Platform的驗證。 |
| `auth.params.connectionString` | [!DNL Snowflake]連線字串。 如需詳細資訊，請閱讀[[!DNL Snowflake] API驗證指南](../api/create/databases/snowflake.md)。 |
| `auth.params.usePrivateLink` | 布林值，判斷您是否使用私人端點。 如果您使用私人端點，請將此值設為`true`。 |
| `connectionSpec.id` | [!DNL Snowflake]的連線規格ID。 |
| `connectionSpec.version` | 您的[!DNL Snowflake]連線規格ID的版本。 |

+++

**回應**

成功的回應會傳回您新產生的基本連線ID和etag。

+++選取以檢視回應範例

```json
{
  "id": "a59d368a-1152-4673-a46e-bd52e8cdb9a9",
  "etag": "\"f50185ed-0000-0200-0000-637e8fad0000\""
}
```

+++

### 擷取繫結至指定私人端點的連線 {#retrieve-connections-by-endpoint}

若要擷取繫結至特定私用端點的連線，請對`/connections`端點提出GET要求，並提供私用端點的識別碼作為查詢引數。

**API格式**

```http
GET /connections?property=auth.params.privateEndpointId=={PRIVATE_ENDPOINT_ID}
```

| 查詢參數 | 說明 |
| --- | --- |
| {PRIVATE_ENDPOINT_ID} | 繫結至您要擷取之連線的私人端點ID。 |

**要求**

下列要求會擷取繫結至識別碼為`02a74b31-a566-4a86-9cea-309b101a7f24`之私人端點的現有連線。

+++選取以檢視請求範例

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections?property=auth.params.privateEndpointId==02a74b31-a566-4a86-9cea-309b101a7f24' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**回應**

成功的回應會傳回繫結至所查詢私人端點的連線清單。

+++選取以檢視回應範例

```json
{
  "items": [
    {
      "id": "42a27b1f-8e3f-48ce-8c29-7e474b29a015",
      "createdAt": 1729154379292,
      "updatedAt": 1729154382031,
      "createdBy": "{CREATED_BY}",
      "updatedBy": "{UPDATED_BY}",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_NAME}",
      "name": "acme-e2e",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      },
      "state": "enabled",
      "auth": {
        "specName": "ConnectionString",
        "params": {
          "connectionString": "{CONNECTION_STRING}",
          "usePrivateLink": true,
          "privateEndpointId": "02a74b31-a566-4a86-9cea-309b101a7f24"
        }
      },
      "version": "\"2f01454b-0000-0200-0000-6766749a0000\"",
      "etag": "\"2f01454b-0000-0200-0000-6766749a0000\"",
      "lastOperation": {
        "started": 0,
        "updated": 0,
        "operation": "create"
      }
    },
    {
      "id": "6350311a-664c-4b08-aad4-4065781aac81",
      "createdAt": 1718199941102,
      "updatedAt": 1718199945147,
      "createdBy": "{CREATED_BY}",
      "updatedBy": "{UPDATED_BY}",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_NAME}",
      "name": "acme demo",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      },
      "state": "enabled",
      "auth": {
        "specName": "ConnectionString",
        "params": {
          "connectionString": "{CONNECTION_STRING}",
          "usePrivateLink": true,
          "privateEndpointId": "02a74b31-a566-4a86-9cea-309b101a7f24"
        }
      },
      "version": "\"3001307e-0000-0200-0000-6766cf710000\"",
      "etag": "\"3001307e-0000-0200-0000-6766cf710000\"",
      "lastOperation": {
        "started": 0,
        "updated": 0,
        "operation": "create"
      }
    }
  ],
  "_links": {
     
  }
}
```

+++

### 擷取與任何私人端點關聯的連線 {#retrieve-connections}

若要擷取與任何私用端點相關聯的連線，請對`/connections`端點提出GET要求，並提供`property=auth.params.usePrivateLink==true`作為查詢引數。

**API格式**

```http
GET /connections?property=auth.params.usePrivateLink==true
```

**要求**

以下請求會擷取貴組織中使用私人端點的所有連線。

+++選取以檢視請求範例

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections?property=auth.params.usePrivateLink==true' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**回應**

成功的回應會傳回與私人端點繫結的所有連線。

+++選取以檢視回應範例

```json
{
  "items": [
    {
      "id": "42a27b1f-8e3f-48ce-8c29-7e474b29a015",
      "createdAt": 1729154379292,
      "updatedAt": 1729154382031,
      "createdBy": "{CREATED_BY}",
      "updatedBy": "{UPDATED_BY}",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_NAME}",
      "name": "acme-e2e",
      "connectionSpec": {
        "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
        "version": "1.0"
      },
      "state": "enabled",
      "auth": {
        "specName": "ConnectionString",
        "params": {
          "connectionString": "{CONNECTION_STRING}",
          "usePrivateLink": true,
          "privateEndpointId": "02a74b31-a566-4a86-9cea-309b101a7f24"
        }
      },
      "version": "\"2f01454b-0000-0200-0000-6766749a0000\"",
      "etag": "\"2f01454b-0000-0200-0000-6766749a0000\"",
      "lastOperation": {
        "started": 0,
        "updated": 0,
        "operation": "create"
      }
    },
    {
      "id": "6350311a-664c-4b08-aad4-4065781aac81",
      "createdAt": 1718199941102,
      "updatedAt": 1718199945147,
      "createdBy": "{CREATED_BY}",
      "updatedBy": "{UPDATED_BY}",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_NAME}",
      "name": "acme demo",
      "connectionSpec": {
        "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
        "version": "1.0"
      },
      "state": "enabled",
      "auth": {
        "specName": "ConnectionString",
        "params": {
          "connectionString": "{CONNECTION_STRING}",
          "usePrivateLink": true
        }
      },
      "version": "\"3001307e-0000-0200-0000-6766cf710000\"",
      "etag": "\"3001307e-0000-0200-0000-6766cf710000\"",
      "lastOperation": {
        "started": 0,
        "updated": 0,
        "operation": "create"
      }
    }
  ],
  "_links": {
     
  }
}
```

+++