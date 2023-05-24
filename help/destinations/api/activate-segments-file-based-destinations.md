---
solution: Experience Platform
title: 使用流服務API激活段到基於檔案的目標
description: 瞭解如何使用流服務API將具有限定配置檔案的檔案導出到雲儲存目標。
type: Tutorial
exl-id: 62028c7a-3ea9-4004-adb7-5e27bbe904fc
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '4337'
ht-degree: 2%

---

# 使用流服務API激活段到基於檔案的目標

>[!IMPORTANT]
>
>* 此測試版功能可供購買Real-Time CDPPrime和Ultimate產品包的客戶使用。 請聯繫您的Adobe代表以瞭解更多資訊。


使用增強的檔案導出功能（當前在測試版中）在導出檔案失去Experience Platform時訪問增強的自定義功能：

* 其他 [檔案命名選項](/help/destinations/ui/activate-batch-profile-destinations.md#file-names)。
* 通過 [改進映射步長](/help/destinations/ui/activate-batch-profile-destinations.md#mapping)。
* 選擇 [檔案類型](/help/destinations/ui/connect-destination.md#file-formatting-and-compression-options) 的子菜單。
* [能夠自定義導出的CSV資料檔案的格式](/help/destinations/ui/batch-destinations-file-formatting-options.md)。

下面列出的六個新的測試版雲儲存卡支援此功能：

* [[!DNL (Beta) Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md)
* [[!DNL (Beta) Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md)
* [[!DNL (Beta) Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md)
* [[!DNL (Beta) Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog)
* [[!DNL (Beta) Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog)
* [[!DNL (Beta) SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog)

本文說明了使用 [流服務API](https://developer.adobe.com/experience-platform-apis/references/destinations/) 將合格的配置檔案從Adobe Experience Platform導出到上面連結的雲儲存位置之一。

>[!TIP]
>
>您還可以使用Experience Platform用戶介面將配置檔案導出到雲儲存目標。 閱讀 [激活基於檔案的目標教程](/help/destinations/ui/activate-batch-profile-destinations.md) 的子菜單。

## API用戶遷移 {#api-migration}

如果您已使用流服務API將配置檔案導出到AmazonS3、Azure Blob或SFTP雲儲存目標，請閱讀 [API遷移指南](/help/destinations/api/api-migration-guide-cloud-storage-destinations.md) 在Adobe將用戶從舊式目標轉移到新目標時執行必要的遷移步驟。

## 快速入門 {#get-started}

![激活段的步驟，突出顯示用戶所處的當前步驟](/help/destinations/assets/api/file-based-segment-export/segment-export-overview.png)

本指南要求對Adobe Experience Platform的下列組成部分有工作上的理解：

* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。
* [[!DNL Segmentation Service]](../../segmentation/api/overview.md): [!DNL Adobe Experience Platform Segmentation Service] 允許您在 [!DNL Adobe Experience Platform] 從 [!DNL Real-Time Customer Profile] 資料。
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙箱，將單個沙箱 [!DNL Platform] 實例到獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

以下各節提供您需要瞭解的其他資訊，以便將資料激活到平台中基於檔案的目標。

### 必要權限 {#permissions}

要導出配置檔案，您需要 **[!UICONTROL 管理目標]**。 **[!UICONTROL 查看目標]**, **[!UICONTROL 激活目標]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

### 讀取示例API調用 {#reading-sample-api-calls}

本教程提供了示例API調用，以演示如何格式化請求。 這些包括路徑、必需的標頭和正確格式化的請求負載。 還提供了API響應中返回的示例JSON。 有關示例API調用文檔中使用的約定的資訊，請參見上的 [如何讀取示例API調用](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 的 [!DNL Experience Platform] 疑難解答指南。

### 收集所需和可選標頭的值 {#gather-values-headers}

為了呼叫 [!DNL Platform] API，必須首先完成 [Experience Platform驗證教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份驗證教程將提供所有中每個必需標頭的值 [!DNL Experience Platform] API調用，如下所示：

* 授權：持 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

資源 [!DNL Experience Platform] 可以與特定的虛擬沙箱隔離。 在請求中 [!DNL Platform] API，您可以指定操作將在其中進行的沙盒的名稱和ID。 這些是可選參數。

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>有關中的沙箱的詳細資訊 [!DNL Experience Platform]，請參見 [沙盒概述文檔](../../sandboxes/home.md)。

所有包含負載(POST、PUT、PATCH)的請求都需要附加的媒體類型報頭：

* Content-Type: `application/json`

### API參考文檔 {#api-reference-documentation}

您可以在本教程中找到所有API操作的附帶參考文檔。 請參閱 [流式服務 — Adobe Developer網站上的目標API文檔](https://developer.adobe.com/experience-platform-apis/references/destinations/)。 我們建議您並行使用本教程和API參考文檔。

### 字彙 {#glossary}

有關本API教程中將遇到的術語的說明，請閱讀 [術語節](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Glossary) 的子文檔。

## 選擇要導出段的目標 {#select-destination}

![激活段的步驟，突出顯示用戶所處的當前步驟](/help/destinations/assets/api/file-based-segment-export/step1.png)

在啟動工作流以導出配置檔案之前，請確定要將段導出到的目標的連接規範和流規範ID。 請使用下表進行參考。

| 目的地 | 連接規範 | 流規範 |
---------|----------|---------|
| Amazon S3 | `4fce964d-3f37-408f-9778-e597338a21ee` | `1a0514a6-33d4-4c7f-aff8-594799c47549` |
| Azure Blob 儲存體 | `6d6b59bf-fb58-4107-9064-4d246c0e5bb2` | `752d422f-b16f-4f0d-b1c6-26e448e3b388` |
| Azure資料湖第2代（ADLS第2代） | `be2c3209-53bc-47e7-ab25-145db8b873e1` | `17be2013-2549-41ce-96e7-a70363bec293` |
| 資料登錄區(DLZ) | `10440537-2a7b-4583-ac39-ed38d4b848e8` | `cd2fc47e-e838-4f38-a581-8fff2f99b63a` |
| Google雲儲存 | `c5d93acb-ea8b-4b14-8f53-02138444ae99` | `585c15c4-6cbf-4126-8f87-e26bff78b657` |
| SFTP | `36965a81-b1c6-401b-99f8-22508f1e6a26` | `fd36aaa4-bf2b-43fb-9387-43785eeeb799` |

{style="table-layout:auto"}

在本教程的後續步驟中，您需要這些ID來構建各種流服務實體。 您還需要參考連接規範本身的部分以設定某些實體，以便從流服務API中檢索連接規範。 請參閱下表中檢索所有目標的連接規範的示例：

>[!BEGINTABS]

>[!TAB Amazon S3]

**要求**

+++檢索 [!DNL connection spec] 為 [!DNL Amazon S3]

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

+++[!DNL Amazon S3]  — 連接規範

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

>[!TAB Azure Blob 儲存體]

**要求**

+++檢索 [!DNL connection spec] 為 [!DNL Azure Blob Storage]

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

>[!TAB Azure資料湖第2代（ADLS第2代）]

**要求**

+++檢索 [!DNL connection spec] 為 [!DNL Azure Data Lake Gen 2(ADLS Gen2])

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

>[!TAB 資料登錄區(DLZ)]

**要求**

+++檢索 [!DNL connection spec] 為 [!DNL Data Landing Zone(DLZ)]

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

>[!TAB Google雲儲存]

**要求**

+++檢索 [!DNL connection spec] 為 [!DNL Google Cloud Storage]

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

+++檢索 [!DNL connection spec] 用於SFTP

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

按照以下步驟設定將資料流導出到雲儲存目標的段。 對於某些步驟，不同雲儲存目標之間的請求和響應會有所不同。 在這些情況下，使用頁面上的頁籤檢索特定於要連接和導出段的目標的請求和響應。 確保使用正確的 `connection spec` 和 `flow spec` 用於您正在配置的目標。

## 建立源連接 {#create-source-connection}

![激活段的步驟，突出顯示用戶所處的當前步驟](/help/destinations/assets/api/file-based-segment-export/step2.png)

在確定要將段導出到哪個目標後，需要建立源連接。 的 [源連接](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Glossary) 表示與內部 [Experience Platform配置檔案儲存](/help/profile/home.md#profile-data-store)。

>[!BEGINSHADEBOX]

**要求**

+++建立源連接 — 請求

請在請求實例中注意帶內聯注釋的突出顯示行，這些行提供附加資訊。 將請求複製貼上到所選終端時刪除內聯注釋。

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
   "name":"Connect to Profile Store",
   "description":"Optional",
   "connectionSpec":{
      "id":"8a9c3494-9708-43d7-ae3f-cda01e5030e1", // this connection spec ID is always the same for Source Connections
      "version":"1.0"
   }
}'
```

+++

**回應**

+++建立源連接 — 響應

```json
{
    "id": "900df191-b983-45cd-90d5-4c7a0326d650",
    "etag": "\"0500ebe1-0000-0200-0000-63e28d060000\""
}
```

+++

>[!ENDSHADEBOX]

成功的響應返回ID(`id`)和 `etag`。 請記下源連接ID，因為以後建立資料流時需要它。

## 建立基本連接 {#create-base-connection}

![激活段的步驟，突出顯示用戶所處的當前步驟](/help/destinations/assets/api/file-based-segment-export/step3.png)

A [基本連接](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Glossary) 安全地將憑據儲存到目標。 根據目標類型，根據該目標進行身份驗證所需的憑據可能會有所不同。 要查找這些驗證參數，請首先檢索 `connection spec` 按部分所述 [選擇要導出段的目標](#select-destination) 然後看 `authSpec` 回答。 引用以下頁籤 `authSpec` 所有受支援目標的屬性。

>[!BEGINTABS]

>[!TAB Amazon S3]

+++[!DNL Amazon S3] - [!DNL Connection spec] 顯示 [!DNL auth spec]

請在中注意帶內聯注釋的突出顯示行 [!DNL connection spec] 下面的示例提供了有關在何處查找驗證參數的附加資訊 [!DNL connection spec]。

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

>[!TAB Azure Blob 儲存體]

+++[!DNL Azure Blob Storage] - [!DNL Connection spec] 顯示 [!DNL auth spec]

請在中注意帶內聯注釋的突出顯示行 [!DNL connection spec] 下面的示例提供了有關在何處查找驗證參數的附加資訊 [!DNL connection spec]。

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


>[!TAB Azure資料湖第2代（ADLS第2代）]

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)] - [!DNL Connection spec] 顯示 [!DNL auth spec]

請在中注意帶內聯注釋的突出顯示行 [!DNL connection spec] 下面的示例提供了有關在何處查找驗證參數的附加資訊 [!DNL connection spec]。

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


>[!TAB 資料登錄區(DLZ)]

+++[!DNL Data Landing Zone(DLZ)] - [!DNL Connection spec] 顯示 [!DNL auth spec]

>[!NOTE]
>
>資料登錄區域目標不需要 [!DNL auth spec]。

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

>[!TAB Google雲儲存]

+++[!DNL Google Cloud Storage] - [!DNL Connection spec] 顯示 [!DNL auth spec]

請在中注意帶內聯注釋的突出顯示行 [!DNL connection spec] 下面的示例提供了有關在何處查找驗證參數的附加資訊 [!DNL connection spec]。

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

+++SFTP - [!DNL Connection spec] 顯示 [!DNL auth spec]

>[!NOTE]
>
>SFTP目標包含兩個單獨的項 [!DNL auth spec]，因為它同時支援密碼和SSH密鑰驗證。

請在中注意帶內聯注釋的突出顯示行 [!DNL connection spec] 下面的示例提供了有關在何處查找驗證參數的附加資訊 [!DNL connection spec]。

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

使用驗證規範中指定的屬性(即 `authSpec` 根據響應)，您可以建立具有特定於每個目標類型的必需憑據的基本連接，如下例所示：

>[!BEGINTABS]

>[!TAB Amazon S3]

**要求**

+++[!DNL Amazon S3]  — 基本連接請求

>[!TIP]
>
>有關如何獲取所需的身份驗證憑據的資訊，請參閱 [驗證到目標](/help/destinations/catalog/cloud-storage/amazon-s3.md#authenticate) 的下界。

請在請求實例中注意帶內聯注釋的突出顯示行，這些行提供附加資訊。 將請求複製貼上到所選終端時，刪除請求中的內聯注釋。

```shell {line-numbers="true" start-line="1" highlight="18"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
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

+++[!DNL Amazon S3] 基本連接響應

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Azure Blob 儲存體]

**要求**

+++[!DNL Azure Blob Storage]  — 基本連接請求

>[!TIP]
>
>有關如何獲取所需的身份驗證憑據的資訊，請參閱 [驗證到目標](/help/destinations/catalog/cloud-storage/azure-blob.md#authenticate) 「Azure Blob儲存目標文檔」頁中的「Azure Blob儲存」部分。

請在請求實例中注意帶內聯注釋的突出顯示行，這些行提供附加資訊。 將請求複製貼上到所選終端時，刪除請求中的內聯注釋。

```shell {line-numbers="true" start-line="1" highlight="17"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
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

+++[!DNL Azure Blob Storage]  — 基本連接響應

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Azure資料湖第2代（ADLS第2代）]

**要求**

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)]  — 基本連接請求

>[!TIP]
>
>有關如何獲取所需的身份驗證憑據的資訊，請參閱 [驗證到目標](/help/destinations/catalog/cloud-storage/adls-gen2.md#authenticate) Azure Data Lake Gen 2(ADLS Gen2)目標文檔頁的「」部分。

請在請求實例中注意帶內聯注釋的突出顯示行，這些行提供附加資訊。 將請求複製貼上到所選終端時，刪除請求中的內聯注釋。

```shell {line-numbers="true" start-line="1" highlight="20"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
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

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)]  — 基本連接響應

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB 資料登錄區(DLZ)]

**要求**

+++[!DNL Data Landing Zone(DLZ)]  — 基本連接請求

>[!TIP]
>
>資料登錄區域目標不需要身份驗證憑據。 有關詳細資訊，請參閱 [驗證到目標](/help/destinations/catalog/cloud-storage/data-landing-zone.md#authenticate) 「資料登錄區域」目標文檔頁面的「資料登錄區域」部分。

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "Data Landing Zone(DLZ) Base Connection"
}'
```

+++

**回應**

+++[!DNL Data Landing Zone]  — 基本連接響應

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Google雲儲存]

**要求**

+++[!DNL Google Cloud Storage]  — 基本連接請求

>[!TIP]
>
>有關如何獲取所需的身份驗證憑據的資訊，請參閱 [驗證到目標](/help/destinations/catalog/cloud-storage/google-cloud-storage.md#authenticate) 「Google雲儲存目標文檔」頁的「CD」部分。

請在請求實例中注意帶內聯注釋的突出顯示行，這些行提供附加資訊。 將請求複製貼上到所選終端時，刪除請求中的內聯注釋。

```shell {line-numbers="true" start-line="1" highlight="18"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
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

+++[!DNL Google Cloud Storage]  — 基本連接響應

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB SFTP]

**要求**

+++帶密碼的SFTP — 基本連接請求

>[!TIP]
>
>有關如何獲取所需的身份驗證憑據的資訊，請參閱 [驗證到目標](/help/destinations/catalog/cloud-storage/sftp.md#authentication-information) 的子目錄。

請在請求實例中注意帶內聯注釋的突出顯示行，這些行提供附加資訊。 將請求複製貼上到所選終端時，刪除請求中的內聯注釋。

```shell {line-numbers="true" start-line="1" highlight="19"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
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

+++帶SSH密鑰的SFTP — 基本連接請求

>[!TIP]
>
>有關如何獲取所需的身份驗證憑據的資訊，請參閱 [驗證到目標](/help/destinations/catalog/cloud-storage/sftp.md#authentication-information) 的子目錄。

請在請求實例中注意帶內聯注釋的突出顯示行，這些行提供附加資訊。 將請求複製貼上到所選終端時，刪除請求中的內聯注釋。

```shell {line-numbers="true" start-line="1" highlight="19"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
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

+++SFTP — 基本連接響應

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!ENDTABS]

### 嚮導出的檔案添加加密

（可選）可以將加密添加到導出的檔案。 為此，您需要從 `encryptionSpecs`。 請參閱下面的請求示例，其中突出顯示了必需參數：


>[!BEGINSHADEBOX]

+++ 查看雲儲存目標的加密規格

```json {line-numbers="true" start-line="1" highlight="26-27"}
           "encryptionSpecs": [
                {
                    "name": "File PGP/GPG Encryption",
                    "type": "FileAsymmetric",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "description": "Defines parameters required for capturing user's inputs for encryption",
                        "type": "object",
                        "properties": {
                            "publicKey": {
                                "description": "Base64 encoded RSA public key",
                                "type": "string",
                                "contentEncoding": "base64"
                            },
                            "encryptionAlgo": {
                                "description": "Algorithm for encryption.",
                                "type": "string",
                                "default": "PGPGPG",
                                "enum": [
                                    "PGPGPG",
                                    "NONE"
                                ]
                            }
                        },
                        "required": [
                            "encryptionAlgo",
                            "publicKey"
                        ]
                    }
                }
            ]
```

+++

**要求**

+++將加密添加到基本連接 — 請求

請在請求實例中注意帶內聯注釋的突出顯示行，這些行提供附加資訊。 將請求複製貼上到所選終端時刪除內聯注釋。

```shell {line-numbers="true" start-line="1" highlight="19"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
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
  "encryptionSpecs":{
     "specName": "Encryption spec",
     "params": {
         "encryptionAlgo":"PGPGPG",
         "publicKey":"<Add public key>"
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

+++將加密添加到基本連接 — 響應

```json
{
    "id": "900df191-b983-45cd-90d5-4c7a0326d650",
    "etag": "\"0500ebe1-0000-0200-0000-63e28d060000\""
}
```

+++

>[!ENDSHADEBOX]

從響應中記錄連接ID。 建立目標連接時，下一步將需要此ID。

## 建立目標連接 {#create-target-connection}

![激活段的步驟，突出顯示用戶所處的當前步驟](/help/destinations/assets/api/file-based-segment-export/step4.png)

接下來，您需要建立目標連接。 [目標連接](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Glossary) 儲存導出段的導出參數。 導出參數包括導出位置、檔案格式、壓縮和其他詳細資訊。 例如，對於CSV檔案，可以選擇多個導出選項。 獲取有關中所有支援的CSV導出選項的詳細資訊 [檔案格式配置頁](/help/destinations/ui/batch-destinations-file-formatting-options.md)。

請參閱 `targetSpec` 目標中提供的屬性 `connection spec` 瞭解每個目標類型的支援屬性。 引用以下頁籤 `targetSpec` 所有受支援目標的屬性。

>[!BEGINTABS]

>[!TAB Amazon S3]

+++[!DNL Amazon S3] - [!DNL Connection spec] 顯示目標連接參數

在中使用內聯注釋記錄突出顯示的行 [!DNL connection spec] 下面的示例，提供了有關在何處查找的其他資訊 [!DNL target spec] 連接規範中的參數。 在下面的示例中，您也可以看到目標參數 *不* 適用於段導出目標。

```json {line-numbers="true" start-line="1" highlight="10,56"}
{
    "items": [
        {
            "id": "4fce964d-3f37-408f-9778-e597338a21ee",
            "name": "Amazon S3",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [...],
            "encryptionSpecs": [...],
            "targetSpec": { //describes the target connection parameters
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
                        "fileType": {
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "NOT_CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "CSV",
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "datasetFileType": { // does not apply to segment export destinations
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
                        "csvOptions": {
                            "conditional": {
                                "field": "fileType",
                                "operator": "EQUALS",
                                "value": "CSV"
                            },
                            "title": "CSV Options",
                            "description": "Select your CSV options",
                            "type": "object",
                            "properties": {
                                "quote": {
                                    "title": "Quote Character",
                                    "description": "Select your Quote character",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Double Quotes (\")",
                                            "const": "\""
                                        },
                                        {
                                            "title":"Null Character (\\)",
                                            "const": ""
                                        }
                                    ],
                                    "default": ""
                                },
                                "escape": {
                                    "title": "Escape Character",
                                    "description": "Select your Escape character",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Back Slash (\\)",
                                            "const": "\\"
                                        },
                                        {
                                            "title": "Single Quote (')",
                                            "const": "'"
                                        }
                                    ],
                                    "default": "\\"
                                },
                                "delimiter": {
                                    "title": "Delimiter",
                                    "description": "Select your Delimiter",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Comma (,)",
                                            "const": ","
                                        },
                                        {
                                            "title": "Tab (\\t)",
                                            "const": "\t"
                                        },
                                        {
                                            "title": "Pipe (|)",
                                            "const": "|"
                                        },
                                        {
                                            "title": "Semicolon (;)",
                                            "const": ";"
                                        },
                                        {
                                            "title": "Colon (:)",
                                            "const": ":"
                                        }
                                    ],
                                    "default": ","
                                },
                                "nullValue": {
                                    "title": "Null Value",
                                    "description": "Select the output value of 'null' fields",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "null",
                                            "const": "null"
                                        },
                                        {
                                            "title": "\"\"",
                                            "const": "\"\""
                                        },
                                        {
                                            "title": "Empty String",
                                            "const": ""
                                        }
                                    ],
                                    "default": "null"
                                },
                                "emptyValue": {
                                    "title": "Empty Value",
                                    "description": "Select the output value of blank fields",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "null",
                                            "const": "null"
                                        },
                                        {
                                            "title": "\"\"",
                                            "const": "\"\""
                                        },
                                        {
                                            "title": "Empty String",
                                            "const": ""
                                        }
                                    ],
                                    "default": ""
                                }
                            }
                        },
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

>[!TAB Azure Blob 儲存體]

+++[!DNL Azure Blob Storage] - [!DNL Connection spec] 顯示目標連接參數

在中使用內聯注釋記錄突出顯示的行 [!DNL connection spec] 下面的示例，提供了有關在何處查找的其他資訊 [!DNL target spec] 連接規範中的參數。 在下面的示例中，您也可以看到目標參數 *不* 適用於段導出目標。

```json {line-numbers="true" start-line="1" highlight="10,44"}
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
                        "fileType": {
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "NOT_CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "CSV",
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "datasetFileType": { // does not apply to segment export destinations
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
                        "csvOptions": {
                            "conditional": {
                                "field": "fileType",
                                "operator": "EQUALS",
                                "value": "CSV"
                            },
                            "title": "CSV Options",
                            "description": "Select your CSV options",
                            "type": "object",
                            "properties": {
                                "quote": {
                                    "title": "Quote Character",
                                    "description": "Select your Quote character",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Double Quotes (\")",
                                            "const": "\""
                                        },
                                        {
                                            "title":"Null Character (\\)",
                                            "const": ""
                                        }
                                    ],
                                    "default": ""
                                },
                                "escape": {
                                    "title": "Escape Character",
                                    "description": "Select your Escape character",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Back Slash (\\)",
                                            "const": "\\"
                                        },
                                        {
                                            "title": "Single Quote (')",
                                            "const": "'"
                                        }
                                    ],
                                    "default": "\\"
                                },
                                "delimiter": {
                                    "title": "Delimiter",
                                    "description": "Select your Delimiter",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Comma (,)",
                                            "const": ","
                                        },
                                        {
                                            "title": "Tab (\\t)",
                                            "const": "\t"
                                        },
                                        {
                                            "title": "Pipe (|)",
                                            "const": "|"
                                        },
                                        {
                                            "title": "Semicolon (;)",
                                            "const": ";"
                                        },
                                        {
                                            "title": "Colon (:)",
                                            "const": ":"
                                        }
                                    ],
                                    "default": ","
                                },
                                "nullValue": {
                                    "title": "Null Value",
                                    "description": "Select the output value of 'null' fields",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "null",
                                            "const": "null"
                                        },
                                        {
                                            "title": "\"\"",
                                            "const": "\"\""
                                        },
                                        {
                                            "title": "Empty String",
                                            "const": ""
                                        }
                                    ],
                                    "default": "null"
                                },
                                "emptyValue": {
                                    "title": "Empty Value",
                                    "description": "Select the output value of blank fields",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "null",
                                            "const": "null"
                                        },
                                        {
                                            "title": "\"\"",
                                            "const": "\"\""
                                        },
                                        {
                                            "title": "Empty String",
                                            "const": ""
                                        }
                                    ],
                                    "default": ""
                                }
                            }
                        },
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


>[!TAB Azure資料湖第2代（ADLS第2代）]

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)] - [!DNL Connection spec] 顯示目標連接參數

在中使用內聯注釋記錄突出顯示的行 [!DNL connection spec] 下面的示例，提供了有關在何處查找的其他資訊 [!DNL target spec] 連接規範中的參數。 在下面的示例中，您也可以看到目標參數 *不* 適用於段導出目標。

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
                        "fileType": {
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "NOT_CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "CSV",
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "datasetFileType": { // does not apply to segment export destinations
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
                        "csvOptions": {
                            "conditional": {
                                "field": "fileType",
                                "operator": "EQUALS",
                                "value": "CSV"
                            },
                            "title": "CSV Options",
                            "description": "Select your CSV options",
                            "type": "object",
                            "properties": {
                                "quote": {
                                    "title": "Quote Character",
                                    "description": "Select your Quote character",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Double Quotes (\")",
                                            "const": "\""
                                        },
                                        {
                                            "title":"Null Character (\\)",
                                            "const": ""
                                        }
                                    ],
                                    "default": ""
                                },
                                "escape": {
                                    "title": "Escape Character",
                                    "description": "Select your Escape character",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Back Slash (\\)",
                                            "const": "\\"
                                        },
                                        {
                                            "title": "Single Quote (')",
                                            "const": "'"
                                        }
                                    ],
                                    "default": "\\"
                                },
                                "delimiter": {
                                    "title": "Delimiter",
                                    "description": "Select your Delimiter",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Comma (,)",
                                            "const": ","
                                        },
                                        {
                                            "title": "Tab (\\t)",
                                            "const": "\t"
                                        },
                                        {
                                            "title": "Pipe (|)",
                                            "const": "|"
                                        },
                                        {
                                            "title": "Semicolon (;)",
                                            "const": ";"
                                        },
                                        {
                                            "title": "Colon (:)",
                                            "const": ":"
                                        }
                                    ],
                                    "default": ","
                                },
                                "nullValue": {
                                    "title": "Null Value",
                                    "description": "Select the output value of 'null' fields",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "null",
                                            "const": "null"
                                        },
                                        {
                                            "title": "\"\"",
                                            "const": "\"\""
                                        },
                                        {
                                            "title": "Empty String",
                                            "const": ""
                                        }
                                    ],
                                    "default": "null"
                                },
                                "emptyValue": {
                                    "title": "Empty Value",
                                    "description": "Select the output value of blank fields",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "null",
                                            "const": "null"
                                        },
                                        {
                                            "title": "\"\"",
                                            "const": "\"\""
                                        },
                                        {
                                            "title": "Empty String",
                                            "const": ""
                                        }
                                    ],
                                    "default": ""
                                }
                            }
                        },
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

>[!TAB 資料登錄區(DLZ)]

+++[!DNL Data Landing Zone(DLZ)] - [!DNL Connection spec] 顯示目標連接參數

在中使用內聯注釋記錄突出顯示的行 [!DNL connection spec] 下面的示例，提供了有關在何處查找的其他資訊 [!DNL target spec] 連接規範中的參數。 在下面的示例中，您也可以看到目標參數 *不* 適用於段導出目標。

```json {line-numbers="true" start-line="1" highlight="9,36"}
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
                        "fileType": {
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "NOT_CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "CSV",
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "datasetFileType": { // does not apply to segment export destinations
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
                        "csvOptions": {
                            "conditional": {
                                "field": "fileType",
                                "operator": "EQUALS",
                                "value": "CSV"
                            },
                            "title": "CSV Options",
                            "description": "Select your CSV options",
                            "type": "object",
                            "properties": {
                                "quote": {
                                    "title": "Quote Character",
                                    "description": "Select your Quote character",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Double Quotes (\")",
                                            "const": "\""
                                        },
                                        {
                                            "title":"Null Character (\\)",
                                            "const": ""
                                        }
                                    ],
                                    "default": ""
                                },
                                "escape": {
                                    "title": "Escape Character",
                                    "description": "Select your Escape character",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Back Slash (\\)",
                                            "const": "\\"
                                        },
                                        {
                                            "title": "Single Quote (')",
                                            "const": "'"
                                        }
                                    ],
                                    "default": "\\"
                                },
                                "delimiter": {
                                    "title": "Delimiter",
                                    "description": "Select your Delimiter",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Comma (,)",
                                            "const": ","
                                        },
                                        {
                                            "title": "Tab (\\t)",
                                            "const": "\t"
                                        },
                                        {
                                            "title": "Pipe (|)",
                                            "const": "|"
                                        },
                                        {
                                            "title": "Semicolon (;)",
                                            "const": ";"
                                        },
                                        {
                                            "title": "Colon (:)",
                                            "const": ":"
                                        }
                                    ],
                                    "default": ","
                                },
                                "nullValue": {
                                    "title": "Null Value",
                                    "description": "Select the output value of 'null' fields",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "null",
                                            "const": "null"
                                        },
                                        {
                                            "title": "\"\"",
                                            "const": "\"\""
                                        },
                                        {
                                            "title": "Empty String",
                                            "const": ""
                                        }
                                    ],
                                    "default": "null"
                                },
                                "emptyValue": {
                                    "title": "Empty Value",
                                    "description": "Select the output value of blank fields",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "null",
                                            "const": "null"
                                        },
                                        {
                                            "title": "\"\"",
                                            "const": "\"\""
                                        },
                                        {
                                            "title": "Empty String",
                                            "const": ""
                                        }
                                    ],
                                    "default": ""
                                }
                            }
                        },
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

>[!TAB Google雲儲存]

+++[!DNL Google Cloud Storage] - [!DNL Connection spec] 顯示目標連接參數

在中使用內聯注釋記錄突出顯示的行 [!DNL connection spec] 下面的示例，提供了有關在何處查找的其他資訊 [!DNL target spec] 連接規範中的參數。 在下面的示例中，您也可以看到目標參數 *不* 適用於段導出目標。

```json {line-numbers="true" start-line="1" highlight="10,44"}
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
                        "fileType": {
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "NOT_CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "CSV",
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "datasetFileType": { // does not apply to segment export destinations
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
                        "csvOptions": {
                            "conditional": {
                                "field": "fileType",
                                "operator": "EQUALS",
                                "value": "CSV"
                            },
                            "title": "CSV Options",
                            "description": "Select your CSV options",
                            "type": "object",
                            "properties": {
                                "quote": {
                                    "title": "Quote Character",
                                    "description": "Select your Quote character",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Double Quotes (\")",
                                            "const": "\""
                                        },
                                        {
                                            "title":"Null Character (\\)",
                                            "const": ""
                                        }
                                    ],
                                    "default": ""
                                },
                                "escape": {
                                    "title": "Escape Character",
                                    "description": "Select your Escape character",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Back Slash (\\)",
                                            "const": "\\"
                                        },
                                        {
                                            "title": "Single Quote (')",
                                            "const": "'"
                                        }
                                    ],
                                    "default": "\\"
                                },
                                "delimiter": {
                                    "title": "Delimiter",
                                    "description": "Select your Delimiter",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Comma (,)",
                                            "const": ","
                                        },
                                        {
                                            "title": "Tab (\\t)",
                                            "const": "\t"
                                        },
                                        {
                                            "title": "Pipe (|)",
                                            "const": "|"
                                        },
                                        {
                                            "title": "Semicolon (;)",
                                            "const": ";"
                                        },
                                        {
                                            "title": "Colon (:)",
                                            "const": ":"
                                        }
                                    ],
                                    "default": ","
                                },
                                "nullValue": {
                                    "title": "Null Value",
                                    "description": "Select the output value of 'null' fields",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "null",
                                            "const": "null"
                                        },
                                        {
                                            "title": "\"\"",
                                            "const": "\"\""
                                        },
                                        {
                                            "title": "Empty String",
                                            "const": ""
                                        }
                                    ],
                                    "default": "null"
                                },
                                "emptyValue": {
                                    "title": "Empty Value",
                                    "description": "Select the output value of blank fields",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "null",
                                            "const": "null"
                                        },
                                        {
                                            "title": "\"\"",
                                            "const": "\"\""
                                        },
                                        {
                                            "title": "Empty String",
                                            "const": ""
                                        }
                                    ],
                                    "default": ""
                                }
                            }
                        },
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

+++SFTP - [!DNL Connection spec] 顯示目標連接參數

在中使用內聯注釋記錄突出顯示的行 [!DNL connection spec] 下面的示例，提供了有關在何處查找的其他資訊 [!DNL target spec] 連接規範中的參數。 在下面的示例中，您也可以看到目標參數 *不* 適用於段導出目標。

```json {line-numbers="true" start-line="1" highlight="10,37"}
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
                        "fileType": {
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "NOT_CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "CSV",
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "datasetFileType": { // does not apply to segment export destinations
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
                        "csvOptions": {
                            "conditional": {
                                "field": "fileType",
                                "operator": "EQUALS",
                                "value": "CSV"
                            },
                            "title": "CSV Options",
                            "description": "Select your CSV options",
                            "type": "object",
                            "properties": {
                                "quote": {
                                    "title": "Quote Character",
                                    "description": "Select your Quote character",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Double Quotes (\")",
                                            "const": "\""
                                        },
                                        {
                                            "title":"Null Character (\\)",
                                            "const": ""
                                        }
                                    ],
                                    "default": ""
                                },
                                "escape": {
                                    "title": "Escape Character",
                                    "description": "Select your Escape character",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Back Slash (\\)",
                                            "const": "\\"
                                        },
                                        {
                                            "title": "Single Quote (')",
                                            "const": "'"
                                        }
                                    ],
                                    "default": "\\"
                                },
                                "delimiter": {
                                    "title": "Delimiter",
                                    "description": "Select your Delimiter",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Comma (,)",
                                            "const": ","
                                        },
                                        {
                                            "title": "Tab (\\t)",
                                            "const": "\t"
                                        },
                                        {
                                            "title": "Pipe (|)",
                                            "const": "|"
                                        },
                                        {
                                            "title": "Semicolon (;)",
                                            "const": ";"
                                        },
                                        {
                                            "title": "Colon (:)",
                                            "const": ":"
                                        }
                                    ],
                                    "default": ","
                                },
                                "nullValue": {
                                    "title": "Null Value",
                                    "description": "Select the output value of 'null' fields",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "null",
                                            "const": "null"
                                        },
                                        {
                                            "title": "\"\"",
                                            "const": "\"\""
                                        },
                                        {
                                            "title": "Empty String",
                                            "const": ""
                                        }
                                    ],
                                    "default": "null"
                                },
                                "emptyValue": {
                                    "title": "Empty Value",
                                    "description": "Select the output value of blank fields",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "null",
                                            "const": "null"
                                        },
                                        {
                                            "title": "\"\"",
                                            "const": "\"\""
                                        },
                                        {
                                            "title": "Empty String",
                                            "const": ""
                                        }
                                    ],
                                    "default": ""
                                }
                            }
                        },
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

