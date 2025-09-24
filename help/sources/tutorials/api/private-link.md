---
title: API來源的私人連結支援
description: 瞭解如何建立並使用Adobe Experience Platform來源的私人連結
exl-id: 9b7fc1be-5f42-4e29-b552-0b0423a40aa1
source-git-commit: 4d82b0a7f5ae9e0a7607fe7cb75261e4d3489eff
workflow-type: tm+mt
source-wordcount: '1515'
ht-degree: 3%

---

# API來源的私人連結支援

>[!AVAILABILITY]
>
>下列來源支援此功能：
>
>* [[!DNL Azure Blob Storage]](../../connectors/cloud-storage/blob.md)
>* [[!DNL ADLS Gen2]](../../connectors/cloud-storage/adls-gen2.md)
>* [[!DNL Azure File Storage]](../../connectors/cloud-storage/azure-file-storage.md)
>
>私人連結支援目前僅適用於已購買Adobe Healthcare Shield或Adobe Privacy &amp; Security Shield的組織。

您可以使用私人連結功能來建立Adobe Experience Platform來源要連線的私人端點。 使用私人IP位址將您的來源安全地連線到虛擬網路，消除對公共IP的需求，並減少您的攻擊面。 不需要複雜的防火牆或網路位址轉譯組態，同時確保資料流量僅能到達核准的服務，藉此簡化網路設定。

請閱讀本指南，瞭解如何使用API來建立和使用私有端點。

>[!BEGINSHADEBOX]

## 私人連結支援的授權使用權益

來源中私人連結支援的授權使用權益量度如下：

* 客戶有權透過支援的來源（[!DNL Azure Blob Storage]、[!DNL ADLS Gen2]和[!DNL Azure File Storage]），跨所有沙箱和組織每年進行最多2 TB的資料傳輸。
* 每個組織最多可以有10個端點用於所有生產沙箱。
* 每個組織最多可以為所有開發沙箱擁有1個端點。

>[!ENDSHADEBOX]

## 快速入門

本指南需要您深入瞭解下列Experience Platform元件：

