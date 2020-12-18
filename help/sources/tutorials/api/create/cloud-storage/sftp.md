---
keywords: Experience Platform;home;popular topics;SFTP;sftp;Secure File Transfer Protocol;secure file transfer protocol
solution: Experience Platform
title: 使用Flow Service API建立SFTP連接器
topic: overview
type: Tutorial
description: 本教學課程使用Flow Service API來引導您完成將Experience Platform連接至SFTP（安全檔案傳輸通訊協定）伺服器的步驟。
translation-type: tm+mt
source-git-commit: 9092c3d672967d3f6f7bf7116c40466a42e6e7b1
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 2%

---


# 使用[!DNL Flow Service] API建立SFTP連接器

>[!NOTE]
>
>SFTP連接器為測試版。 功能和檔案可能會有所變更。 有關使用beta標籤連接器的詳細資訊，請參閱[來源概觀](../../../../home.md#terms-and-conditions)。

本教學課程使用[!DNL Flow Service] API來引導您完成將Experience Platform連接至SFTP（安全檔案傳輸通訊協定）伺服器的步驟。

## 快速入門

本指南需要有效瞭解Adobe Experience Platform的下列元件：

* [來源](../../../../home.md):Experience Platform可讓您從各種來源擷取資料，同時讓您能夠使用平台服務來建構、標示和增強傳入資料。
* [沙盒](../../../../../sandboxes/home.md):Experience Platform提供虛擬沙盒，可將單一Platform實例分割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您需要知道的其他資訊，以便使用[!DNL Flow Service] API成功連線至SFTP伺服器。

### 收集必要的認證

要使[!DNL Flow Service]連接到SFTP，必須為以下連接屬性提供值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `host` | 與您的SFTP伺服器相關聯的名稱或IP位址。 |
| `username` | 可存取您SFTP伺服器的使用者名稱。 |
| `password` | SFTP伺服器的密碼。 |
| `privateKeyContent` | Base64編碼的SSH私鑰內容。 SSH私鑰OpenSSH(RSA/DSA)格式。 |
| `passPhrase` | 如果密鑰檔案或密鑰內容受密碼片語保護，則解密密鑰的密碼或密碼。 如果PrivateKeyContent受到密碼保護，則此參數必須與PrivateKeyContent的密碼短語一起使用，作為值。 |

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集必要標題的值

若要呼叫[!DNL Platform] API，您必須先完成[驗證教學課程](../../../../../tutorials/authentication.md)。 完成驗證教學課程後，所有[!DNL Experience Platform] API呼叫中每個所需標題的值都會顯示在下面：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有資源（包括屬於[!DNL Flow Service]的資源）都隔離到特定的虛擬沙盒。 對[!DNL Platform] API的所有請求都需要一個標題，該標題指定要在中執行操作的沙盒的名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的媒體類型標題：

* `Content-Type: application/json`

## 建立連線

連接指定源，並包含該源的憑據。 每個SFTP帳戶只需要一個連線，因為它可用來建立多個來源連接器以匯入不同的資料。

### 使用基本驗證建立SFTP連線

若要使用基本驗證建立SFTP連線，請在提供連線`host`、`userName`和`password`的值時，向[!DNL Flow Service] API提出POST要求。

**API格式**

```http
POST /connections
```

**請求**

若要建立SFTP連線，其唯一連線規格ID必須作為POST要求的一部分提供。 SFTP的連接規範ID為`b7bf2577-4520-42c9-bae9-cad01560f7bc`。

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

成功的響應返回新建立的連接的唯一標識符(`id`)。 在下一個教學課程中，瀏覽您的SFTP伺服器時需要此ID。

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

### 使用SSH公鑰驗證建立SFTP連接

要使用SSH公鑰身份驗證建立SFTP連接，請向[!DNL Flow Service] API發出POST請求，同時提供連接的`host`、`userName`、`privateKeyContent`和`passPhrase`值。

**API格式**

```http
POST /connections
```

**請求**

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
| `auth.params.host` | SFTP伺服器的主機名稱。 |
| `auth.params.username` | 與您的SFTP伺服器相關聯的使用者名稱。 |
| `auth.params.privateKeyContent` | base64編碼的SSH私鑰內容。 SSH私鑰OpenSSH(RSA/DSA)格式。 |
| `auth.params.passPhrase` | 如果密鑰檔案或密鑰內容受密碼片語保護，則解密密鑰的密碼或密碼。 如果PrivateKeyContent受到密碼保護，則此參數必須與PrivateKeyContent的密碼短語一起使用，作為值。 |
| `connectionSpec.id` | SFTP伺服器連接規範ID:`b7bf2577-4520-42c9-bae9-cad01560f7bc` |

**回應**

成功的響應返回新建立的連接的唯一標識符(`id`)。 在下一個教學課程中，瀏覽您的SFTP伺服器時需要此ID。

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## 後續步驟

在本教程中，您已使用[!DNL Flow Service] API建立SFTP連線，並取得連線的唯一ID值。 您可以使用此連線ID來探索使用Flow Service API[或](../../explore/cloud-storage.md)使用Flow Service API[收錄拼花資料的雲端儲存空間。](../../cloud-storage-parquet.md)