通過使用上述規範，您可以構建特定於所需雲儲存目標的目標連接請求，如下面的頁籤所示。

>[!BEGINTABS]

>[!TAB Amazon S3]

**要求**

+++[!DNL Amazon S3]  — 目標連接請求

>[!TIP]
>
>有關如何獲取所需目標參數的資訊，請參閱 [填寫目標詳細資訊](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details) 的下界 [!DNL Amazon S3] 目標文檔頁面。

請在請求實例中注意帶內聯注釋的突出顯示行，這些行提供附加資訊。 將請求複製貼上到所選終端時，刪除請求中的內聯注釋。

```shell {line-numbers="true" start-line="1" highlight="19"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Amazon S3 Beta Target Connection",
    "baseConnectionId": "<FROM_STEP_CREATE_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "bucketName": "your-bucket-name",
        "path": "folder/subfolder",
        "compression": "NONE",
        "fileType": "JSON"
    },
    "connectionSpec": {
        "id": "4fce964d-3f37-408f-9778-e597338a21ee", // Amazon S3 connection spec id
        "version": "1.0"
    }
}'
```

+++

+++[!DNL Amazon S3]  — 具有CSV選項的目標連接請求

>[!TIP]
>
>有關可用於檔案導出的CSV選項的詳細資訊，請參閱 [檔案格式配置頁](/help/destinations/ui/batch-destinations-file-formatting-options.md) 。

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
   "name":"Amazon S3 Beta Target Connection",
   "baseConnectionId":"<FROM_STEP_CREATE_BASE_CONNECTION>",
   "params":{
      "mode":"Server-to-server",
      "bucketName":"your-bucket-name",
      "path":"folder/subfolder",
      "compression":"GZIP",
      "fileType":"CSV",
      "csvOptions":{
         "nullValue":"null",
         "emptyValue":"",
         "escape":"\\",
         "quote":"",
         "delimiter":","
      }
   },
   "connectionSpec":{
      "id":"4fce964d-3f37-408f-9778-e597338a21ee",
      "version":"1.0"
   }
}'
```

+++

**回應**

+++目標連接 — 響應

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Azure Blob 儲存體]

**要求**

+++[!DNL Azure Blob Storage]  — 目標連接請求

>[!TIP]
>
>有關如何獲取所需目標參數的資訊，請參閱 [填寫目標詳細資訊](/help/destinations/catalog/cloud-storage/azure-blob.md#destination-details) 的下界 [!DNL Azure Blob Storage] 目標文檔頁面。

請在請求實例中注意帶內聯注釋的突出顯示行，這些行提供附加資訊。 將請求複製貼上到所選終端時，刪除請求中的內聯注釋。

```shell {line-numbers="true" start-line="1" highlight="19"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Azure Blob Storage Beta Target Connection",
    "baseConnectionId": "<FROM_STEP_CREATE_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "container": "your-container-name",
        "path": "folder/subfolder",
        "compression": "NONE",
        "fileType": "JSON"
    },
    "connectionSpec": {
        "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2", // Azure Blob Storage connection spec id
        "version": "1.0"
    }
}'
```

+++

+++[!DNL Azure Blob Storage]  — 具有CSV選項的目標連接請求

>[!TIP]
>
>有關可用於檔案導出的CSV選項的詳細資訊，請參閱 [檔案格式配置頁](/help/destinations/ui/batch-destinations-file-formatting-options.md) 。

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
   "name":"Azure Blob Storage Beta Target Connection",
   "baseConnectionId":"<FROM_STEP_CREATE_BASE_CONNECTION>",
   "params":{
      "mode":"Server-to-server",
      "bucketName":"your-bucket-name",
      "path":"folder/subfolder",
      "compression":"GZIP",
      "fileType":"CSV",
      "csvOptions":{
         "nullValue":"null",
         "emptyValue":"",
         "escape":"\\",
         "quote":"",
         "delimiter":","
      }
   },
   "connectionSpec":{
      "id":"6d6b59bf-fb58-4107-9064-4d246c0e5bb2",
      "version":"1.0"
   }
}'
```

