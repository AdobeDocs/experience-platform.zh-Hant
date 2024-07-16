---
keywords: Experience Platform；首頁；熱門主題；Azure；Azure檔案儲存；Azure檔案儲存
solution: Experience Platform
title: 使用Flow Service API建立Azure檔案儲存基礎連線
type: Tutorial
description: 瞭解如何使用Flow Service API將Azure檔案儲存體連線至Adobe Experience Platform。
exl-id: 0c585ae2-be2d-4167-b04b-836f7e2c04a9
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 4%

---

# 使用[!DNL Flow Service] API建立[!DNL Azure File Storage]基本連線

基礎連線代表來源和Adobe Experience Platform之間的已驗證連線。

本教學課程將逐步引導您使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)為[!DNL Azure File Storage]建立基礎連線的步驟。

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

* [來源](../../../../home.md)： [!DNL Experience Platform]允許從各種來源擷取資料，同時讓您能夠使用[!DNL Platform]服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)： [!DNL Experience Platform]提供可將單一[!DNL Platform]執行個體分割成個別虛擬環境的虛擬沙箱，以利開發及改進數位體驗應用程式。

下列章節提供您需瞭解的其他資訊，才能使用[!DNL Flow Service] API成功連線到[!DNL Azure File Storage]。

### 收集必要的認證

為了讓[!DNL Flow Service]與[!DNL Azure File Storage]連線，您必須提供下列連線屬性的值：

| 認證 | 說明 |
| ---------- | ----------- |
| `host` | 您正在存取之[!DNL Azure File Storag]e執行個體的端點。 |
| `userId` | 具有足夠許可權存取[!DNL Azure File Storage]端點的使用者。 |
| `password` | 您的[!DNL Azure File Storage]執行個體的密碼 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 [!DNL Azure File Storage]的連線規格識別碼為： `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8`。 |

如需開始使用的詳細資訊，請參閱[此Azure檔案儲存檔案](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-windows)。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱[Platform API快速入門](../../../../../landing/api-guide.md)的指南。

## 建立基礎連線

基礎連線會保留您的來源和平台之間的資訊，包括來源的驗證認證、連線的目前狀態，以及您唯一的基本連線ID。 基礎連線ID可讓您從來源內部探索及導覽檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

若要建立基底連線ID，請在提供[!DNL Azure File Storage]驗證認證作為要求引數的一部分時，向`/connections`端點提出POST要求。

**API格式**

```http
POST /connections
```

**要求**

下列要求會建立[!DNL Azure File Storage]的基礎連線：

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
| `auth.params.host` | 您正在存取之[!DNL Azure File Storage]執行個體的端點…… |
| `auth.params.userId` | 具有足夠許可權存取[!DNL Azure File Storage]端點的使用者。 |
| `auth.params.password` | [!DNL Azure File Storage]存取金鑰。 |
| `connectionSpec.id` | [!DNL Azure File Storage]連線規格識別碼： `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8`。 |

**回應**

成功的回應會傳回新建立的基礎連線的詳細資料，包括其唯一識別碼(`id`)。 建立來源連線的下一個步驟需要此ID。

```json
{
    "id": "f9377f50-607a-4818-b77f-50607a181860",
    "etag": "\"2f0276fa-0000-0200-0000-5eab3abb0000\""
}
```

## 後續步驟

依照本教學課程中的指示，您已使用[!DNL Flow Service] API建立[!DNL Azure File Storage]連線，並已取得連線的唯一ID值。 您可在下一個教學課程中使用此ID，瞭解如何使用Flow Service API[探索協力廠商雲端儲存空間](../../explore/cloud-storage.md)。
