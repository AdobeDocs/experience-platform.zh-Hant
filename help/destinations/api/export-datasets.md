---
solution: Experience Platform
title: 使用流量服務API匯出資料集
description: 瞭解如何使用流量服務API將資料集匯出至所選目的地。
type: Tutorial
exl-id: f23a4b22-da04-4b3c-9b0c-790890077eaa
source-git-commit: 8b2b40be94bb35f0c6117bfc1d51f8ce282f2b29
workflow-type: tm+mt
source-wordcount: '5220'
ht-degree: 3%

---

# 使用[!DNL Flow Service API]匯出資料集

>[!AVAILABILITY]
>
>* 已購買Real-Time CDP Prime和Ultimate套件、Adobe Journey Optimizer或Customer Journey Analytics的客戶可使用此功能。 如需詳細資訊，請聯絡您的Adobe代表。

>[!IMPORTANT]
>
>**動作專案**： Experience Platform [&#128279;](/help/release-notes/latest/latest.md#destinations)的2024年9月發行版本匯入了為匯出資料集資料流設定`endTime`日期的選項。 Adobe也針對2024年9月版本&#x200B;*之前建立*&#x200B;的所有資料集匯出資料流，引入了2025年9月1日的預設結束日期。
>
>對於這些資料流中的任一資料流，您需要在結束日期之前手動更新資料流中的結束日期，否則您的匯出將在該日期停止。 使用Experience Platform UI檢視哪些資料流將設定在2025年9月1日停止。
>
>同樣地，對於您建立但未指定`endTime`日期的任何資料流，這些資料流將預設為從建立日期起六個月的結束時間。

<!--

>You can retrieve a list of such dataflows by performing the following API call: `https://platform.adobe.io/data/foundation/flowservice/flows?property=scheduleParams.endTime==UNIXTIMESTAMPTHATWEWILLUSE`
>

-->

本文說明使用[!DNL Flow Service API]從Adobe Experience Platform將[資料集](/help/catalog/datasets/overview.md)匯出至您偏好的雲端儲存空間位置（例如[!DNL Amazon S3]、SFTP位置或[!DNL Google Cloud Storage]）所需的工作流程。

>[!TIP]
>
>您也可以使用Experience Platform使用者介面來匯出資料集。 如需詳細資訊，請參閱[匯出資料集UI教學課程](/help/destinations/ui/export-datasets.md)。

## 可用於匯出的資料集 {#datasets-to-export}

您可以匯出的資料集取決於Experience Platform應用程式(Real-Time CDP、Adobe Journey Optimizer)、層級(Prime或Ultimate)以及您購買的任何附加元件(例如：Data Distiller)。

請參閱UI教學課程頁面[&#128279;](/help/destinations/ui/export-datasets.md#datasets-to-export)上的表格，瞭解您可以匯出哪些資料集。

## 支援的目的地 {#supported-destinations}

目前，您可以將資料集匯出至熒幕擷取畫面中強調並列於下方的雲端儲存空間目的地。

![支援資料集匯出的目的地](/help/destinations/assets/ui/export-datasets/destinations-supporting-dataset-exports.png)

* [[!DNL Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md)
* [[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md)
* [[!DNL Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md)
* [[!DNL Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog)
* [[!DNL Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog)
* [[!DNL SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog)

## 先決條件 {#prerequisites}

若要匯出資料集，請注意下列先決條件：

* 若要將資料集匯出至雲端儲存空間目的地，您必須已成功[連線至目的地](/help/destinations/ui/connect-destination.md)。 如果您尚未這麼做，請前往[目的地目錄](/help/destinations/catalog/overview.md)，瀏覽支援的目的地，並設定您要使用的目的地。
* 需要啟用設定檔資料集才能在即時客戶設定檔中使用。 [閱讀更多資訊](/help/ingestion/tutorials/ingest-batch-data.md#enable-for-profile)以瞭解如何啟用此選項。

## 快速入門 {#get-started}

![概述 — 建立目的地和匯出資料集的步驟](../assets/api/export-datasets/export-datasets-api-workflow-get-started.png)

本指南需要您深入了解下列 Adobe Experience Platform 元件：

* [[!DNL Experience Platform datasets]](/help/catalog/datasets/overview.md)：所有成功內嵌至Adobe Experience Platform的資料都會以資料集的形式儲存在[!DNL Data Lake]中。 資料集是資料集合的儲存和管理結構，通常是包含方案 (欄) 和欄位 (列) 的表格。 資料集也包含中繼資料，可說明其儲存資料的各個層面。
   * [[!DNL Sandboxes]](../../sandboxes/home.md)： [!DNL Experience Platform]提供的虛擬沙箱可將單一[!DNL Experience Platform]執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

以下小節提供您必須知道的其他資訊，才能將資料集匯出到Experience Platform中的雲端儲存空間目標。

### 必要權限 {#permissions}

若要匯出資料集，您需要&#x200B;**[!UICONTROL 檢視目的地]**、**[!UICONTROL 檢視資料集]**&#x200B;以及&#x200B;**[!UICONTROL 管理和啟用資料集目的地]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

為確保您擁有匯出資料集的必要許可權以及目的地支援匯出資料集，請瀏覽目的地目錄。 如果目的地有&#x200B;**[!UICONTROL 啟用]**&#x200B;或&#x200B;**[!UICONTROL 匯出資料集]**&#x200B;控制項，則您擁有適當的許可權。

### 讀取範例 API 呼叫 {#reading-sample-api-calls}

本教學課程提供範例API呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭和正確格式化的請求承載。 此外，也提供 API 回應中傳回的範例 JSON。 如需檔案中所使用範例API呼叫慣例的詳細資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集必要和選用標題的值 {#gather-values-headers}

若要呼叫[!DNL Experience Platform] API，您必須先完成[Experience Platform驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程會提供所有 [!DNL Experience Platform] API 呼叫中每個必要標頭的值，如下所示：

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

在本教學課程中，您可以找到所有API作業的隨附參考檔案。 請參閱Adobe Developer網站[&#128279;](https://developer.adobe.com/experience-platform-apis/references/destinations/)上的[!DNL Flow Service] - Destinations API檔案。 我們建議您同時使用本教學課程和API參考檔案。

### 字彙 {#glossary}

如需在此API教學課程中將會遇到的術語說明，請閱讀API參考檔案的[字彙表區段](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Glossary)。

### 收集所需目的地的連線規格和流量規格 {#gather-connection-spec-flow-spec}

在開始匯出資料集的工作流程之前，請確定您要將資料集匯出到的目的地的連線規格和流程規格ID。 請參考下表。


| 目標 | 連線規格 | 流量規格 |
---------|----------|---------|
| [!DNL Amazon S3] | `4fce964d-3f37-408f-9778-e597338a21ee` | `269ba276-16fc-47db-92b0-c1049a3c131f` |
| [!DNL Azure Blob Storage] | `6d6b59bf-fb58-4107-9064-4d246c0e5bb2` | `95bd8965-fc8a-4119-b9c3-944c2c2df6d2` |
| [!DNL Azure Data Lake Gen 2(ADLS Gen2)] | `be2c3209-53bc-47e7-ab25-145db8b873e1` | `17be2013-2549-41ce-96e7-a70363bec293` |
| [!DNL Data Landing Zone(DLZ)] | `10440537-2a7b-4583-ac39-ed38d4b848e8` | `cd2fc47e-e838-4f38-a581-8fff2f99b63a` |
| [!DNL Google Cloud Storage] | `c5d93acb-ea8b-4b14-8f53-02138444ae99` | `585c15c4-6cbf-4126-8f87-e26bff78b657` |
| SFTP | `36965a81-b1c6-401b-99f8-22508f1e6a26` | `354d6aad-4754-46e4-a576-1b384561c440` |

{style="table-layout:auto"}

您需要這些ID來建構各種[!DNL Flow Service]實體。 您也必須參考[!DNL Connection Spec]本身的某些部分來設定某些實體，以便從[!DNL Flow Service APIs]擷取[!DNL Connection Spec]。 請參閱以下範例，擷取表格中所有目的地的連線規格：

>[!BEGINTABS]

>[!TAB Amazon S3]

**要求**

+++擷取[!DNL Amazon S3]的[!DNL connection spec]

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/4fce964d-3f37-408f-9778-e597338a21ee' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```

+++

**回應**

+++[!DNL Amazon S3] — 連線規格

```json
{
    "items": [
        {
            "id": "4fce964d-3f37-408f-9778-e597338a21ee",
            "name": "Amazon S3",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
//...
```

+++

>[!TAB Azure Blob儲存體]

**要求**

+++擷取[!DNL Azure Blob Storage]的[!DNL connection spec]

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/6d6b59bf-fb58-4107-9064-4d246c0e5bb2' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```

+++

**回應**

+++[!DNL Azure Blob Storage] - [!DNL Connection spec]

```json
{
    "items": [
        {
            "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2",
            "name": "Azure Blob Storage",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
//...
```

+++

>[!TAB Azure Data Lake Gen 2(ADLS Gen2)]

**要求**

+++擷取[!DNL Azure Data Lake Gen 2(ADLS Gen2]的[!DNL connection spec])

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/be2c3209-53bc-47e7-ab25-145db8b873e1' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```

+++

**回應**

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)] - [!DNL Connection spec]

```json
{
    "items": [
        {
            "id": "be2c3209-53bc-47e7-ab25-145db8b873e1",
            "name": "Azure Data Lake Gen2",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
//...
```

+++

>[!TAB 資料登陸區域(DLZ)]

**要求**

+++擷取[!DNL Data Landing Zone(DLZ)]的[!DNL connection spec]

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/10440537-2a7b-4583-ac39-ed38d4b848e8' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```

+++

**回應**

+++[!DNL Data Landing Zone(DLZ)] - [!DNL Connection spec]

```json
{
    "items": [
        {
            "id": "10440537-2a7b-4583-ac39-ed38d4b848e8",
            "name": "Data Landing Zone",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
//...
```

+++

>[!TAB Google雲端儲存空間]

**要求**

+++擷取[!DNL Google Cloud Storage]的[!DNL connection spec]

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/c5d93acb-ea8b-4b14-8f53-02138444ae99' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```

+++

**回應**

+++[!DNL Google Cloud Storage] - [!DNL Connection spec]

```json
{
    "items": [
        {
            "id": "c5d93acb-ea8b-4b14-8f53-02138444ae99",
            "name": "Google Cloud Storage",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
//...
```

+++

>[!TAB SFTP]

**要求**

+++擷取SFTP的[!DNL connection spec]

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/36965a81-b1c6-401b-99f8-22508f1e6a26' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```

+++

**回應**

+++SFTP - [!DNL Connection spec]

```json
{
    "items": [
        {
            "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
            "name": "SFTP",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
//...
```

+++

>[!ENDTABS]

請依照下列步驟，將資料集資料流設定為雲端儲存空間目的地。 對於某些步驟，請求和回應會因不同的雲端儲存空間目的地而異。 在這些情況下，請使用頁面上的索引標籤，擷取您要連線並匯出資料集的目標的特定請求和回應。 請確定您設定的目的地使用正確的[!DNL connection spec]和[!DNL flow spec]。

## 擷取資料集清單 {#retrieve-list-of-available-datasets}

![顯示匯出資料集工作流程步驟1的圖表](../assets/api/export-datasets/export-datasets-api-workflow-retrieve-datasets.png)

若要擷取符合啟用資格的資料集清單，首先要對以下端點進行API呼叫。

>[!BEGINSHADEBOX]

**要求**

+++擷取合格的資料集 — 請求

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/23598e46-f560-407b-88d5-ea6207e49db0/configs?outputType=activationDatasets&outputField=datasets&start=0&limit=20&properties=name,state' \
--header 'accept: application/json' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```

請注意，若要擷取合格的資料集，要求URL中使用的[!DNL connection spec] ID必須是資料湖來源連線規格ID `23598e46-f560-407b-88d5-ea6207e49db0`，而且必須指定兩個查詢引數`outputField=datasets`和`outputType=activationDatasets`。 所有其他查詢引數都是[目錄服務API](https://developer.adobe.com/experience-platform-apis/references/catalog/)支援的標準引數。

+++

**回應**

+++擷取資料集 — 回應

```json
{
    "items": [
        {
            "id": "5ef3e324052581191aa6a466",
            "name": "AAM Authenticated Profiles Meta Data",
            "description": "Activation profile export dataset",
            "fileDescription": {
                "persisted": true,
                "containerFormat": "parquet",
                "format": "parquet"
            },
            "aspect": "production",
            "state": "DRAFT"
        },
        {
            "id": "5ef3e3259ad2a1191ab7dd7d",
            "name": "AAM Devices Data",
            "description": "Activation profile export dataset",
            "fileDescription": {
                "persisted": true,
                "containerFormat": "parquet",
                "format": "parquet"
            },
            "aspect": "production",
            "state": "DRAFT"
        },
        {
            "id": "5ef3e325582424191b1beb42",
            "name": "AAM Devices Profile Meta Data",
            "description": "Activation profile export dataset",
            "fileDescription": {
                "persisted": true,
                "containerFormat": "parquet",
                "format": "parquet"
            },
            "aspect": "production",
            "state": "DRAFT"
        },
        {
            "id": "5ef3e328582424191b1beb44",
            "name": "AAM Realtime",
            "description": "Activation profile export dataset",
            "fileDescription": {
                "persisted": true,
                "containerFormat": "parquet",
                "format": "parquet"
            },
            "aspect": "production",
            "state": "DRAFT"
        },
        {
            "id": "5ef3e328fe742a191b2b3ea5",
            "name": "AAM Realtime Profile Updates",
            "description": "Activation profile export dataset",
            "fileDescription": {
                "persisted": true,
                "containerFormat": "parquet",
                "format": "parquet"
            },
            "aspect": "production",
            "state": "DRAFT"
        }
    ],
    "pageInfo": {
        "start": 0,
        "end": 4,
        "total": 149,
        "hasNext": true
    }
}
```

+++

>[!ENDSHADEBOX]

成功的回應包含符合啟用條件的資料集清單。 這些資料集可在下一步中建構來源連線時使用。

如需每個傳回資料集的不同回應引數相關資訊，請參閱[資料集API開發人員檔案](https://developer.adobe.com/experience-platform-apis/references/catalog/#tag/Datasets/operation/listDatasets)。

## 建立來源連線 {#create-source-connection}

![顯示匯出資料集工作流程步驟2的圖表](../assets/api/export-datasets/export-datasets-api-workflow-create-source-connection.png)

擷取您要匯出的資料集清單後，您可以使用這些資料集ID建立來源連線。

>[!BEGINSHADEBOX]

**要求**

+++建立來源連線 — 請求

請注意請求範例中反白顯示內嵌註解的行，這些註解會提供額外資訊。 將請求複製貼上您選擇的終端機時，移除請求中的內嵌註解。

```shell {line-numbers="true" start-line="1" highlight="12,16"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
  "name": "Connecting to Data Lake",
  "description": "Data Lake source connection to export datasets",
  "connectionSpec": {
    "id": "23598e46-f560-407b-88d5-ea6207e49db0", // this connection spec ID is always the same for Source Connections
    "version": "1.0"
  },
  "params": {
    "datasets": [ // datasets to activate
      {
        "dataSetId": "5ef3e3259ad2a1191ab7dd7d",
        "name": "AAM Devices Data"
      }
    ]
  }
}'
```

+++



**回應**

+++建立來源連線 — 回應

```json
{
    "id": "900df191-b983-45cd-90d5-4c7a0326d650",
    "etag": "\"0500ebe1-0000-0200-0000-63e28d060000\""
}
```

+++

>[!ENDSHADEBOX]

成功的回應會傳回新建立的來源連線的識別碼(`id`)和`etag`。 記下來源連線ID，因為稍後建立資料流時會需要它。

另請記住：

* 在此步驟中建立的來源連線需要連結至資料流，其資料集才能啟動至目的地。 請參閱[建立資料流](#create-dataflow)區段，瞭解如何將來源連線連結到資料流的資訊。
* 來源連線的資料集ID在建立後即無法修改。 如果您需要從來源連線新增或移除資料集，則必須建立新的來源連線，並將新來源連線的ID連結至資料流。

## 建立（目標）基礎連線 {#create-base-connection}

![顯示匯出資料集工作流程步驟3的圖表](../assets/api/export-datasets/export-datasets-api-workflow-create-base-connection.png)

基礎連線會將認證安全地儲存到您的目的地。 根據目的地型別，針對該目的地進行驗證所需的認證可能會有所不同。 若要尋找這些驗證引數，請先依照[收集連線規格和流程規格](#gather-connection-spec-flow-spec)一節中的說明，擷取您所要目的地的[!DNL connection spec]，然後檢視回應的`authSpec`。 請參考下列標籤，以取得所有支援目的地的`authSpec`屬性。

>[!BEGINTABS]

>[!TAB Amazon S3]

+++[!DNL Amazon S3] - [!DNL Connection spec]顯示[!DNL auth spec]

請注意下方[!DNL connection spec]範例中反白顯示內嵌註解的一行，這些註解提供了在[!DNL connection spec]中尋找驗證引數的位置的其他資訊。

```json {line-numbers="true" start-line="1" highlight="8"}
{
    "items": [
        {
            "id": "4fce964d-3f37-408f-9778-e597338a21ee",
            "name": "Amazon S3",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [ // describes the authentication parameters
                {
                    "name": "Access Key",
                    "type": "KeyBased",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "description": "Defines auth params required for connecting to amazon-s3",
                        "type": "object",
                        "properties": {
                            "s3AccessKey": {
                                "description": "Access key id",
                                "type": "string",
                                "pattern": "^[A-Z2-7]{20}$"
                            },
                            "s3SecretKey": {
                                "description": "Secret access key for the user account",
                                "type": "string",
                                "format": "password",
                                "pattern": "^[A-Za-z0-9\/\\+]{40}$"
                            }
                        },
                        "required": [
                            "s3SecretKey",
                            "s3AccessKey"
                        ]
                    }
                }
            ],
//...
```

+++

>[!TAB Azure Blob儲存體]

+++[!DNL Azure Blob Storage] - [!DNL Connection spec]顯示[!DNL auth spec]

請注意下方[!DNL connection spec]範例中反白顯示內嵌註解的一行，這些註解提供了在[!DNL connection spec]中尋找驗證引數的位置的其他資訊。

```json {line-numbers="true" start-line="1" highlight="8"}
{
    "items": [
        {
            "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2",
            "name": "Azure Blob Storage",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [ // describes the authentication parameters
                {
                    "name": "ConnectionString",
                    "type": "ConnectionString",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "description": "Connection String for Azure Blob based destinations",
                        "type": "object",
                        "properties": {
                            "connectionString": {
                                "description": "connection string for login",
                                "type": "string",
                                "format": "password"
                            }
                        },
                        "required": [
                            "connectionString"
                        ]
                    }
                }
            ],
//...
```

+++


>[!TAB Azure Data Lake Gen 2(ADLS Gen2)]

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)] - [!DNL Connection spec]顯示[!DNL auth spec]

請注意下方[!DNL connection spec]範例中反白顯示內嵌註解的一行，這些註解提供了在[!DNL connection spec]中尋找驗證引數的位置的其他資訊。

```json {line-numbers="true" start-line="1" highlight="8"}
{
    "items": [
        {
            "id": "be2c3209-53bc-47e7-ab25-145db8b873e1",
            "name": "Azure Data Lake Gen2",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [ // describes the authentication parameters
                {
                    "name": "Azure Service Principal Auth",
                    "type": "AzureServicePrincipal",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "description": "defines auth params required for connecting to adlsgen2 using service principal",
                        "type": "object",
                        "properties": {
                            "url": {
                                "description": "Endpoint for Azure Data Lake Storage Gen2.",
                                "type": "string"
                            },
                            "servicePrincipalId": {
                                "description": "Service Principal Id to connect to ADLSGen2.",
                                "type": "string"
                            },
                            "servicePrincipalKey": {
                                "description": "Service Principal Key to connect to ADLSGen2.",
                                "type": "string",
                                "format": "password"
                            },
                            "tenant": {
                                "description": "Tenant information(domain name or tenant ID).",
                                "type": "string"
                            }
                        },
                        "required": [
                            "servicePrincipalKey",
                            "url",
                            "tenant",
                            "servicePrincipalId"
                        ]
                    }
                }
            ],
//...
```

+++


>[!TAB 資料登陸區域(DLZ)]

+++[!DNL Data Landing Zone(DLZ)] - [!DNL Connection spec]顯示[!DNL auth spec]

>[!NOTE]
>
>資料登陸區域目的地不需要[!DNL auth spec]。

```json
{
    "items": [
        {
            "id": "10440537-2a7b-4583-ac39-ed38d4b848e8",
            "name": "Data Landing Zone",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [],
//...
```

+++

>[!TAB Google雲端儲存空間]

+++[!DNL Google Cloud Storage] - [!DNL Connection spec]顯示[!DNL auth spec]

請注意下方[!DNL connection spec]範例中反白顯示內嵌註解的一行，這些註解提供了在[!DNL connection spec]中尋找驗證引數的位置的其他資訊。

```json {line-numbers="true" start-line="1" highlight="8"}
{
    "items": [
        {
            "id": "c5d93acb-ea8b-4b14-8f53-02138444ae99",
            "name": "Google Cloud Storage",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [ // describes the authentication parameters
                {
                    "name": "Google Cloud Storage authentication credentials",
                    "type": "GoogleCloudStorageAuth",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "description": "defines auth params required for connecting to google cloud storage connector.",
                        "type": "object",
                        "properties": {
                            "accessKeyId": {
                                "description": "Access Key Id for the user account",
                                "type": "string"
                            },
                            "secretAccessKey": {
                                "description": "Secret Access Key for the user account",
                                "type": "string",
                                "format": "password"
                            }
                        },
                        "required": [
                            "accessKeyId",
                            "secretAccessKey"
                        ]
                    }
                }
            ],
//...
```

+++

>[!TAB SFTP]

+++SFTP - [!DNL Connection spec]顯示[!DNL auth spec]

>[!NOTE]
>
>SFTP目的地在[!DNL auth spec]中包含兩個個別的專案，因為它同時支援密碼和SSH金鑰驗證。

請注意下方[!DNL connection spec]範例中反白顯示內嵌註解的一行，這些註解提供了在[!DNL connection spec]中尋找驗證引數的位置的其他資訊。

```json {line-numbers="true" start-line="1" highlight="8"}
{
    "items": [
        {
            "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
            "name": "SFTP",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [ // describes the authentication parameters
                {
                    "name": "SFTP with Password",
                    "type": "SFTP",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "description": "defines auth params required for connecting to sftp locations with a password",
                        "type": "object",
                        "properties": {
                            "domain": {
                                "description": "Domain of server",
                                "type": "string"
                            },
                            "username": {
                                "description": "Username",
                                "type": "string"
                            },
                            "password": {
                                "description": "Password",
                                "type": "string",
                                "format": "password"
                            }
                        },
                        "required": [
                            "password",
                            "domain",
                            "username"
                        ]
                    }
                },
                {
                    "name": "SFTP with SSH Key",
                    "type": "SFTP",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "description": "defines auth params required for connecting to sftp locations using SSH Key",
                        "type": "object",
                        "properties": {
                            "domain": {
                                "description": "Domain of server",
                                "type": "string"
                            },
                            "username": {
                                "description": "Username",
                                "type": "string"
                            },
                            "sshKey": {
                                "description": "Base64 string of the private SSH key",
                                "type": "string",
                                "format": "password",
                                "contentEncoding": "base64",
                                "uiAttributes": {
                                    "tooltip": {
                                        "id": "platform_destinations_connect_sftp_ssh",
                                        "fallbackUrl": "http://www.adobe.com/go/destinations-sftp-connection-parameters-en "
                                    }
                                }
                            }
                        },
                        "required": [
                            "sshKey",
                            "domain",
                            "username"
                        ]
                    }
                }
            ],
//...
```

+++

>[!ENDTABS]

使用驗證規格（亦即回應中的`authSpec`）中指定的屬性，您可以使用每個目的地型別特定的必要認證來建立基礎連線，如下列範例所示：

>[!BEGINTABS]

>[!TAB Amazon S3]

**要求**

+++[!DNL Amazon S3] — 基底連線要求

>[!TIP]
>
>如需有關如何取得所需驗證認證的資訊，請參閱Amazon S3目的地檔案頁面的[對目的地進行驗證](/help/destinations/catalog/cloud-storage/amazon-s3.md#authenticate)區段。

請注意請求範例中反白顯示內嵌註解的行，這些註解會提供額外資訊。 將請求複製貼上您選擇的終端機時，移除請求中的內嵌註解。

```shell {line-numbers="true" start-line="1" highlight="18"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: <API-KEY>' \
--header 'x-gw-ims-org-id: <IMS-ORG-ID>' \
--header 'x-sandbox-name: <SANDBOX-NAME>' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "Amazon S3 Base Connection",
  "auth": {
    "specName": "Access Key",
    "params": {
      "s3SecretKey": "<Add secret key>",
      "s3AccessKey": "<Add access key>"
    }
  },
  "connectionSpec": {
    "id": "4fce964d-3f37-408f-9778-e597338a21ee", // Amazon S3 connection spec
    "version": "1.0"
  }
}'
```

+++

**回應**

+++[!DNL Amazon S3]基本連線回應

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Azure Blob儲存體]

**要求**

+++[!DNL Azure Blob Storage] — 基底連線要求

>[!TIP]
>
>有關如何取得所需驗證認證的資訊，請參閱Azure Blob儲存體目的地檔案頁面的[對目的地](/help/destinations/catalog/cloud-storage/azure-blob.md#authenticate)驗證區段。

請注意請求範例中反白顯示內嵌註解的行，這些註解會提供額外資訊。 將請求複製貼上您選擇的終端機時，移除請求中的內嵌註解。

```shell {line-numbers="true" start-line="1" highlight="16"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: <API-KEY>' \
--header 'x-gw-ims-org-id: <IMS-ORG-ID>' \
--header 'x-sandbox-name: <SANDBOX-NAME>' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "Azure Blob Storage Base Connection",
  "auth": {
    "specName": "ConnectionString",
    "params": {
      "connectionString": "<Add Azure Blob connection string>"
    }
  },
  "connectionSpec": {
    "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2", // Azure Blob Storage connection spec
    "version": "1.0"
  }
}'
```

+++

**回應**

+++[!DNL Azure Blob Storage] — 基底連線回應

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Azure Data Lake Gen 2(ADLS Gen2)]

**要求**

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)] — 基底連線要求

>[!TIP]
>
>有關如何取得所需驗證認證的資訊，請參閱Azure Data Lake Gen 2(ADLS Gen2)目的地檔案頁面的[對目的地](/help/destinations/catalog/cloud-storage/adls-gen2.md#authenticate)驗證區段。

請注意請求範例中反白顯示內嵌註解的行，這些註解會提供額外資訊。 將請求複製貼上您選擇的終端機時，移除請求中的內嵌註解。

```shell {line-numbers="true" start-line="1" highlight="20"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: <API-KEY>' \
--header 'x-gw-ims-org-id: <IMS-ORG-ID>' \
--header 'x-sandbox-name: <SANDBOX-NAME>' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "Azure Data Lake Gen 2(ADLS Gen2) Base Connection",
  "auth": {
    "specName": "Azure Service Principal Auth",
    "params": {
      "servicePrincipalKey": "<Add servicePrincipalKey>",
      "url": "<Add url>",
      "tenant": "<Add tenant>",
      "servicePrincipalId": "<Add servicePrincipalId>"
    }
  },
  "connectionSpec": {
    "id": "be2c3209-53bc-47e7-ab25-145db8b873e1", // Azure Data Lake Gen 2(ADLS Gen2) connection spec
    "version": "1.0"
  }
}'
```

+++

**回應**

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)] — 基底連線回應

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB 資料登陸區域(DLZ)]

**要求**

+++[!DNL Data Landing Zone(DLZ)] — 基底連線要求

>[!TIP]
>
>資料登陸區域目的地不需要驗證認證。 如需詳細資訊，請參閱資料登陸區域目的地檔案頁面的[對目的地](/help/destinations/catalog/cloud-storage/data-landing-zone.md#authenticate)驗證區段。

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: <API-KEY>' \
--header 'x-gw-ims-org-id: <IMS-ORG-ID>' \
--header 'x-sandbox-name: <SANDBOX-NAME>' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "Data Landing Zone Base Connection",
  "connectionSpec": {
    "id": "3567r537-2a7b-4583-ac39-ed38d4b848e8",
    "version": "1.0"
  }
}'
```

+++

**回應**

+++[!DNL Data Landing Zone] — 基底連線回應

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Google雲端儲存空間]

**要求**

+++[!DNL Google Cloud Storage] — 基底連線要求

>[!TIP]
>
>如需有關如何取得所需驗證認證的資訊，請參閱Google雲端儲存空間目的地檔案頁面的[對目的地進行驗證](/help/destinations/catalog/cloud-storage/google-cloud-storage.md#authenticate)區段。

請注意請求範例中反白顯示內嵌註解的行，這些註解會提供額外資訊。 將請求複製貼上您選擇的終端機時，移除請求中的內嵌註解。

```shell {line-numbers="true" start-line="1" highlight="18"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: <API-KEY>' \
--header 'x-gw-ims-org-id: <IMS-ORG-ID>' \
--header 'x-sandbox-name: <SANDBOX-NAME>' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "Google Cloud Storage Base Connection",
  "auth": {
    "specName": "Google Cloud Storage authentication credentials",
    "params": {
      "accessKeyId": "<Add accessKeyId>",
      "secretAccessKey": "<Add secret Access Key>"
    }
  },
  "connectionSpec": {
    "id": "c5d93acb-ea8b-4b14-8f53-02138444ae99", // Google Cloud Storage connection spec
    "version": "1.0"
  }
}'
```

+++

**回應**

+++[!DNL Google Cloud Storage] — 基底連線回應

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB SFTP]

**要求**

+++使用密碼的SFTP — 基本連線要求

>[!TIP]
>
>如需有關如何取得所需驗證認證的資訊，請參閱SFTP目的地檔案頁面的[對目的地進行驗證](/help/destinations/catalog/cloud-storage/sftp.md#authentication-information)區段。

請注意請求範例中反白顯示內嵌註解的行，這些註解會提供額外資訊。 將請求複製貼上您選擇的終端機時，移除請求中的內嵌註解。

```shell {line-numbers="true" start-line="1" highlight="19"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: <API-KEY>' \
--header 'x-gw-ims-org-id: <IMS-ORG-ID>' \
--header 'x-sandbox-name: <SANDBOX-NAME>' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "SFTP with password Base Connection",
  "auth": {
    "specName": "SFTP with Password",
    "params": {
      "domain": "<Add domain>",
      "username": "<Add username>",
      "password": "<Add password>"
    }
  },
  "connectionSpec": {
    "id": "36965a81-b1c6-401b-99f8-22508f1e6a26", // SFTP connection spec
    "version": "1.0"
  }
}'
```

+++

+++使用SSH金鑰的SFTP — 基本連線要求

>[!TIP]
>
>如需有關如何取得所需驗證認證的資訊，請參閱SFTP目的地檔案頁面的[對目的地進行驗證](/help/destinations/catalog/cloud-storage/sftp.md#authentication-information)區段。

請注意請求範例中反白顯示內嵌註解的行，這些註解會提供額外資訊。 將請求複製貼上您選擇的終端機時，移除請求中的內嵌註解。

```shell {line-numbers="true" start-line="1" highlight="19"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: <API-KEY>' \
--header 'x-gw-ims-org-id: <IMS-ORG-ID>' \
--header 'x-sandbox-name: <SANDBOX-NAME>' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "SFTP with SSH key Base Connection",
  "auth": {
    "specName": "SFTP with SSH Key",
    "params": {
      "domain": "<Add domain>",
      "username": "<Add username>",
      "sshKey": "<Add SSH key>"
    }
  },
  "connectionSpec": {
    "id": "36965a81-b1c6-401b-99f8-22508f1e6a26", // SFTP connection spec
    "version": "1.0"
  }
}'
```

+++

**回應**

+++SFTP — 基本連線回應

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!ENDTABS]

記下回應中的連線ID。 建立目標連線時，下個步驟需要此ID。

## 建立目標連線 {#create-target-connection}

![顯示匯出資料集工作流程步驟4的圖表](../assets/api/export-datasets/export-datasets-api-workflow-create-target-connection.png)

接下來，您需要建立目標連線，以儲存資料集的匯出引數。 匯出引數包括位置、檔案格式、壓縮和其他細節。 請參閱目的地的連線規格中提供的`targetSpec`屬性，以瞭解每個目的地型別的支援屬性。 請參考下列標籤，以取得所有支援目的地的`targetSpec`屬性。

>[!IMPORTANT]
>
>僅壓縮模式支援匯出至JSON檔案。 壓縮和非壓縮模式都支援匯出至[!DNL Parquet]個檔案。
>
>匯出的JSON檔案格式為NDJSON，這是大資料生態系統中的標準交換格式。 Adobe建議使用與NDJSON相容的使用者端來讀取匯出的檔案。

>[!BEGINTABS]

>[!TAB Amazon S3]

+++[!DNL Amazon S3] - [!DNL Connection spec]顯示目標連線引數

請注意下方[!DNL connection spec]範例中有內嵌註解之醒目提示的行，這些註解提供了在連線規格中何處尋找[!DNL target spec]引數的相關額外資訊。 您也可以在下列範例中看到目標引數是&#x200B;*不*&#x200B;適用於資料集匯出目的地。

```json {line-numbers="true" start-line="1" highlight="10,41,56"}
{
    "items": [
        {
            "id": "4fce964d-3f37-408f-9778-e597338a21ee",
            "name": "Amazon S3",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [...],
            "encryptionSpecs": [...],
            "targetSpec": { // describes the target connection parameters
                "name": "User based target",
                "type": "UserNamespace",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "bucketName": {
                            "title": "Bucket name",
                            "description": "Bucket name",
                            "type": "string",
                            "pattern": "(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
                            "uiAttributes": {
                                "tooltip": {
                                    "id": "platform_destinations_connect_s3_bucket",
                                    "fallbackUrl": "http://www.adobe.com/go/destinations-amazon-s3-connection-parameters-en"
                                }
                            }
                        },
                        "path": {
                            "title": "Folder path",
                            "description": "Output path for copying files",
                            "type": "string",
                            "pattern": "^[0-9a-zA-Z\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\/?)+$",
                            "uiAttributes": {
                                "tooltip": {
                                    "id": "platform_destinations_connect_s3_folderpath",
                                    "fallbackUrl": "http://www.adobe.com/go/destinations-amazon-s3-connection-parameters-en"
                                }
                            }
                        },
                        "fileType": {...}, // not applicable to dataset destinations
                        "datasetFileType": {
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "csvOptions": {...}, // not applicable to dataset destinations
                        "compression": {
                            "title": "Compression format",
                            "description": "Select the desired file compression format.",
                            "type": "string",
                            "enum": [
                                "NONE",
                                "GZIP"
                            ]
                        }
                    },
                    "required": [
                        "bucketName",
                        "path",
                        "datasetFileType",
                        "compression",
                        "fileType"
                    ]
                }
//...
```

+++

>[!TAB Azure Blob儲存體]

+++[!DNL Azure Blob Storage] - [!DNL Connection spec]顯示目標連線引數

請注意下方[!DNL connection spec]範例中有內嵌註解之醒目提示的行，這些註解提供了在連線規格中何處尋找[!DNL target spec]引數的相關額外資訊。 您也可以在下列範例中看到目標引數是&#x200B;*不*&#x200B;適用於資料集匯出目的地。

```json {line-numbers="true" start-line="1" highlight="10,29,44"}
{
    "items": [
        {
            "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2",
            "name": "Azure Blob Storage",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [...],
            "encryptionSpecs": [...],
            "targetSpec": { // describes the target connection parameters
                "name": "User based target",
                "type": "UserNamespace",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "path": {
                            "title": "Folder path",
                            "description": "Output path (relative) indicating where to upload the data",
                            "type": "string",
                            "pattern": "^[0-9a-zA-Z\/\\!\\-_\\.\\*\\'\\(\\)]+$"
                        },
                        "container": {
                            "title": "Container",
                            "description": "Container within the storage where to upload the data",
                            "type": "string",
                            "pattern": "^[a-z0-9](?!.*--)[a-z0-9-]{1,61}[a-z0-9]$"
                        },
                        "fileType": {...}, // not applicable to dataset destinations
                        "datasetFileType": {
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "csvOptions": {...}, // not applicable to dataset destinations
                        "compression": {
                            "title": "Compression format",
                            "description": "Select the desired file compression format.",
                            "type": "string",
                            "enum": [
                                "NONE",
                                "GZIP"
                            ]
                        }
                    },
                    "required": [
                        "container",
                        "path",
                        "datasetFileType",
                        "compression",
                        "fileType"
                    ]
                }
//...
```

+++


>[!TAB Azure Data Lake Gen 2(ADLS Gen2)]

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)] - [!DNL Connection spec]顯示目標連線引數

請注意下方[!DNL connection spec]範例中有內嵌註解之醒目提示的行，這些註解提供了在連線規格中何處尋找[!DNL target spec]引數的相關額外資訊。 您也可以在下列範例中看到目標引數是&#x200B;*不*&#x200B;適用於資料集匯出目的地。

```json {line-numbers="true" start-line="1" highlight="10,22,37"}
{
    "items": [
        {
            "id": "be2c3209-53bc-47e7-ab25-145db8b873e1",
            "name": "Azure Data Lake Gen2",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [...],
            "encryptionSpecs": [...],
            "targetSpec": { // describes the target connection parameters
                "name": "User based target",
                "type": "UserNamespace",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "path": {
                            "title": "Folder path",
                            "description": "Enter the path to your Azure Data Lake Storage folder",
                            "type": "string"
                        },
                        "fileType": {...}, // not applicable to dataset destinations
                        "datasetFileType": {
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "csvOptions":{...}, // not applicable to dataset destinations
                        "compression": {
                            "title": "Compression format",
                            "description": "Select the desired file compression format.",
                            "type": "string",
                            "enum": [
                                "NONE",
                                "GZIP"
                            ]
                        }
                    },
                    "required": [
                        "path",
                        "datasetFileType",
                        "compression",
                        "fileType"
                    ]
                }
//...
```

+++

>[!TAB 資料登陸區域(DLZ)]

+++[!DNL Data Landing Zone(DLZ)] - [!DNL Connection spec]顯示目標連線引數

請注意下方[!DNL connection spec]範例中有內嵌註解之醒目提示的行，這些註解提供了在連線規格中何處尋找[!DNL target spec]引數的相關額外資訊。 您也可以在下列範例中看到目標引數是&#x200B;*不*&#x200B;適用於資料集匯出目的地。

```json {line-numbers="true" start-line="1" highlight="9,21,36"}
"items": [
    {
        "id": "10440537-2a7b-4583-ac39-ed38d4b848e8",
        "name": "Data Landing Zone",
        "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
        "version": "1.0",
        "authSpec": [],
        "encryptionSpecs": [],
        "targetSpec": { // describes the target connection parameters
            "name": "User based target",
            "type": "UserNamespace",
            "spec": {
                "$schema": "http://json-schema.org/draft-07/schema#",
                "type": "object",
                "properties": {
                    "path": {
                        "title": "Folder path",
                        "description": "Enter the path to your Azure Data Lake Storage folder",
                        "type": "string"
                    },
                    "fileType": {...}, // not applicable to dataset destinations
                    "datasetFileType": {
                        "conditional": {
                            "field": "flowSpec.attributes._workflow",
                            "operator": "CONTAINS",
                            "value": "DATASETS"
                        },
                        "title": "File Type",
                        "description": "Select file format",
                        "type": "string",
                        "enum": [
                            "JSON",
                            "PARQUET"
                        ]
                    },
                    "csvOptions": {...}, // not applicable to dataset destinations
                    "compression": {
                        "title": "Compression format",
                        "description": "Select the desired file compression format.",
                        "type": "string",
                        "enum": [
                            "NONE",
                            "GZIP"
                        ]
                    }
                },
                "required": [
                    "path",
                    "datasetFileType",
                    "compression",
                    "fileType"
                ]
            }
//...
```

+++

>[!TAB Google雲端儲存空間]

+++[!DNL Google Cloud Storage] - [!DNL Connection spec]顯示目標連線引數

請注意下方[!DNL connection spec]範例中有內嵌註解之醒目提示的行，這些註解提供了在連線規格中何處尋找[!DNL target spec]引數的相關額外資訊。 您也可以在下列範例中看到目標引數是&#x200B;*不*&#x200B;適用於資料集匯出目的地。

```json {line-numbers="true" start-line="1" highlight="10,29,44"}
{
    "items": [
        {
            "id": "c5d93acb-ea8b-4b14-8f53-02138444ae99",
            "name": "Google Cloud Storage",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [...],
            "encryptionSpecs": [...],
            "targetSpec": { // describes the target connection parameters
                "name": "User based target",
                "type": "UserNamespace",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "bucketName": {
                            "title": "Bucket name",
                            "description": "Bucket name",
                            "type": "string",
                            "pattern": "(?!^goog.*$)(?!^.*g(o|0)(o|0)gle.*$)(((?=^.{3,63}$)(^([a-z0-9]|[a-z0-9][a-z0-9\\-_]*)[a-z0-9]$))|((?=^.{3,222}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]{1,63}|[a-z0-9][a-z0-9\\-_]{1,61}[a-z0-9])\\.)*([a-z0-9]{1,63}|[a-z0-9][a-z0-9\\-_]{1,61}[a-z0-9])$)))"
                        },
                        "path": {
                            "title": "Folder path",
                            "description": "Output path for copying files",
                            "type": "string",
                            "pattern": "^[0-9a-zA-Z\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\/?)+$"
                        },
                        "fileType": {...}, // not applicable to dataset destinations
                        "datasetFileType": {
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "csvOptions": {...}, // not applicable to dataset destinations
                        "compression": {
                            "title": "Compression format",
                            "description": "Select the desired file compression format.",
                            "type": "string",
                            "enum": [
                                "NONE",
                                "GZIP"
                            ]
                        }
                    },
                    "required": [
                        "bucketName",
                        "path",
                        "datasetFileType",
                        "compression",
                        "fileType"
                    ]
                }
//...
```

+++

>[!TAB SFTP]

+++SFTP - [!DNL Connection spec]顯示目標連線引數

請注意下方[!DNL connection spec]範例中有內嵌註解之醒目提示的行，這些註解提供了在連線規格中何處尋找[!DNL target spec]引數的相關額外資訊。 您也可以在下列範例中看到目標引數是&#x200B;*不*&#x200B;適用於資料集匯出目的地。

```json {line-numbers="true" start-line="1" highlight="10,22,37"}
{
    "items": [
        {
            "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
            "name": "SFTP",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [...],
            "encryptionSpecs": [...],
            "targetSpec": { // describes the target connection parameters
                "name": "User based target",
                "type": "UserNamespace",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "remotePath": {
                            "title": "Folder path",
                            "description": "Enter your folder path",
                            "type": "string"
                        },
                        "fileType": {...}, // not applicable to dataset destinations
                        "datasetFileType": {
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "csvOptions": {...}, // not applicable to dataset destinations
                        "compression": {
                            "title": "Compression format",
                            "description": "Select the desired file compression format.",
                            "type": "string",
                            "enum": [
                                "GZIP",
                                "NONE"
                            ]
                        }
                    },
                    "required": [
                        "remotePath",
                        "datasetFileType",
                        "compression",
                        "fileType"
                    ]
                },
//...
```

+++

>[!ENDTABS]


透過使用上述規格，您可以建構專屬於您所需雲端儲存空間目的地的目標連線要求，如下方標籤所示。

>[!BEGINTABS]

>[!TAB Amazon S3]

**要求**

+++[!DNL Amazon S3] - Target連線要求

>[!TIP]
>
>如需有關如何取得所需目標引數的資訊，請參閱[!DNL Amazon S3]目的地檔案頁面的[填寫目的地詳細資料](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details)區段。
>如需`datasetFileType`的其他支援值，請參閱API參考檔案。

請注意請求範例中反白顯示內嵌註解的行，這些註解會提供額外資訊。 將請求複製貼上您選擇的終端機時，移除請求中的內嵌註解。

```shell {line-numbers="true" start-line="1" highlight="19"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Amazon S3 Target Connection",
    "baseConnectionId": "<FROM_STEP_CREATE_TARGET_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "bucketName": "your-bucket-name",
        "path": "folder/subfolder",
        "compression": "NONE",
        "datasetFileType": "JSON"
    },
    "connectionSpec": {
        "id": "4fce964d-3f37-408f-9778-e597338a21ee", // Amazon S3 connection spec id
        "version": "1.0"
    }
}'
```

+++

**回應**

+++目標連線 — 回應

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Azure Blob儲存體]

**要求**

+++[!DNL Azure Blob Storage] - Target連線要求

>[!TIP]
>
>如需有關如何取得所需目標引數的資訊，請參閱[!DNL Azure Blob Storage]目的地檔案頁面的[填寫目的地詳細資料](/help/destinations/catalog/cloud-storage/azure-blob.md#destination-details)區段。
>如需`datasetFileType`的其他支援值，請參閱API參考檔案。


請注意請求範例中反白顯示內嵌註解的行，這些註解會提供額外資訊。 將請求複製貼上您選擇的終端機時，移除請求中的內嵌註解。

```shell {line-numbers="true" start-line="1" highlight="19"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Azure Blob Storage Target Connection",
    "baseConnectionId": "<FROM_STEP_CREATE_TARGET_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "container": "your-container-name",
        "path": "folder/subfolder",
        "compression": "NONE",
        "datasetFileType": "JSON"
    },
    "connectionSpec": {
        "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2", // Azure Blob Storage connection spec id
        "version": "1.0"
    }
}'
```

+++

**回應**

+++目標連線 — 回應

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Azure Data Lake Gen 2(ADLS Gen2)]

**要求**

+++[!DNL Azure Blob Storage] - Target連線要求

>[!TIP]
>
>有關如何取得必要目標引數的資訊，請參閱Azure [!DNL Data Lake Gen 2(ADLS Gen2)]目的地檔案頁面的[填寫目的地詳細資料](/help/destinations/catalog/cloud-storage/adls-gen2.md#destination-details)區段。
>如需`datasetFileType`的其他支援值，請參閱API參考檔案。

請注意請求範例中反白顯示內嵌註解的行，這些註解會提供額外資訊。 將請求複製貼上您選擇的終端機時，移除請求中的內嵌註解。

```shell {line-numbers="true" start-line="1" highlight="18"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Azure Data Lake Gen 2(ADLS Gen2) Target Connection",
    "baseConnectionId": "<FROM_STEP_CREATE_TARGET_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "path": "folder/subfolder",
        "compression": "NONE",
        "datasetFileType": "JSON"
    },
    "connectionSpec": {
        "id": "be2c3209-53bc-47e7-ab25-145db8b873e1", // Azure Data Lake Gen 2(ADLS Gen2) connection spec id
        "version": "1.0"
    }
}'
```

+++

**回應**

+++目標連線 — 回應

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB 資料登陸區域(DLZ)]

**要求**

+++[!DNL Data Landing Zone] - Target連線要求

>[!TIP]
>
>如需有關如何取得所需目標引數的資訊，請參閱[!DNL Data Landing Zone]目的地檔案頁面的[填寫目的地詳細資料](/help/destinations/catalog/cloud-storage/data-landing-zone.md#destination-details)區段。
>如需`datasetFileType`的其他支援值，請參閱API參考檔案。

請注意請求範例中反白顯示內嵌註解的行，這些註解會提供額外資訊。 將請求複製貼上您選擇的終端機時，移除請求中的內嵌註解。

```shell {line-numbers="true" start-line="1" highlight="18"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Data Landing Zone Target Connection",
    "baseConnectionId": "<FROM_STEP_CREATE_TARGET_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "path": "folder/subfolder",
        "compression": "NONE",
        "datasetFileType": "JSON"
    },
    "connectionSpec": {
        "id": "10440537-2a7b-4583-ac39-ed38d4b848e8", // Data Landing Zone connection spec id
        "version": "1.0"
    }
}'
```

+++

**回應**

+++目標連線 — 回應

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Google雲端儲存空間]

**要求**

+++[!DNL Google Cloud Storage] - Target連線要求

>[!TIP]
>
>如需有關如何取得所需目標引數的資訊，請參閱[!DNL Google Cloud Storage]目的地檔案頁面的[填寫目的地詳細資料](/help/destinations/catalog/cloud-storage/google-cloud-storage.md#destination-details)區段。
>如需`datasetFileType`的其他支援值，請參閱API參考檔案。


請注意請求範例中反白顯示內嵌註解的行，這些註解會提供額外資訊。 將請求複製貼上您選擇的終端機時，移除請求中的內嵌註解。

```shell {line-numbers="true" start-line="1" highlight="19"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Google Cloud Storage Target Connection",
    "baseConnectionId": "<FROM_STEP_CREATE_TARGET_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "bucketName": "your-bucket-name",
        "path": "folder/subfolder",
        "compression": "NONE",
        "datasetFileType": "JSON"
    },
    "connectionSpec": {
        "id": "c5d93acb-ea8b-4b14-8f53-02138444ae99", // Google Cloud Storage connection spec id
        "version": "1.0"
    }
}'
```

+++

**回應**

+++目標連線 — 回應

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB SFTP]

**要求**

+++SFTP - Target連線要求

>[!TIP]
>
>如需有關如何取得所需目標引數的資訊，請參閱SFTP目的地檔案頁面的[填寫目的地詳細資料](/help/destinations/catalog/cloud-storage/google-cloud-storage.md#destination-details)區段。
>如需`datasetFileType`的其他支援值，請參閱API參考檔案。

請注意請求範例中反白顯示內嵌註解的行，這些註解會提供額外資訊。 將請求複製貼上您選擇的終端機時，移除請求中的內嵌註解。

```shell {line-numbers="true" start-line="1" highlight="18"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "SFTP Target Connection",
    "baseConnectionId": "<FROM_STEP_CREATE_TARGET_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "remotePath": "folder/subfolder",
        "compression": "NONE",
        "datasetFileType": "JSON"
    },
    "connectionSpec": {
        "id": "36965a81-b1c6-401b-99f8-22508f1e6a26", // SFTP connection spec id
        "version": "1.0"
    }
}'
```

+++

**回應**

+++Target連線 — 回應

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!ENDTABS]

記下回應中的Target連線ID。 建立資料流以匯出資料集時，下個步驟將需要此ID。

## 建立資料流 {#create-dataflow}

![顯示匯出資料集工作流程步驟5的圖表](../assets/api/export-datasets/export-datasets-api-workflow-set-up-dataflow.png)

目的地設定的最後一步是設定資料流。 資料流會將先前建立的實體連結在一起，並提供設定資料集匯出排程的選項。 若要建立資料流，請根據您所需的雲端儲存空間目的地，使用下列裝載，並取代先前步驟中的實體ID。

>[!BEGINTABS]

>[!TAB Amazon S3]

**要求**

+++建立資料集資料流到[!DNL Amazon S3]目的地 — 請求

請注意請求範例中反白顯示內嵌註解的行，這些註解會提供額外資訊。 將請求複製貼上您選擇的終端機時，移除請求中的內嵌註解。

```shell {line-numbers="true" start-line="1" highlight="12,22-25"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/flows' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Activate datasets to an Amazon S3 cloud storage destination",
    "description": "This operation creates a dataflow to export datasets to an Amazon S3 cloud storage destination",
    "flowSpec": {
        "id": "269ba276-16fc-47db-92b0-c1049a3c131f", // Amazon S3 flow spec ID
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "<FROM_STEP_CREATE_SOURCE_CONNECTION>"
    ],
    "targetConnectionIds": [
        "<FROM_STEP_CREATE_TARGET_CONNECTION>"
    ],
    "transformations": [],
    "scheduleParams": { // specify the scheduling info
        "exportMode": DAILY_FULL_EXPORT or FIRST_FULL_THEN_INCREMENTAL
        "interval": 3, // also supports 6, 9, 12 hour increments
        "timeUnit": "hour", // also supports "day" for daily increments. 
        "interval": 1, // when you select "timeUnit": "day"
        "startTime": 1675901210, // UNIX timestamp start time (in seconds)
        "endTime": 1975901210, // UNIX timestamp end time (in seconds)
        "foldernameTemplate": "%DESTINATION%_%DATASET_ID%_%DATETIME(YYYYMMdd_HHmmss)%"
    }
}'
```

下表提供`scheduleParams`區段中所有引數的說明，可讓您自訂資料集匯出的匯出時間、頻率、位置等。

| 參數 | 說明 |
|---------|----------|
| `exportMode` | 選取`"DAILY_FULL_EXPORT"`或`"FIRST_FULL_THEN_INCREMENTAL"`。 如需有關這兩個選項的詳細資訊，請參閱批次目的地啟動教學課程中的[匯出完整檔案](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files)和[匯出增量檔案](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files)。 三個可用的匯出選項為： <br> **完整檔案 — 一次**： `"DAILY_FULL_EXPORT"`只能搭配`timeUnit`：`day`和`interval`：`0`使用，以一次完整匯出資料集。 不支援資料集的每日完整匯出。 如果您需要每日匯出，請使用增量匯出選項。<br> **每日增量匯出**：針對每日增量匯出選取`"FIRST_FULL_THEN_INCREMENTAL"`、`timeUnit`：`day`和`interval`：`1`。<br> **每小時增量匯出**：針對每小時增量匯出選取`"FIRST_FULL_THEN_INCREMENTAL"`、`timeUnit`：`hour`和`interval`：`3`、`6`、`9`或`12`。 |
| `timeUnit` | 根據您想要匯出資料集檔案的頻率，選取`day`或`hour`。 |
| `interval` | 選取`timeUnit`為天時的`1`，以及時間單位為`hour`時的`3`，`6`，`9`，`12`。 |
| `startTime` | 開始匯出資料集的日期和時間（以UNIX秒為單位）。 |
| `endTime` | 資料集匯出應該結束的日期和時間（以UNIX秒為單位）。 |
| `foldernameTemplate` | 在儲存匯出檔案的儲存位置中，指定預期的資料夾名稱結構。 <ul><li><code>資料集ID</code> = <span>資料集的唯一識別碼。</span></li><li><code>目的地</code> = <span>目的地的名稱。</span></li><li><code>日期時間</code> = <span>格式為yyyyMMdd_HHmmss.</span>的日期和時間</li><li><code>匯出時間</code> = <span>格式化為`exportTime=YYYYMMDDHHMM`的資料匯出排程時間。</span></li><li><code>DESTINATION_INSTANCE_NAME</code> = <span>目的地的特定執行個體名稱。</span></li><li><code>DESTINATION_INSTANCE_ID</code> = <span>目的地執行個體的唯一識別碼。</span></li><li><code>沙箱名稱</code> = <span>沙箱環境的名稱。</span></li><li><code>組織名稱</code> = <span>組織的名稱。</span></li></ul> |

{style="table-layout:auto"}
+++

**回應**

+++建立資料流 — 回應

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Azure Blob儲存體]

**要求**

+++建立資料集資料流到[!DNL Azure Blob Storage]目的地 — 請求

請注意請求範例中反白顯示內嵌註解的行，這些註解會提供額外資訊。 將請求複製貼上您選擇的終端機時，移除請求中的內嵌註解。

```shell {line-numbers="true" start-line="1" highlight="12,22-25"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/flows' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Activate datasets to an Azure Blob Storage cloud storage destination",
    "description": "This operation creates a dataflow to export datasets to an Azure Blob Storage cloud storage destination",
    "flowSpec": {
        "id": "95bd8965-fc8a-4119-b9c3-944c2c2df6d2", // Azure Blob Storage flow spec ID
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "<FROM_STEP_CREATE_SOURCE_CONNECTION>"
    ],
    "targetConnectionIds": [
        "<FROM_STEP_CREATE_TARGET_CONNECTION>"
    ],
    "transformations": [],
    "scheduleParams": { // specify the scheduling info
        "exportMode": DAILY_FULL_EXPORT or FIRST_FULL_THEN_INCREMENTAL
        "interval": 3, // also supports 6, 9, 12 hour increments
        "timeUnit": "hour", // also supports "day" for daily increments. 
        "interval": 1, // when you select "timeUnit": "day"
        "startTime": 1675901210, // UNIX timestamp start time (in seconds)
        "endTime": 1975901210, // UNIX timestamp end time (in seconds)
        "foldernameTemplate": "%DESTINATION%_%DATASET_ID%_%DATETIME(YYYYMMdd_HHmmss)%"
    }
}'
```

下表提供`scheduleParams`區段中所有引數的說明，可讓您自訂資料集匯出的匯出時間、頻率、位置等。

| 參數 | 說明 |
|---------|----------|
| `exportMode` | 選取`"DAILY_FULL_EXPORT"`或`"FIRST_FULL_THEN_INCREMENTAL"`。 如需有關這兩個選項的詳細資訊，請參閱批次目的地啟動教學課程中的[匯出完整檔案](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files)和[匯出增量檔案](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files)。 三個可用的匯出選項為： <br> **完整檔案 — 一次**： `"DAILY_FULL_EXPORT"`只能搭配`timeUnit`：`day`和`interval`：`0`使用，以一次完整匯出資料集。 不支援資料集的每日完整匯出。 如果您需要每日匯出，請使用增量匯出選項。<br> **每日增量匯出**：針對每日增量匯出選取`"FIRST_FULL_THEN_INCREMENTAL"`、`timeUnit`：`day`和`interval`：`1`。<br> **每小時增量匯出**：針對每小時增量匯出選取`"FIRST_FULL_THEN_INCREMENTAL"`、`timeUnit`：`hour`和`interval`：`3`、`6`、`9`或`12`。 |
| `timeUnit` | 根據您想要匯出資料集檔案的頻率，選取`day`或`hour`。 |
| `interval` | 選取`timeUnit`為天時的`1`，以及時間單位為`hour`時的`3`，`6`，`9`，`12`。 |
| `startTime` | 開始匯出資料集的日期和時間（以UNIX秒為單位）。 |
| `endTime` | 資料集匯出應該結束的日期和時間（以UNIX秒為單位）。 |
| `foldernameTemplate` | 在儲存匯出檔案的儲存位置中，指定預期的資料夾名稱結構。 <ul><li><code>資料集ID</code> = <span>資料集的唯一識別碼。</span></li><li><code>目的地</code> = <span>目的地的名稱。</span></li><li><code>日期時間</code> = <span>格式為yyyyMMdd_HHmmss.</span>的日期和時間</li><li><code>匯出時間</code> = <span>格式化為`exportTime=YYYYMMDDHHMM`的資料匯出排程時間。</span></li><li><code>DESTINATION_INSTANCE_NAME</code> = <span>目的地的特定執行個體名稱。</span></li><li><code>DESTINATION_INSTANCE_ID</code> = <span>目的地執行個體的唯一識別碼。</span></li><li><code>沙箱名稱</code> = <span>沙箱環境的名稱。</span></li><li><code>組織名稱</code> = <span>組織的名稱。</span></li></ul> |

{style="table-layout:auto"}

+++

**回應**

+++建立資料流 — 回應

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Azure Data Lake Gen 2(ADLS Gen2)]

**要求**

+++建立資料集資料流到[!DNL Azure Data Lake Gen 2(ADLS Gen2)]目的地 — 請求

請注意請求範例中反白顯示內嵌註解的行，這些註解會提供額外資訊。 將請求複製貼上您選擇的終端機時，移除請求中的內嵌註解。

```shell {line-numbers="true" start-line="1" highlight="12,22-25"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/flows' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Activate datasets to an Azure Data Lake Gen 2(ADLS Gen2) cloud storage destination",
    "description": "This operation creates a dataflow to export datasets to an Azure Data Lake Gen 2(ADLS Gen2) cloud storage destination",
    "flowSpec": {
        "id": "17be2013-2549-41ce-96e7-a70363bec293", // Azure Data Lake Gen 2(ADLS Gen2) flow spec ID
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "<FROM_STEP_CREATE_SOURCE_CONNECTION>"
    ],
    "targetConnectionIds": [
        "<FROM_STEP_CREATE_TARGET_CONNECTION>"
    ],
    "transformations": [],
    "scheduleParams": { // specify the scheduling info
        "exportMode": DAILY_FULL_EXPORT or FIRST_FULL_THEN_INCREMENTAL
        "interval": 3, // also supports 6, 9, 12 hour increments
        "timeUnit": "hour", // also supports "day" for daily increments. 
        "interval": 1, // when you select "timeUnit": "day"
        "startTime": 1675901210, // UNIX timestamp start time (in seconds)
        "endTime": 1975901210, // UNIX timestamp end time (in seconds)
        "foldernameTemplate": "%DESTINATION%_%DATASET_ID%_%DATETIME(YYYYMMdd_HHmmss)%"
    }
}'
```

下表提供`scheduleParams`區段中所有引數的說明，可讓您自訂資料集匯出的匯出時間、頻率、位置等。

| 參數 | 說明 |
|---------|----------|
| `exportMode` | 選取`"DAILY_FULL_EXPORT"`或`"FIRST_FULL_THEN_INCREMENTAL"`。 如需有關這兩個選項的詳細資訊，請參閱批次目的地啟動教學課程中的[匯出完整檔案](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files)和[匯出增量檔案](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files)。 三個可用的匯出選項為： <br> **完整檔案 — 一次**： `"DAILY_FULL_EXPORT"`只能搭配`timeUnit`：`day`和`interval`：`0`使用，以一次完整匯出資料集。 不支援資料集的每日完整匯出。 如果您需要每日匯出，請使用增量匯出選項。<br> **每日增量匯出**：針對每日增量匯出選取`"FIRST_FULL_THEN_INCREMENTAL"`、`timeUnit`：`day`和`interval`：`1`。<br> **每小時增量匯出**：針對每小時增量匯出選取`"FIRST_FULL_THEN_INCREMENTAL"`、`timeUnit`：`hour`和`interval`：`3`、`6`、`9`或`12`。 |
| `timeUnit` | 根據您想要匯出資料集檔案的頻率，選取`day`或`hour`。 |
| `interval` | 選取`timeUnit`為天時的`1`，以及時間單位為`hour`時的`3`，`6`，`9`，`12`。 |
| `startTime` | 開始匯出資料集的日期和時間（以UNIX秒為單位）。 |
| `endTime` | 資料集匯出應該結束的日期和時間（以UNIX秒為單位）。 |
| `foldernameTemplate` | 在儲存匯出檔案的儲存位置中，指定預期的資料夾名稱結構。 <ul><li><code>資料集ID</code> = <span>資料集的唯一識別碼。</span></li><li><code>目的地</code> = <span>目的地的名稱。</span></li><li><code>日期時間</code> = <span>格式為yyyyMMdd_HHmmss.</span>的日期和時間</li><li><code>匯出時間</code> = <span>格式化為`exportTime=YYYYMMDDHHMM`的資料匯出排程時間。</span></li><li><code>DESTINATION_INSTANCE_NAME</code> = <span>目的地的特定執行個體名稱。</span></li><li><code>DESTINATION_INSTANCE_ID</code> = <span>目的地執行個體的唯一識別碼。</span></li><li><code>沙箱名稱</code> = <span>沙箱環境的名稱。</span></li><li><code>組織名稱</code> = <span>組織的名稱。</span></li></ul> |

{style="table-layout:auto"}

+++

**回應**

+++建立資料流 — 回應

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB 資料登陸區域(DLZ)]

**要求**

+++建立資料集資料流到[!DNL Data Landing Zone]目的地 — 請求

請注意請求範例中反白顯示內嵌註解的行，這些註解會提供額外資訊。 將請求複製貼上您選擇的終端機時，移除請求中的內嵌註解。

```shell {line-numbers="true" start-line="1" highlight="12,22-25"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/flows' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Activate datasets to a Data Landing Zone cloud storage destination",
    "description": "This operation creates a dataflow to export datasets to a Data Landing Zone cloud storage destination",
    "flowSpec": {
        "id": "cd2fc47e-e838-4f38-a581-8fff2f99b63a", // Data Landing Zone flow spec ID
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "<FROM_STEP_CREATE_SOURCE_CONNECTION>"
    ],
    "targetConnectionIds": [
        "<FROM_STEP_CREATE_TARGET_CONNECTION>"
    ],
    "transformations": [],
    "scheduleParams": { // specify the scheduling info
        "exportMode": DAILY_FULL_EXPORT or FIRST_FULL_THEN_INCREMENTAL
        "interval": 3, // also supports 6, 9, 12 hour increments
        "timeUnit": "hour", // also supports "day" for daily increments. 
        "interval": 1, // when you select "timeUnit": "day"
        "startTime": 1675901210, // UNIX timestamp start time (in seconds)
        "endTime": 1975901210, // UNIX timestamp end time (in seconds)
        "foldernameTemplate": "%DESTINATION%_%DATASET_ID%_%DATETIME(YYYYMMdd_HHmmss)%"
    }
}'
```

下表提供`scheduleParams`區段中所有引數的說明，可讓您自訂資料集匯出的匯出時間、頻率、位置等。

| 參數 | 說明 |
|---------|----------|
| `exportMode` | 選取`"DAILY_FULL_EXPORT"`或`"FIRST_FULL_THEN_INCREMENTAL"`。 如需有關這兩個選項的詳細資訊，請參閱批次目的地啟動教學課程中的[匯出完整檔案](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files)和[匯出增量檔案](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files)。 三個可用的匯出選項為： <br> **完整檔案 — 一次**： `"DAILY_FULL_EXPORT"`只能搭配`timeUnit`：`day`和`interval`：`0`使用，以一次完整匯出資料集。 不支援資料集的每日完整匯出。 如果您需要每日匯出，請使用增量匯出選項。<br> **每日增量匯出**：針對每日增量匯出選取`"FIRST_FULL_THEN_INCREMENTAL"`、`timeUnit`：`day`和`interval`：`1`。<br> **每小時增量匯出**：針對每小時增量匯出選取`"FIRST_FULL_THEN_INCREMENTAL"`、`timeUnit`：`hour`和`interval`：`3`、`6`、`9`或`12`。 |
| `timeUnit` | 根據您想要匯出資料集檔案的頻率，選取`day`或`hour`。 |
| `interval` | 選取`timeUnit`為天時的`1`，以及時間單位為`hour`時的`3`，`6`，`9`，`12`。 |
| `startTime` | 開始匯出資料集的日期和時間（以UNIX秒為單位）。 |
| `endTime` | 資料集匯出應該結束的日期和時間（以UNIX秒為單位）。 |
| `foldernameTemplate` | 在儲存匯出檔案的儲存位置中，指定預期的資料夾名稱結構。 <ul><li><code>資料集ID</code> = <span>資料集的唯一識別碼。</span></li><li><code>目的地</code> = <span>目的地的名稱。</span></li><li><code>日期時間</code> = <span>格式為yyyyMMdd_HHmmss.</span>的日期和時間</li><li><code>匯出時間</code> = <span>格式化為`exportTime=YYYYMMDDHHMM`的資料匯出排程時間。</span></li><li><code>DESTINATION_INSTANCE_NAME</code> = <span>目的地的特定執行個體名稱。</span></li><li><code>DESTINATION_INSTANCE_ID</code> = <span>目的地執行個體的唯一識別碼。</span></li><li><code>沙箱名稱</code> = <span>沙箱環境的名稱。</span></li><li><code>組織名稱</code> = <span>組織的名稱。</span></li></ul> |

{style="table-layout:auto"}
+++

**回應**

+++建立資料流 — 回應

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Google雲端儲存空間]

**要求**

+++建立資料集資料流到[!DNL Google Cloud Storage]目的地 — 請求

請注意請求範例中反白顯示內嵌註解的行，這些註解會提供額外資訊。 將請求複製貼上您選擇的終端機時，移除請求中的內嵌註解。

```shell {line-numbers="true" start-line="1" highlight="12,22-25"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/flows' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Activate datasets to a Google Cloud Storage cloud storage destination",
    "description": "This operation creates a dataflow to export datasets to a Google Cloud Storage destination",
    "flowSpec": {
        "id": "585c15c4-6cbf-4126-8f87-e26bff78b657", // Google Cloud Storage flow spec ID
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "<FROM_STEP_CREATE_SOURCE_CONNECTION>"
    ],
    "targetConnectionIds": [
        "<FROM_STEP_CREATE_TARGET_CONNECTION>"
    ],
    "transformations": [],
    "scheduleParams": { // specify the scheduling info
        "exportMode": DAILY_FULL_EXPORT or FIRST_FULL_THEN_INCREMENTAL
        "interval": 3, // also supports 6, 9, 12 hour increments
        "timeUnit": "hour", // also supports "day" for daily increments. 
        "interval": 1, // when you select "timeUnit": "day"
        "startTime": 1675901210, // UNIX timestamp start time (in seconds)
        "endTime": 1975901210, // UNIX timestamp end time (in seconds)
        "foldernameTemplate": "%DESTINATION%_%DATASET_ID%_%DATETIME(YYYYMMdd_HHmmss)%"
    }
}'
```

下表提供`scheduleParams`區段中所有引數的說明，可讓您自訂資料集匯出的匯出時間、頻率、位置等。

| 參數 | 說明 |
|---------|----------|
| `exportMode` | 選取`"DAILY_FULL_EXPORT"`或`"FIRST_FULL_THEN_INCREMENTAL"`。 如需有關這兩個選項的詳細資訊，請參閱批次目的地啟動教學課程中的[匯出完整檔案](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files)和[匯出增量檔案](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files)。 三個可用的匯出選項為： <br> **完整檔案 — 一次**： `"DAILY_FULL_EXPORT"`只能搭配`timeUnit`：`day`和`interval`：`0`使用，以一次完整匯出資料集。 不支援資料集的每日完整匯出。 如果您需要每日匯出，請使用增量匯出選項。<br> **每日增量匯出**：針對每日增量匯出選取`"FIRST_FULL_THEN_INCREMENTAL"`、`timeUnit`：`day`和`interval`：`1`。<br> **每小時增量匯出**：針對每小時增量匯出選取`"FIRST_FULL_THEN_INCREMENTAL"`、`timeUnit`：`hour`和`interval`：`3`、`6`、`9`或`12`。 |
| `timeUnit` | 根據您想要匯出資料集檔案的頻率，選取`day`或`hour`。 |
| `interval` | 選取`timeUnit`為天時的`1`，以及時間單位為`hour`時的`3`，`6`，`9`，`12`。 |
| `startTime` | 開始匯出資料集的日期和時間（以UNIX秒為單位）。 |
| `endTime` | 資料集匯出應該結束的日期和時間（以UNIX秒為單位）。 |
| `foldernameTemplate` | 在儲存匯出檔案的儲存位置中，指定預期的資料夾名稱結構。 <ul><li><code>資料集ID</code> = <span>資料集的唯一識別碼。</span></li><li><code>目的地</code> = <span>目的地的名稱。</span></li><li><code>日期時間</code> = <span>格式為yyyyMMdd_HHmmss.</span>的日期和時間</li><li><code>匯出時間</code> = <span>格式化為`exportTime=YYYYMMDDHHMM`的資料匯出排程時間。</span></li><li><code>DESTINATION_INSTANCE_NAME</code> = <span>目的地的特定執行個體名稱。</span></li><li><code>DESTINATION_INSTANCE_ID</code> = <span>目的地執行個體的唯一識別碼。</span></li><li><code>沙箱名稱</code> = <span>沙箱環境的名稱。</span></li><li><code>組織名稱</code> = <span>組織的名稱。</span></li></ul> |

{style="table-layout:auto"}

+++

**回應**

+++建立資料流 — 回應

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB SFTP]

**要求**

+++建立資料集資料流至SFTP目的地 — 請求

請注意請求範例中反白顯示內嵌註解的行，這些註解會提供額外資訊。 將請求複製貼上您選擇的終端機時，移除請求中的內嵌註解。

```shell {line-numbers="true" start-line="1" highlight="12,22-25"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/flows' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Activate datasets to an SFTP cloud storage destination",
    "description": "This operation creates a dataflow to export datasets to an SFTP cloud storage destination",
    "flowSpec": {
        "id": "354d6aad-4754-46e4-a576-1b384561c440", // SFTP flow spec ID
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "<FROM_STEP_CREATE_SOURCE_CONNECTION>"
    ],
    "targetConnectionIds": [
        "<FROM_STEP_CREATE_TARGET_CONNECTION>"
    ],
    "transformations": [],
    "scheduleParams": { // specify the scheduling info
        "exportMode": DAILY_FULL_EXPORT or FIRST_FULL_THEN_INCREMENTAL
        "interval": 3, // also supports 6, 9, 12 hour increments
        "timeUnit": "hour", // also supports "day" for daily increments. 
        "interval": 1, // when you select "timeUnit": "day"
        "startTime": 1675901210, // UNIX timestamp start time (in seconds)
        "endTime": 1975901210, // UNIX timestamp end time (in seconds)
        "foldernameTemplate": "%DESTINATION%_%DATASET_ID%_%DATETIME(YYYYMMdd_HHmmss)%"
    }
}'
```

下表提供`scheduleParams`區段中所有引數的說明，可讓您自訂資料集匯出的匯出時間、頻率、位置等。

| 參數 | 說明 |
|---------|----------|
| `exportMode` | 選取`"DAILY_FULL_EXPORT"`或`"FIRST_FULL_THEN_INCREMENTAL"`。 如需有關這兩個選項的詳細資訊，請參閱批次目的地啟動教學課程中的[匯出完整檔案](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files)和[匯出增量檔案](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files)。 三個可用的匯出選項為： <br> **完整檔案 — 一次**： `"DAILY_FULL_EXPORT"`只能搭配`timeUnit`：`day`和`interval`：`0`使用，以一次完整匯出資料集。 不支援資料集的每日完整匯出。 如果您需要每日匯出，請使用增量匯出選項。<br> **每日增量匯出**：針對每日增量匯出選取`"FIRST_FULL_THEN_INCREMENTAL"`、`timeUnit`：`day`和`interval`：`1`。<br> **每小時增量匯出**：針對每小時增量匯出選取`"FIRST_FULL_THEN_INCREMENTAL"`、`timeUnit`：`hour`和`interval`：`3`、`6`、`9`或`12`。 |
| `timeUnit` | 根據您想要匯出資料集檔案的頻率，選取`day`或`hour`。 |
| `interval` | 選取`timeUnit`為天時的`1`，以及時間單位為`hour`時的`3`，`6`，`9`，`12`。 |
| `startTime` | 開始匯出資料集的日期和時間（以UNIX秒為單位）。 |
| `endTime` | 資料集匯出應該結束的日期和時間（以UNIX秒為單位）。 |
| `foldernameTemplate` | 在儲存匯出檔案的儲存位置中，指定預期的資料夾名稱結構。 <ul><li><code>資料集ID</code> = <span>資料集的唯一識別碼。</span></li><li><code>目的地</code> = <span>目的地的名稱。</span></li><li><code>日期時間</code> = <span>格式為yyyyMMdd_HHmmss.</span>的日期和時間</li><li><code>匯出時間</code> = <span>格式化為`exportTime=YYYYMMDDHHMM`的資料匯出排程時間。</span></li><li><code>DESTINATION_INSTANCE_NAME</code> = <span>目的地的特定執行個體名稱。</span></li><li><code>DESTINATION_INSTANCE_ID</code> = <span>目的地執行個體的唯一識別碼。</span></li><li><code>沙箱名稱</code> = <span>沙箱環境的名稱。</span></li><li><code>組織名稱</code> = <span>組織的名稱。</span></li></ul> |

{style="table-layout:auto"}

+++

**回應**

+++建立資料流 — 回應

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!ENDTABS]

記下回應中的資料流ID。 擷取資料流執行以驗證成功的日期集匯出時，下個步驟將需要此ID。

## 取得資料流執行 {#get-dataflow-runs}

![顯示匯出資料集工作流程步驟6的圖表](../assets/api/export-datasets/export-datasets-api-workflow-validate-dataflow.png)

若要檢查資料流的執行，請使用資料流執行API：

>[!BEGINSHADEBOX]

**要求**

+++取得資料流執行 — 要求

在擷取資料流執行的請求中，在建立資料流時，將您在上一步驟中取得的資料流ID新增為查詢引數。

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/runs?property=flowId==eb54b3b3-3949-4f12-89c8-64eafaba858f' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
```

+++

**回應**

+++取得資料流執行 — 回應

```json
{
    "items": [
        {
            "id": "4b7728dd-83c9-4c38-95a4-24ddab545404",
            "createdAt": 1675807718296,
            "updatedAt": 1675807731834,
            "createdBy": "aep_activation_batch@AdobeID",
            "updatedBy": "acp_foundation_connectors@AdobeID",
            "createdClient": "aep_activation_batch",
            "updatedClient": "acp_foundation_connectors",
            "sandboxId": "7dfdcd30-0a09-11ea-8ea6-7bf93ce86c28",
            "sandboxName": "sand-1",
            "imsOrgId": "5555467B5D8013E50A494220@AdobeOrg",
            "flowId": "aae5ec63-b0ac-4808-9a44-abf2ea67bd5a",
            "flowSpec": {
                "id": "615d3489-36d2-4671-9467-4ae1129facd3",
                "version": "1.0"
            },
            "providerRefId": "ba56f98e0c49b572adb249980c39b1c7",
            "etag": "\"08005e9e-0000-0200-0000-63e2cbf30000\"",
            "metrics": {
                "durationSummary": {
                    "startedAtUTC": 1675807719411,
                    "completedAtUTC": 1675807719416
                },
                "sizeSummary": {
                    "inputBytes": 0
                },
                "recordSummary": {
                    "inputRecordCount": 0,
                    "skippedRecordCount": 0,
                    "sourceSummaries": [
                        {
                            "id": "ea2b1205-4692-49de-b448-ebf75b1d188a",
                            "inputRecordCount": 0,
                            "skippedRecordCount": 0,
                            "entitySummaries": [
                                {
//...
```

+++

>[!ENDSHADEBOX]

您可以在API參考檔案中找到有關資料流執行API[&#128279;](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Dataflow-runs/operation/getFlowRuns)傳回的各種引數的資訊。

## 驗證資料集匯出成功 {#verify}

匯出資料集時，Experience Platform會在您提供的儲存位置中建立`.json`或`.parquet`檔案。 預期會根據您在[建立資料流](#create-dataflow)時提供的匯出排程，將新檔案儲存在您的儲存位置。

Experience Platform會在您指定的儲存位置中建立資料夾結構，並存放匯出的資料集檔案。 每次匯出時都會建立一個新資料夾，其模式如下：

`folder-name-you-provided/datasetID/exportTime=YYYYMMDDHHMM`

預設檔案名稱是隨機產生的，並確保匯出的檔案名稱是唯一的。

### 範例資料集檔案 {#sample-files}

這些檔案存在於您的儲存位置即表示匯出成功。 若要瞭解匯出的檔案是如何建構的，您可以下載範例[.parquet檔案](../assets/common/part-00000-tid-253136349007858095-a93bcf2e-d8c5-4dd6-8619-5c662e261097-672704-1-c000.parquet)或[.json檔案](../assets/common/part-00000-tid-4172098795867639101-0b8c5520-9999-4cff-bdf5-1f32c8c47cb9-451986-1-c000.json)。

#### 壓縮的資料集檔案 {#compressed-dataset-files}

在[建立目標連線](#create-target-connection)的步驟中，您可以選取要壓縮的匯出資料集檔案。

請注意兩種檔案型別在壓縮時的檔案格式差異：

* 匯出壓縮的JSON檔案時，匯出的檔案格式為`json.gz`
* 匯出壓縮的parquet檔案時，匯出的檔案格式為`gz.parquet`
* JSON檔案只能以壓縮模式匯出。

## API錯誤處理 {#api-error-handling}

本教學課程中的API端點會遵循一般Experience Platform API錯誤訊息原則。 如需解譯錯誤回應的詳細資訊，請參閱Experience Platform疑難排解指南中的[API狀態碼](/help/landing/troubleshooting.md#api-status-codes)和[請求標頭錯誤](/help/landing/troubleshooting.md#request-header-errors)。

## 已知限制 {#known-limitations}

檢視關於資料集匯出的[已知限制](/help/destinations/ui/export-datasets.md#known-limitations)。

## 常見問題 {#faq}

檢視關於資料集匯出的常見問題[&#128279;](/help/destinations/ui/export-datasets.md#faq)的清單。

## 後續步驟 {#next-steps}

依照本教學課程中的指示，您已成功將Experience Platform連線至其中一個慣用的批次雲端儲存目的地，並設定資料流至個別目的地以匯出資料集。 如需詳細資訊，請參閱下列頁面，例如如何使用流量服務API編輯現有資料流：

* [目的地概觀](../home.md)
* [目的地目錄概觀](../catalog/overview.md)
* [使用流程服務API更新目的地資料流程](../api/update-destination-dataflows.md)