+++

**回應**

+++目標連接 — 響應

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Azure資料湖第2代（ADLS第2代）]

**要求**

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)]  — 目標連接請求

>[!TIP]
>
>有關如何獲取所需目標參數的資訊，請參閱 [填寫目標詳細資訊](/help/destinations/catalog/cloud-storage/adls-gen2.md#destination-details) Azure的部分 [!DNL Data Lake Gen 2(ADLS Gen2)] 目標文檔頁面。

請在請求實例中注意帶內聯注釋的突出顯示行，這些行提供附加資訊。 將請求複製貼上到所選終端時，刪除請求中的內聯注釋。

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
    "baseConnectionId": "<FROM_STEP_CREATE_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "path": "folder/subfolder",
        "compression": "NONE",
        "fileType": "JSON"
    },
    "connectionSpec": {
        "id": "be2c3209-53bc-47e7-ab25-145db8b873e1", // Azure Data Lake Gen 2(ADLS Gen2) connection spec id
        "version": "1.0"
    }
}'
```

+++

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)]  — 具有CSV選項的目標連接請求

>[!TIP]
>
>有關可用於檔案導出的CSV選項的詳細資訊，請參閱 [檔案格式配置頁](/help/destinations/ui/batch-destinations-file-formatting-options.md) 。

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
   "name":"Azure Data Lake Gen 2(ADLS Gen2)",
   "baseConnectionId":"<FROM_STEP_CREATE_BASE_CONNECTION>",
   "params":{
      "mode":"Server-to-server",
      "bucketName":"your-bucket-name",
      "path":"folder/subfolder",
      "compression":"GZIP",
      "fileType":"CSV",
      "csvOptions":{
         "nullValue":"null",
         "emptyValue":"",
         "escape":"\\",
         "quote":"",
         "delimiter":","
      }
   },
   "connectionSpec":{
      "id":"be2c3209-53bc-47e7-ab25-145db8b873e1",
      "version":"1.0"
   }
}'
```

