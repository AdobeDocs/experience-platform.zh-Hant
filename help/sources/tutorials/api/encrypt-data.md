---
title: 加密資料擷取
description: Adobe Experience Platform可讓您透過雲端儲存批次來源內嵌加密的檔案。
hide: true
hidefromtoc: true
source-git-commit: f0bbefcd9b4595f02c400ea0c5bb76bfa6c5e33e
workflow-type: tm+mt
source-wordcount: '914'
ht-degree: 2%

---

# 加密資料擷取

Adobe Experience Platform可讓您透過雲端儲存批次來源內嵌加密的檔案。 透過加密的資料內嵌，您可以運用非對稱的加密機制，以安全的方式將批次資料傳輸至Experience Platform。 目前支援的非對稱加密機制為PGP和GPG。

加密的資料擷取程式如下：

1. [使用Experience PlatformAPI建立加密金鑰組](#create-encryption-key-pair). 加密密鑰對由私鑰和公鑰組成。 建立後，您可以複製或下載公開金鑰，及其對應的公開金鑰ID和到期時間。 在此過程中，私鑰將由Experience Platform儲存在安全保管庫中。
2. 使用公開金鑰加密您要擷取的資料檔案。
3. 將加密的檔案放入雲端儲存空間。
4. 一旦加密檔案準備就緒， [為雲儲存源建立源連接和資料流](#create-a-dataflow-for-encrypted-data). 在流程建立步驟期間，您必須提供 `encryption` 參數，並加入您的公開金鑰ID。
5. Experience Platform從安全保管庫中檢索私鑰以在獲取時解密資料。

本檔案提供如何產生加密金鑰組以加密您的資料，以及將加密的資料內嵌至使用雲端儲存來源Experience Platform的步驟。

## 快速入門

本教學課程需要您妥善了解下列Adobe Experience Platform元件：

* [來源](../../home.md):Experience Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。
   * [雲端儲存空間來源](../api/collect/cloud-storage.md):建立資料流，將雲儲存源中的批資料帶入Experience Platform。
* [沙箱](../../../sandboxes/home.md):Experience Platform提供可將單一Platform執行個體分割成個別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱 [Platform API快速入門](../../../landing/api-guide.md).

## 建立加密密鑰對 {#create-encryption-key-pair}

將加密資料擷取至Experience Platform的第一步，是透過向 `/encryption/keys` 端點 [!DNL Connectors] API。

**API格式**

```http
POST /data/foundation/connectors/encryption/keys
```

**要求**

以下請求使用PGP加密算法生成加密密鑰對。

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
| `encryptionAlgorithm` | 您使用的加密算法類型。 支援的加密類型包括 `PGP` 和 `GPG`. |
| `params.passPhrase` | 密碼短語為您的加密密鑰提供了額外的保護層。 建立時，Experience Platform將密碼短語儲存在與公鑰不同的安全保管庫中。 您必須提供非空白字串作為密碼短語。 |

**回應**

成功的回應會傳回您的公開金鑰、公開金鑰ID，以及金鑰的到期時間。 到期時間會自動設為金鑰產生日期後180天。 當前無法配置到期時間。

```json
{
    ​"publicKey": "{PUBLIC_KEY}",
    ​"publicKeyId": "{PUBLIC_KEY_ID}",
    ​"expiryTime": "1684843168"
}
```

## 使用將雲儲存源連接到Experience Platform [!DNL Flow Service] API

擷取加密金鑰組後，您現在可以繼續為雲端儲存空間來源建立來源連線，並將加密的資料帶入Platform。

首先，您必須建立基本連線，才能根據Platform驗證來源。 要建立基本連接並驗證源，請從下面的清單中選擇要使用的源：

* [Amazon S3](../api/create/cloud-storage/s3.md)
* [[!DNL Apache HDFS]](../api/create/cloud-storage/hdfs.md)
* [Azure Blob](../api/create/cloud-storage/blob.md)
* [Azure資料湖儲存Gen2](../api/create/cloud-storage/adls-gen2.md)
* [Azure檔案儲存](../api/create/cloud-storage/azure-file-storage.md)
* [Data Landing Zone](../api/create/cloud-storage/data-landing-zone.md)
* [FTP](../api/create/cloud-storage/ftp.md)
* [Google雲端儲存空間](../api/create/cloud-storage/google.md)
* [Oracle對象儲存](../api/create/cloud-storage/oracle-object-storage.md)
* [SFTP](../api/create/cloud-storage/sftp.md)

建立基本連線後，您必須依照 [為雲儲存源建立源連接](../api/collect/cloud-storage.md) 建立源連接、目標連接和映射。

## 為加密資料建立資料流 {#create-a-dataflow-for-encrypted-data}

>[!NOTE]
>
>您必須具備以下條件，才能建立用於加密資料內嵌的資料流：
>* [公開金鑰ID](#create-encryption-key-pair)
>* [源連接ID](../api/collect/cloud-storage.md#source)
>* [Target連線ID](../api/collect/cloud-storage.md#target)
>* [對應ID](../api/collect/cloud-storage.md#mapping)


若要建立資料流，請向 `/flows` 端點 [!DNL Flow Service] API。 若要內嵌加密資料，您必須新增 `encryption` 區段 `transformations` 屬性，並包含 `publicKeyId` 是在先前的步驟中建立。

**API格式**

```http
POST /flows
```

**要求**

以下請求將建立資料流，以為雲儲存源內嵌加密的資料。

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
| `flowSpec.id` | 與雲儲存源對應的流規格ID。 |
| `sourceConnectionIds` | 源連接ID。 此ID代表從來源到Platform的資料傳輸。 |
| `targetConnectionIds` | 目標連接ID。 此ID代表資料匯入Platform後的登陸位置。 |
| `transformations[x].params.mappingId` | 對應ID。 |
| `transformations.name` | 擷取加密的檔案時，您必須提供 `Encryption` 作為資料流的其他轉換參數。 |
| `transformations[x].params.publicKeyId` | 您建立的公開金鑰ID。 此ID是用於加密雲儲存資料的加密密鑰對的一半。 |
| `scheduleParams.startTime` | 資料流的開始時間（以Epoch時間表示）。 |
| `scheduleParams.frequency` | 資料流收集資料的頻率。 可接受的值包括： `once`, `minute`, `hour`, `day`，或 `week`. |
| `scheduleParams.interval` | 該間隔指定兩個連續流運行之間的週期。 間隔的值應為非零整數。 頻率設為時不需要間隔 `once` 且應大於或等於 `15` 的其他頻率值。 |

**回應**

成功的回應會傳回ID(`id`)的資料流。

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## 後續步驟

依照本教學課程，您已為雲端儲存資料建立加密金鑰組，並建立資料流，以使用 [!DNL Flow Service API]. 有關資料流的完整性、錯誤和度量的狀態更新，請參閱 [使用監視資料流 [!DNL Flow Service] API](./monitor.md).