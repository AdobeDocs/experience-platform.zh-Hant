---
title: 加密的資料擷取
description: 瞭解如何使用API透過雲端儲存批次來源內嵌加密的檔案。
exl-id: 83a7a154-4f55-4bf0-bfef-594d5d50f460
source-git-commit: adb48b898c85561efb2d96b714ed98a0e3e4ea9b
workflow-type: tm+mt
source-wordcount: '1736'
ht-degree: 3%

---

# 加密的資料擷取

您可以使用雲端儲存批次來源，將加密資料檔案擷取至Adobe Experience Platform。 透過加密的資料擷取，您可以運用非對稱的加密機制，將批次資料安全地傳輸至Experience Platform。 目前，支援的非對稱加密機製為PGP和GPG。

加密的資料擷取程式如下：

1. [使用Experience PlatformAPI建立加密金鑰組](#create-encryption-key-pair)。 加密金鑰組由私密金鑰和公開金鑰組成。 建立後，您可以複製或下載公開金鑰，以及其對應的公開金鑰ID和到期時間。 在此過程中，私密金鑰將由Experience Platform儲存在安全的儲存庫中。 **注意：**&#x200B;回應中的公開金鑰是Base64編碼的，必須在使用之前解密。
2. 使用公開金鑰來加密您要擷取的資料檔案。
3. 將加密檔案放入雲端儲存空間。
4. 加密檔案準備就緒後，[為您的雲端儲存空間來源](#create-a-dataflow-for-encrypted-data)建立來源連線和資料流。 在流程建立步驟期間，您必須提供`encryption`引數並包含您的公開金鑰ID。
5. Experience Platform會從安全儲存庫中擷取私密金鑰，以在擷取資料時解密資料。

>[!IMPORTANT]
>
>單一加密檔案的大小上限為1 GB。 例如，您可以在單一資料流執行中擷取2 GB的資料，但該資料中的任何個別檔案都不能超過1 GB。

本檔案提供如何產生加密金鑰組以加密您的資料，以及使用雲端儲存空間來源將加密資料擷取到Experience Platform的步驟。

## 快速入門 {#get-started}

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

* [來源](../../home.md)：Experience Platform允許從各種來源擷取資料，同時讓您能夠使用Platform服務來建構、加標籤以及增強傳入的資料。
   * [雲端儲存空間來源](../api/collect/cloud-storage.md)：建立資料流，將批次資料從您的雲端儲存空間來源帶入Experience Platform。
* [沙箱](../../../sandboxes/home.md)：Experience Platform提供的虛擬沙箱可將單一Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱[Platform API快速入門](../../../landing/api-guide.md)的指南。

### 加密檔案支援的副檔名 {#supported-file-extensions-for-encrypted-files}

加密檔案支援的副檔名清單為：

* .csv
* .tsv
* .json
* .parquet
* .csv.gpg
* .tsv.gpg
* .json.gpg
* .parquet.gpg
* .csv.pgp
* .tsv.pgp
* .json.pgp
* .parquet.pgp
* .gpg
* .pgp

>[!NOTE]
>
>Adobe Experience Platform來源中的加密檔案擷取支援openPGP，而不支援任何特定的PGP專屬版本。

## 建立加密金鑰組 {#create-encryption-key-pair}

將加密資料擷取至Experience Platform的第一步，是透過向[!DNL Connectors] API的`/encryption/keys`端點發出POST要求來建立您的加密金鑰組。

**API格式**

```http
POST /data/foundation/connectors/encryption/keys
```

**要求**

+++檢視範例請求

下列要求會使用PGP加密演演算法產生加密金鑰組。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/encryption/keys' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
  -H 'x-sandbox-name: {{SANDBOX_NAME}}' \
  -H 'Content-Type: application/json' 
  -d '{
      "encryptionAlgorithm": "PGP",
      "params": {
          "passPhrase": "{{PASSPHRASE}}"
      }
  }'
```

| 參數 | 說明 |
| --- | --- |
| `encryptionAlgorithm` | 您使用的加密演演算法型別。 支援的加密型別為`PGP`和`GPG`。 |
| `params.passPhrase` | 密碼可為您的加密金鑰提供額外的保護層。 建立後，Experience Platform會將複雜密碼與公開金鑰儲存在不同的安全儲存庫中。 您必須提供非空白字串作為複雜密碼。 |

+++

**回應**

+++檢視範例回應

成功的回應會傳回Base64編碼的公開金鑰、公開金鑰ID，以及金鑰的到期時間。 到期時間會自動設定為產生金鑰日期後的180天。 到期時間目前無法設定。

```json
{
    ​"publicKey": "{PUBLIC_KEY}",
    ​"publicKeyId": "{PUBLIC_KEY_ID}",
    ​"expiryTime": "1684843168"
}
```

| 屬性 | 說明 |
| --- | --- |
| `publicKey` | 公開金鑰是用來加密雲端儲存空間中的資料。 此金鑰對應至在此步驟中建立的私密金鑰。 不過，私密金鑰會立即移至Experience Platform。 |
| `publicKeyId` | 公開金鑰ID可用來建立資料流，以及將加密的雲端儲存空間資料擷取到Experience Platform。 |
| `expiryTime` | 到期時間會定義加密金鑰組的到期日。 此日期會自動設定為產生金鑰的日期後180天，並以unix時間戳記格式顯示。 |

+++

### 擷取加密金鑰 {#retrieve-encryption-keys}

若要擷取您組織中的所有加密金鑰，請向`/encryption/keys` endpoit=nt發出GET要求。

**API格式**

```http
GET /data/foundation/connectors/encryption/keys
```

**要求**

+++檢視範例請求

以下請求會擷取貴組織中的所有加密金鑰。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/encryption/keys' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
```

+++

**回應**

+++檢視範例回應

成功的回應會傳回您的加密演演算法、公開金鑰、公開金鑰ID，以及您金鑰對應的到期時間。

```json
{
    "encryptionAlgorithm": "{ENCRYPTION_ALGORITHM}",
    "publicKeyId": "{PUBLIC_KEY_ID}",
    "publicKey": "{PUBLIC_KEY}",
    "expiryTime": "{EXPIRY_TIME}"
}
```

+++

### 依ID擷取加密金鑰 {#retrieve-encryption-keys-by-id}

若要擷取一組特定的加密金鑰，請向`/encryption/keys`端點提出GET要求，並提供您的公開金鑰ID作為標頭引數。

**API格式**

```http
GET /data/foundation/connectors/encryption/keys/{PUBLIC_KEY_ID}
```

**要求**

+++檢視範例請求

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/encryption/keys/{publicKeyId}' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
```

+++

**回應**

+++檢視範例回應

成功的回應會傳回您的加密演演算法、公開金鑰、公開金鑰ID，以及您金鑰對應的到期時間。

```json
{
    "encryptionAlgorithm": "{ENCRYPTION_ALGORITHM}",
    "publicKeyId": "{PUBLIC_KEY_ID}",
    "publicKey": "{PUBLIC_KEY}",
    "expiryTime": "{EXPIRY_TIME}"
}
```

+++

### 建立客戶自控金鑰組 {#create-customer-managed-key-pair}

您可以選擇建立簽署驗證金鑰組，以簽署並擷取您的加密資料。

在此階段，您必須產生自己的私密金鑰和公開金鑰組合，然後使用您的私密金鑰簽署您的加密資料。 接下來，您必須在Base64中編碼您的公開金鑰，然後將其共用給Experience Platform，以便Platform驗證您的簽名。

### 共用您的公開金鑰以Experience Platform

若要共用您的公開金鑰，請在提供加密演演算法和Base64編碼公開金鑰的同時，向`/customer-keys`端點提出POST要求。

**API格式**

```http
POST /data/foundation/connectors/encryption/customer-keys
```

**要求**

+++檢視範例請求

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/encryption/customer-keys' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
  -H 'x-sandbox-name: {{SANDBOX_NAME}}' \
  -H 'Content-Type: application/json' 
  -d '{
      "encryptionAlgorithm": {{ENCRYPTION_ALGORITHM}},       
      "publicKey": {{BASE_64_ENCODED_PUBLIC_KEY}}
    }'
```

| 參數 | 說明 |
| --- | --- |
| `encryptionAlgorithm` | 您使用的加密演演算法型別。 支援的加密型別為`PGP`和`GPG`。 |
| `publicKey` | 與您用來簽署已加密之客戶自控金鑰對應的公開金鑰。 此金鑰必須使用Base64編碼。 |

+++

**回應**

+++檢視範例回應

```json
{    
  "publicKeyId": "e31ae895-7896-469a-8e06-eb9207ddf1c2" 
} 
```

| 屬性 | 說明 |
| --- | --- |
| `publicKeyId` | 此公開金鑰ID會傳回，以回應與Experience Platform共用您的客戶自控金鑰。 在為已簽署和加密的資料建立資料流時，您可以提供此公開金鑰ID作為簽署驗證金鑰ID。 |

+++

## 使用[!DNL Flow Service] API連線您的雲端儲存空間來源以Experience Platform

擷取加密金鑰組後，您現在可以繼續並為雲端儲存空間來源建立來源連線，並將加密的資料匯入Platform。

首先，您必須建立基礎連線，以針對Platform驗證您的來源。 若要建立基礎連線並驗證您的來源，請從下列清單中選取您要使用的來源：

* [Amazon S3](../api/create/cloud-storage/s3.md)
* [[!DNL Apache HDFS]](../api/create/cloud-storage/hdfs.md)
* [Azure Blob](../api/create/cloud-storage/blob.md)
* [Azure Data Lake Storage Gen2](../api/create/cloud-storage/adls-gen2.md)
* [Azure 檔案儲存體](../api/create/cloud-storage/azure-file-storage.md)
* [資料登陸區域](../api/create/cloud-storage/data-landing-zone.md)
* [FTP](../api/create/cloud-storage/ftp.md)
* [Google Cloud Storage](../api/create/cloud-storage/google.md)
* [Oracle Object Storage](../api/create/cloud-storage/oracle-object-storage.md)
* [SFTP](../api/create/cloud-storage/sftp.md)

建立基礎連線後，您必須遵循教學課程中概述的步驟，針對[建立雲端儲存空間來源](../api/collect/cloud-storage.md)的來源連線，以建立來源連線、目標連線和對應。

## 為加密的資料建立資料流 {#create-a-dataflow-for-encrypted-data}

>[!NOTE]
>
>您必須具備下列專案，才能為加密的資料擷取建立資料流：
>
>* [公開金鑰識別碼](#create-encryption-key-pair)
>* [Source連線ID](../api/collect/cloud-storage.md#source)
>* [目標連線識別碼](../api/collect/cloud-storage.md#target)
>* [對應ID](../api/collect/cloud-storage.md#mapping)

若要建立資料流，請向[!DNL Flow Service] API的`/flows`端點提出POST要求。 若要內嵌加密的資料，您必須將`encryption`區段新增至`transformations`屬性，並包含在先前步驟中建立的`publicKeyId`。

**API格式**

```http
POST /flows
```

>[!BEGINTABS]

>[!TAB 建立加密資料擷取的資料流]

**要求**

+++檢視範例請求

以下請求會建立資料流，以擷取雲端儲存空間的加密資料。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
  -H 'x-sandbox-name: {{SANDBOX_NAME}}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "ACME Customer Data",
    "description": "ACME Customer Data (Encrypted)",
    "flowSpec": {
        "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "655f7c1b-1977-49b3-a429-51379ecf0e15"
    ],
    "targetConnectionIds": [
        "de688225-d619-481c-ae3b-40c250fd7c79"
    ],
    "transformations": [
        {
            "name": "Mapping",
            "params": {
                "mappingId": "6b6e24213dbe4f57bd8207d21034ff03",
                "mappingVersion":"0"
            }
        },
        {
            "name": "Encryption",
            "params": {
                "publicKeyId":"311ef6f8-9bcd-48cf-a9e9-d12c45fb7a17"
            }
        }
    ],
    "scheduleParams": {
        "startTime": "1675793392",
        "frequency": "once"
    }
}'
```

| 屬性 | 說明 |
| --- | --- |
| `flowSpec.id` | 與雲端儲存空間來源對應的流量規格ID。 |
| `sourceConnectionIds` | 來源連線ID。 此ID代表資料從來源傳輸至Platform的過程。 |
| `targetConnectionIds` | 目標連線ID。 此ID代表資料傳入Platform後著陸的位置。 |
| `transformations[x].params.mappingId` | 對應ID。 |
| `transformations.name` | 擷取加密檔案時，您必須提供`Encryption`作為資料流的其他轉換引數。 |
| `transformations[x].params.publicKeyId` | 您建立的公開金鑰ID。 此ID是用來加密雲端儲存體資料的加密金鑰組的一半。 |
| `scheduleParams.startTime` | 資料流的開始時間（以Epoch時間計）。 |
| `scheduleParams.frequency` | 資料流收集資料的頻率。 可接受的值包括： `once`、`minute`、`hour`、`day`或`week`。 |
| `scheduleParams.interval` | 間隔會指定兩個連續資料流執行之間的期間。 間隔的值應為非零整數。 當頻率設定為`once`時不需要間隔，其他頻率值應該大於或等於`15`。 |

+++

**回應**

+++檢視範例回應

成功的回應會傳回您加密資料之新建立資料流的識別碼(`id`)。

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

+++

>[!TAB 建立資料流以擷取加密和簽署的資料]

**要求**

+++檢視範例請求

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
  -H 'x-sandbox-name: {{SANDBOX_NAME}}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "ACME Customer Data (with Sign Verification)",
    "description": "ACME Customer Data (with Sign Verification)",
    "flowSpec": {
        "id": "9753525b-82c7-4dce-8a9b-5ccfce2b9876",
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "655f7c1b-1977-49b3-a429-51379ecf0e15"
    ],
    "targetConnectionIds": [
        "de688225-d619-481c-ae3b-40c250fd7c79"
    ],
    "transformations": [
        {
            "name": "Mapping",
            "params": {
                "mappingId": "6b6e24213dbe4f57bd8207d21034ff03",
                "mappingVersion":"0"
            }
        },
        {
            "name": "Encryption",
            "params": {
                "publicKeyId":"311ef6f8-9bcd-48cf-a9e9-d12c45fb7a17",
                "signVerificationKeyId":"e31ae895-7896-469a-8e06-eb9207ddf1c2"
            }
        }
    ],
    "scheduleParams": {
        "startTime": "1675793392",
        "frequency": "once"
    }
}'
```

| 屬性 | 說明 |
| --- | --- |
| `params.signVerificationKeyId` | 簽署驗證金鑰ID與使用Experience Platform共用Base64編碼公開金鑰後擷取的公開金鑰ID相同。 |

+++

**回應**

+++檢視範例回應

成功的回應會傳回您加密資料之新建立資料流的識別碼(`id`)。

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

+++

>[!ENDTABS]

### 刪除加密金鑰 {#delete-encryption-keys}

若要刪除您的加密金鑰，請向`/encryption/keys`端點提出DELETE要求，並提供您的公開金鑰識別碼作為標頭引數。

**API格式**

```http
DELETE /data/foundation/connectors/encryption/keys/{PUBLIC_KEY_ID}
```

**要求**

+++檢視範例請求

```shell
curl -X DELETE \
  'https://platform.adobe.io/data/foundation/connectors/encryption/keys/{publicKeyId}' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
```

+++

**回應**

成功的回應會傳回HTTP狀態204 （無內容）和空白內文。

### 驗證加密金鑰 {#validate-encryption-keys}

若要驗證您的加密金鑰，請向`/encryption/keys/validate/`端點發出GET要求，並提供您要驗證為標頭引數的公開金鑰ID。

```http
GET /data/foundation/connectors/encryption/keys/validate/{PUBLIC_KEY_ID}
```

**要求**

+++檢視範例請求

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/encryption/keys/validate/{publicKeyId}' \
  -H 'Authorization: Bearer {{ACCESS_TOKEN}}' \
  -H 'x-api-key: {{API_KEY}}' \
  -H 'x-gw-ims-org-id: {{ORG_ID}}' \
```

+++

**回應**

成功的回應會傳回確認ID有效或無效的訊息。

>[!BEGINTABS]

>[!TAB 有效]

有效的公開金鑰識別碼傳回`Active`狀態以及您的公開金鑰識別碼。

```json
{
    "publicKeyId": "{PUBLIC_KEY_ID}",
    "status": "Active"
}
```

>[!TAB 無效]

無效的公開金鑰識別碼傳回`Expired`狀態以及您的公開金鑰識別碼。

```json
{
    "publicKeyId": "{PUBLIC_KEY_ID}",
    "status": "Expired"
}
```

>[!ENDTABS]


## 週期性內嵌的限制 {#restrictions-on-recurring-ingestion}

加密的資料擷取不支援在來源中擷取循環或多層資料夾。 所有加密的檔案都必須包含在單一資料夾中。 也不支援在單一來源路徑中包含多個資料夾的萬用字元。

以下是支援的資料夾結構範例，其中來源路徑為`/ACME-customers/*.csv.gpg`。

在此案例中，粗體的檔案會擷取到Experience Platform中。

* ACME — 客戶
   * **檔案1.csv.gpg**
   * File2.json.gpg
   * **檔案3.csv.gpg**
   * File4.json
   * **檔案5.csv.gpg**

以下是來源路徑為`/ACME-customers/*`的不支援資料夾結構範例。

在此案例中，流程執行將失敗，並傳回錯誤訊息，指出無法從來源複製資料。

* ACME — 客戶
   * File1.csv.gpg
   * File2.json.gpg
   * 子資料夾1
      * File3.csv.gpg
      * File4.json.gpg
      * File5.csv.gpg
* ACME忠誠度
   * File6.csv.gpg


## 後續步驟

依照此教學課程，您已為雲端儲存空間資料建立加密金鑰組，並使用[!DNL Flow Service API]為資料流擷取加密資料。 如需資料流完整性、錯誤和量度的狀態更新，請參閱[使用 [!DNL Flow Service] API](./monitor.md)監視資料流的指南。