+++

**回應**

+++目標連接 — 響應

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB 資料登錄區(DLZ)]

**要求**

+++[!DNL Data Landing Zone]  — 目標連接請求

>[!TIP]
>
>有關如何獲取所需目標參數的資訊，請參閱 [填寫目標詳細資訊](/help/destinations/catalog/cloud-storage/data-landing-zone.md#destination-details) 的下界 [!DNL Data Landing Zone] 目標文檔頁面。

請在請求實例中注意帶內聯注釋的突出顯示行，這些行提供附加資訊。 將請求複製貼上到所選終端時，刪除請求中的內聯注釋。

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
    "baseConnectionId": "<FROM_STEP_CREATE_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "path": "folder/subfolder",
        "compression": "NONE",
        "fileType": "JSON"
    },
    "connectionSpec": {
        "id": "10440537-2a7b-4583-ac39-ed38d4b848e8", // Data Landing Zone connection spec id
        "version": "1.0"
    }
}'
```

+++

+++[!DNL Data Landing Zone]  — 具有CSV選項的目標連接請求

>[!TIP]
>
>有關可用於檔案導出的CSV選項的詳細資訊，請參閱 [檔案格式配置頁](/help/destinations/ui/batch-destinations-file-formatting-options.md) 。

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
   "name":"Data Landing Zone Beta Target Connection",
   "baseConnectionId":"<FROM_STEP_CREATE_BASE_CONNECTION>",
   "params":{
      "mode":"Server-to-server",
      "bucketName":"your-bucket-name",
      "path":"folder/subfolder",
      "compression":"GZIP",
      "fileType":"CSV",
      "csvOptions":{
         "nullValue":"null",
         "emptyValue":"",
         "escape":"\\",
         "quote":"",
         "delimiter":","
      }
   },
   "connectionSpec":{
      "id":"10440537-2a7b-4583-ac39-ed38d4b848e8",
      "version":"1.0"
   }
}'
```

+++

**回應**

+++目標連接 — 響應

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Google雲儲存]

**要求**

+++[!DNL Google Cloud Storage]  — 目標連接請求

>[!TIP]
>
>有關如何獲取所需目標參數的資訊，請參閱 [填寫目標詳細資訊](/help/destinations/catalog/cloud-storage/google-cloud-storage.md#destination-details) 的下界 [!DNL Google Cloud Storage] 目標文檔頁面。

請在請求實例中注意帶內聯注釋的突出顯示行，這些行提供附加資訊。 將請求複製貼上到所選終端時，刪除請求中的內聯注釋。

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
    "baseConnectionId": "<FROM_STEP_CREATE_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "bucketName": "your-bucket-name",
        "path": "folder/subfolder",
        "compression": "NONE",
        "fileType": "JSON"
    },
    "connectionSpec": {
        "id": "c5d93acb-ea8b-4b14-8f53-02138444ae99", // Google Cloud Storage connection spec id
        "version": "1.0"
    }
}'
```

+++

+++[!DNL Google Cloud Storage]  — 具有CSV選項的目標連接請求

>[!TIP]
>
>有關可用於檔案導出的CSV選項的詳細資訊，請參閱 [檔案格式配置頁](/help/destinations/ui/batch-destinations-file-formatting-options.md) 。

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
   "name":"Google Cloud Storage Beta Target Connection",
   "baseConnectionId":"<FROM_STEP_CREATE_BASE_CONNECTION>",
   "params":{
      "mode":"Server-to-server",
      "bucketName":"your-bucket-name",
      "path":"folder/subfolder",
      "compression":"GZIP",
      "fileType":"CSV",
      "csvOptions":{
         "nullValue":"null",
         "emptyValue":"",
         "escape":"\\",
         "quote":"",
         "delimiter":","
      }
   },
   "connectionSpec":{
      "id":"c5d93acb-ea8b-4b14-8f53-02138444ae99",
      "version":"1.0"
   }
}'
```

+++

**回應**

+++目標連接 — 響應

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB SFTP]

**要求**

+++SFTP — 目標連接請求

>[!TIP]
>
>有關如何獲取所需目標參數的資訊，請參閱 [填寫目標詳細資訊](/help/destinations/catalog/cloud-storage/google-cloud-storage.md#destination-details) 的子目錄。

請在請求實例中注意帶內聯注釋的突出顯示行，這些行提供附加資訊。 將請求複製貼上到所選終端時，刪除請求中的內聯注釋。

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
    "baseConnectionId": "<FROM_STEP_CREATE_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "remotePath": "folder/subfolder",
        "compression": "NONE",
        "fileType": "JSON"
    },
    "connectionSpec": {
        "id": "36965a81-b1c6-401b-99f8-22508f1e6a26", // SFTP connection spec id
        "version": "1.0"
    }
}'
```

+++

+++SFTP — 具有CSV選項的目標連接請求

>[!TIP]
>
>有關可用於檔案導出的CSV選項的詳細資訊，請參閱 [檔案格式配置頁](/help/destinations/ui/batch-destinations-file-formatting-options.md) 。

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
   "name":"SFTP Target Connection",
   "baseConnectionId":"<FROM_STEP_CREATE_BASE_CONNECTION>",
   "params":{
      "mode":"Server-to-server",
      "bucketName":"your-bucket-name",
      "path":"folder/subfolder",
      "compression":"GZIP",
      "fileType":"CSV",
      "csvOptions":{
         "nullValue":"null",
         "emptyValue":"",
         "escape":"\\",
         "quote":"",
         "delimiter":","
      }
   },
   "connectionSpec":{
      "id":"36965a81-b1c6-401b-99f8-22508f1e6a26",
      "version":"1.0"
   }
}'
```

+++

**回應**

+++目標連接 — 響應

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!ENDTABS]

注意 `target connection ID` 從回應中。 在建立要導出段的資料流時，下一步將需要此ID。

成功的響應返回ID(`id`)和 `etag`。 在以後建立資料流時，請記下目標連接ID，因為您需要它。

## 建立資料流 {#create-dataflow}

![激活段的步驟，突出顯示用戶所處的當前步驟](/help/destinations/assets/api/file-based-segment-export/step5.png)

