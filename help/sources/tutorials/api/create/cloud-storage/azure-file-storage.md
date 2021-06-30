---
keywords: Experience Platform；首頁；熱門主題；Azure;Azure檔案儲存；Azure檔案儲存
solution: Experience Platform
title: 使用流服務API建立Azure檔案儲存基礎連接
topic-legacy: overview
type: Tutorial
description: 了解如何使用流量服務API將Azure檔案儲存連線至Adobe Experience Platform。
exl-id: 0c585ae2-be2d-4167-b04b-836f7e2c04a9
source-git-commit: 59a8e2aa86508e53f181ac796f7c03f9fcd76158
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 1%

---

# 使用[!DNL Flow Service] API建立[!DNL Azure File Storage]基本連線

基本連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程會逐步引導您使用[[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)建立[!DNL Azure File Storage]基本連線的步驟。

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
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 [!DNL Azure File Storage]的連接規範ID為：`be5ec48c-5b78-49d5-b8fa-7c89ec4569b8`。 |

有關入門的詳細資訊，請參閱[此Azure檔案儲存文檔](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-windows)。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱[Platform API快速入門手冊](../../../../../landing/api-guide.md)。

## 建立基本連接

基本連接在源和平台之間保留資訊，包括源的驗證憑據、連接的當前狀態和唯一基本連接ID。 基本連線ID可讓您從來源探索和導覽檔案，並識別您要擷取的特定項目，包括其資料類型和格式的相關資訊。

若要建立基本連線ID，請在提供[!DNL Azure File Storage]驗證憑證作為請求參數的一部分時，向`/connections`端點提出POST請求。

**API格式**

```http
POST /connections
```

**要求**

以下請求為[!DNL Azure File Storage]建立基本連接：

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

成功的響應返回新建立的基本連接的詳細資訊，包括其唯一標識符(`id`)。 在下一步建立源連接時需要此ID。

```json
{
    "id": "f9377f50-607a-4818-b77f-50607a181860",
    "etag": "\"2f0276fa-0000-0200-0000-5eab3abb0000\""
}
```

## 後續步驟

依照本教學課程，您已使用[!DNL Flow Service] API建立[!DNL Azure File Storage]連線，並取得連線的唯一ID值。 在您了解如何使用流量服務API](../../explore/cloud-storage.md)探索協力廠商雲端儲存空間時，您可以在下一個教學課程中使用此ID。[
