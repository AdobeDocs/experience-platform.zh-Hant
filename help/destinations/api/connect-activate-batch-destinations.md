---
keywords: Experience Platform；首頁；熱門主題
solution: Experience Platform
title: 使用流程服務API連線到批次目的地並啟用資料
description: 使用流程服務API的逐步指示，在Experience Platform中建立批次雲端儲存空間或電子郵件行銷目的地，並啟用資料
type: Tutorial
exl-id: 41fd295d-7cda-4ab1-a65e-b47e6c485562
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '3416'
ht-degree: 2%

---

# 連線至檔案式電子郵件行銷目的地，並使用流量服務API啟用資料

>[!IMPORTANT]
> 
>* 若要連線到目的地，您需要&#x200B;**[!UICONTROL 檢視目的地]**&#x200B;和&#x200B;**[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions)。
>
>* 若要啟用資料，您需要&#x200B;**[!UICONTROL 檢視目的地]**、**[!UICONTROL 啟用目的地]**、**[!UICONTROL 檢視設定檔]**&#x200B;和&#x200B;**[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions)。
>
>* 若要匯出&#x200B;*身分*，您需要&#x200B;**[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions)。<br> ![選取工作流程中反白的身分名稱空間，以啟用目的地的對象。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以啟用目的地的對象。"){width="100" zoomable="yes"}
>
>閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

此教學課程示範如何使用流程服務API來建立檔案式[電子郵件行銷目的地](../catalog/email-marketing/overview.md)、建立資料流到您新建立的目的地，以及透過CSV檔案將資料匯出到您新建立的目的地。

>[!TIP]
> 
>若要瞭解如何使用Flow Service API啟用雲端儲存空間目的地的資料，請閱讀[專用API教學課程](/help/destinations/api/activate-segments-file-based-destinations.md)。

本教學課程在所有範例中都使用[!DNL Adobe Campaign]目的地，但檔案式電子郵件行銷目的地的步驟相同。

![概觀 — 建立目的地和啟用對象的步驟](../assets/api/email-marketing/overview.png)

如果您偏好使用Experience Platform使用者介面來連線到目的地並啟用資料，請參閱[連線到目的地](../ui/connect-destination.md)和[啟用對象資料到批次設定檔匯出目的地](../ui/activate-batch-profile-destinations.md)教學課程。

## 快速入門 {#get-started}

本指南需要您深入了解下列 Adobe Experience Platform 元件：

* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md)： [!DNL Experience Platform]用來組織客戶體驗資料的標準化架構。
* [[!DNL Segmentation Service]](../../segmentation/api/overview.md)： [!DNL Adobe Experience Platform Segmentation Service]可讓您從[!DNL Real-Time Customer Profile]資料在[!DNL Adobe Experience Platform]中建立對象。
* [[!DNL Sandboxes]](../../sandboxes/home.md)： [!DNL Experience Platform]提供的虛擬沙箱可將單一[!DNL Experience Platform]執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

以下小節提供您需要瞭解的其他資訊，以便在Experience Platform中啟用批次目的地的資料。

### 收集必要的認證 {#gather-required-credentials}

若要完成本教學課程中的步驟，您應準備好下列憑證，端視您要連線及啟用對象的目的地型別而定。

* 針對[!DNL Amazon S3]連線： `accessId`，`secretKey`
* 針對[!DNL Amazon S3]與[!DNL Adobe Campaign]的連線： `accessId`，`secretKey`
* 對於SFTP連線： `domain`、`port`、`username`、`password`或`sshKey` （取決於連線至FTP位置的連線方法）
* 針對[!DNL Azure Blob]連線： `connectionString`

>[!NOTE]
>
>[!DNL Amazon S3]連線的認證`accessId`、`secretKey`與[!DNL Adobe Campaign]的[!DNL Amazon S3]連線的`accessId`、`secretKey`相同。

### 讀取範例 API 呼叫 {#reading-sample-api-calls}