目標配置的下一步是建立資料流。 A [資料流](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Glossary) 將先前建立的實體關聯在一起，還提供了配置段導出時間表的選項。 要建立資料流，請根據所需的雲儲存目標使用下面的負載，並替換前面步驟中的流實體ID。 請注意，在此步驟中，不會向資料流添加任何與屬性或標識映射相關的資訊。 接下來的步驟是。

>[!BEGINTABS]

>[!TAB Amazon S3]

**要求**

+++建立段將資料流導出到 [!DNL Amazon S3] 目標 — 請求

請在請求實例中注意帶內聯注釋的突出顯示行，這些行提供附加資訊。 將請求複製貼上到所選終端時，刪除請求中的內聯注釋。

```shell {line-numbers="true" start-line="1" highlight="12,22-25"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/flows' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Activate segments to an Amazon S3 cloud storage destination",
    "description": "This operation creates a dataflow to export segments to an Amazon S3 cloud storage destination",
    "flowSpec": {
        "id": "1a0514a6-33d4-4c7f-aff8-594799c47549", // Amazon S3 flow spec ID
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "<FROM_STEP_CREATE_SOURCE_CONNECTION>"
    ],
    "targetConnectionIds": [
        "<FROM_STEP_CREATE_TARGET_CONNECTION>"
    ],
    "transformations": []
}'
```

+++

**回應**

+++建立資料流 — 響應

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Azure Blob 儲存體]

**要求**

+++建立段將資料流導出到 [!DNL Azure Blob Storage] 目標 — 請求

請在請求實例中注意帶內聯注釋的突出顯示行，這些行提供附加資訊。 將請求複製貼上到所選終端時，刪除請求中的內聯注釋。

```shell {line-numbers="true" start-line="1" highlight="12,22-25"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/flows' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Activate segments to an Azure Blob Storage cloud storage destination",
    "description": "This operation creates a dataflow to export segments to an Azure Blob Storage cloud storage destination",
    "flowSpec": {
        "id": "752d422f-b16f-4f0d-b1c6-26e448e3b388", // Azure Blob Storage flow spec ID
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "<FROM_STEP_CREATE_SOURCE_CONNECTION>"
    ],
    "targetConnectionIds": [
        "<FROM_STEP_CREATE_TARGET_CONNECTION>"
    ],
    "transformations": [
        {
        "name": "GeneralTransform",
        "params": {
            "mandatoryFields": [],
            "primaryFields": [],
            "profileMapping": {},
            "segmentSelectors": {
            "selectors": []
            }
        }
        }
    ]
}'
```

+++

**回應**

+++建立資料流 — 響應

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Azure資料湖第2代（ADLS第2代）]

**要求**

+++建立段將資料流導出到 [!DNL Azure Data Lake Gen 2(ADLS Gen2)] 目標 — 請求

請在請求實例中注意帶內聯注釋的突出顯示行，這些行提供附加資訊。 將請求複製貼上到所選終端時，刪除請求中的內聯注釋。

```shell {line-numbers="true" start-line="1" highlight="12,22-25"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/flows' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Activate segments to an Azure Data Lake Gen 2(ADLS Gen2) cloud storage destination",
    "description": "This operation creates a dataflow to export segments to an Azure Data Lake Gen 2(ADLS Gen2) cloud storage destination",
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
    "transformations": []
}'
```

+++

**回應**

+++建立資料流 — 響應

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB 資料登錄區(DLZ)]

**要求**

+++建立段將資料流導出到 [!DNL Data Landing Zone] 目標 — 請求

請在請求實例中注意帶內聯注釋的突出顯示行，這些行提供附加資訊。 將請求複製貼上到所選終端時，刪除請求中的內聯注釋。

```shell {line-numbers="true" start-line="1" highlight="12,22-25"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/flows' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Activate segments to a Data Landing Zone cloud storage destination",
    "description": "This operation creates a dataflow to export segments to a Data Landing Zone cloud storage destination",
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
    "transformations": []
}'
```

+++

**回應**

+++建立資料流 — 響應

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Google雲儲存]

**要求**

+++建立段將資料流導出到 [!DNL Google Cloud Storage] 目標 — 請求

請在請求實例中注意帶內聯注釋的突出顯示行，這些行提供附加資訊。 將請求複製貼上到所選終端時，刪除請求中的內聯注釋。

```shell {line-numbers="true" start-line="1" highlight="12,22-25"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/flows' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Activate segments to a Google Cloud Storage cloud storage destination",
    "description": "This operation creates a dataflow to export segments to a Google Cloud Storage destination",
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
    "transformations": []
}'
```

+++

**回應**

+++建立資料流 — 響應

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB SFTP]

**要求**

+++建立段將資料流導出到SFTP目標 — 請求

請在請求實例中注意帶內聯注釋的突出顯示行，這些行提供附加資訊。 將請求複製貼上到所選終端時，刪除請求中的內聯注釋。

```shell {line-numbers="true" start-line="1" highlight="12,22-25"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/flows' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Activate segments to an SFTP cloud storage destination",
    "description": "This operation creates a dataflow to export segments to an SFTP cloud storage destination",
    "flowSpec": {
        "id": "fd36aaa4-bf2b-43fb-9387-43785eeeb799", // SFTP flow spec ID
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "<FROM_STEP_CREATE_SOURCE_CONNECTION>"
    ],
    "targetConnectionIds": [
        "<FROM_STEP_CREATE_TARGET_CONNECTION>"
    ],
    "transformations": []
}'
```

+++

**回應**

+++建立資料流 — 響應

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!ENDTABS]

從響應中注意資料流ID。 以後的步驟中將需要此ID。

### 將段添加到導出

在此步驟中，還可以選擇要導出到目標的段。 有關此步驟和向資料流添加段的請求格式的詳細資訊，請查看中的示例 [更新目標資料流](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Dataflows/operation/patchFlowById) 文檔中的「 API引用」部分。


## 設定屬性和標識映射 {#attribute-and-identity-mapping}

![激活段的步驟，突出顯示用戶所處的當前步驟](/help/destinations/assets/api/file-based-segment-export/step6.png)

建立資料流後，需要為要導出的屬性和標識設定映射。 這包括三個步驟，如下所列：

1. 建立輸入架構
2. 建立輸出架構
3. 設定映射集以連接建立的架構

例如，要獲得UI中顯示的以下映射，您需要完成上面列出的三個步驟，並在下一個標題中詳細說明。

![映射步驟示例](/help/destinations/assets/api/file-based-segment-export/mapping-example.png)

### 建立輸入架構

要建立輸入架構，首先需要檢索 [聯合架構](/help/profile/ui/union-schema.md) 以及可導出到目標的標識。 這是屬性和標識的架構，您可以選擇它作為源映射。

![顯示選定源欄位視圖中的屬性和標識選項的錄制](/help/destinations/assets/api/file-based-segment-export/select-source-field.gif)

查看以下檢索屬性和標識的請求和響應示例。

>[!BEGINSHADEBOX]

**獲取屬性的請求**

+++從聯合架構獲取可用屬性 — 請求

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/ups/config/entityTypes/_xdm.context.profile?property=fullSchema==true&property=includeRelationshipDescriptors==true' \ 
--header 'x-gw-ims-org-id: {ORG_ID}' \ 
--header 'x-api-key: {API_KEY}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \ 
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
```

+++

**回應**

+++從聯合架構獲取可用屬性 — 響應

為簡單起見，以下答復已縮短。

```json
       "person": {
            "title": "Person",
            "description": "An individual actor, contact, or owner.",
            "meta:referencedFrom": [
                "https://ns.adobe.com/xdm/context/person"
            ],
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "birthDate": {
                    "meta:xdmType": "date",
                    "type": "string",
                    "format": "date",
                    "title": "Birth date(YYYY-MM-DD)",
                    "description": "The full date a person was born."
                },
                "birthDayAndMonth": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "title": "Birth date (MM-DD)",
                    "description": "The day and month a person was born, in the format MM-DD. This field should be used when the day and month of a person's birth is known, but not the year."
                },
                "birthYear": {
                    "meta:xdmType": "short",
                    "type": "integer",
                    "minimum": 1,
                    "maximum": 32767,
                    "title": "Birth year",
                    "description": "The year a person was born including the century, for example, 1983.  This field should be used when only the person's age is known, not the full birth date."
                },
                "gender": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "title": "Gender",
                    "description": "Gender identity of the person.\n",
                    "enum": [
                        "male",
                        "female",
                        "not_specified",
                        "non_specific"
                    ],
                    "meta:enum": {
                        "male": "Male",
                        "female": "Female",
                        "not_specified": "Not Specified",
                        "non_specific": "Non-specific"
                    },
                    "default": "not_specified"
                },
                "maritalStatus": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "title": "Marital Status",
                    "description": "Describes a person's relationship with a significant other.",
                    "enum": [
                        "married",
                        "single",
                        "divorced",
                        "widowed",
                        "not_specified"
                    ],
                    "meta:enum": {
                        "divorced": "Divorced",
                        "not_specified": "Not Specified",
                        "married": "Married",
                        "single": "Single",
                        "widowed": "Widowed"
                    },
                    "default": "not_specified"
                },
                "name": {
                    "title": "Full name",
                    "description": "The person's full name.",
                    "meta:referencedFrom": [
                        "https://ns.adobe.com/xdm/context/person-name"
                    ],
                    "type": "object",
                    "meta:xdmType": "object",
                    "properties": {
                        "courtesyTitle": {
                            "type": "string",
                            "meta:xdmType": "string",
                            "title": "Courtesy title",
                            "description": "Normally an abbreviation of a persons title, honorific, or salutation. The `courtesyTitle` is used in front of full or last name in opening texts. For example, Mr. Miss. or Dr."
                        },
                        "firstName": {
                            "type": "string",
                            "meta:xdmType": "string",
                            "title": "First name",
                            "description": "The first segment of the name in the writing order most commonly accepted in the language of the name. In many cultures this is the preferred personal or given name. The `firstName` and `lastName` properties have been introduced to maintain compatibility with existing systems that model names in a simplified, non-semantic, and non-internationalizable way. Using `xdm:fullName` is always preferable."
                        },
                        "fullName": {
                            "type": "string",
                            "meta:xdmType": "string",
                            "title": "Full name",
                            "description": "The full name of the person, in writing order most commonly accepted in the language of the name."
                        },
                        "lastName": {
                            "type": "string",
                            "meta:xdmType": "string",
                            "title": "Last name",
                            "description": "The last segment of the name in the writing order most commonly accepted in the language of the name. In many cultures this is the inherited family name, surname, patronymic, or matronymic name. The `firstName` and `lastName` properties have been introduced to maintain compatibility with existing systems that model names in a simplified, non-semantic, and non-internationalizable way. Using `xdm:fullName` is always preferable."
                        },
                        "middleName": {
                            "type": "string",
                            "meta:xdmType": "string",
                            "title": "Middle name",
                            "description": "Middle, alternative, or additional names supplied between the first name and last name."
                        },
                        "suffix": {
                            "type": "string",
                            "meta:xdmType": "string",
                            "title": "Suffix",
                            "description": "A group of letters provided after a person's name to provide additional information. The `suffix` is used at the end of someones name. For example Jr., Sr., M.D., PhD, I, II, III, etc."
                        }
                    }
                },
                "nationality": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "title": "Nationality",
                    "description": "The legal relationship between a person and their state represented using the ISO 3166-1 Alpha-2 code."
                },
                "taxId": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "title": "Tax ID",
                    "description": "The Tax / Fiscal ID of the person, e.g. the TIN in the US or the CIF/NIF in Spain.",
                    "meta:status": "deprecated"
                },
                "type": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "title": "Type",
                    "description": "The type of individual in different business contexts like B2C."
                }
            }
        }
