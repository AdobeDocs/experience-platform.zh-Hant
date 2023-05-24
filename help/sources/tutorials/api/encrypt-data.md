---
title: 加密資料接收
description: Adobe Experience Platform允許您通過雲儲存批處理源接收加密檔案。
hide: true
hidefromtoc: true
exl-id: 83a7a154-4f55-4bf0-bfef-594d5d50f460
source-git-commit: 8531459da97be648d0a63ffc2af77ce41124585d
workflow-type: tm+mt
source-wordcount: '967'
ht-degree: 2%

---

# 加密資料接收

Adobe Experience Platform允許您通過雲儲存批處理源接收加密檔案。 通過加密資料接收，您可以利用非對稱加密機制將批資料安全地傳輸到Experience Platform。 目前，支援的非對稱加密機制是PGP和GPG。

加密資料接收過程如下：

1. [使用Experience PlatformAPI建立加密密鑰對](#create-encryption-key-pair)。 加密密鑰對由私鑰和公鑰組成。 建立後，可以複製或下載公鑰及其相應的公鑰ID和到期時間。 在此過程中，私鑰將通過Experience Platform儲存在安全保管庫中。 **注：** 響應中的公鑰是Base64編碼的，在使用前必須解密。
2. 使用公鑰加密要攝取的資料檔案。
3. 將加密檔案放入雲儲存中。
4. 加密檔案準備好後， [為雲儲存源建立源連接和資料流](#create-a-dataflow-for-encrypted-data)。 在流建立步驟中，必須提供 `encryption` 參數並包括公鑰ID。
5. Experience Platform從安全保管庫檢索私鑰，以在接收時解密資料。

>[!IMPORTANT]
>
>單個加密檔案的最大大小為1 GB。 例如，您可以在單個資料流運行中接收值為2 GB的資料，但是，該資料中的任何單個檔案都不能超過1 GB。

本文檔提供了如何生成加密密鑰對以加密資料以及使用雲儲存源將加密資料接收到Experience Platform的步驟。

## 快速入門

本教程要求您對以下Adobe Experience Platform元件有一定的瞭解：

* [源](../../home.md):Experience Platform允許從各種源接收資料，同時讓您能夠使用平台服務構建、標籤和增強傳入資料。
   * [雲儲存源](../api/collect/cloud-storage.md):建立資料流，將雲儲存源中的批資料帶到Experience Platform。
* [沙箱](../../../sandboxes/home.md):Experience Platform提供虛擬沙箱，將單個平台實例分區為獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

### 使用平台API

有關如何成功調用平台API的資訊，請參見上的指南 [平台API入門](../../../landing/api-guide.md)。

## 建立加密密鑰對 {#create-encryption-key-pair}

將加密資料導入Experience Platform的第一步是通過向POST請求建立加密密鑰對 `/encryption/keys` 端點 [!DNL Connectors] API。

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
| `encryptionAlgorithm` | 您正在使用的加密算法類型。 支援的加密類型包括 `PGP` 和 `GPG`。 |
| `params.passPhrase` | 密碼短語為加密密鑰提供了額外的保護層。 在建立時，Experience Platform將密碼短語與公鑰儲存在不同的安全保管庫中。 必須提供非空字串作為密碼短語。 |

**回應**

成功的響應將返回Base64編碼的公鑰、公鑰ID和密鑰的到期時間。 到期時間自動設定為密鑰生成日期後180天。 到期時間當前不可配置。

```json
{
    ​"publicKey": "{PUBLIC_KEY}",
    ​"publicKeyId": "{PUBLIC_KEY_ID}",
    ​"expiryTime": "1684843168"
}
```

## 使用 [!DNL Flow Service] API

檢索完加密密鑰對後，您現在可以繼續並建立雲儲存源的源連接，並將加密的資料帶到平台。

首先，必須建立基本連接，以根據平台驗證源。 要建立基連接並驗證源，請從下面的清單中選擇要使用的源：

* [Amazon S3](../api/create/cloud-storage/s3.md)
* [[!DNL Apache HDFS]](../api/create/cloud-storage/hdfs.md)
* [Azure Blob](../api/create/cloud-storage/blob.md)
* [Azure資料湖儲存第2代](../api/create/cloud-storage/adls-gen2.md)
* [Azure檔案儲存](../api/create/cloud-storage/azure-file-storage.md)
* [Data Landing Zone](../api/create/cloud-storage/data-landing-zone.md)
* [FTP](../api/create/cloud-storage/ftp.md)
* [Google雲儲存](../api/create/cloud-storage/google.md)
* [Oracle對象儲存](../api/create/cloud-storage/oracle-object-storage.md)
* [SFTP](../api/create/cloud-storage/sftp.md)

建立基本連接後，必須按照本教程中介紹的步驟 [為雲儲存源建立源連接](../api/collect/cloud-storage.md) 建立源連接、目標連接和映射。

## 為加密資料建立資料流 {#create-a-dataflow-for-encrypted-data}

>[!NOTE]
>
>要建立用於加密資料接收的資料流，必須具有以下功能：
>* [公鑰ID](#create-encryption-key-pair)
>* [源連接ID](../api/collect/cloud-storage.md#source)
>* [目標連接ID](../api/collect/cloud-storage.md#target)
>* [對應 ID](../api/collect/cloud-storage.md#mapping)


要建立資料流，請向 `/flows` 端點 [!DNL Flow Service] API。 要接收加密資料，必須添加 `encryption` 的 `transformations` 屬性並包括 `publicKeyId` 是在較早的步驟中建立的。

**API格式**

```http
POST /flows
```

**要求**

以下請求建立資料流，以接收雲儲存源的加密資料。

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
| `flowSpec.id` | 與雲儲存源對應的流規範ID。 |
| `sourceConnectionIds` | 源連接ID。 此ID表示從源到平台的資料傳輸。 |
| `targetConnectionIds` | 目標連接ID。 此ID表示資料一旦被移到平台時的降落位置。 |
| `transformations[x].params.mappingId` | 映射ID。 |
| `transformations.name` | 接收加密檔案時，必須提供 `Encryption` 作為資料流的附加轉換參數。 |
| `transformations[x].params.publicKeyId` | 您建立的公鑰ID。 此ID是用於加密雲儲存資料的加密密鑰對的一半。 |
| `scheduleParams.startTime` | 資料流在紀元時間中的開始時間。 |
| `scheduleParams.frequency` | 資料流收集資料的頻率。 可接受值包括： `once`。 `minute`。 `hour`。 `day`或 `week`。 |
| `scheduleParams.interval` | 該間隔指定兩個連續流運行之間的期間。 間隔的值應為非零整數。 頻率設定為時不需要間隔 `once` 應大於或等於 `15` 其他頻率值。 |

**回應**

成功的響應返回ID(`id`)。

```json
{
    "id": "dbc5c132-bc2a-4625-85c1-32bc2a262558",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

## 後續步驟

按照本教程，您為雲儲存資料建立了加密密鑰對，並建立了資料流，以使用 [!DNL Flow Service API]。 有關資料流的完整性、錯誤和度量的狀態更新，請閱讀上的指南 [使用 [!DNL Flow Service] API](./monitor.md)。
