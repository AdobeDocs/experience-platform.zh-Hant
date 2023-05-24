---
keywords: Experience Platform；首頁；熱門主題；Azure;Azure檔案儲存；Azure檔案儲存
solution: Experience Platform
title: 使用流服務API建立Azure檔案儲存基連接
type: Tutorial
description: 瞭解如何使用流服務API將Azure檔案儲存連接到Adobe Experience Platform。
exl-id: 0c585ae2-be2d-4167-b04b-836f7e2c04a9
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 1%

---

# 建立 [!DNL Azure File Storage] 基本連接使用 [!DNL Flow Service] API

基連接表示源和Adobe Experience Platform之間經過驗證的連接。

本教程將指導您完成建立基本連接的步驟 [!DNL Azure File Storage] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)。

## 快速入門

本指南要求對Adobe Experience Platform的下列組成部分有工作上的理解：

* [源](../../../../home.md): [!DNL Experience Platform] 允許從各種源接收資料，同時讓您能夠使用 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙箱，將單個沙箱 [!DNL Platform] 實例到獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

以下各節提供了要成功連接到所需的其他資訊 [!DNL Azure File Storage] 使用 [!DNL Flow Service] API。

### 收集所需憑據

為了 [!DNL Flow Service] 連接 [!DNL Azure File Storage]，必須為以下連接屬性提供值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `host` | 的端點 [!DNL Azure File Storag]正在訪問的實例。 |
| `userId` | 具有足夠訪問權限的用戶 [!DNL Azure File Storage] 端點。 |
| `password` | 您的密碼 [!DNL Azure File Storage] 實例 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 連接規範ID [!DNL Azure File Storage] 為： `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8`。 |

有關入門的詳細資訊，請參閱 [此Azure檔案儲存文檔](https://docs.microsoft.com/en-us/azure/storage/files/storage-how-to-use-files-windows)。

### 使用平台API

有關如何成功調用平台API的資訊，請參見上的指南 [平台API入門](../../../../../landing/api-guide.md)。

## 建立基本連接

基本連接將保留源和平台之間的資訊，包括源的驗證憑據、連接的當前狀態和唯一的基本連接ID。 基本連接ID允許您從源中瀏覽和導航檔案，並標識要攝取的特定項目，包括有關其資料類型和格式的資訊。

要建立基本連接ID，請向 `/connections` 提供端點 [!DNL Azure File Storage] 身份驗證憑據作為請求參數的一部分。

**API格式**

```http
POST /connections
```

**要求**

以下請求為 [!DNL Azure File Storage]:

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
| `auth.params.userId` | 具有足夠訪問權限的用戶 [!DNL Azure File Storage] 端點。 |
| `auth.params.password` | 的 [!DNL Azure File Storage] 訪問密鑰。 |
| `connectionSpec.id` | 的 [!DNL Azure File Storage] 連接規範ID: `be5ec48c-5b78-49d5-b8fa-7c89ec4569b8`。 |

**回應**

成功的響應返回新建立的基本連接的詳細資訊，包括其唯一標識符(`id`)。 在下一步建立源連接時需要此ID。

```json
{
    "id": "f9377f50-607a-4818-b77f-50607a181860",
    "etag": "\"2f0276fa-0000-0200-0000-5eab3abb0000\""
}
```

## 後續步驟

按照本教程，您建立了 [!DNL Azure File Storage] 使用 [!DNL Flow Service] API，並已獲取連接的唯一ID值。 在學習如何 [使用流服務API瀏覽第三方雲儲存](../../explore/cloud-storage.md)。