```

+++

>[!ENDSHADEBOX]



>[!BEGINSHADEBOX]

**獲取身份的請求**

+++獲取可在映射步驟中使用的可用標識

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/idnamespace/identities' \ 
--header 'x-gw-ims-org-id: {ORG_ID}' \ 
--header 'x-api-key: {API_KEY}' \ 
--header 'x-sandbox-name: {SANDBOX_NAME}' \ 
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
```

+++

**回應**

+++ 查看要在輸入架構中使用的可用標識

響應返回在建立輸入模式時可以使用的標識。 請注意，此響應將返回 [標準](/help/identity-service/namespaces.md#standard) 和 [自定義](/help/identity-service/namespaces.md#manage-namespaces) 在Experience Platform中設定的標識命名空間。

```json
[
    {
        "updateTime": 1551688425455,
        "code": "CORE",
        "status": "ACTIVE",
        "description": "Adobe Audience Manger UUID",
        "id": 0,
        "createTime": 1551688425455,
        "idType": "COOKIE",
        "namespaceType": "Standard",
        "name": "CORE",
        "custom": false
    },
    {
        "updateTime": 1551688425455,
        "code": "ECID",
        "status": "ACTIVE",
        "description": "Adobe Experience Cloud ID",
        "id": 4,
        "createTime": 1551688425455,
        "idType": "COOKIE",
        "namespaceType": "Standard",
        "name": "ECID",
        "custom": false
    },
    {
        "updateTime": 1551688425455,
        "code": "AdCloud",
        "status": "ACTIVE",
        "description": "Adobe AdCloud - ID Syncing Partner",
        "id": 411,
        "createTime": 1551688425455,
        "idType": "COOKIE",
        "namespaceType": "Standard",
        "name": "AdCloud",
        "custom": false
    },
    {
        "updateTime": 1551688425455,
        "code": "Email_LC_SHA256",
        "status": "ACTIVE",
        "description": "Email addresses need to be hashed using SHA256 and lowercased. Please also note that leading and trailing spaces need to be trimmed before an email address is normalized. You won't be able to change this setting later",
        "id": 11,
        "createTime": 1551688425455,
        "idType": "Email",
        "namespaceType": "Standard",
        "name": "Emails (SHA256, lowercased)",
        "custom": false,
        "hashFunction": "SHA256",
        "transform": "lowercase"
    },
    {
        "updateTime": 1597996026101,
        "code": "Phone_E.164",
        "status": "ACTIVE",
        "description": "Namespace for raw phone numbers in E.164 format. + sign is required",
        "id": 17,
        "createTime": 1597996026101,
        "idType": "Phone",
        "namespaceType": "Standard",
        "name": "Phone (E.164)",
        "custom": false
    },
    {
        "updateTime": 1551688425455,
        "code": "GAID",
        "status": "ACTIVE",
        "description": "This datasource is associated to a Google Ad ID",
        "id": 20914,
        "createTime": 1551688425455,
        "idType": "DEVICE",
        "namespaceType": "Standard",
        "name": "Google Ad ID (GAID)",
        "custom": false
    },
    {
        "updateTime": 1476993749000,
        "code": "IDFA",
        "status": "ACTIVE",
        "description": "Apple ID for Advertisers. See: https://support.apple.com/en-us/HT202074 for more info.",
        "id": 20915,
        "createTime": 1476993749000,
        "idType": "DEVICE",
        "namespaceType": "Standard",
        "name": "Apple IDFA (ID for Advertisers)",
        "custom": false
    },
    {
        "updateTime": 1551688425455,
        "code": "AAID",
        "status": "ACTIVE",
        "description": "Adobe Analytics (Legacy ID)",
        "id": 10,
        "createTime": 1551688425455,
        "idType": "COOKIE",
        "namespaceType": "Standard",
        "name": "Adobe Analytics (Legacy ID)",
        "custom": false
    },
    {
        "updateTime": 1551688425455,
        "code": "Email",
        "status": "ACTIVE",
        "description": "Email",
        "id": 6,
        "createTime": 1551688425455,
        "idType": "Email",
        "namespaceType": "Standard",
        "name": "Email",
        "custom": false
    },
    {
        "updateTime": 1551688425455,
        "code": "WAID",
        "status": "ACTIVE",
        "description": "Windows AID",
        "id": 8,
        "createTime": 1551688425455,
        "idType": "DEVICE",
        "namespaceType": "Standard",
        "name": "Windows AID",
        "custom": false
    },
    {
        "updateTime": 1551688425455,
        "code": "TNTID",
        "status": "ACTIVE",
        "description": "Adobe Target (TNTID)",
        "id": 9,
        "createTime": 1551688425455,
        "idType": "COOKIE",
        "namespaceType": "Standard",
        "name": "TNTID",
        "custom": false
    },
    {
        "updateTime": 1556676464714,
        "code": "Google",
        "status": "ACTIVE",
        "id": 771,
        "createTime": 1556676464714,
        "idType": "COOKIE",
        "namespaceType": "Integration",
        "name": "Google",
        "custom": false
    },
    {
        "updateTime": 1604597776019,
        "code": "Phone_SHA256_E.164",
        "status": "ACTIVE",
        "description": "Phone numbers need to be hashed using SHA256 without any dashes. Hash should be completed by customers on raw phone numbers in E.164 format. Please note that some destinations may have different phone number formatting requirements. Refer to documentation or consult your Adobe representative",
        "id": 18,
        "createTime": 1604597776019,
        "idType": "Phone",
        "namespaceType": "Standard",
        "name": "Phone (SHA256_E.164)",
        "custom": false,
        "hashFunction": "SHA256"
    },
    {
        "updateTime": 1604597776019,
        "code": "Phone_SHA256",
        "status": "ACTIVE",
        "description": "Remove symbols, letters, and any leading zeroes before hashing. Prefix the country code before hashing. Please note that some destinations may have different phone number formatting requirements. Refer to documentation or consult your Adobe representative",
        "id": 15,
        "createTime": 1597995542594,
        "idType": "Phone",
        "namespaceType": "Standard",
        "name": "Phone (SHA256)",
        "custom": false,
        "hashFunction": "SHA256"
    },
    {
        "updateTime": 1551688425455,
        "code": "Phone",
        "status": "ACTIVE",
        "description": "Phone",
        "id": 7,
        "createTime": 1551688425455,
        "idType": "PHONE_NUMBER",
        "namespaceType": "Standard",
        "name": "Phone",
        "custom": false
    }
]
```

+++

>[!ENDSHADEBOX]

接下來，您需要從上面複製響應並使用它建立輸入架構。 您可以從上面的響應複製整個JSON響應，並將其放入 `jsonSchema` 對象。

>[!BEGINSHADEBOX]

**請求建立輸入架構**

+++建立輸入模式 — 請求

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/conversion/schemas/' \ 
--header 'x-gw-ims-org-id: {ORG_ID}' \ 
--header 'x-api-key: {API_KEY}' \ 
--header 'x-sandbox-name: {SANDBOX_NAME}' \ 
--header 'Authorization: Bearer {ACCESS_TOKEN}' \ 
--header 'Content-Type: application/json' \ 
--data-raw '{
    "name":"Sample Schema for Flow Mapping",
    "jsonSchema":{...insert response from union schema response here}
    '
```

+++

**回應**

+++建立輸入模式 — 響應

```json
{
   "id":"8db56468c2ab475dbf17c2621f92c0f8",
   "version":0,
   "jsonSchema":{
      "title":"XDM Individual Profile",
      "description":"An XDM Individual Profile forms a singular representation of the attributes and interests of both identified and partially-identified individuals. Less-identified profiles may contain only anonymous behavioral signals, such as browser cookies, while highly-identified profiles may contain detailed personal information such as name, date of birth, location, and email address. As a profile grows, it becomes a robust repository of personal information, identification information, contact details, and communication preferences for an individual.",
      "type":"object",
      "properties":{ // this section returns the contents that you have added to the jsonSchema object in the request
      }
   }
}
```

+++

>[!ENDSHADEBOX]

響應中的ID表示已建立的輸入架構的唯一標識符。 從響應複製ID，因為您將在稍後的步驟中重新使用它。

### 建立輸出架構

接下來，必須設定導出的輸出架構。 首先，您需要查找並檢查現有合作夥伴架構。

>[!BEGINSHADEBOX]

**要求**

+++請求獲取輸出架構的夥伴架構

請注意，下面的示例使用 `connection spec ID` 為AmazonS3。 請將此值替換為特定於目標的連接規範ID。

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/4fce964d-3f37-408f-9778-e597338a21ee' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
```

+++

**使用示例架構的響應**

Inspect執行上述呼叫時您獲得的響應。 您需要深入到響應以查找對象 `targetSpec.attributes.partnerSchema.jsonSchema`

+++ 響應獲取輸出架構的夥伴架構

```json
{
   "title":"defaultschema",
   "type":"object",
   "properties":{
      "attributes":{
         "type":"object",
         "meta:xdmType":"map",
         "additionalProperties":{
            "type":"object",
            "properties":{
               "value":{
                  "type":"string",
                  "title":"Value"
               }
            },
            "meta:xdmType":"object"
         }
      },
      "identityMap":{
         "type":"object",
         "meta:xdmField":"xdm:identityMap",
         "meta:xdmType":"map",
         "additionalProperties":{
            "type":"array",
            "items":{
               "type":"object",
               "properties":{
                  "id":{
                     "type":"string",
                     "title":"Identifier",
                     "description":"Identity of the consumer in the related namespace.",
                     "meta:xdmType":"string",
                     "meta:xdmField":"xdm:id"
                  },
                  "primary":{
                     "type":"boolean",
                     "title":"Primary",
                     "default":false,
                     "description":"Indicates this identity is the preferred identity. Is used as a hint to help systems better organize how identities are queried.",
                     "meta:xdmType":"boolean",
                     "meta:xdmField":"xdm:primary"
                  },
                  "authenticatedState":{
                     "enum":[
                        "ambiguous",
                        "authenticated",
                        "loggedOut"
                     ],
                     "type":"string",
                     "default":"ambiguous",
                     "meta:enum":{
                        "ambiguous":"Ambiguous",
                        "loggedOut":"User was identified by a login action at some point of time previously, but is not currently logged in.",
                        "authenticated":"User identified by a login or similar action that was valid at the time of the event observation."
                     },
                     "description":"The state this identity is authenticated as for this observed ExperienceEvent.",
                     "meta:xdmType":"string",
                     "meta:xdmField":"xdm:authenticatedState"
                  }
               },
               "meta:xdmType":"object",
               "meta:referencedFrom":"https://ns.adobe.com/xdm/context/identityitem"
            },
            "meta:xdmType":"array"
         }
      },
      "segmentMembership":{
         "title":"Segment membership map",
         "type":"object",
         "meta:xdmField":"xdm:segmentMembership",
         "meta:xdmType":"map",
         "additionalProperties":{
            "type":"object",
            "title":"Segment membership per namespace",
            "meta:xdmType":"map",
            "additionalProperties":{
               "type":"object",
               "properties":{
                  "status":{
                     "enum":[
                        "realized",
                        "exited"
                     ],
                     "type":"string",
                     "title":"Status",
                     "default":"realized",
                     "meta:enum":{
                        "exited":"Entity is exiting the segment.",
                        "realized":"Entity is entering the segment."
                     },
                     "description":"Is the segment participation realized as part of the current request.",
                     "meta:xdmType":"string",
                     "meta:xdmField":"xdm:status"
                  },
                  "payload":{
                     "type":"object",
                     "title":"Payload",
                     "required":[
                        "payloadType"
                     ],
                     "properties":{
                        "payloadType":{
                           "enum":[
                              "boolean",
                              "number",
                              "propensity",
                              "string"
                           ],
                           "type":"string",
                           "title":"Payload Type",
                           "meta:enum":{
                              "number":"Number",
                              "string":"String",
                              "boolean":"Boolean",
                              "propensity":"Propensity"
                           },
                           "description":"The type of payload.",
                           "meta:xdmType":"string",
                           "meta:xdmField":"xdm:payloadType"
                        },
                        "payloadNumberValue":{
                           "type":"number",
                           "title":"Value",
                           "description":"The number.",
                           "meta:xdmType":"number",
                           "meta:xdmField":"xdm:payloadNumberValue"
                        },
                        "payloadStringValue":{
                           "type":"string",
                           "title":"Value",
                           "description":"The string value.",
                           "meta:xdmType":"string",
                           "meta:xdmField":"xdm:payloadStringValue"
                        },
                        "payloadBooleanValue":{
                           "type":"boolean",
                           "title":"Value",
                           "description":"The boolean value.",
                           "meta:xdmType":"boolean",
                           "meta:xdmField":"xdm:payloadBooleanValue"
                        },
                        "payloadPropensityValue":{
                           "type":"number",
                           "title":"Value",
                           "maximum":1,
                           "description":"The propensity.",
                           "meta:xdmType":"number",
                           "meta:xdmField":"xdm:payloadPropensityValue",
                           "exclusiveMinimum":0
                        }
                     },
                     "description":"Values that are directly related with the segment realization. This payload exists with the same 'validUntil' as the segment realization. Note that the intention is that exactly one payload value be included, as indicated by the payload type. This was originally modeled using 'oneOf', but due to limitations in our tooling that was removed. This more semantically meaningful representation will be re-introduced in the future.",
                     "meta:xdmType":"object",
                     "meta:xdmField":"xdm:payload"
                  },
                  "version":{
                     "type":"string",
                     "title":"Version",
                     "description":"The version of the segment definition used in this segment assertion. Version can be omitted in audience lists when all memberships versions are the same.",
                     "meta:xdmType":"string",
                     "meta:xdmField":"xdm:version"
                  },
                  "segmentID":{
                     "type":"object",
                     "title":"Segment ID",
                     "properties":{
                        "_id":{
                           "type":"string",
                           "title":"Identifier",
                           "format":"uri-reference",
                           "description":"Identity of the segment in the related namespace.",
                           "meta:xdmType":"string",
                           "meta:xdmField":"@id"
                        },
                        "xid":{
                           "type":"string",
                           "title":"Experience identifier",
                           "description":"When present, this value represents a cross-namespace identifier that is unique across all namespace-scoped identifiers in all namespaces.",
                           "meta:xdmType":"string",
                           "meta:xdmField":"xdm:xid"
                        },
                        "namespace":{
                           "type":"object",
                           "title":"Namespace",
                           "required":[
                              "code"
                           ],
                           "properties":{
                              "code":{
                                 "type":"string",
                                 "title":"Code",
                                 "description":"The code is a human readable identifier for the namespace and can be used to request the technical namespace id which is used for identity graph processing.",
                                 "meta:xdmType":"string",
                                 "meta:xdmField":"xdm:code"
                              }
                           },
                           "description":"The namespace associated with the `xid` attribute.",
                           "meta:xdmType":"object",
                           "meta:xdmField":"xdm:namespace",
                           "meta:referencedFrom":"https://ns.adobe.com/xdm/context/namespace"
                        }
                     },
                     "description":"The identity of the segment or snapshot definition in with the domain of the specific system that processes that type of segment. Deprecated.",
                     "meta:status":"deprecated",
                     "meta:xdmType":"object",
                     "meta:xdmField":"xdm:segmentID",
                     "meta:referencedFrom":"https://ns.adobe.com/xdm/context/segmentidentity"
                  },
                  "validUntil":{
                     "type":"string",
                     "title":"Valid until",
                     "format":"date-time",
                     "description":"The timestamp for when the segment assertion should no longer be assumed to be valid and should either be ignored or revalidated.",
                     "meta:xdmType":"date-time",
                     "meta:xdmField":"xdm:validUntil"
                  },
                  "profileStitchID":{
                     "type":"object",
                     "properties":{
                        "_id":{
                           "type":"string",
                           "title":"Identifier",
                           "format":"uri-reference",
                           "description":"Identity of the profile stitch in the related namespace.",
                           "meta:xdmType":"string",
                           "meta:xdmField":"@id"
                        },
                        "xid":{
                           "type":"string",
                           "title":"Experience identifier",
                           "description":"When present, this value represents a cross-namespace identifier that is unique across all namespace-scoped identifiers in all namespaces.",
                           "meta:xdmType":"string",
                           "meta:xdmField":"xdm:xid"
                        },
                        "namespace":{
                           "type":"object",
                           "title":"Namespace",
                           "required":[
                              "code"
                           ],
                           "properties":{
                              "code":{
                                 "type":"string",
                                 "title":"Code",
                                 "description":"The code is a human readable identifier for the namespace and can be used to request the technical namespace id which is used for identity graph processing.",
                                 "meta:xdmType":"string",
                                 "meta:xdmField":"xdm:code"
                              }
                           },
                           "description":"The namespace associated with the `xid` attribute.",
                           "meta:xdmType":"object",
                           "meta:xdmField":"xdm:namespace",
                           "meta:referencedFrom":"https://ns.adobe.com/xdm/context/namespace"
                        }
                     },
                     "meta:xdmType":"object",
                     "meta:xdmField":"xdm:profileStitchID",
                     "meta:referencedFrom":"https://ns.adobe.com/xdm/context/profileStitchIdentity"
                  },
                  "lastQualificationTime":{
                     "type":"string",
                     "title":"Last qualification time",
                     "format":"date-time",
                     "description":"The timestamp when the assertion of segment membership was made.",
                     "meta:xdmType":"date-time",
                     "meta:xdmField":"xdm:lastQualificationTime"
                  }
               },
               "meta:xdmType":"object",
               "meta:referencedFrom":"https://ns.adobe.com/xdm/context/segmentmembership"
            }
         }
      }
   }
}
```

+++

>[!ENDSHADEBOX]

接下來，需要建立輸出架構。 複製您上面的JSON響應並將其貼上到 `jsonSchema` 對象。

>[!BEGINSHADEBOX]

**要求**

+++建立輸出架構 — 請求

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/conversion/schemas' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer TOKEN' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Sample Schema for Flow Mapping",
"jsonSchema":{...insert JSON from the response above here}
}
'
```

+++

**回應**

+++建立輸出架構 — 響應

```json
{
    "id": "2f4fd51934c1409fb1d8207dd9f43dc9",
    "version": 0,
    "jsonSchema": {
        "title": "defaultschema",
        "type": "object",
        "properties": {
            "identityMap": {
                "type": "object",
                "meta:xdmField": "xdm:identityMap",
                "meta:xdmType": "map",
                "additionalProperties": {
                    "meta:xdmType": "array",
                    "items": {
                        "meta:referencedFrom": "https://ns.adobe.com/xdm/context/identityitem",
                        "properties": {
                            "primary": {
                                "meta:xdmField": "xdm:primary",
                                "meta:xdmType": "boolean",
                                "description": "Indicates this identity is the preferred identity. Is used as a hint to help systems better organize how identities are queried.",
                                "default": false,
                                "type": "boolean",
                                "title": "Primary"
                            },
                            "id": {
                                "meta:xdmField": "xdm:id",
                                "meta:xdmType": "string",
                                "description": "Identity of the consumer in the related namespace.",
                                "type": "string",
                                "title": "Identifier"
                            },
                            "authenticatedState": {
                                "meta:xdmField": "xdm:authenticatedState",
                                "meta:xdmType": "string",
                                "meta:enum": {
                                    "loggedOut": "User was identified by a login action at some point of time previously, but is not currently logged in.",
                                    "authenticated": "User identified by a login or similar action that was valid at the time of the event observation.",
                                    "ambiguous": "Ambiguous"
                                },
                                "enum": [
                                    "ambiguous",
                                    "authenticated",
                                    "loggedOut"
                                ],
                                "default": "ambiguous",
                                "type": "string",
                                "description": "The state this identity is authenticated as for this observed ExperienceEvent."
                            }
                        },
                        "meta:xdmType": "object",
                        "type": "object"
                    },
                    "type": "array"
                }
            },
            "segmentMembership": {
                "title": "Segment membership map",
                "type": "object",
                "meta:xdmField": "xdm:segmentMembership",
                "meta:xdmType": "map",
                "additionalProperties": {
                    "additionalProperties": {
                        "meta:referencedFrom": "https://ns.adobe.com/xdm/context/segmentmembership",
                        "properties": {
                            "version": {
                                "meta:xdmField": "xdm:version",
                                "meta:xdmType": "string",
                                "description": "The version of the segment definition used in this segment assertion. Version can be omitted in audience lists when all memberships versions are the same.",
                                "type": "string",
                                "title": "Version"
                            },
                            "validUntil": {
                                "meta:xdmField": "xdm:validUntil",
                                "meta:xdmType": "date-time",
                                "description": "The timestamp for when the segment assertion should no longer be assumed to be valid and should either be ignored or revalidated.",
                                "format": "date-time",
                                "type": "string",
                                "title": "Valid until"
                            },
                            "status": {
                                "meta:xdmField": "xdm:status",
                                "meta:xdmType": "string",
                                "meta:enum": {
                                    "exited": "Entity is exiting the segment.",
                                    "realized": "Entity is entering the segment."
                                },
                                "enum": [
                                    "realized",
                                    "exited"
                                ],
                                "default": "realized",
                                "description": "Is the segment participation realized as part of the current request.",
                                "type": "string",
                                "title": "Status"
                            },
                            "segmentID": {
                                "meta:xdmField": "xdm:segmentID",
                                "meta:referencedFrom": "https://ns.adobe.com/xdm/context/segmentidentity",
                                "properties": {
                                    "xid": {
                                        "meta:xdmField": "xdm:xid",
                                        "meta:xdmType": "string",
                                        "description": "When present, this value represents a cross-namespace identifier that is unique across all namespace-scoped identifiers in all namespaces.",
                                        "type": "string",
                                        "title": "Experience identifier"
                                    },
                                    "namespace": {
                                        "meta:xdmField": "xdm:namespace",
                                        "required": [
                                            "code"
                                        ],
                                        "meta:referencedFrom": "https://ns.adobe.com/xdm/context/namespace",
                                        "properties": {
                                            "code": {
                                                "meta:xdmField": "xdm:code",
                                                "meta:xdmType": "string",
                                                "description": "The code is a human readable identifier for the namespace and can be used to request the technical namespace id which is used for identity graph processing.",
                                                "type": "string",
                                                "title": "Code"
                                            }
                                        },
                                        "meta:xdmType": "object",
                                        "type": "object",
                                        "description": "The namespace associated with the `xid` attribute.",
                                        "title": "Namespace"
                                    },
                                    "_id": {
                                        "meta:xdmField": "@id",
                                        "meta:xdmType": "string",
                                        "description": "Identity of the segment in the related namespace.",
                                        "format": "uri-reference",
                                        "type": "string",
                                        "title": "Identifier"
                                    }
                                },
                                "meta:xdmType": "object",
                                "type": "object",
                                "description": "The identity of the segment or snapshot definition in with the domain of the specific system that processes that type of segment. Deprecated.",
                                "meta:status": "deprecated",
                                "title": "Segment ID"
                            },
                            "profileStitchID": {
                                "meta:xdmField": "xdm:profileStitchID",
                                "meta:referencedFrom": "https://ns.adobe.com/xdm/context/profileStitchIdentity",
                                "properties": {
                                    "xid": {
                                        "meta:xdmField": "xdm:xid",
                                        "meta:xdmType": "string",
                                        "description": "When present, this value represents a cross-namespace identifier that is unique across all namespace-scoped identifiers in all namespaces.",
                                        "type": "string",
                                        "title": "Experience identifier"
                                    },
                                    "namespace": {
                                        "meta:xdmField": "xdm:namespace",
                                        "required": [
                                            "code"
                                        ],
                                        "meta:referencedFrom": "https://ns.adobe.com/xdm/context/namespace",
                                        "properties": {
                                            "code": {
                                                "meta:xdmField": "xdm:code",
                                                "meta:xdmType": "string",
                                                "description": "The code is a human readable identifier for the namespace and can be used to request the technical namespace id which is used for identity graph processing.",
                                                "type": "string",
                                                "title": "Code"
                                            }
                                        },
                                        "meta:xdmType": "object",
                                        "type": "object",
                                        "description": "The namespace associated with the `xid` attribute.",
                                        "title": "Namespace"
                                    },
                                    "_id": {
                                        "meta:xdmField": "@id",
                                        "meta:xdmType": "string",
                                        "description": "Identity of the profile stitch in the related namespace.",
                                        "format": "uri-reference",
                                        "type": "string",
                                        "title": "Identifier"
                                    }
                                },
                                "meta:xdmType": "object",
                                "type": "object"
                            },
                            "payload": {
                                "meta:xdmField": "xdm:payload",
                                "meta:xdmType": "object",
                                "required": [
                                    "payloadType"
                                ],
                                "properties": {
                                    "payloadType": {
                                        "meta:xdmField": "xdm:payloadType",
                                        "meta:xdmType": "string",
                                        "description": "The type of payload.",
                                        "meta:enum": {
                                            "string": "String",
                                            "propensity": "Propensity",
                                            "number": "Number",
                                            "boolean": "Boolean"
                                        },
                                        "enum": [
                                            "boolean",
                                            "number",
                                            "propensity",
                                            "string"
                                        ],
                                        "type": "string",
                                        "title": "Payload Type"
                                    },
                                    "payloadStringValue": {
                                        "meta:xdmField": "xdm:payloadStringValue",
                                        "meta:xdmType": "string",
                                        "description": "The string value.",
                                        "type": "string",
                                        "title": "Value"
                                    },
                                    "payloadPropensityValue": {
                                        "meta:xdmField": "xdm:payloadPropensityValue",
                                        "meta:xdmType": "number",
                                        "maximum": 1,
                                        "exclusiveMinimum": 0,
                                        "description": "The propensity.",
                                        "type": "number",
                                        "title": "Value"
                                    },
                                    "payloadNumberValue": {
                                        "meta:xdmField": "xdm:payloadNumberValue",
                                        "meta:xdmType": "number",
                                        "description": "The number.",
                                        "type": "number",
                                        "title": "Value"
                                    },
                                    "payloadBooleanValue": {
                                        "meta:xdmField": "xdm:payloadBooleanValue",
                                        "meta:xdmType": "boolean",
                                        "description": "The boolean value.",
                                        "type": "boolean",
                                        "title": "Value"
                                    }
                                },
                                "type": "object",
                                "description": "Values that are directly related with the segment realization. This payload exists with the same 'validUntil' as the segment realization. Note that the intention is that exactly one payload value be included, as indicated by the payload type. This was originally modeled using 'oneOf', but due to limitations in our tooling that was removed. This more semantically meaningful representation will be re-introduced in the future.",
                                "title": "Payload"
                            },
                            "lastQualificationTime": {
                                "meta:xdmField": "xdm:lastQualificationTime",
                                "meta:xdmType": "date-time",
                                "description": "The timestamp when the assertion of segment membership was made.",
                                "format": "date-time",
                                "type": "string",
                                "title": "Last qualification time"
                            }
                        },
                        "meta:xdmType": "object",
                        "type": "object"
                    },
                    "meta:xdmType": "map",
                    "type": "object",
                    "title": "Segment membership per namespace"
                }
            },
            "attributes": {
                "type": "object",
                "meta:xdmType": "map",
                "additionalProperties": {
                    "properties": {
                        "value": {
                            "type": "string",
                            "title": "Value"
                        }
                    },
                    "meta:xdmType": "object",
                    "type": "object"
                }
            },
            "firstName": {
                "title": "firstName",
                "type": "string"
            },
            "Email": {
                "title": "Email",
                "type": "array",
                "items": {
                    "type": "object",
                    "properties": {
                        "id": {
                            "title": "id",
                            "type": "string",
                            "meta:xdmType": "string"
                        }
                    },
                    "meta:xdmType": "object"
                },
                "meta:xdmType": "array"
            }
        }
    }
}
```

響應中的ID表示已建立的輸入架構的唯一標識符。 從響應複製ID，因為您將在稍後的步驟中重新使用它。

>[!ENDSHADEBOX]

### 建立映射集 {#create-mapping-set}

接下來，使用 [資料準備API](https://developer.adobe.com/experience-platform-apis/references/data-prep/#tag/Mapping-sets/operation/createMappingSet) 使用輸入模式ID、輸出模式ID和所需欄位映射建立映射集。

>[!BEGINSHADEBOX]

**要求**

+++建立映射集 — 請求

>[!IMPORTANT]
>
>* 在下面顯示的映射對象中， `destination` 參數不接受點 `"."`。 例如，您需要使用配置示例中突出顯示的personalEmail_address或segmentMembership_status。
>* 當源屬性是標識屬性並包含點時，會出現一種特定情況。 在這種情況下，該屬性需要用 `//`，如下所示。
>* 另請注意，即使下面的示例配置包括 `Email` 和 `Phone_E.164`，您只能導出每個資料流的一個標識屬性。