* [來源](../../home.md)： Experience Platform允許從各種來源擷取資料，同時讓您能夠使用Experience Platform服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../sandboxes/home.md)： Experience Platform提供的虛擬沙箱可將單一Experience Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

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
      "connectionSpec": {
          "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
          "version": "1.0"
    }
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 您的私人端點的名稱。 |
| `subscriptionId` | 與您的[!DNL Azure]訂閱相關聯的識別碼。 如需詳細資訊，請參閱[!DNL Azure]的[指南，從 [!DNL Azure Portal]](https://learn.microsoft.com/en-us/azure/azure-portal/get-subscription-tenant-id)擷取您的訂閱和租使用者ID。 |
| `resourceGroupName` | [!DNL Azure]上資源群組的名稱。 資源群組包含[!DNL Azure]解決方案的相關資源。 如需詳細資訊，請閱讀[!DNL Azure]管理資源群組[的](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/manage-resource-groups-portal)指南。 |
| `resourceName` | 資源的名稱。 在[!DNL Azure]中，資源是指虛擬機器器、網頁應用程式和資料庫等執行個體。 如需詳細資訊，請閱讀[!DNL Azure]上的[指南，瞭解 [!DNL Azure] 資源管理員](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/overview)。 |
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
| `subscriptionId` | 與您的[!DNL Azure]訂閱相關聯的識別碼。 如需詳細資訊，請參閱[!DNL Azure]的[指南，從 [!DNL Azure Portal]](https://learn.microsoft.com/en-us/azure/azure-portal/get-subscription-tenant-id)擷取您的訂閱和租使用者ID。 |
| `resourceGroupName` | [!DNL Azure]上資源群組的名稱。 資源群組包含[!DNL Azure]解決方案的相關資源。 如需詳細資訊，請閱讀[!DNL Azure]管理資源群組[的](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/manage-resource-groups-portal)指南。 |
| `resourceName` | 資源的名稱。 在[!DNL Azure]中，資源是指虛擬機器器、網頁應用程式和資料庫等執行個體。 如需詳細資訊，請閱讀[!DNL Azure]上的[指南，瞭解 [!DNL Azure] 資源管理員](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/overview)。 |
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

## 啟用[!DNL Interactive Authoring] {#enable-interactive-authoring}

>[!IMPORTANT]
>
>您必須先啟用[!DNL Interactive Authoring]，才能建立或更新流程，以及建立、更新或探索連線之前。

[!DNL Interactive Authoring]用於探索連線或帳戶以及預覽資料等功能。 若要啟用[!DNL Interactive Authoring]，請向`/privateEndpoints/interactiveAuthoring`發出POST要求，並在查詢引數中將`enable`指定為運運算元。

**API格式**

```http
POST /privateEndpoints/interactiveAuthoring?op=enable
```

| 查詢參數 | 說明 |
| --- | --- |
| `op` | 您要執行的作業。 若要啟用[!DNL Interactive Authoring]，請將`op`值設定為`enable`。 |

**要求**

下列要求會啟用您私人端點的[!DNL Interactive Authoring]，並將TTL設為60分鐘。

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
| `autoTerminationMinutes` | [!DNL Interactive Authoring] TTL （存留時間）以分鐘為單位。 [!DNL Interactive Authoring]用於探索連線或帳戶以及預覽資料等功能。 您最多可以設定120分鐘的TTL。 預設TTL為60分鐘。 |

+++

**回應**

成功的回應會傳回HTTP狀態202 （已接受）。

## 擷取[!DNL Interactive Authoring]狀態 {#retrieve-interactive-authoring-status}

若要檢視您私人端點的[!DNL Interactive Authoring]目前狀態，請向`/privateEndpoints/interactiveAuthoring`發出GET要求。

**API格式**

```http
GET /privateEndpoints/interactiveAuthoring
```

**要求**

下列要求會擷取[!DNL Interactive Authoring]的狀態：

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
| `status` | [!DNL Interactive Authoring]的狀態。 有效值包括： `disabled`、`enabling`、`enabled`。 |

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

若要在Experience Platform中建立與私人端點的連線，請對`/connections` API的[!DNL Flow Service]端點提出POST要求。

**API格式**

```http
POST /connections/
```

**要求**

下列要求會建立[!DNL Azure Blob Storage]的已驗證基底連線，同時使用私用端點。

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
      "name": "Azure Blob Storage base connection",
      "description": "A base connection for a Azure Blob Storage source that uses a private link.",
      "auth": {
          "specName": "ConnectionString",
          "params": {
              "connectionString": "{CONNECTION_STRING}",
              "usePrivateLink" : true
          }
      },
      "connectionSpec": {
          "id": "4c10e202-c428-4796-9208-5f1f5732b1cf",
          "version": "1.0"
      }
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 基礎連線的名稱。 |
| `description` | （選用）提供連線其他資訊的說明。 |
| `auth.specName` | 用來將您的來源連線至Experience Platform的驗證。 |
| `auth.params.connectionString` | [!DNL Azure Blob Storage]連線字串。 如需詳細資訊，請閱讀[[!DNL Azure Blob Storage] API驗證指南](../api/create/cloud-storage/blob.md)。 |
| `auth.params.usePrivateLink` | 布林值，判斷您是否使用私人端點。 如果您使用私人端點，請將此值設為`true`。 |
| `connectionSpec.id` | [!DNL Azure Blob Storage]的連線規格ID。 |
| `connectionSpec.version` | 您的[!DNL Azure Blob Storage]連線規格ID的版本。 |

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

## 附錄

請閱讀本節，以瞭解在API中使用[!DNL Azure]私人連結的其他資訊。

### 核准[!DNL Azure Blob]和[!DNL Azure Data Lake Gen2]的私人端點

若要核准[!DNL Azure Blob]和[!DNL Azure Data Lake Gen2]來源的私人端點要求，請登入[!DNL Azure Portal]。 在左側導覽中選取&#x200B;**[!DNL Data storage]**，然後前往&#x200B;**[!DNL Security + networking]**&#x200B;標籤並選擇&#x200B;**[!DNL Networking]**。 接下來，選取「**[!DNL Private endpoints]**」以檢視與您帳戶相關聯的私人端點清單及其目前的連線狀態。 若要核准擱置的要求，請選取所要的端點，然後按一下&#x200B;**[!DNL Approve]**。

![含有擱置中私人端點清單的Azure入口網站。](../../images/tutorials/private-links/azure.png)

<!--

### Configure your [!DNL Snowflake] account to connect to private links

You must complete the following prerequisite steps in order to use the [!DNL Snowflake] source with private links.

First, you must raise a support ticket in [!DNL Snowflake] and request for the **endpoint service resource ID** of the [!DNL Azure] region of your [!DNL Snowflake] account. Follow the steps below to raise a [!DNL Snowflake] ticket:

1. Navigate to the [[!DNL Snowflake] UI](https://app.snowflake.com) and sign in with your email account. During this step, you must ensure that your email is verified in profile settings.
2. Select your **user menu** and then select **support** to access [!DNL Snowflake] support.
3. To create a support case, select **[!DNL + Support Case]**. Then, fill out the form with relevant details and attach any necessary files.
4. When finished, submit the case.

The endpoint resource ID is formatted as follows:

```shell
subscriptions/{SUBSCRIPTION_ID}/resourceGroups/az{REGION}-privatelink/providers/microsoft.network/privatelinkservices/sf-pvlinksvc-az{REGION}
```

+++Select to view example

```shell
/subscriptions/4575fb04-6859-4781-8948-7f3a92dc06a3/resourceGroups/azwestus2-privatelink/providers/microsoft.network/privatelinkservices/sf-pvlinksvc-azwestus2
```

+++

| Parameter | Description | Example |
| --- | --- | --- |
| `{SUBSCRIPTION_ID}` | The unique ID that identifies your [!DNL Azure] subscription. | `a1b2c3d4-5678-90ab-cdef-1234567890ab` |
| `{REGION}` | The [!DNL Azure] region of your [!DNL Snowflake] account. | `azwestus2` |

### Retrieve your private link configuration details

To retrieve your private link configuration details, you must run the following command in [!DNL Snowflake]:

```sql
USE ROLE accountadmin;
SELECT key, value::varchar
FROM TABLE(FLATTEN(input => PARSE_JSON(SYSTEM$GET_PRIVATELINK_CONFIG())));
```

Next, retrieve values for the following properties:

* `privatelink-account-url`
* `regionless-privatelink-account-url`
* `privatelink_ocsp-url`

Once you have retrieved the values, you can make the following call to create a private link for [!DNL Snowflake].

**Request**

The following request creates a private endpoint for [!DNL Snowflake]:

>[!BEGINTABS]

>[!TAB Template]

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints/' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "{ENDPOINT_NAME}",
    "subscriptionId": "{AZURE_SUBSCRIPTION_ID}",
    "resourceGroupName": "{RESOURCE_GROUP_NAME}",
    "resourceName": "{SNOWFLAKE_ENDPOINT_SERVICE_NAME}",
    "fqdns": [
      "{PRIVATELINK_ACCOUNT_URL}",
      "{REGIONLESS_PRIVATELINK_ACCOUNT_URL}",
      "{PRIVATELINK_OCSP_URL}"
    ],
    "connectionSpec": {
      "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
      "version": "1.0"
    }
  }'
```

>[!TAB Example]

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/privateEndpoints/' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "TEST_Snowflake_PE",
    "subscriptionId": "4575fb04-6859-4781-8948-7f3a92dc06a3",
    "resourceGroupName": "azwestus2-privatelink",
    "resourceName": "sf-pvlinksvc-azwestus2",
    "fqdns": [
      "hf06619.west-us-2.privatelink.snowflakecomputing.com",
      "adobe-segmentationdbint.privatelink.snowflakecomputing.com",
      "ocsp.hf06619.west-us-2.privatelink.snowflakecomputing.com"
    ],
    "connectionSpec": {
      "id": "b2e08744-4f1a-40ce-af30-7abac3e23cf3",
      "version": "1.0"
    }
  }'
```

>[!ENDTABS]

-->