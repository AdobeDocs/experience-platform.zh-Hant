---
keywords: Experience Platform；首頁；熱門主題；Oracle服務雲；oracle服務雲
title: 使用流服務API建立Oracle服務雲源連接
description: 瞭解如何使用流服務API將Adobe Experience Platform連接到Oracle服務雲。
exl-id: 00c0bc9c-a740-4bab-a882-2cfed8abe758
source-git-commit: 1695b7d638feb648d5cd7af07879f3ed13f938eb
workflow-type: tm+mt
source-wordcount: '527'
ht-degree: 1%

---

# 使用以下項建立Oracle服務雲源連接： [!DNL Flow Service] API

基連接表示源和Adobe Experience Platform之間經過驗證的連接。

本教程將引導您完成使用以下步驟建立Oracle服務雲的基本連接： [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)。

## 快速入門

本指南要求對以下Experience Platform元件進行工作理解：

* [源](../../../../home.md):Experience Platform允許從各種源接收資料，同時讓您能夠使用平台服務構建、標籤和增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供虛擬沙箱，將單個平台實例分區為獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

以下各節提供您需要瞭解的其他資訊，以便使用 [!DNL Flow Service] API。

### 收集所需憑據

為了 [!DNL Flow Service] 要與Oracle服務雲連接，必須提供以下連接屬性的值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `host` | oracle服務雲實例的主機URL。 |
| `username` | oracle服務雲用戶帳戶的用戶名。 |
| `password` | oracle服務雲帳戶的密碼。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 oracle服務雲的連接規範ID為： `ba5126ec-c9ac-11eb-b8bc-0242ac130003`。 |

有關驗證Oracle服務雲帳戶的詳細資訊，請參閱 [[!DNL Oracle] 認證指南](https://docs.oracle.com/en/cloud/saas/b2c-service/20c/cxska/OKCS_Authenticate_and_Authorize.html)。

### 使用平台API

有關如何成功調用平台API的資訊，請參見上的指南 [平台API入門](../../../../../landing/api-guide.md)。

## 建立基本連接

基本連接將保留源和平台之間的資訊，包括源的驗證憑據、連接的當前狀態和唯一的基本連接ID。 基本連接ID允許您從源中瀏覽和導航檔案，並標識要攝取的特定項目，包括有關其資料類型和格式的資訊。

要建立基本連接ID，請向 `/connections` 端點，同時提供Oracle服務雲身份驗證憑據作為請求參數的一部分。

**API格式**

```http
POST /connections
```

**要求**

以下請求為Oracle服務雲建立基連接：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Base connection for Oracle Service Cloud",
      "description": "Base connection for Oracle Service Cloud",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "host": "{HOST}",
              "username": "{USERNAME}",
              "password": "{PASSWORD}"
          }
      },
      "connectionSpec": {
          "id": "ba5126ec-c9ac-11eb-b8bc-0242ac130003",
          "version": "1.0"
      }
  }'
```

| 參數 | 說明 |
| --------- | ----------- |
| `auth.params.host` | oracle服務雲實例的主機URL。 |
| `auth.params.username` | 與您的Oracle服務雲帳戶關聯的用戶名。 |
| `auth.params.password` | 與您的Oracle服務雲帳戶關聯的密碼。 |
| `connectionSpec.id` | oracle服務雲連接規範ID: `ba5126ec-c9ac-11eb-b8bc-0242ac130003` |

**回應**

成功的響應返回新建立的連接，包括其唯一標識符(`id`)。 在下一步中瀏覽CRM系統需要此ID。

```json
{
    "id": "4267c2ab-2104-474f-a7c2-ab2104d74f86",
    "etag": "\"0200f1c5-0000-0200-0000-5e4352bf0000\""
}
```

## 後續步驟

通過遵循本教程，您已使用 [!DNL Flow Service] API。 您可以在以下教程中使用此基本連接ID:

* [使用 [!DNL Flow Service] API](../../explore/tabular.md)
* [建立資料流，使用 [!DNL Flow Service] API](../../collect/customer-success.md)