```shell {line-numbers="true" start-line="1" highlight="16-38"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer TOKEN' \
--header 'Content-Type: application/json' \
--data-raw '{
    "inputSchema": {
        "id": "81d7fc5376e54eb58d5186fd30d5a8c9"
    },  
    "outputSchema": {
        "id": "2f4fd51934c1409fb1d8207dd9f43dc9"
    },
    "mappings": [
        {
            "destination": "firstName",
            "source": "person.name.firstName",
            "sourceType": "ATTRIBUTE"
        }, 
        {
            "destination": "Email",
            "source": "identityMap.Email",
            "sourceType": "ATTRIBUTE"
        },
        {
            "destination": "Phone_E_164",
            "source": "identityMap.Phone_E//.164",
            "sourceType": "ATTRIBUTE"
        },
        {
            "destination": "personalEmail_address",
            "source": "personalEmail.address",
            "sourceType": "ATTRIBUTE"
        },        
        {
            "destination": "segmentMembership_status",
            "source": "segmentMembership.ups.seg_id.status",
            "sourceType": "ATTRIBUTE"
        }        
    ],
    "xdmVersion": "1.0"
}'
```

+++

**回應**

+++ 建立映射集 — 響應

```json
{
    "id": "5f0031f8ccd4444dac9c5c391389e9e8",
    "version": 0,
    "createdDate": 1678999005197,
    "modifiedDate": 1678999005197,
    "createdBy": "example@AdobeID",
    "modifiedBy": "example@AdobeID"
}
```