本教學課程提供範例API呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭和正確格式化的請求承載。 此外，也提供 API 回應中傳回的範例 JSON。 如需檔案中所使用範例API呼叫慣例的詳細資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集必要和選用標題的值 {#gather-values-headers}

若要呼叫[!DNL Experience Platform] API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程會提供所有 [!DNL Experience Platform] API 呼叫中每個必要標頭的值，如下所示：

* 授權：持有人`{ACCESS_TOKEN}`
* x-api-key： `{API_KEY}`
* x-gw-ims-org-id： `{ORG_ID}`

[!DNL Experience Platform]中的資源可以隔離到特定的虛擬沙箱。 在對[!DNL Experience Platform] API的請求中，您可以指定將執行作業的沙箱名稱和ID。 這些是選用引數。

* x-sandbox-name： `{SANDBOX_NAME}`

>[!NOTE]
>
>如需[!DNL Experience Platform]中沙箱的詳細資訊，請參閱[沙箱概觀檔案](../../sandboxes/home.md)。

包含裝載(POST、PUT、PATCH)的所有請求都需要額外的媒體型別標頭：

* Content-Type： `application/json`

### API參考檔案 {#api-reference-documentation}

在本教學課程中，您可以找到所有API作業的隨附參考檔案。 請參閱Adobe I/O](https://www.adobe.io/experience-platform-apis/references/flow-service/)上的[流程服務API檔案。 我們建議您同時使用本教學課程和API參考檔案。

## 取得可用目的地的清單 {#get-the-list-of-available-destinations}

![目的地步驟概述步驟1](../assets/api/batch-destination/step1.png)

首先，您必須決定要將資料啟動到的目的地。 首先，請執行呼叫以請求您可以連線並啟用對象的目標可用目的地清單。 對`connectionSpecs`端點執行下列GET請求，以傳回可用目的地的清單：

**API格式**

```http
GET /connectionSpecs
```

**要求**

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs' \
--header 'accept: application/json' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```


**回應**

成功的回應包含可用目的地的清單及其唯一識別碼(`id`)。 儲存您計畫使用的目的地值，因為後續步驟需要它。 例如，如果您想要連線並將對象傳送至[!DNL Adobe Campaign]，請在回應中尋找下列程式碼片段：

```json
{
    "id": "0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
  "name": "Adobe Campaign",
  ...
  ...
}
```

下表包含常用批次目的地的連線規格ID以供您參考：

| 目標 | 連線規格ID |
---------|----------|
| [!DNL Adobe Campaign] | `0b23e41a-cb4a-4321-a78f-3b654f5d7d97` |
| [!DNL Oracle Eloqua] | `c1e44b6b-e7c8-404b-9031-58f0ef760604` |
| [!DNL Oracle Responsys] | `a5e28ddf-e265-426e-83a1-9d03a3a6822b` |
| [!DNL Salesforce Marketing Cloud] | `f599a5b3-60a7-4951-950a-cc4115c7ea27` |

{style="table-layout:auto"}

## 連線到您的[!DNL Experience Platform]資料 {#connect-to-your-experience-platform-data}

![目的地步驟概述步驟2](../assets/api/batch-destination/step2.png)

接下來，您必須連線至您的[!DNL Experience Platform]資料，才能匯出設定檔資料，並在您偏好的目的地啟用該資料。 此包含兩個子步驟，如下所述。

1. 首先，您必須透過設定基礎連線，執行呼叫以授權存取[!DNL Experience Platform]中的資料。
2. 然後，使用基本連線ID執行另一個呼叫，您會在其中建立&#x200B;*來源連線*，以建立與您[!DNL Experience Platform]資料的連線。

### 在[!DNL Experience Platform]中授權存取您的資料

**API格式**

```http
POST /connections
```

**要求**

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
            "name": "Base connection to Experience Platform",
            "description": "This call establishes the connection to Experience Platform data",
            "connectionSpec": {
                "id": "{CONNECTION_SPEC_ID}",
                "version": "1.0"
            }
}'
```

| 屬性 | 說明 |
| --------- | ----------- |
| `name` | 提供基礎連線至Experience Platform [!DNL Profile store]的名稱。 |
| `description` | 您可以選擇提供基本連線的說明。 |
| `connectionSpec.id` | 使用[Experience Platform設定檔存放區](/help/profile/home.md#profile-data-store) - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`的連線規格ID。 |

{style="table-layout:auto"}

**回應**

成功的回應包含基底連線的唯一識別碼(`id`)。 將此值儲存為建立來源連線之下一個步驟所需的值。

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### 連線到您的[!DNL Experience Platform]資料 {#connect-to-platform-data}

**API格式**

```http
POST /sourceConnections
```

**要求**

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
            "name": "Connecting to Profile store",
            "description": "Optional",
            "connectionSpec": {
                "id": "{CONNECTION_SPEC_ID}",
                "version": "1.0"
            },
            "baseConnectionId": "{BASE_CONNECTION_ID}",
            "data": {
                "format": "CSV",
                "schema": null
            },
            "params" : {}
}'
```

| 屬性 | 說明 |
| --------- | ----------- |
| `name` | 提供來源連線至Experience Platform [!DNL Profile store]的名稱。 |
| `description` | 您可以選擇提供來源連線的說明。 |
| `connectionSpec.id` | 使用[Experience Platform設定檔存放區](/help/profile/home.md#profile-data-store) - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`的連線規格ID。 |
| `baseConnectionId` | 使用您在上一步中取得的基本連線ID。 |
| `data.format` | `CSV`是目前唯一支援的檔案匯出格式。 |

{style="table-layout:auto"}

**回應**

成功回應傳回新建立的來源連線至[!DNL Profile store]的唯一識別碼(`id`)。 這可確認您已成功連線至您的[!DNL Experience Platform]資料。 將此值依後續步驟的需要儲存。

```json
{
    "id": "ed48ae9b-c774-4b6e-88ae-9bc7748b6e97"
}
```

## 連線到批次目的地 {#connect-to-batch-destination}

![目的地步驟概述步驟3](../assets/api/batch-destination/step3.png)

在此步驟中，您會設定與所需批次雲端儲存空間或電子郵件行銷目的地的連線。 此包含兩個子步驟，如下所述。

1. 首先，您必須透過設定基礎連線，執行呼叫以授權存取目的地平台。
2. 然後，使用基本連線ID進行另一個呼叫，以建立&#x200B;*目標連線*，這會指定儲存體帳戶中要傳送已匯出資料檔案的位置，以及要匯出的資料格式。

### 授權存取批次目的地 {#authorize-access-to-batch-destination}

**API格式**

```http
POST /connections
```

**要求**

