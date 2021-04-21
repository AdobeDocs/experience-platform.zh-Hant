---
keywords: Experience Platform; home；熱門主題；檔案傳輸協定；檔案傳輸協定
solution: Experience Platform
title: 使用流程服務API建立FTP來源連線
topic-legacy: overview
type: Tutorial
description: 瞭解如何使用Flow Service API將Adobe Experience Platform連接至FTP（檔案傳輸通訊協定）伺服器。
exl-id: a7bef346-b357-49bc-ac54-ac8b42adac50
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 2%

---

# 使用[!DNL Flow Service] API建立FTP來源連線

>[!NOTE]
>
>FTP連接器處於測試階段。 功能和檔案可能會有所變更。 有關使用beta標籤連接器的詳細資訊，請參閱[ Sources綜覽](../../../../home.md#terms-and-conditions)。

本教學課程使用[!DNL Flow Service] API來引導您完成將[!DNL Experience Platform]連接至FTP（檔案傳輸通訊協定）伺服器的步驟。

## 快速入門

本指南需要對Adobe Experience Platform的下列組成部分有切實的瞭解：

* [來源](../../../../home.md): [!DNL Experience Platform] 允許從各種來源接收資料，同時提供使用服務構建、標籤和增強傳入資料的 [!DNL Platform] 能力。
* [沙盒](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙盒，可將單一執行個體分 [!DNL Platform] 割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您需要知道的其他資訊，以便使用[!DNL Flow Service] API成功連線至FTP伺服器。

### 收集必要的認證

要使[!DNL Flow Service]連接到FTP，必須為以下連接屬性提供值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `host` | 與您的FTP伺服器相關聯的名稱或IP位址。 |
| `username` | 可存取您FTP伺服器的使用者名稱。 |
| `password` | FTP伺服器的密碼。 |

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集必要標題的值

若要呼叫[!DNL Platform] API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程後，所有[!DNL Experience Platform] API呼叫中每個所需標題的值都會顯示在下面：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有資源（包括屬於[!DNL Flow Service]的資源）都與特定虛擬沙盒隔離。 對[!DNL Platform] API的所有請求都需要一個標題，該標題指定要在中執行操作的沙盒的名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含裝載(POST、PUT、PATCH)的請求都需要附加的媒體類型標題：

* `Content-Type: application/json`

## 建立連線

連接指定源，並包含該源的憑據。 每個FTP帳戶只需要一個連線，因為它可用來建立多個來源連接器，以匯入不同的資料。

### 使用基本驗證建立FTP連線

若要使用基本驗證建立FTP連線，請向[!DNL Flow Service] API提出POST要求，同時提供連線的`host`、`userName`和`password`值。

**API格式**

```http
POST /connections
```

**要求**

若要建立FTP連線，其唯一的連線規格ID必須作為POST要求的一部分提供。 FTP的連接規範ID為`fb2e94c9-c031-467d-8103-6bd6e0a432f2`。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `connectionSpec.id` | FTP伺服器連線規格ID:`fb2e94c9-c031-467d-8103-6bd6e0a432f2` |

**回應**

成功的響應返回新建立的連接的唯一標識符(`id`)。 在下一個教學課程中探索FTP伺服器時，需要此ID。

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## 後續步驟

在本教程中，您已使用[!DNL Flow Service] API建立FTP連線，並已取得連線的唯一ID值。 您可以使用此連線ID來探索使用Flow Service API](../../explore/cloud-storage.md)或[使用Flow Service API](../../cloud-storage-parquet.md)來內嵌Parce資料的雲端儲存空間。[
