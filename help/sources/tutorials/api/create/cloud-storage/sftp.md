---
keywords: Experience Platform;home;popular topics;SFTP;sftp;Secure File Transfer Protocol;secure file transfer protocol
solution: Experience Platform
title: 使用Flow Service API建立SFTP連接器
topic: overview
type: Tutorial
description: 本教學課程使用Flow Service API來引導您完成將Experience Platform連接至SFTP（安全檔案傳輸通訊協定）伺服器的步驟。
translation-type: tm+mt
source-git-commit: 71653681a0f4b31319bd352202bf55fb3947a455
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 2%

---


# 使用 [!DNL Flow Service] API建立SFTP連接器

>[!NOTE]
>
>SFTP連接器為測試版。 功能和檔案可能會有所變更。 如需使用 [測試版標籤連接器的詳細資訊](../../../../home.md#terms-and-conditions) ，請參閱來源概觀。

[!DNL Flow Service] 用於收集和集中Adobe Experience Platform內不同來源的客戶資料。 該服務提供用戶介面和REST風格的API，所有支援的源都可從中連接。

本教學課程使 [!DNL Flow Service] 用API來引導您完成連線至SFTP(安全檔案傳 [!DNL Experience Platform] 輸通訊協定)伺服器的步驟。

如果您想要使用中的使用者介面 [!DNL Experience Platform], [](../../../ui/create/cloud-storage/ftp-sftp.md) UI教學課程會提供執行類似動作的逐步指示。

## 快速入門

本指南需要有效瞭解Adobe Experience Platform的下列元件：

* [來源](../../../../home.md): [!DNL Experience Platform] 允許從各種來源接收資料，同時提供使用服務構建、標籤和增強傳入資料的 [!DNL Platform] 能力。
* [沙盒](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙盒，可將單一執行個體分 [!DNL Platform] 割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您需要知道的其他資訊，以便使用 [!DNL Flow Service] API成功連線至SFTP伺服器。

### 收集必要的認證

為了連 [!DNL Flow Service] 接到SFTP，必須為以下連接屬性提供值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `host` | 與您的SFTP伺服器相關聯的名稱或IP位址。 |
| `username` | 可存取您SFTP伺服器的使用者名稱。 |
| `password` | SFTP伺服器的密碼。 |
| `privateKeyContent` | Base64編碼的SSH私鑰內容。 SSH私鑰OpenSSH(RSA/DSA)格式。 |
| `passPhrase` | 如果密鑰檔案或密鑰內容受密碼片語保護，則解密密鑰的密碼或密碼。 如果PrivateKeyContent受到密碼保護，則此參數必須與PrivateKeyContent的密碼短語一起使用，作為值。 |

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱疑難排解指 [南中有關如何讀取範例API呼叫的](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)[!DNL Experience Platform] 章節。

### 收集必要標題的值

若要呼叫API，您必 [!DNL Platform] 須先完成驗證教 [學課程](../../../../../tutorials/authentication.md)。 完成驗證教學課程後，將提供所有 [!DNL Experience Platform] API呼叫中每個必要標題的值，如下所示：

* 授權：生產者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

中的所有資 [!DNL Experience Platform]源（包括屬於的資源）都 [!DNL Flow Service]被隔離到特定的虛擬沙盒中。 對API的所 [!DNL Platform] 有請求都需要一個標題，該標題會指定要在中執行的操作的沙盒名稱：

* x-sandbox-name: `{SANDBOX_NAME}`

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的媒體類型標題：

* 內容類型： `application/json`

## 建立連線

連接指定源，並包含該源的憑據。 每個SFTP帳戶只需要一個連線，因為它可用來建立多個來源連接器以匯入不同的資料。

### 使用基本驗證建立SFTP連線

若要使用基本驗證建立SFTP連線，請向 [!DNL Flow Service] API提出POST要求，同時提供您連線的 `host`、 `userName`和值 `password`。

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
| `connectionSpec.id` | SFTP伺服器連接規範ID: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

**回應**

成功的響應返回新建立的連接的`id`唯一標識符()。 在下一個教學課程中，瀏覽您的SFTP伺服器時需要此ID。

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

### 使用SSH公鑰驗證建立SFTP連接

若要使用SSH公開金鑰驗證建立SFTP連線，請向 [!DNL Flow Service] API提出POST要求，同時提供您連線的 `host`、 `userName`、 `privateKeyContent`和值 `passPhrase`。

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
| `connectionSpec.id` | SFTP伺服器連接規範ID: `b7bf2577-4520-42c9-bae9-cad01560f7bc` |

**回應**

成功的響應返回新建立的連接的`id`唯一標識符()。 在下一個教學課程中，瀏覽您的SFTP伺服器時需要此ID。

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## 後續步驟

在本教學課程中，您已使用 [!DNL Flow Service] API建立SFTP連線，並取得連線的唯一ID值。 您可以使用此連線ID來 [探索使用Flow Service API的雲端儲存空間](../../explore/cloud-storage.md) ，或 [使用Flow Service API內嵌鑲木地板資料](../../cloud-storage-parquet.md)。