下列要求會建立與[!DNL Adobe Campaign]目的地的基底連線。 根據您要將檔案匯出至([!DNL Amazon S3]、SFTP、[!DNL Azure Blob])的儲存位置，請保留適當的`auth`規格並刪除其他規格。

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "S3 Connection for Adobe Campaign",
    "description": "summer advertising campaign",
    "connectionSpec": {
        "id": "0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
        "version": "1.0"
    },
    "auth": {
        "specName": "S3",
        "params": {
            "accessId": "{ACCESS_ID}",
            "secretKey": "{SECRET_KEY}"
        }
    }
    "auth": {
        "specName": "SFTP with Password",
        "params": {
            "domain": "{DOMAIN}",
            "host": "{HOST}",
            "username": "{USERNAME}",
            "password": "{PASSWORD}"
        }
    }
    "auth": {
        "specName": "SFTP with SSH Key",
        "params": {
            "domain": "{DOMAIN}",
            "host": "{HOST}",
            "username": "{USERNAME}",
            "sshKey": "{SSH_KEY}"
        }
    }        
    "auth": {
        "specName": "Azure Blob",
        "params": {
            "connectionString": "{AZURE_BLOB_CONNECTION_STRING}"
        }
    }    
}'
```

請參閱下列請求範例，以連線至其他支援的批次雲端儲存空間及電子郵件行銷目的地。

+++ 連線到[!DNL Amazon S3]目的地的要求範例

下列要求會建立與[!DNL Amazon S3]目的地的基底連線。

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Connect to Amazon S3",
    "description": "summer advertising campaign",
    "connectionSpec": {
        "id": "4890fc95-5a1f-4983-94bb-e060c08e3f81",
        "version": "1.0"
    },
    "auth": {
        "specName": "Access Key",
        "params": {
            "s3AccessKey": "{AMAZON_S3_ACCESS_KEY}",
            "s3SecretKey": "{AMAZON_S3_SECRET_KEY}"
        }
    }
}'
```

+++

+++ 連線到[!DNL Azure Blob]目的地的要求範例

下列要求會建立與[!DNL Azure Blob]目的地的基底連線。

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Connect to Azure Blob",
    "description": "Summer advertising campaign",
    "connectionSpec": {
        "id": "e258278b-a4cf-43ac-b158-4fa0ca0d948b",
        "version": "1.0"
    },
    "auth": {
        "specName": "ConnectionString",
        "params": {
            "connectionString": "{AZURE_BLOB_CONNECTION_STRING}"
        }
    }
}'
```

+++

+++ 連線到[!DNL Oracle Eloqua]目的地的要求範例

下列要求會建立與[!DNL Oracle Eloqua]目的地的基底連線。 根據您要將檔案匯出到的儲存位置，保留適當的`auth`規格並刪除其他規格。

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Connect to Eloqua destination",
    "description": "summer advertising campaign",
    "connectionSpec": {
        "id": "c1e44b6b-e7c8-404b-9031-58f0ef760604",
        "version": "1.0"
    },
    "auth": {
        "specName": "SFTP with Password",
        "params": {
            "domain": "{DOMAIN}",
            "host": "{HOST}",
            "username": "{USERNAME}",
            "password": "{PASSWORD}"
        }
    }
    "auth": {
        "specName": "SFTP with SSH Key",
        "params": {
            "domain": "{DOMAIN}",
            "host": "{HOST}",
            "username": "{USERNAME}",
            "sshKey": "{SSH_KEY}"
        }
    }    
}'
```

+++

+++ 連線到[!DNL Oracle Responsys]目的地的要求範例

下列要求會建立與[!DNL Oracle Responsys]目的地的基底連線。 根據您要將檔案匯出到的儲存位置，保留適當的`auth`規格並刪除其他規格。

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Connect to Responsys destination",
    "description": "summer advertising campaign",
    "connectionSpec": {
        "id": "a5e28ddf-e265-426e-83a1-9d03a3a6822b",
        "version": "1.0"
    },
    "auth": {
        "specName": "SFTP with Password",
        "params": {
            "domain": "{DOMAIN}",
            "host": "{HOST}",
            "username": "{USERNAME}",
            "password": "{PASSWORD}"
        }
    }
    "auth": {
        "specName": "SFTP with SSH Key",
        "params": {
            "domain": "{DOMAIN}",
            "host": "{HOST}",
            "username": "{USERNAME}",
            "sshKey": "{SSH_KEY}"
        }
    }    
}'
```

+++

+++ 連線到[!DNL Salesforce Marketing Cloud]目的地的要求範例

下列要求會建立與[!DNL Salesforce Marketing Cloud]目的地的基底連線。 根據您要將檔案匯出到的儲存位置，保留適當的`auth`規格並刪除其他規格。

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Connect to Salesforce Marketing Cloud",
    "description": "summer advertising campaign",
    "connectionSpec": {
        "id": "f599a5b3-60a7-4951-950a-cc4115c7ea27",
        "version": "1.0"
    },
    "auth": {
        "specName": "SFTP with Password",
        "params": {
            "domain": "{DOMAIN}",
            "host": "{HOST}",
            "username": "{USERNAME}",
            "password": "{PASSWORD}"
        }
    }
    "auth": {
        "specName": "SFTP with SSH Key",
        "params": {
            "domain": "{DOMAIN}",
            "host": "{HOST}",
            "username": "{USERNAME}",
            "sshKey": "{SSH_KEY}"
        }
    }    
}'
```

+++

+++ 使用密碼目的地連線至SFTP的請求範例

