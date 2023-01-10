---
keywords: Experience Platform；首頁；熱門主題；Azure;Azure檔案儲存；Azure檔案儲存
solution: Experience Platform
title: 使用流服務API建立Azure檔案儲存基礎連接
type: Tutorial
description: 了解如何使用流量服務API將Azure檔案儲存連線至Adobe Experience Platform。
exl-id: 0c585ae2-be2d-4167-b04b-836f7e2c04a9
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 1%

---

# 建立 [!DNL Azure File Storage] 基本連接使用 [!DNL Flow Service] API

基本連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程會逐步引導您完成建立基礎連線的步驟 [!DNL Azure File Storage] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../../../home.md): [!DNL Experience Platform] 可讓您從各種來源擷取資料，同時使用來建構、加標籤及增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供可分割單一沙箱的虛擬沙箱 [!DNL Platform] 例項放入個別的虛擬環境，以協助開發及改進數位體驗應用程式。

以下各節提供您需要了解的其他資訊，以便成功連接到 [!DNL Azure File Storage] 使用 [!DNL Flow Service] API。

### 收集所需憑據

為了 [!DNL Flow Service] 連線 [!DNL Azure File Storage]，您必須提供下列連線屬性的值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `host` | 的端點 [!DNL Azure File Storag]您正在存取的例項。 |
| `userId` | 具有足夠存取權的使用者 [!DNL Azure File Storage] 端點。 |
| `password` | 您 [!DNL Azure File Storage] 執行個體 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 的連接規範ID [!DNL Azure File Storage] 為： `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8`. |

如需快速入門的詳細資訊，請參閱 [此Azure檔案儲存文檔](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-windows).

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱 [Platform API快速入門](../../../../../landing/api-guide.md).

## 建立基本連接

基本連接在源和平台之間保留資訊，包括源的驗證憑據、連接的當前狀態和唯一基本連接ID。 基本連線ID可讓您從來源探索和導覽檔案，並識別您要擷取的特定項目，包括其資料類型和格式的相關資訊。

若要建立基本連線ID，請向 `/connections` 端點提供 [!DNL Azure File Storage] 驗證憑證作為要求參數的一部分。

**API格式**

```http
POST /connections
```

**要求**

下列請求會為 [!DNL Azure File Storage]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `auth.params.host` | 的端點 [!DNL Azure File Storage] 正在訪問的實例…… |
| `auth.params.userId` | 具有足夠存取權的使用者 [!DNL Azure File Storage] 端點。 |
| `auth.params.password` | 此 [!DNL Azure File Storage] 存取金鑰。 |
| `connectionSpec.id` | 此 [!DNL Azure File Storage] 連接規範ID: `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8`. |

**回應**

成功的回應會傳回新建立之基本連線的詳細資訊，包括其唯一識別碼(`id`)。 在下一步建立源連接時需要此ID。

```json
{
    "id": "f9377f50-607a-4818-b77f-50607a181860",
    "etag": "\"2f0276fa-0000-0200-0000-5eab3abb0000\""
}
```

## 後續步驟

依照本教學課程，您已建立 [!DNL Azure File Storage] 使用 [!DNL Flow Service] API，並已取得連線的唯一ID值。 您可以在下一個教學課程中使用此ID，以了解如何 [使用流量服務API探索協力廠商雲端儲存空間](../../explore/cloud-storage.md).
