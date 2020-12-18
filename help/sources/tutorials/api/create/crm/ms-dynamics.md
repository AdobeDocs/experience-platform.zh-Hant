---
keywords: Experience Platform;home;popular topics;Microsoft Dynamics;microsoft dynamics;dynamics;Dynamics
solution: Experience Platform
title: 使用Flow Service API建立Microsoft Dynamics連接器
topic: overview
type: Tutorial
description: 本教學課程使用Flow Service API來引導您完成將平台連接至Microsoft Dynamics（以下稱為「Dynamics」）帳戶以收集CRM資料的步驟。
translation-type: tm+mt
source-git-commit: 9092c3d672967d3f6f7bf7116c40466a42e6e7b1
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 2%

---


# 使用[!DNL Flow Service] API建立[!DNL Microsoft Dynamics]連接器

[!DNL Flow Service] 用於收集和集中Adobe Experience Platform內不同來源的客戶資料。該服務提供用戶介面和REST風格的API，所有支援的源都可從中連接。

本教學課程使用[!DNL Flow Service] API來引導您完成將[!DNL Platform]連接至[!DNL Microsoft Dynamics]（以下稱為「Dynamics」）帳戶以收集CRM資料的步驟。

## 快速入門

本指南需要有效瞭解Adobe Experience Platform的下列元件：

* [來源](../../../../home.md): [!DNL Experience Platform] 允許從各種來源接收資料，同時提供使用服務構建、標籤和增強傳入資料的 [!DNL Platform] 能力。
* [沙盒](../../../../../sandboxes/home.md):提[!DNL xperience Platform] 供虛擬沙盒，將單一執行個體分割 [!DNL Platform] 成不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您必須知道的其他資訊，以便使用[!DNL Flow Service] API成功將[!DNL Platform]連線至Dynamics帳戶。

### 收集必要的認證

要使[!DNL Flow Service]連接到[!DNL Dynamics]，必須為以下連接屬性提供值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `serviceUri` | [!DNL Dynamics]實例的服務URL。 |
| `username` | [!DNL Dynamics]使用者帳戶的使用者名稱。 |
| `password` | [!DNL Dynamics]帳戶的密碼。 |

有關開始使用的詳細資訊，請造訪[本Dynamics檔案](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth)。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集必要標題的值

若要呼叫[!DNL Platform] API，您必須先完成[驗證教學課程](../../../../../tutorials/authentication.md)。 完成驗證教學課程後，所有[!DNL Experience Platform] API呼叫中每個所需標題的值都會顯示在下面：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有資源（包括屬於[!DNL Flow Service]的資源）都隔離到特定的虛擬沙盒。 對[!DNL Platform] API的所有請求都需要一個標題，該標題指定要在中執行操作的沙盒的名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的媒體類型標題：

* `Content-Type: application/json`

## 建立連線

連接指定源，並包含該源的憑據。 每個[!DNL Dynamics]帳戶只需要一個連接，因為它可用於建立多個源連接器以導入不同的資料。

**API格式**

```http
POST /connections
```

**請求**

要建立[!DNL Dynamics]連接，必須在POST請求中提供其唯一連接規範ID。 [!DNL Dynamics]的連接規範ID為`38ad80fe-8b06-4938-94f4-d4ee80266b07`。

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Dynamics Connection",
        "description": "connection for Dynamics account",
        "auth": {
            "specName": "Basic Authentication for Dynamics-Online",
            "params": {
                "serviceUri": "{SERVICE_URI}",
                "username": "{USERNAME}",
                "password": "{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
            "version": "1.0"
        }
    }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `auth.params.serviceUri` | 與[!DNL Dynamics]實例關聯的服務URI。 |
| `auth.params.username` | 與[!DNL Dynamics]帳戶關聯的使用者名稱。 |
| `auth.params.password` | 與[!DNL Dynamics]帳戶關聯的密碼。 |
| `connectionSpec.id` | 在上一步中檢索的[!DNL Dynamics]帳戶的連接規範`id`。 |

**回應**

成功的響應返回新建立的連接，包括其唯一標識符(`id`)。 在下一步中探索您的CRM系統時，需要此ID。

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

## 後續步驟

在本教程中，您使用[!DNL Flow Service] API建立了[!DNL Dynamics]連接，並獲取了該連接的唯一ID值。 您可在下一個教學課程中使用此ID，同時學習如何使用Flow Service API[來探索CRM系統。](../../explore/crm.md)