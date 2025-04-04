---
keywords: Experience Platform；首頁；熱門主題；檔案傳輸通訊協定；檔案傳輸通訊協定
solution: Experience Platform
title: 使用流量服務API建立FTP基本連線
type: Tutorial
description: 瞭解如何使用流量服務API將Adobe Experience Platform連線至FTP （檔案傳輸通訊協定）伺服器。
exl-id: a7bef346-b357-49bc-ac54-ac8b42adac50
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 4%

---

# 使用[!DNL Flow Service] API建立FTP基本連線

>[!NOTE]
>
>FTP聯結器為Beta版。 功能和檔案可能會有所變更。 如需使用Beta標籤聯結器的詳細資訊，請參閱[來源概觀](../../../../home.md#terms-and-conditions)。

基礎連線代表來源和Adobe Experience Platform之間的已驗證連線。

本教學課程將逐步引導您使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)為[!DNL FTP] （檔案傳輸通訊協定）建立基礎連線。

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

* [來源](../../../../home.md)： [!DNL Experience Platform]允許從各種來源擷取資料，同時讓您能夠使用[!DNL Experience Platform]服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)： [!DNL Experience Platform]提供可將單一[!DNL Experience Platform]執行個體分割成個別虛擬環境的虛擬沙箱，以利開發及改進數位體驗應用程式。

下列章節提供您需瞭解的其他資訊，才能使用[!DNL Flow Service] API成功連線到[!DNL FTP]伺服器。

### 收集必要的認證

為了讓[!DNL Flow Service]連線到[!DNL FTP]，您必須提供下列連線屬性的值：

| 認證 | 說明 |
| ---------- | ----------- |
| `host` | 與您的[!DNL FTP]伺服器關聯的名稱或IP位址。 |
| `username` | 可存取您[!DNL FTP]伺服器的使用者名稱。 |
| `password` | [!DNL FTP]伺服器的密碼。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 [!DNL FTP]的連線規格識別碼為： `fb2e94c9-c031-467d-8103-6bd6e0a432f2`。 |

### 使用Experience Platform API

如需如何成功呼叫Experience Platform API的詳細資訊，請參閱[Experience Platform API快速入門](../../../../../landing/api-guide.md)指南。

## 建立基礎連線

基本連線會保留來源與Experience Platform之間的資訊，包括來源的驗證認證、連線的目前狀態，以及唯一的基本連線ID。 基礎連線ID可讓您從來源內部探索及導覽檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

若要建立基底連線ID，請在提供您的[!DNL FTP]驗證認證作為要求引數的一部分時，對`/connections`端點提出POST要求。

**API格式**

```http
POST /connections
```

**要求**

下列要求會建立[!DNL FTP]的基礎連線：

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
| `auth.params.password` | 與您的FTP伺服器關聯的密碼。 |
| `connectionSpec.id` | FTP伺服器連線規格識別碼： `fb2e94c9-c031-467d-8103-6bd6e0a432f2` |

**回應**

成功的回應會傳回新建立之連線的唯一識別碼(`id`)。 在下一個教學課程中，探索您的FTP伺服器時，需要此ID。

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## 後續步驟

依照本教學課程，您已使用[!DNL Flow Service] API建立FTP連線，並已取得連線的唯一ID值。 您可以使用此連線ID來使用Flow Service API](../../explore/cloud-storage.md) [探索雲端儲存空間。
