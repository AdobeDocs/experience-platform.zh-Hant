---
title: 使用流程服務API建立SFTP基礎連線
description: 了解如何使用流量服務API將Adobe Experience Platform連線至SFTP（安全檔案傳輸通訊協定）伺服器。
exl-id: b965b4bf-0b55-43df-bb79-c89609a9a488
source-git-commit: 922e9a26f1791056b251ead2ce2702dfbf732193
workflow-type: tm+mt
source-wordcount: '895'
ht-degree: 1%

---

# 使用建立SFTP基礎連線 [!DNL Flow Service] API

基本連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程會逐步引導您完成建立基礎連線的步驟 [!DNL SFTP] （安全檔案傳輸通訊協定）使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../../../home.md):Experience Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供可將單一Platform執行個體分割成個別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

>[!IMPORTANT]
>
>建議您避免使用 [!DNL SFTP] 源連接。 若要解決限制，請每行使用單一JSON物件，然後使用多行來建立後續檔案。

以下小節提供您需要知道的其他資訊，以便成功連接到 [!DNL SFTP] 使用 [!DNL Flow Service] API。

### 收集所需憑據

為了 [!DNL Flow Service] 連接到 [!DNL SFTP]，您必須提供下列連線屬性的值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `host` | 與您的 [!DNL SFTP] 伺服器。 |
| `port` | 您要連接的SFTP伺服器埠。 若未提供，則值預設為 `22`. |
| `username` | 具有 [!DNL SFTP] 伺服器。 |
| `password` | 您 [!DNL SFTP] 伺服器。 |
| `privateKeyContent` | Base64編碼的SSH私密金鑰內容。 OpenSSH金鑰的類型必須分類為RSA或DSA。 |
| `passPhrase` | 如果密鑰檔案或密鑰內容受密碼短語保護，則解密私鑰的密碼短語或密碼。 若 `privateKeyContent` 受密碼保護，此參數需要與私鑰內容的密碼短語一起使用，作為值。 |
| `maxConcurrentConnections` | 此參數可讓您指定平台在連線至您的SFTP伺服器時所建立的同時連線數量上限。 您必須將此值設為小於SFTP設定的限制。 **附註**:為現有SFTP帳戶啟用此設定時，它只會影響未來的資料流，而不會影響現有的資料流。 |
| `folderPath` | 要提供訪問權限的資料夾的路徑。 [!DNL SFTP] 源，可提供資料夾路徑，以指定用戶對所選子資料夾的訪問權限。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 的連接規範ID [!DNL SFTP] 為： `b7bf2577-4520-42c9-bae9-cad01560f7bc`. |

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱 [Platform API快速入門](../../../../../landing/api-guide.md).

## 建立基本連接

基本連接在源和平台之間保留資訊，包括源的驗證憑據、連接的當前狀態和唯一基本連接ID。 基本連線ID可讓您從來源探索和導覽檔案，並識別您要擷取的特定項目，包括其資料類型和格式的相關資訊。

此 [!DNL SFTP] 來源支援透過SSH公開金鑰進行基本驗證和驗證。 在此步驟中，您也可以指定要提供存取權的子資料夾的路徑。

若要建立基本連線ID，請向 `/connections` 端點提供 [!DNL SFTP] 驗證憑證作為要求參數的一部分。

>[!IMPORTANT]
>
>此 [!DNL SFTP] 連接器支援RSA或DSA類型OpenSSH金鑰。 確定您的關鍵檔案內容開頭為 `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` 結尾是 `"-----END [RSA/DSA] PRIVATE KEY-----"`. 如果私鑰檔案是PPK格式檔案，請使用PuTTY工具從PPK格式轉換為OpenSSH格式。

**API格式**

```http
POST /connections
```

**要求**

下列請求會為 [!DNL SFTP]:

>[!BEGINTABS]

>[!TAB 基本驗證]

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d  '{
      "name": "SFTP connector with password",
      "description": "SFTP connector password",
      "auth": {
          "specName": "Basic Authentication for sftp",
          "params": {
              "host": "{HOST}",
              "port": 22,
              "userName": "{USERNAME}",
              "password": "{PASSWORD}",
              "maxConcurrentConnections": 5,
              "folderPath": "acme/business/customers/holidaySales"
          }
      },
      "connectionSpec": {
          "id": "b7bf2577-4520-42c9-bae9-cad01560f7bc",
          "version": "1.0"
      }
  }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `auth.params.host` | SFTP伺服器的主機名稱。 |
| `auth.params.port` | SFTP伺服器的埠。 此整數值預設為22。 |
| `auth.params.username` | 與您的SFTP伺服器相關聯的使用者名稱。 |
| `auth.params.password` | 與您的SFTP伺服器相關聯的密碼。 |
| `auth.params.maxConcurrentConnections` | 將Platform連線至SFTP時指定的最大同時連線數。 啟用後，此值必須至少設為1。 |
| `auth.params.folderPath` | 要提供訪問權限的資料夾的路徑。 |
| `connectionSpec.id` | SFTP伺服器連接規範ID: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

>[!TAB SSH公開金鑰驗證]

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "SFTP connector with SSH authentication",
      "description": "SFTP connector with SSH authentication",
      "auth": {
          "specName": "SSH PublicKey Authentication for sftp",
          "params": {
              "host": "{HOST}",
              "port": 22,
              "userName": "{USERNAME}",
              "privateKeyContent": "{PRIVATE_KEY_CONTENT}",
              "passPhrase": "{PASSPHRASE}",
              "maxConcurrentConnections": 5,
              "folderPath": "acme/business/customers/holidaySales"
          }
      },
      "connectionSpec": {
          "id": "b7bf2577-4520-42c9-bae9-cad01560f7bc",
          "version": "1.0"
      }
  }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `auth.params.host` | 您的 [!DNL SFTP] 伺服器。 |
| `auth.params.port` | SFTP伺服器的埠。 此整數值預設為22。 |
| `auth.params.username` | 與您的 [!DNL SFTP] 伺服器。 |
| `auth.params.privateKeyContent` | Base64編碼的SSH私密金鑰內容。 OpenSSH金鑰的類型必須分類為RSA或DSA。 |
| `auth.params.passPhrase` | 如果密鑰檔案或密鑰內容受密碼短語保護，則解密私鑰的密碼短語或密碼。 如果PrivateKeyContent受密碼保護，則此參數需要與PrivateKeyContent的密碼短語一起使用，作為值。 |
| `auth.params.maxConcurrentConnections` | 將Platform連線至SFTP時指定的最大同時連線數。 啟用後，此值必須至少設為1。 |
| `auth.params.folderPath` | 要提供訪問權限的資料夾的路徑。 |
| `connectionSpec.id` | 此 [!DNL SFTP] 伺服器連接規範ID: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

>[!ENDTABS]

**回應**

成功的回應會傳回唯一識別碼(`id`)。 在下一個教學課程中，探索您的SFTP伺服器需要此ID。

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## 後續步驟

依照本教學課程，您已建立 [!DNL SFTP] 使用 [!DNL Flow Service] API，並已取得連線的唯一ID值。 您可將此連線ID用於 [使用流量服務API探索雲端儲存空間](../../explore/cloud-storage.md).