以下請求會建立與SFTP目的地的基底連線。

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Connect to SFTP with password",
    "description": "summer advertising campaign",
    "connectionSpec": {
        "id": "64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0",
        "version": "1.0"
    },
    "auth": {
        "specName": "Basic Authentication for sftp",
        "params": {
            "host": "{HOST}",
            "username": "{USERNAME}",
            "password": "{PASSWORD}"
        }
    }
}'
```

+++

| 屬性 | 說明 |
| --------- | ----------- |
| `name` | 提供批次目的地的基本連線名稱。 |
| `description` | 您可以選擇提供基本連線的說明。 |
| `connectionSpec.id` | 使用所需批次目的地的連線規格ID。 您在步驟[取得可用目的地的清單](#get-the-list-of-available-destinations)中取得此識別碼。 |
| `auth.specname` | 表示目的地的驗證格式。 若要尋找您目的地的specName，請對連線規格端點](https://developer.adobe.com/experience-platform-apis/references/flow-service/#operation/retrieveConnectionSpec)執行[GET呼叫，提供您所要目的地的連線規格。 在回應中尋找引數`authSpec.name`。 <br>例如，對於Adobe Campaign目的地，您可以使用任何`S3`、`SFTP with Password`或`SFTP with SSH Key`。 |
| `params` | 根據您連線的目的地，您必須提供不同的必要驗證引數。 針對Amazon S3連線，您必須提供Amazon S3儲存位置的存取ID和秘密金鑰。 <br>若要找出您目的地所需的引數，請對連線規格端點](https://developer.adobe.com/experience-platform-apis/references/flow-service/#operation/retrieveConnectionSpec)執行[GET呼叫，提供您所要目的地的連線規格。 在回應中尋找引數`authSpec.spec.required`。 |

{style="table-layout:auto"}

**回應**

成功的回應包含基底連線的唯一識別碼(`id`)。 將此值儲存為建立目標連線的下一個步驟所需的值。

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### 指定儲存位置和資料格式 {#specify-storage-location-data-format}

[!DNL Adobe Experience Platform]以[!DNL CSV]個檔案的形式，匯出批次電子郵件行銷和雲端儲存目的地的資料。 在此步驟中，您可以決定要匯出檔案之儲存位置的路徑。

>[!IMPORTANT]
> 
>[!DNL Adobe Experience Platform]會自動分割匯出檔案，每個檔案為500萬筆記錄（列）。 每一列代表一個設定檔。
>
>分割檔案名稱會附加一個數字，表示檔案是較大匯出的一部分，例如： `filename.csv`、`filename_2.csv`、`filename_3.csv`。

**API格式**

```http
POST /targetConnections
```

**要求**

以下請求會建立與[!DNL Adobe Campaign]目的地的目標連線，以判斷匯出的檔案會停留在您的儲存位置。 根據您要將檔案匯出到的儲存位置，保留適當的`params`規格並刪除其他規格。

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "TargetConnection for Adobe Campaign",
    "description": "Connection to Adobe Campaign",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
        "version": "1.0"
    },
    "data": {
        "format": "json",
        "schema": {
            "id": "1.0",
            "version": "1.0"
        }
    },
    "params": {
        "mode": "S3",
        "bucketName": "{BUCKET_NAME}",
        "path": "{FILEPATH}",
        "format": "CSV"
    }
    "params": {
        "mode": "AZURE_BLOB",
        "container": "{CONTAINER}",
        "path": "{FILEPATH}",
        "format": "CSV"
    }
    "params": {
        "mode": "FTP",
        "remotePath": "{REMOTE_PATH}",
        "format": "CSV"
    }        
}'
```

請參閱下列請求範例，為其他支援的批次雲端儲存和電子郵件行銷目的地設定儲存位置。

+++ 設定[!DNL Amazon S3]目的地儲存位置的要求範例

以下請求會建立與[!DNL Amazon S3]目的地的目標連線，以判斷匯出的檔案會停留在您的儲存位置。

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "TargetConnection for Amazon S3",
    "description": "Connection to Amazon S3",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "4890fc95-5a1f-4983-94bb-e060c08e3f81",
        "version": "1.0"
    },
    "data": {
        "format": "json",
        "schema": {
            "id": "1.0",
            "version": "1.0"
        }
    },
    "params": {
        "mode": "S3",
        "bucketName": "{BUCKET_NAME}",
        "path": "{FILEPATH}",
        "format": "CSV"
    }
}'
```

+++

+++ 設定[!DNL Azure Blob]目的地儲存位置的要求範例

以下請求會建立與[!DNL Azure Blob]目的地的目標連線，以判斷匯出的檔案會停留在您的儲存位置。

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "TargetConnection for Azure Blob",
    "description": "Connection to Azure Blob",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "e258278b-a4cf-43ac-b158-4fa0ca0d948b",
        "version": "1.0"
    },
    "data": {
        "format": "json",
        "schema": {
            "id": "1.0",
            "version": "1.0"
        }
    },
    "params": {
        "mode": "AZURE_BLOB",
        "container": "{CONTAINER}",
        "path": "{FILEPATH}",
        "format": "CSV"
    }
}'
```

+++

+++ 設定[!DNL Oracle Eloqua]目的地儲存位置的要求範例

