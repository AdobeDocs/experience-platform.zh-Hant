---
keywords: Experience Platform；首頁；熱門主題；SFTP;sftp；安全檔案傳輸通訊協定；安全檔案傳輸通訊協定
solution: Experience Platform
title: 使用流程服務API建立SFTP基礎連線
topic-legacy: overview
type: Tutorial
description: 了解如何使用流量服務API將Adobe Experience Platform連線至SFTP（安全檔案傳輸通訊協定）伺服器。
exl-id: b965b4bf-0b55-43df-bb79-c89609a9a488
source-git-commit: 9ad09fba3119b631576f22574a2151c74f91e07b
workflow-type: tm+mt
source-wordcount: '809'
ht-degree: 1%

---

# 使用[!DNL Flow Service] API建立SFTP基本連線

基本連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程會逐步帶您了解使用[[!DNL Flow Service]  API](https://www.adobe.io/experience-platform-apis/references/flow-service/)為[!DNL SFTP]（安全檔案傳輸通訊協定）建立基本連線的步驟。

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../../../home.md):Experience Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供可將單一Platform執行個體分割成個別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

>[!IMPORTANT]
>
>建議您在使用[!DNL SFTP]來源連線擷取JSON物件時，避免使用新的行或回車。 若要解決限制，請每行使用單一JSON物件，然後使用多行來建立後續檔案。

以下各節提供您需要知道的其他資訊，以便使用[!DNL Flow Service] API成功連接到[!DNL SFTP]伺服器。

### 收集所需憑據

要使[!DNL Flow Service]連接到[!DNL SFTP]，必須為以下連接屬性提供值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `host` | 與[!DNL SFTP]伺服器相關聯的名稱或IP地址。 |
| `port` | 您要連接的SFTP伺服器埠。 若未提供，則值預設為`22`。 |
| `username` | 可訪問[!DNL SFTP]伺服器的用戶名。 |
| `password` | [!DNL SFTP]伺服器的密碼。 |
| `privateKeyContent` | Base64編碼的SSH私密金鑰內容。 OpenSSH金鑰的類型必須分類為RSA或DSA。 |
| `passPhrase` | 如果密鑰檔案或密鑰內容受密碼短語保護，則解密私鑰的密碼短語或密碼。 如果`privateKeyContent`受密碼保護，則此參數需要與私鑰內容的密碼短語一起使用，作為值。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 [!DNL SFTP]的連接規範ID為：`b7bf2577-4520-42c9-bae9-cad01560f7bc`。 |

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱[Platform API快速入門手冊](../../../../../landing/api-guide.md)。

## 建立基本連接

基本連接在源和平台之間保留資訊，包括源的驗證憑據、連接的當前狀態和唯一基本連接ID。 基本連線ID可讓您從來源探索和導覽檔案，並識別您要擷取的特定項目，包括其資料類型和格式的相關資訊。

若要建立基本連線ID，請在提供[!DNL SFTP]驗證憑證作為請求參數的一部分時，向`/connections`端點提出POST請求。

### 使用基本身份驗證建立[!DNL SFTP]基本連接

若要使用基本驗證建立[!DNL SFTP]基本連線，請向[!DNL Flow Service] API發出POST請求，同時提供連線的`host`、`userName`和`password`值。

**API格式**

```http
POST /connections
```

**要求**

以下請求使用基本身份驗證為[!DNL SFTP]建立基本連接：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d  '{
        "name": "SFTP connector with password",
        "description": "SFTP connector password",
        "auth": {
            "specName": "Basic Authentication for sftp",
            "params": {
                "host": "{HOST}",
                "userName": "{USERNAME}",
                "password": "{PASSWORD}"
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
| `auth.params.username` | 與您的SFTP伺服器相關聯的使用者名稱。 |
| `auth.params.password` | 與您的SFTP伺服器相關聯的密碼。 |
| `connectionSpec.id` | SFTP伺服器連接規範ID:`b7bf2577-4520-42c9-bae9-cad01560f7bc` |

**回應**

成功的響應返回新建立的連接的唯一標識符(`id`)。 在下一個教學課程中，探索您的SFTP伺服器需要此ID。

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

### 使用SSH公鑰身份驗證建立[!DNL SFTP]基本連接

若要使用SSH公開金鑰驗證建立[!DNL SFTP]基本連線，請向[!DNL Flow Service] API提出POST請求，同時提供連線的`host`、`userName`、`privateKeyContent`和`passPhrase`值。

>[!IMPORTANT]
>
>[!DNL SFTP]連接器支援RSA或DSA類型OpenSSH金鑰。 確保密鑰檔案內容的開頭為`"-----BEGIN [RSA/DSA] PRIVATE KEY-----"`，結尾為`"-----END [RSA/DSA] PRIVATE KEY-----"`。 如果私鑰檔案是PPK格式檔案，請使用PuTTY工具從PPK格式轉換為OpenSSH格式。

**API格式**

```http
POST /connections
```

**要求**

以下請求使用SSH公鑰身份驗證為[!DNL SFTP]建立基連接：

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "SFTP connector with SSH authentication",
        "description": "SFTP connector with SSH authentication",
        "auth": {
            "specName": "SSH PublicKey Authentication for sftp",
            "params": {
                "host": "{HOST}",
                "userName": "{USERNAME}",
                "privateKeyContent": "{PRIVATE_KEY_CONTENT}",
                "passPhrase": "{PASSPHRASE}"
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
| `auth.params.host` | [!DNL SFTP]伺服器的主機名。 |
| `auth.params.username` | 與您的[!DNL SFTP]伺服器關聯的用戶名。 |
| `auth.params.privateKeyContent` | Base64編碼的SSH私密金鑰內容。 OpenSSH金鑰的類型必須分類為RSA或DSA。 |
| `auth.params.passPhrase` | 如果密鑰檔案或密鑰內容受密碼短語保護，則解密私鑰的密碼短語或密碼。 如果PrivateKeyContent受密碼保護，則此參數需要與PrivateKeyContent的密碼短語一起使用，作為值。 |
| `connectionSpec.id` | [!DNL SFTP]伺服器連接規範ID:`b7bf2577-4520-42c9-bae9-cad01560f7bc` |

**回應**

成功的響應返回新建立的連接的唯一標識符(`id`)。 在下一個教學課程中探索您的[!DNL SFTP]伺服器時需要此ID。

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## 後續步驟

依照本教學課程，您已使用[!DNL Flow Service] API建立[!DNL SFTP]連線，並取得連線的唯一ID值。 您可以使用此連線ID來使用流量服務API](../../explore/cloud-storage.md)或[使用流量服務API](../../cloud-storage-parquet.md)內嵌Parquet資料，以探索雲儲存空間。[
