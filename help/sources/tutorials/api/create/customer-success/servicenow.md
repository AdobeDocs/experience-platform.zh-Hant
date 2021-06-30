---
keywords: Experience Platform；首頁；熱門主題；servicenow;ServiceNow
solution: Experience Platform
title: 使用流服務API建立ServiceNow Base連接
topic-legacy: overview
type: Tutorial
description: 了解如何使用Flow Service API將Adobe Experience Platform連線至ServiceNow伺服器。
exl-id: 39d0e628-5c07-4371-a5af-ac06385db891
source-git-commit: ff0f6bc6b8a57b678b329fe2b47c53919e0e2d64
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 1%

---

# 使用[!DNL Flow Service] API建立[!DNL ServiceNow]基本連線

基本連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程會逐步引導您使用[[!DNL Flow Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)建立[!DNL Google ServiceNow]基本連線的步驟。

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../../../home.md): [!DNL Experience Platform] 可讓您從各種來源擷取資料，同時使用服務來建構、加標籤及增強傳入 [!DNL Platform] 資料。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供可將單一執行個體分割成個 [!DNL Platform] 別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

以下各節提供您需要知道的其他資訊，以便使用[!DNL Flow Service] API成功連接到[!DNL ServiceNow]伺服器。

### 收集所需憑據

要使[!DNL Flow Service]連接到[!DNL ServiceNow]，必須為以下連接屬性提供值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `endpoint` | [!DNL ServiceNow]伺服器的端點。 |
| `username` | 用於連接到[!DNL ServiceNow]伺服器進行身份驗證的用戶名。 |
| `password` | 連接到[!DNL ServiceNow]伺服器以進行身份驗證的密碼。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 [!DNL ServiceNow]的連接規範ID為：`eb13cb25-47ab-407f-ba89-c0125281c563`。 |

有關入門的詳細資訊，請參閱[此ServiceNow文檔](https://developer.servicenow.com/app.do#!/rest_api_doc?v=newyork&amp;id=r_TableAPI-GET)。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱[Platform API快速入門手冊](../../../../../landing/api-guide.md)。

## 建立基本連接

基本連接在源和平台之間保留資訊，包括源的驗證憑據、連接的當前狀態和唯一基本連接ID。 基本連線ID可讓您從來源探索和導覽檔案，並識別您要擷取的特定項目，包括其資料類型和格式的相關資訊。

若要建立基本連線ID，請在提供[!DNL ServiceNow]驗證憑證作為請求參數的一部分時，向`/connections`端點提出POST請求。

**API格式**

```http
POST /connections
```

**要求**

以下請求為[!DNL ServiceNow]建立基本連接：

```shell
curl -X POST \
    'http://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Connection for service-now",
        "description": "Connection for service-now,
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                "endpoint": "{ENDPOINT}",
                "username": "{USERNAME}",
                "password": "{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "eb13cb25-47ab-407f-ba89-c0125281c563",
            "version": "1.0"
        }
    }'
```

| 參數 | 說明 |
| --------- | ----------- |
| `auth.params.server` | [!DNL ServiceNow]伺服器的端點。 |
| `auth.params.username` | 用於連接到[!DNL ServiceNow]伺服器進行身份驗證的用戶名。 |
| `auth.params.password` | 連接到[!DNL ServiceNow]伺服器以進行身份驗證的密碼。 |
| `connectionSpec.id` | [!DNL ServiceNow]連接規範ID:`eb13cb25-47ab-407f-ba89-c0125281c563` |

**回應**

成功的響應返回新建立的連接，包括其唯一標識符(`id`)。 在下一個步驟中探索您的CRM系統時需要此ID。

```json
{
    "id": "8a3ca3dd-6d00-4c95-bca3-dd6d00dc954b",
    "etag": "\"8e0052a2-0000-0200-0000-5e25fb330000\""
}
```

## 後續步驟

依照本教學課程，您已使用[!DNL Flow Service] API建立[!DNL ServiceNow]連線，並取得連線的唯一ID值。 在您了解如何使用流量服務API](../../explore/customer-success.md)探索客戶成功系統時，您可以在下一個教學課程中使用此連線ID。[