以下請求會建立與[!DNL Oracle Eloqua]目的地的目標連線，以判斷匯出的檔案會停留在您的儲存位置。 根據您要將檔案匯出到的儲存位置，保留適當的`params`規格並刪除其他規格。

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "TargetConnection for Oracle Eloqua",
    "description": "Connection to Oracle Eloqua",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "c1e44b6b-e7c8-404b-9031-58f0ef760604",
        "version": "1.0"
    },
    "data": {
        "format": "json",
        "schema": {
            "id": "1.0",
            "version": "1.0"
        }
    },
    "params": {
        "mode": "S3",
        "bucketName": "{BUCKET_NAME}",
        "path": "{FILEPATH}",
        "format": "CSV"
    }
    "params": {
        "mode": "FTP",
        "remotePath": "{REMOTE_PATH}",
        "format": "CSV"
    }        
}'
```

+++

+++ 設定[!DNL Oracle Responsys]目的地儲存位置的要求範例

以下請求會建立與[!DNL Oracle Responsys]目的地的目標連線，以判斷匯出的檔案會停留在您的儲存位置。 根據您要將檔案匯出到的儲存位置，保留適當的`params`規格並刪除其他規格。

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "TargetConnection for Oracle Responsys",
    "description": "Connection to Oracle Responsys",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "a5e28ddf-e265-426e-83a1-9d03a3a6822b",
        "version": "1.0"
    },
    "data": {
        "format": "json",
        "schema": {
            "id": "1.0",
            "version": "1.0"
        }
    },
    "params": {
        "mode": "S3",
        "bucketName": "{BUCKET_NAME}",
        "path": "{FILEPATH}",
        "format": "CSV"
    }
    "params": {
        "mode": "FTP",
        "remotePath": "{REMOTE_PATH}",
        "format": "CSV"
    }        
}'
```

+++

+++ 設定[!DNL Salesforce Marketing Cloud]目的地儲存位置的要求範例

以下請求會建立與[!DNL Salesforce Marketing Cloud]目的地的目標連線，以判斷匯出的檔案會停留在您的儲存位置。 根據您要將檔案匯出到的儲存位置，保留適當的`params`規格並刪除其他規格。

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "TargetConnection for Salesforce Marketing Cloud",
    "description": "Connection to Salesforce Marketing Cloud",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "f599a5b3-60a7-4951-950a-cc4115c7ea27",
        "version": "1.0"
    },
    "data": {
        "format": "json",
        "schema": {
            "id": "1.0",
            "version": "1.0"
        }
    },
    "params": {
        "mode": "S3",
        "bucketName": "{BUCKET_NAME}",
        "path": "{FILEPATH}",
        "format": "CSV"
    }
    "params": {
        "mode": "FTP",
        "remotePath": "{REMOTE_PATH}",
        "format": "CSV"
    }        
}'
```

+++

+++ 設定SFTP目的地儲存位置的請求範例

以下請求會建立與SFTP目的地的目標連線，以判斷匯出的檔案會著陸至您的儲存位置。

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "TargetConnection for SFTP",
    "description": "Connection to SFTP",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0",
        "version": "1.0"
    },
    "data": {
        "format": "json",
        "schema": {
            "id": "1.0",
            "version": "1.0"
        }
    },
    "params": {
        "mode": "FTP",
        "remotePath": "{REMOTE_PATH}",
    }
}'
```

+++