+++

>[!ENDSHADEBOX]

請注意映射集的ID，因為在下一步中需要該ID來使用映射集ID更新現有資料流。

接下來，獲取要更新的資料流的ID。

>[!BEGINSHADEBOX]

請參閱 [檢索目標資料流的詳細資訊](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Dataflows/operation/getFlowById) 的子菜單。

>[!ENDSHADEBOX]

最後，您需要將資料流與剛剛建立的映射集資訊PATCH。

>[!BEGINSHADEBOX]

**要求**

+++ 使用映射集資訊更新資料流 — 請求

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/df8245a8-dd8f-42da-a04a-2d3a92654d9e' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'If-Match: ETAG_HERE' \
--data-raw '[
   {
      "op":"ADD",
      "path":"/transformations/0/params/profileMapping",
      "value":{
         "mappingId":"304ca6a2fff244949c956cad1cd9eae6",
         "mappingVersion":0
      }
   }
]'
```

+++

**回應**

+++ 使用映射集資訊更新資料流 — 響應

來自流服務API的響應返回已更新資料流的ID。

```json
{
    "id": "1c246ae4-ba0d-43cd-a0ec-f16fe0a56b55",
    "etag": "\"1500c67f-0000-0200-0000-64137ee00000\""
}
```

+++

>[!ENDSHADEBOX]

## 進行其他資料流更新 {#other-dataflow-updates}

![激活段的步驟，突出顯示用戶所處的當前步驟](/help/destinations/assets/api/file-based-segment-export/step7.png)

要對資料流進行任何更新，請使用 `PATCH` operation。例如，您可以更新資料流以選擇欄位作為強制鍵或重複資料消除鍵。

### 添加強制鍵 {#add-mandatory-key}

添加 [強制密鑰](/help/destinations/ui/activate-batch-profile-destinations.md#mandatory-attributes)，請參閱下面的請求和響應示例

>[!BEGINSHADEBOX]

**要求**

+++添加標識作為必填欄位 — 請求

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/runs?property=flowId==eb54b3b3-3949-4f12-89c8-64eafaba858f' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '
[
  {
    "op": "add",
    "path": "/transformations/0/params/mandatoryFields",
    "value": [
      "GAID"
    ]
  }
]'
```

+++

+++將XDM屬性添加為必填欄位 — 請求

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/runs?property=flowId==eb54b3b3-3949-4f12-89c8-64eafaba858f' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '
[
  {
    "op": "add",
    "path": "/transformations/0/params/mandatoryFields",
    "value": [
      "GAID"
    ]
  }
]'
```

+++

**回應**

+++添加必填欄位 — 響應

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!ENDSHADEBOX]

### 添加重複資料消除密鑰 {#add-deduplication-key}

添加 [重複資料消除密鑰](/help/destinations/ui/activate-batch-profile-destinations.md#deduplication-keys)，請參閱下面的請求和響應示例

>[!BEGINSHADEBOX]

**要求**

+++添加標識作為重複資料消除密鑰 — 請求

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/runs?property=flowId==eb54b3b3-3949-4f12-89c8-64eafaba858f' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '
[
  {
    "op": "add",
    "path": "/transformations/0/params/primaryFields",
    "value": [
      {
        "identityNamespace": "GAID",
        "fieldType": "IDENTITY"
      }
    ]
  }
]'
```

+++

+++添加XDM屬性作為重複資料消除鍵 — 請求

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/runs?property=flowId==eb54b3b3-3949-4f12-89c8-64eafaba858f' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '
[
  {
    "op": "add",
    "path": "/transformations/0/params/primaryFields",
    "value": [
      {
        "identityNamespace": "GAID",
        "fieldType": "IDENTITY"
      }
    ]
  }
]'
```

+++

**回應**

+++添加必填欄位 — 響應

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!ENDSHADEBOX]

## 驗證資料流（獲取資料流運行） {#get-dataflow-runs}

![激活段的步驟，突出顯示用戶所處的當前步驟](/help/destinations/assets/api/file-based-segment-export/step8.png)

要檢查資料流的執行，請使用「資料流運行API」：

>[!BEGINSHADEBOX]

**要求**

+++獲取資料流運行 — 請求

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/runs?property=flowId==eb54b3b3-3949-4f12-89c8-64eafaba858f' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw ''
```

+++

**回應**

+++獲取資料流運行 — 響應

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

您可以找到 [Dataflow返回的各種參數運行API](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Dataflow-runs/operation/getFlowRuns) 的FTP伺服器連接設定。

## API錯誤處理 {#api-error-handling}

本教程中的API端點遵循一般Experience PlatformAPI錯誤消息原則。 請參閱 [API狀態代碼](/help/landing/troubleshooting.md#api-status-codes) 和 [請求標頭錯誤](/help/landing/troubleshooting.md#request-header-errors) 有關解釋錯誤響應的詳細資訊，請參閱「Platform troubleshooting guide（平台故障排除指南）」。

## 後續步驟 {#next-steps}

按照本教程，您已成功將平台連接到您首選的雲儲存目標之一，並將資料流設定到相應的目標以導出段。 有關更多詳細資訊，請參閱以下頁，如如何使用流服務API編輯現有資料流：

* [目的地概觀](../home.md)
* [目標目錄概述](../catalog/overview.md)
* [使用流服務API更新目標資料流](../api/update-destination-dataflows.md)
