---
keywords: Experience Platform；首頁；熱門主題；Azure;Azure檔案儲存；Azure檔案儲存
solution: Experience Platform
title: 使用流服務API建立Azure檔案儲存源連接
topic-legacy: overview
type: Tutorial
description: 了解如何使用流量服務API將Azure檔案儲存連線至Adobe Experience Platform。
exl-id: 0c585ae2-be2d-4167-b04b-836f7e2c04a9
source-git-commit: e150f05df2107d7b3a2e95a55dc4ad072294279e
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 2%

---

# 使用[!DNL Flow Service] API建立[!DNL Azure File Storage]源連接

[!DNL Flow Service] 可用來收集和集中Adobe Experience Platform中各種不同來源的客戶資料。該服務提供用戶介面和RESTful API，所有受支援的源都可從中連接。

本教學課程使用[!DNL Flow Service] API來引導您完成將[!DNL Azure File Storage]連線至[!DNL Experience Platform]的步驟。

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../../../home.md): [!DNL Experience Platform] 可讓您從各種來源擷取資料，同時使用服務來建構、加標籤及增強傳入 [!DNL Platform] 資料。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供可將單一執行個體分割成個 [!DNL Platform] 別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

以下各節提供您需要知道的其他資訊，以便使用[!DNL Flow Service] API成功連接到[!DNL Azure File Storage]。

### 收集所需憑據

要使[!DNL Flow Service]與[!DNL Azure File Storage]連接，必須為以下連接屬性提供值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `host` | 您正在訪問的[!DNL Azure File Storag]e實例的端點。 |
| `userId` | 對[!DNL Azure File Storage]端點具有足夠訪問權限的用戶。 |
| `password` | [!DNL Azure File Storage]實例的密碼 |
| 連接規範ID | 建立連線所需的唯一識別碼。 [!DNL Azure File Storage]的連接規範ID為：`be5ec48c-5b78-49d5-b8fa-7c89ec4569b8` |

有關入門的詳細資訊，請參閱[此Azure檔案儲存文檔](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-windows)。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定要求格式。 這些功能包括路徑、必要標題和格式正確的請求裝載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所使用慣例的資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集必要標題的值

若要呼叫[!DNL Platform] API，您必須先完成[authentication tutorial](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程後，將提供所有[!DNL Experience Platform] API呼叫中每個必要標題的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有資源，包括屬於[!DNL Flow Service]的資源，都與特定虛擬沙箱隔離。 對[!DNL Platform] API的所有請求都需要標題，以指定作業將在下列位置進行的沙箱名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含裝載(POST、PUT、PATCH)的請求都需要其他媒體類型標題：

* `Content-Type: application/json`

## 建立連線

連接指定源，並包含該源的憑據。 每個[!DNL Azure File Storage]帳戶只需一個連接，因為它可用於建立多個源連接器以導入不同的資料。

**API格式**

```http
POST /connections
```

**要求**

若要建立[!DNL Azure File Storage]連線，必須在POST請求中提供其唯一連線規格ID。 [!DNL Azure File Storage]的連接規範ID為`be5ec48c-5b78-49d5-b8fa-7c89ec4569b8`。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
        -d '{
        "name": "Azure File Storage connection",
        "description": "An Azure File Storage test connection",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                    "host": "{HOST}",
                    "userId": "{USER_ID}",
                    "password": "{PASSWORD}"
                }
        },
        "connectionSpec": {
            "id": "be5ec48c-5b78-49d5-b8fa-7c89ec4569b8",
            "version": "1.0"
        }
    }'
```

| 屬性 | 說明 |
| --------- | ----------- |
| `auth.params.host` | 您正在訪問的[!DNL Azure File Storage]實例的端點。 |
| `auth.params.userId` | 對[!DNL Azure File Storage]端點具有足夠訪問權限的用戶。 |
| `auth.params.password` | [!DNL Azure File Storage]訪問密鑰。 |
| `connectionSpec.id` | [!DNL Azure File Storage]連接規範ID:`be5ec48c-5b78-49d5-b8fa-7c89ec4569b8`。 |

**回應**

成功的響應返回新建立連接的詳細資訊，包括其唯一標識符(`id`)。 在下一個教學課程中探索資料時需要此ID。

```json
{
    "id": "f9377f50-607a-4818-b77f-50607a181860",
    "etag": "\"2f0276fa-0000-0200-0000-5eab3abb0000\""
}
```

## 後續步驟

依照本教學課程，您已使用[!DNL Flow Service] API建立[!DNL Azure File Storage]連線，並取得連線的唯一ID值。 在您了解如何使用流量服務API](../../explore/cloud-storage.md)探索協力廠商雲端儲存空間時，您可以在下一個教學課程中使用此ID。[