| 屬性 | 說明 |
| --------- | ----------- |
| `name` | 提供批次目的地的目標連線名稱。 |
| `description` | 您可以選擇提供目標連線的說明。 |
| `baseConnectionId` | 使用您在上述步驟中建立之基本連線的ID。 |
| `connectionSpec.id` | 使用所需批次目的地的連線規格ID。 您在步驟[取得可用目的地的清單](#get-the-list-of-available-destinations)中取得此識別碼。 |
| `params` | 視您連線的目的地而定，您必須為儲存位置提供不同的必要引數。 針對Amazon S3連線，您必須提供Amazon S3儲存位置的存取ID和秘密金鑰。 <br>若要找出您目的地所需的引數，請對連線規格端點](https://developer.adobe.com/experience-platform-apis/references/flow-service/#operation/retrieveConnectionSpec)執行[GET呼叫，提供您所要目的地的連線規格。 在回應中尋找引數`targetSpec.spec.required`。 |
| `params.mode` | 視您目的地支援的模式而定，您必須在此處提供不同的值。 若要找出您目的地所需的引數，請對連線規格端點](https://developer.adobe.com/experience-platform-apis/references/flow-service/#operation/retrieveConnectionSpec)執行[GET呼叫，提供您所需目的地的連線規格。 在回應中尋找引數`targetSpec.spec.properties.mode.enum`，並選取所要的模式。 |
| `params.bucketName` | 對於S3連線，請提供要匯出檔案的儲存貯體名稱。 |
| `params.path` | 對於S3連線，請在要匯出檔案的儲存位置中提供檔案路徑。 |
| `params.format` | `CSV`是目前唯一支援的檔案匯出型別。 |

{style="table-layout:auto"}

**回應**

成功的回應會傳回新建立之目標連線到批次目的地的唯一識別碼(`id`)。 視需要在後續步驟中儲存此值。

```json
{
    "id": "12ab90c7-519c-4291-bd20-d64186b62da8"
}
```

## 建立資料流 {#create-dataflow}

![目的地步驟概述步驟4](../assets/api/batch-destination/step4.png)

使用您在上一步中取得的流量規格、來源連線及目標連線ID，您現在可以在[!DNL Experience Platform]資料與匯出資料檔案的目的地之間建立資料流。 將此步驟視為建構管道，稍後資料會透過管道在[!DNL Experience Platform]和您想要的目的地之間流動。

若要建立資料流，請執行POST要求，如下所示，同時在承載中提供下列提及的值。

**API格式**

```http
POST /flows
```

**要求**

```shell
curl -X POST \
'https://platform.adobe.io/data/foundation/flowservice/flows' \
-H 'Authorization: Bearer {ACCESS_TOKEN}' \
-H 'x-api-key: {API_KEY}' \
-H 'x-gw-ims-org-id: {ORG_ID}' \
-H 'x-sandbox-name: {SANDBOX_NAME}' \
-H 'Content-Type: application/json' \
-d  '{
   
        "name": "activate audiences to Adobe Campaign",
        "description": "This operation creates a dataflow which we will later use to activate audiences to Adobe Campaign",
        "flowSpec": {
            "id": "{FLOW_SPEC_ID}",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "{SOURCE_CONNECTION_ID}"
        ],
        "targetConnectionIds": [
            "{TARGET_CONNECTION_ID}"
        ],
        "transformations": [
            {
                "name": "GeneralTransform",
                "params": {
                    "segmentSelectors": {
                        "selectors": []
                    },
                    "profileSelectors": {
                        "selectors": []
                    }
                }
            }
        ]
    }
```

| 屬性 | 說明 |
| --------- | ----------- |
| `name` | 為您正在建立的資料流命名。 |
| `description` | 您可以選擇為資料流提供說明。 |
| `flowSpec.Id` | 使用您要連線之批次目的地的流程規格ID。 若要擷取流程規格ID，請對`flowspecs`端點執行GET作業，如[流程規格API參考檔案](https://www.adobe.io/experience-platform-apis/references/flow-service/#operation/retrieveFlowSpec)所示。 在回應中，尋找`upsTo`並複製您要連線之批次目的地的對應ID。 例如，若為Adobe Campaign，尋找`upsToCampaign`並複製`id`引數。 |
| `sourceConnectionIds` | 使用您在步驟[連線至您的Experience Platform資料](#connect-to-your-experience-platform-data)中取得的來源連線ID。 |
| `targetConnectionIds` | 使用您在步驟[連線到批次目的地](#connect-to-batch-destination)中取得的目標連線識別碼。 |
| `transformations` | 在下一步中，您會將要啟用的對象和設定檔屬性填入此區段中。 |

下表包含常用批次目的地的流量規格ID以供您參考：

| 目標 | 流量規格ID |
---------|----------|
| 所有雲端儲存空間目的地([!DNL Amazon S3]、SFTP、[!DNL Azure Blob])和[!DNL Oracle Eloqua] | `71471eba-b620-49e4-90fd-23f1fa0174d8` |
| [!DNL Oracle Responsys] | `51d675ce-e270-408d-91fc-22717bdf2148` |
| [!DNL Salesforce Marketing Cloud] | `493b2bd6-26e4-4167-ab3b-5e910bba44f0` |

**回應**

成功的回應傳回新建立的資料流和`etag`的識別碼(`id`)。 視需要在下一個步驟記下這兩個值，以啟動對象並匯出資料檔案。

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5",
    "etag": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```


## 啟用新目的地的資料 {#activate-data}

![目的地步驟概述步驟5](../assets/api/batch-destination/step5.png)

建立所有連線和資料流後，您現在可以將設定檔資料啟動到目的地平台。 在此步驟中，您可以選取要匯出至目的地的對象和設定檔屬性。

您也可以決定匯出檔案的檔案命名格式，以及哪些屬性應該用作[重複資料刪除索引鍵](../ui/activate-batch-profile-destinations.md#mandatory-keys)或[必要屬性](../ui/activate-batch-profile-destinations.md#mandatory-attributes)。 在此步驟中，您也可以決定傳送資料至目的地的排程。

若要將對象啟用至您的新目的地，您必須執行JSON PATCH操作，類似於以下範例。 您可以在一次呼叫中啟用多個對象和設定檔屬性。 若要深入瞭解JSON PATCH，請參閱[RFC規格](https://tools.ietf.org/html/rfc6902)。

**API格式**

```http
PATCH /flows
```

**要求**

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'If-Match: "{ETAG}"' \
--data-raw '[
    {
        "op": "add",
        "path": "/transformations/0/params/segmentSelectors/selectors/-",
        "value": {
            "type": "PLATFORM_SEGMENT",
            "value": {
                "name": "Name of the audience that you are activating",
                "description": "Description of the audience that you are activating",
                "id": "{SEGMENT_ID}",
                "filenameTemplate": "%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                "exportMode": "DAILY_FULL_EXPORT",
                "schedule": {
                    "frequency": "ONCE",
                    "startDate": "2021-12-20",
                    "startTime": "17:00"
                } 
            }
        }
    },
{
        "op": "add",
        "path": "/transformations/0/params/segmentSelectors/selectors/-",
        "value": {
            "type": "PLATFORM_SEGMENT",
            "value": {
                "name": "Name of the audience that you are activating",
                "description": "Description of the audience that you are activating",
                "id": "{SEGMENT_ID}",
                "filenameTemplate": "%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                "exportMode": "DAILY_FULL_EXPORT",
                "schedule": {
                    "frequency": "ONCE",
                    "triggerType": "SCHEDULED",
                    "startDate": "2021-12-20",
                    "startTime": "17:00"
                },   
            }
        }
    },
{
        "op": "add",
        "path": "/transformations/0/params/profileSelectors/selectors/-",
        "value": {
            "type": "JSON_PATH",
            "value": {
                "path": "{PROFILE_ATTRIBUTE}"
            }
        }
    }
]
```

| 屬性 | 說明 |
| --------- | ----------- |
| `{DATAFLOW_ID}` | 在URL中，使用您在上一步建立的資料流ID。 |
| `{ETAG}` | 從上一步驟中的回應取得`{ETAG}`，[建立資料流](#create-dataflow)。 上一步驟中的回應格式已逸出引號。 您必須在請求標頭中使用未逸出的值。 請參閱下列範例： <br> <ul><li>回應範例： `"etag":""7400453a-0000-1a00-0000-62b1c7a90000""`</li><li>要在您的請求中使用的值： `"etag": "7400453a-0000-1a00-0000-62b1c7a90000"`</li></ul> <br>每次成功更新資料流時，etag值都會更新。 |
| `{SEGMENT_ID}` | 提供您要匯出至此目的地的對象ID。 若要擷取您要啟動之對象的對象ID，請參閱Experience Platform API參考中的[擷取對象定義](https://www.adobe.io/experience-platform-apis/references/segmentation/#operation/retrieveSegmentDefinitionById)。 |
| `{PROFILE_ATTRIBUTE}` | 例如, `"person.lastName"` |
| `op` | 用於定義更新資料流所需動作的操作呼叫。 作業包括： `add`、`replace`和`remove`。 若要將對象新增至資料流，請使用`add`作業。 |
| `path` | 定義要更新的流程部分。 將對象新增至資料流時，請使用範例中指定的路徑。 |
| `value` | 您想要用來更新引數的新值。 |
| `id` | 指定您要新增至目的地資料流的對象ID。 |
| `name` | *選擇性*。 指定您要新增至目的地資料流的對象名稱。 請注意，此欄位並非必填欄位，您可以在不提供名稱的情況下成功將對象新增至目的地資料流。 |
| `filenameTemplate` | 此欄位會決定匯出至目的地之檔案的檔案名稱格式。 <br>下列選項可供使用： <br> <ul><li>`%DESTINATION_NAME%`：必要。 匯出的檔案包含目的地名稱。</li><li>`%SEGMENT_ID%`：必要。 匯出的檔案包含匯出對象的ID。</li><li>`%SEGMENT_NAME%`：選擇性。 匯出的檔案包含匯出對象的名稱。</li><li>`DATETIME(YYYYMMdd_HHmmss)`或`%TIMESTAMP%`：選擇性。 選取這兩個檔案選項之一，加入Experience Platform產生檔案的時間。</li><li>`custom-text`：選擇性。 將此預留位置取代為您要在檔案名稱結尾附加的任何自訂文字。</li></ul> <br>如需設定檔案名稱的詳細資訊，請參閱批次目的地啟動教學課程中的[設定檔案名稱](/help/destinations/ui/activate-batch-profile-destinations.md#file-names)一節。 |
| `exportMode` | 強制。 選取`"DAILY_FULL_EXPORT"`或`"FIRST_FULL_THEN_INCREMENTAL"`。 如需有關這兩個選項的詳細資訊，請參閱批次目的地啟動教學課程中的[匯出完整檔案](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files)和[匯出增量檔案](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files)。 |
| `startDate` | 選取對象應開始將設定檔匯出至您的目的地的日期。 |
| `frequency` | 強制。<br> <ul><li>對於`"DAILY_FULL_EXPORT"`匯出模式，您可以選取`ONCE`或`DAILY`。</li><li>對於`"FIRST_FULL_THEN_INCREMENTAL"`匯出模式，您可以選取`"DAILY"`、`"EVERY_3_HOURS"`、`"EVERY_6_HOURS"`、`"EVERY_8_HOURS"`、`"EVERY_12_HOURS"`。</li></ul> |
| `triggerType` | 僅適用於&#x200B;*批次目的地*。 只有在`frequency`選取器中選取`"DAILY_FULL_EXPORT"`模式時才需要此欄位。 <br>必要。<br> <ul><li>選取`"AFTER_SEGMENT_EVAL"`讓啟動工作在每日Experience Platform批次細分工作完成後立即執行。 這可確保在啟動工作執行時，最新的設定檔會匯出至您的目的地。</li><li>選取`"SCHEDULED"`讓啟動工作以固定時間執行。 這可確保Experience Platform設定檔資料每天在同一時間匯出，但您匯出的設定檔可能不是最新狀態，端視批次細分工作是否在啟動工作開始之前完成。 選取此選項時，您也必須新增`startTime`以指示UTC中應該進行每日匯出的時間。</li></ul> |
| `endDate` | 僅適用於&#x200B;*批次目的地*。 只有在批次檔案匯出目的地(例如Amazon S3、SFTP或Azure Blob)中將對象新增至資料流時，才需要此欄位。 <br>在選取`"exportMode":"DAILY_FULL_EXPORT"`和`"frequency":"ONCE"`時不適用。 <br>設定對象成員停止匯出至目的地的日期。 |
| `startTime` | 僅適用於&#x200B;*批次目的地*。 只有在批次檔案匯出目的地(例如Amazon S3、SFTP或Azure Blob)中將對象新增至資料流時，才需要此欄位。 <br>必要。 選取包含對象成員的檔案應該產生並匯出至您的目的地的時間。 |

{style="table-layout:auto"}

>[!TIP]
>
> 請參閱[更新資料流中的對象元件](/help/destinations/api/update-destination-dataflows.md#update-segment)，瞭解如何更新匯出對象的各種元件（檔案名稱範本、匯出時間等）。

**回應**

尋找202接受的回應。 未傳回任何回應內文。 若要驗證要求是否正確，請參閱下一步[驗證資料流](#validate-dataflow)。

## 驗證資料流 {#validate-dataflow}

![目的地步驟概述步驟6](../assets/api/batch-destination/step6.png)

在教學課程的最後一步，您應該驗證對象和設定檔屬性是否確實已正確對應至資料流。

若要驗證，請執行下列GET請求：

**API格式**

```http
GET /flows
```

**要求**

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--header 'x-sandbox-name: prod' \
--header 'If-Match: "{ETAG}"' 
```

* `{DATAFLOW_ID}`：使用上一步驟的資料流。
* `{ETAG}`：使用上一步驟的etag。

**回應**

傳回的回應應包含您在上一步中提交的對象和設定檔屬性，並將其納入`transformations`引數。 回應中的範例`transformations`引數可能如下所示：

```json
"transformations":[
   {
      "name":"GeneralTransform",
      "params":{
         "profileSelectors":{
            "selectors":[
               {
                  "type":"JSON_PATH",
                  "value":{
                     "path":"homeAddress.countryCode",
                     "operator":"EXISTS",
                     "mapping":{
                        "sourceType":"text/x.schema-path",
                        "source":"homeAddress.countryCode",
                        "destination":"homeAddress.countryCode",
                        "identity":false,
                        "primaryIdentity":false,
                        "functionVersion":0,
                        "copyModeMapping":false,
                        "sourceAttribute":"homeAddress.countryCode",
                        "destinationXdmPath":"homeAddress.countryCode"
                     }
                  }
               },
               {
                  "type":"JSON_PATH",
                  "value":{
                     "path":"person.name.firstName",
                     "operator":"EXISTS",
                     "mapping":{
                        "sourceType":"text/x.schema-path",
                        "source":"person.name.firstName",
                        "destination":"person.name.firstName",
                        "identity":false,
                        "primaryIdentity":false,
                        "functionVersion":0,
                        "copyModeMapping":false,
                        "sourceAttribute":"person.name.firstName",
                        "destinationXdmPath":"person.name.firstName"
                     }
                  }
               },
               {
                  "type":"JSON_PATH",
                  "value":{
                     "path":"person.name.lastName",
                     "operator":"EXISTS",
                     "mapping":{
                        "sourceType":"text/x.schema-path",
                        "source":"person.name.lastName",
                        "destination":"person.name.lastName",
                        "identity":false,
                        "primaryIdentity":false,
                        "functionVersion":0,
                        "copyModeMapping":false,
                        "sourceAttribute":"person.name.lastName",
                        "destinationXdmPath":"person.name.lastName"
                     }
                  }
               },
               {
                  "type":"JSON_PATH",
                  "value":{
                     "path":"personalEmail.address",
                     "operator":"EXISTS",
                     "mapping":{
                        "sourceType":"text/x.schema-path",
                        "source":"personalEmail.address",
                        "destination":"personalEmail.address",
                        "identity":false,
                        "primaryIdentity":false,
                        "functionVersion":0,
                        "copyModeMapping":false,
                        "sourceAttribute":"personalEmail.address",
                        "destinationXdmPath":"personalEmail.address"
                     }
                  }
               },
               {
                  "type":"JSON_PATH",
                  "value":{
                     "path":"segmentMembership.status",
                     "operator":"EXISTS",
                     "mapping":{
                        "sourceType":"text/x.schema-path",
                        "source":"segmentMembership.status",
                        "destination":"segmentMembership.status",
                        "identity":false,
                        "primaryIdentity":false,
                        "functionVersion":0,
                        "copyModeMapping":false,
                        "sourceAttribute":"segmentMembership.status",
                        "destinationXdmPath":"segmentMembership.status"
                     }
                  }
               }
            ],
            "mandatoryFields":[
               "person.name.firstName",
               "person.name.lastName"
            ],
            "primaryFields":[
               {
                  "fieldType":"ATTRIBUTE",
                  "attributePath":"personalEmail.address"
               }
            ]
         },
         "segmentSelectors":{
            "selectors":[
               {
                  "type":"PLATFORM_SEGMENT",
                  "value":{
                     "id":"9f7d37fd-7039-4454-94ef-2b0cd6c3206a",
                     "name":"Interested in Mountain Biking",
                     "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                     "exportMode":"DAILY_FULL_EXPORT",
                     "schedule":{
                        "frequency":"ONCE",
                        "startDate":"2021-12-20",
                        "startTime":"17:00"
                     },
                     "createTime":"1640016962",
                     "updateTime":"1642534355"
                  }
               },
               {
                  "type":"PLATFORM_SEGMENT",
                  "value":{
                     "id":"25768be6-ebd5-45cc-8913-12fb3f348613",
                     "name":"Loyalty Segment",
                     "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                     "exportMode":"FIRST_FULL_THEN_INCREMENTAL",
                     "schedule":{
                        "frequency":"EVERY_6_HOURS",
                        "startDate":"2021-12-22",
                        "endDate":"2021-12-31",
                        "startTime":"17:00"
                     },
                     "createTime":"1640016962",
                     "updateTime":"1642534355"
                  }
               }
            ]
         }
      }
   }
]
```

## API錯誤處理 {#api-error-handling}

本教學課程中的API端點會遵循一般Experience Platform API錯誤訊息原則。 如需解譯錯誤回應的詳細資訊，請參閱Experience Platform疑難排解指南中的[API狀態碼](/help/landing/troubleshooting.md#api-status-codes)和[請求標頭錯誤](/help/landing/troubleshooting.md#request-header-errors)。

## 後續步驟 {#next-steps}

依照本教學課程中的指示，您已成功將Experience Platform連線至其中一個慣用的檔案式電子郵件行銷目的地，並設定資料流至個別目的地以匯出資料檔案。 現在，傳出資料可用於電子郵件行銷活動、目標定位廣告和許多其他使用案例的目的地。 如需詳細資訊，請參閱下列頁面，例如如何使用流量服務API編輯現有資料流：

* [目的地概觀](../home.md)
* [目的地目錄概觀](../catalog/overview.md)
* [使用流程服務API更新目的地資料流程](../api/update-destination-dataflows.md)
