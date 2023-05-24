---
title: 使用流服務API建立SFTP基連接
description: 瞭解如何使用流服務API將Adobe Experience Platform連接到SFTP（安全檔案傳輸協定）伺服器。
exl-id: b965b4bf-0b55-43df-bb79-c89609a9a488
source-git-commit: 922e9a26f1791056b251ead2ce2702dfbf732193
workflow-type: tm+mt
source-wordcount: '895'
ht-degree: 1%

---

# 使用 [!DNL Flow Service] API

基連接表示源和Adobe Experience Platform之間經過驗證的連接。

本教程將指導您完成建立基本連接的步驟 [!DNL SFTP] （安全檔案傳輸協定） [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)。

## 快速入門

本指南要求對Adobe Experience Platform的下列組成部分有工作上的理解：

* [源](../../../../home.md):Experience Platform允許從各種源接收資料，同時讓您能夠使用平台服務構建、標籤和增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供虛擬沙箱，將單個平台實例分區為獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

>[!IMPORTANT]
>
>建議在使用JSON對象插入時避免新行或回車 [!DNL SFTP] 源連接。 要繞過限制，請每行使用一個JSON對象，並使用多行來獲取後續檔案。

以下各節提供了成功連接到 [!DNL SFTP] 使用 [!DNL Flow Service] API。

### 收集所需憑據

為了 [!DNL Flow Service] 連接到 [!DNL SFTP]，必須為以下連接屬性提供值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `host` | 與您的 [!DNL SFTP] 伺服器。 |
| `port` | 您要連接的SFTP伺服器埠。 如果未提供，則值預設為 `22`。 |
| `username` | 有權訪問您的 [!DNL SFTP] 伺服器。 |
| `password` | 您的密碼 [!DNL SFTP] 伺服器。 |
| `privateKeyContent` | Base64編碼的SSH私鑰內容。 OpenSSH密鑰的類型必須分為RSA或DSA。 |
| `passPhrase` | 如果密鑰檔案或密鑰內容受密碼片語保護，則解密私鑰的密碼或密碼。 如果 `privateKeyContent` 受密碼保護，此參數需要與私鑰內容的密碼短語一起使用作值。 |
| `maxConcurrentConnections` | 此參數允許您為平台在連接到SFTP伺服器時將建立的併發連接數指定最大限制。 必須將此值設定為小於SFTP設定的限制。 **注釋**:當為現有SFTP帳戶啟用此設定時，它將僅影響將來的資料流，而不影響現有的資料流。 |
| `folderPath` | 要提供訪問權限的資料夾的路徑。 [!DNL SFTP] 源，可提供資料夾路徑以指定用戶對所選子資料夾的訪問權限。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 連接規範ID [!DNL SFTP] 為： `b7bf2577-4520-42c9-bae9-cad01560f7bc`。 |

### 使用平台API

有關如何成功調用平台API的資訊，請參見上的指南 [平台API入門](../../../../../landing/api-guide.md)。

## 建立基本連接

基本連接將保留源和平台之間的資訊，包括源的驗證憑據、連接的當前狀態和唯一的基本連接ID。 基本連接ID允許您從源中瀏覽和導航檔案，並標識要攝取的特定項目，包括有關其資料類型和格式的資訊。

的 [!DNL SFTP] 源支援通過SSH公鑰進行基本身份驗證和身份驗證。 在此步驟中，您還可以指定要提供訪問權限的子資料夾的路徑。

要建立基本連接ID，請向 `/connections` 提供端點 [!DNL SFTP] 身份驗證憑據作為請求參數的一部分。

>[!IMPORTANT]
>
>的 [!DNL SFTP] 連接器支援RSA或DSA類型OpenSSH密鑰。 確保密鑰檔案內容以 `"-----BEGIN [RSA/DSA] PRIVATE KEY-----"` 結尾 `"-----END [RSA/DSA] PRIVATE KEY-----"`。 如果私鑰檔案是PPK格式檔案，請使用PuTTY工具將PPK格式轉換為OpenSSH格式。

**API格式**

```http
POST /connections
```

**要求**

以下請求為 [!DNL SFTP]:

>[!BEGINTABS]

>[!TAB 基本身份驗證]

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
| `auth.params.host` | SFTP伺服器的主機名。 |
| `auth.params.port` | SFTP伺服器的埠。 此整數值預設為22。 |
| `auth.params.username` | 與SFTP伺服器關聯的用戶名。 |
| `auth.params.password` | 與SFTP伺服器關聯的密碼。 |
| `auth.params.maxConcurrentConnections` | 將平台連接到SFTP時指定的最大併發連接數。 啟用後，此值必須至少設定為1。 |
| `auth.params.folderPath` | 要提供訪問權限的資料夾的路徑。 |
| `connectionSpec.id` | SFTP伺服器連接規範ID: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

>[!TAB SSH公鑰身份驗證]

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
| `auth.params.host` | 您的主機名 [!DNL SFTP] 伺服器。 |
| `auth.params.port` | SFTP伺服器的埠。 此整數值預設為22。 |
| `auth.params.username` | 與您的 [!DNL SFTP] 伺服器。 |
| `auth.params.privateKeyContent` | Base64編碼的SSH私鑰內容。 OpenSSH密鑰的類型必須分為RSA或DSA。 |
| `auth.params.passPhrase` | 如果密鑰檔案或密鑰內容受密碼片語保護，則解密私鑰的密碼或密碼。 如果PrivateKeyContent受密碼保護，則此參數需要與PrivateKeyContent的密碼短語一起作為值使用。 |
| `auth.params.maxConcurrentConnections` | 將平台連接到SFTP時指定的最大併發連接數。 啟用後，此值必須至少設定為1。 |
| `auth.params.folderPath` | 要提供訪問權限的資料夾的路徑。 |
| `connectionSpec.id` | 的 [!DNL SFTP] 伺服器連接規範ID: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

>[!ENDTABS]

**回應**

成功的響應返回唯一標識符(`id`)。 在下一教程中瀏覽SFTP伺服器時需要此ID。

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## 後續步驟

按照本教程，您建立了 [!DNL SFTP] 使用 [!DNL Flow Service] API，並已獲取連接的唯一ID值。 您可以使用此連接ID [使用流服務API瀏覽雲儲存](../../explore/cloud-storage.md)。
