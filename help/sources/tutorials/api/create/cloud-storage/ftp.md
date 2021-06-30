---
keywords: Experience Platform；首頁；熱門主題；檔案傳輸協定；檔案傳輸協定
solution: Experience Platform
title: 使用流量服務API建立FTP基礎連線
topic-legacy: overview
type: Tutorial
description: 了解如何使用流量服務API將Adobe Experience Platform連線至FTP（檔案傳輸通訊協定）伺服器。
exl-id: a7bef346-b357-49bc-ac54-ac8b42adac50
source-git-commit: 59a8e2aa86508e53f181ac796f7c03f9fcd76158
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 1%

---

# 使用[!DNL Flow Service] API建立FTP基礎連線

>[!NOTE]
>
>FTP連接器為測試版。 功能和檔案可能會有所變更。 有關使用測試版標籤連接器的詳細資訊，請參閱[來源概述](../../../../home.md#terms-and-conditions)。

基本連線代表來源和Adobe Experience Platform之間已驗證的連線。

本教學課程會逐步帶您了解使用[[!DNL Flow Service]  API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml)為[!DNL FTP]（檔案傳輸通訊協定）建立基本連線的步驟。

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../../../home.md): [!DNL Experience Platform] 可讓您從各種來源擷取資料，同時使用服務來建構、加標籤及增強傳入 [!DNL Platform] 資料。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供可將單一執行個體分割成個 [!DNL Platform] 別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

以下各節提供您需要知道的其他資訊，以便使用[!DNL Flow Service] API成功連接到[!DNL FTP]伺服器。

### 收集所需憑據

要使[!DNL Flow Service]連接到[!DNL FTP]，必須為以下連接屬性提供值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `host` | 與[!DNL FTP]伺服器相關聯的名稱或IP地址。 |
| `username` | 可訪問[!DNL FTP]伺服器的用戶名。 |
| `password` | [!DNL FTP]伺服器的密碼。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 [!DNL FTP]的連接規範ID為：`fb2e94c9-c031-467d-8103-6bd6e0a432f2`。 |

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱[Platform API快速入門手冊](../../../../../landing/api-guide.md)。

## 建立基本連接

基本連接在源和平台之間保留資訊，包括源的驗證憑據、連接的當前狀態和唯一基本連接ID。 基本連線ID可讓您從來源探索和導覽檔案，並識別您要擷取的特定項目，包括其資料類型和格式的相關資訊。

若要建立基本連線ID，請在提供[!DNL FTP]驗證憑證作為請求參數的一部分時，向`/connections`端點提出POST請求。

**API格式**

```http
POST /connections
```

**要求**

以下請求為[!DNL FTP]建立基本連接：

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
| `connectionSpec.id` | FTP伺服器連接規範ID:`fb2e94c9-c031-467d-8103-6bd6e0a432f2` |

**回應**

成功的響應返回新建立的連接的唯一標識符(`id`)。 在下一個教學課程中探索您的FTP伺服器需要此ID。

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## 後續步驟

依照本教學課程，您已使用[!DNL Flow Service] API建立FTP連線，並取得連線的唯一ID值。 您可以使用此連線ID來使用流量服務API](../../explore/cloud-storage.md)或[使用流量服務API](../../cloud-storage-parquet.md)內嵌Parquet資料，以探索雲儲存空間。[
