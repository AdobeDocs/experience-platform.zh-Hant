---
title: 使用流量服務API建立SFTP基本連線
description: 瞭解如何使用流量服務API將Adobe Experience Platform連線至SFTP （安全檔案傳輸通訊協定）伺服器。
exl-id: b965b4bf-0b55-43df-bb79-c89609a9a488
source-git-commit: f6d1cc811378f2f37968bf0a42b428249e52efd8
workflow-type: tm+mt
source-wordcount: '938'
ht-degree: 2%

---

# 使用[!DNL Flow Service] API建立SFTP基本連線

基礎連線代表來源和Adobe Experience Platform之間的已驗證連線。

本教學課程將逐步引導您使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)為[!DNL SFTP] （安全檔案傳輸通訊協定）建立基礎連線。

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

* [來源](../../../../home.md)：Experience Platform允許從各種來源擷取資料，同時讓您能夠使用Platform服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)：Experience Platform提供的虛擬沙箱可將單一Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

>[!IMPORTANT]
>
>當擷取具有[!DNL SFTP]來源連線的JSON物件時，建議避免換行或歸位。 若要解決此限制，請在每行使用單一JSON物件，並使用多行作為後續檔案。

下列章節提供您需瞭解的其他資訊，才能使用[!DNL Flow Service] API成功連線到[!DNL SFTP]伺服器。

### 收集必要的認證

為了讓[!DNL Flow Service]連線到[!DNL SFTP]，您必須提供下列連線屬性的值：

| 認證 | 說明 |
| ---------- | ----------- |
| `host` | 與您的[!DNL SFTP]伺服器關聯的名稱或IP位址。 |
| `port` | 您連線的SFTP伺服器連線埠。 如果未提供，則值預設為`22`。 |
| `username` | 可存取您[!DNL SFTP]伺服器的使用者名稱。 |
| `password` | [!DNL SFTP]伺服器的密碼。 |
| `privateKeyContent` | Base64編碼SSH私密金鑰內容。 OpenSSH金鑰的型別必須分類為RSA或DSA。 |
| `passPhrase` | 如果金鑰檔案或金鑰內容受密語保護，則將私密金鑰解密的密語或密碼。 如果`privateKeyContent`受密碼保護，此引數必須搭配私密金鑰內容的密碼短語作為值使用。 |
| `maxConcurrentConnections` | 此引數可讓您指定在連線至您的SFTP伺服器時，Platform將建立的同時連線數目上限。 您必須將此值設定為小於SFTP設定的限制。 **注意**：為現有SFTP帳戶啟用此設定時，只會影響未來的資料流，不會影響現有的資料流。 |
| `folderPath` | 您要提供存取權的資料夾路徑。 [!DNL SFTP]來源，您可以提供資料夾路徑，以指定使用者對您所選子資料夾的存取權。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 [!DNL SFTP]的連線規格識別碼為： `b7bf2577-4520-42c9-bae9-cad01560f7bc`。 |

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱[Platform API快速入門](../../../../../landing/api-guide.md)的指南。

## 建立基礎連線

>[!TIP]
>
>建立後，您無法變更[!DNL SFTP]基本連線的驗證型別。 若要變更驗證型別，您必須建立新的基礎連線。

基礎連線會保留您的來源和平台之間的資訊，包括來源的驗證認證、連線的目前狀態，以及您唯一的基本連線ID。 基礎連線ID可讓您從來源內部探索及導覽檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

[!DNL SFTP]來源支援基本驗證和透過SSH公開金鑰的驗證。 在此步驟中，您也可以指定要提供存取權的子資料夾路徑。

若要建立基底連線ID，請在提供[!DNL SFTP]驗證認證作為要求引數的一部分時，向`/connections`端點提出POST要求。

>[!IMPORTANT]
>
>[!DNL SFTP]聯結器支援RSA或DSA型別OpenSSH金鑰。 確定您的金鑰檔案內容以`"-----BEGIN [RSA/DSA] PRIVATE KEY-----"`開頭並以`"-----END [RSA/DSA] PRIVATE KEY-----"`結尾。 如果私密金鑰檔案是PPK格式檔案，請使用PuTTY工具從PPK轉換為OpenSSH格式。

**API格式**

```http
POST /connections
```

>[!BEGINTABS]

>[!TAB 基本驗證]

+++要求

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
| `auth.params.port` | SFTP伺服器的連線埠。 此整數值預設為22。 |
| `auth.params.username` | 與您的SFTP伺服器相關聯的使用者名稱。 |
| `auth.params.password` | 與您的SFTP伺服器關聯的密碼。 |
| `auth.params.maxConcurrentConnections` | 將Platform連線至SFTP時指定的同時連線數目上限。 啟用時，此值必須設定為至少1。 |
| `auth.params.folderPath` | 您要提供存取權的資料夾路徑。 |
| `connectionSpec.id` | SFTP伺服器連線規格識別碼： `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

+++

+++回應

成功的回應會傳回新建立之連線的唯一識別碼(`id`)。 在下一個教學課程中，探索您的SFTP伺服器時，需要此ID。

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

+++

>[!TAB SSH公開金鑰驗證]

+++要求

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
| `auth.params.host` | [!DNL SFTP]伺服器的主機名稱。 |
| `auth.params.port` | SFTP伺服器的連線埠。 此整數值預設為22。 |
| `auth.params.username` | 與您的[!DNL SFTP]伺服器相關聯的使用者名稱。 |
| `auth.params.privateKeyContent` | Base64編碼SSH私密金鑰內容。 OpenSSH金鑰的型別必須分類為RSA或DSA。 |
| `auth.params.passPhrase` | 如果金鑰檔案或金鑰內容受密語保護，則將私密金鑰解密的密語或密碼。 如果PrivateKeyContent受密碼保護，此引數必須搭配PrivateKeyContent的密碼短語作為值使用。 |
| `auth.params.maxConcurrentConnections` | 將Platform連線至SFTP時指定的同時連線數目上限。 啟用時，此值必須設定為至少1。 |
| `auth.params.folderPath` | 您要提供存取權的資料夾路徑。 |
| `connectionSpec.id` | [!DNL SFTP]伺服器連線規格識別碼： `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

+++

+++回應

成功的回應會傳回新建立之連線的唯一識別碼(`id`)。 在下一個教學課程中，探索您的SFTP伺服器時，需要此ID。

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

+++

>[!ENDTABS]

## 後續步驟

依照本教學課程中的指示，您已使用[!DNL Flow Service] API建立[!DNL SFTP]連線，並已取得連線的唯一ID值。 您可以使用此連線ID來使用Flow Service API](../../explore/cloud-storage.md) [探索雲端儲存空間。
