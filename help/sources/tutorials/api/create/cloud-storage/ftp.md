---
keywords: Experience Platform；首頁；熱門主題；檔案傳輸協定；檔案傳輸協定
solution: Experience Platform
title: 使用流量服務API建立FTP基礎連線
type: Tutorial
description: 了解如何使用流量服務API將Adobe Experience Platform連線至FTP（檔案傳輸通訊協定）伺服器。
exl-id: a7bef346-b357-49bc-ac54-ac8b42adac50
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 1%

---

# 使用建立FTP基礎連線 [!DNL Flow Service] API

>[!NOTE]
>
>FTP連接器為測試版。 功能和檔案可能會有所變更。 請參閱 [來源概觀](../../../../home.md#terms-and-conditions) 有關使用測試版標籤連接器的詳細資訊。

基本連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程會逐步引導您完成建立基礎連線的步驟 [!DNL FTP] （檔案傳輸通訊協定）使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../../../home.md): [!DNL Experience Platform] 可讓您從各種來源擷取資料，同時使用來建構、加標籤及增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供可分割單一沙箱的虛擬沙箱 [!DNL Platform] 例項放入個別的虛擬環境，以協助開發及改進數位體驗應用程式。

以下小節提供您需要知道的其他資訊，以便成功連接到 [!DNL FTP] 使用 [!DNL Flow Service] API。

### 收集所需憑據

為了 [!DNL Flow Service] 連接到 [!DNL FTP]，您必須提供下列連線屬性的值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `host` | 與您的 [!DNL FTP] 伺服器。 |
| `username` | 具有 [!DNL FTP] 伺服器。 |
| `password` | 您 [!DNL FTP] 伺服器。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 的連接規範ID [!DNL FTP] 為： `fb2e94c9-c031-467d-8103-6bd6e0a432f2`. |

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱 [Platform API快速入門](../../../../../landing/api-guide.md).

## 建立基本連接

基本連接在源和平台之間保留資訊，包括源的驗證憑據、連接的當前狀態和唯一基本連接ID。 基本連線ID可讓您從來源探索和導覽檔案，並識別您要擷取的特定項目，包括其資料類型和格式的相關資訊。

若要建立基本連線ID，請向 `/connections` 端點提供 [!DNL FTP] 驗證憑證作為要求參數的一部分。

**API格式**

```http
POST /connections
```

**要求**

下列請求會為 [!DNL FTP]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d  '{
        "name": "FTP connector with password",
        "description": "FTP connector password",
        "auth": {
            "specName": "Basic Authentication for FTP",
            "params": {
                "host": "{HOST}",
                "userName": "{USERNAME}",
                "password": "{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "fb2e94c9-c031-467d-8103-6bd6e0a432f2",
            "version": "1.0"
        }
    }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `auth.params.host` | FTP伺服器的主機名稱。 |
| `auth.params.username` | 與您的FTP伺服器相關聯的使用者名稱。 |
| `auth.params.password` | 與您的FTP伺服器相關聯的密碼。 |
| `connectionSpec.id` | FTP伺服器連接規範ID: `fb2e94c9-c031-467d-8103-6bd6e0a432f2` |

**回應**

成功的回應會傳回唯一識別碼(`id`)。 在下一個教學課程中探索您的FTP伺服器需要此ID。

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## 後續步驟

依照本教學課程，您已使用 [!DNL Flow Service] API，並已取得連線的唯一ID值。 您可將此連線ID用於 [使用流量服務API探索雲端儲存空間](../../explore/cloud-storage.md).
