---
keywords: Experience Platform；首頁；熱門主題；檔案傳輸協定；檔案傳輸協定
solution: Experience Platform
title: 使用流服務API建立FTP基連接
type: Tutorial
description: 瞭解如何使用流服務API將Adobe Experience Platform連接到FTP（檔案傳輸協定）伺服器。
exl-id: a7bef346-b357-49bc-ac54-ac8b42adac50
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 1%

---

# 使用 [!DNL Flow Service] API

>[!NOTE]
>
>FTP接頭處於Beta狀態。 功能和文檔可能會更改。 查看 [源概述](../../../../home.md#terms-and-conditions) 的子菜單。

基連接表示源和Adobe Experience Platform之間經過驗證的連接。

本教程將指導您完成建立基本連接的步驟 [!DNL FTP] （檔案傳輸協定） [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)。

## 快速入門

本指南要求對Adobe Experience Platform的下列組成部分有工作上的理解：

* [源](../../../../home.md): [!DNL Experience Platform] 允許從各種源接收資料，同時讓您能夠使用 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙箱，將單個沙箱 [!DNL Platform] 實例到獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

以下各節提供了成功連接到 [!DNL FTP] 使用 [!DNL Flow Service] API。

### 收集所需憑據

為了 [!DNL Flow Service] 連接到 [!DNL FTP]，必須為以下連接屬性提供值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `host` | 與您的 [!DNL FTP] 伺服器。 |
| `username` | 有權訪問您的 [!DNL FTP] 伺服器。 |
| `password` | 您的密碼 [!DNL FTP] 伺服器。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 連接規範ID [!DNL FTP] 為： `fb2e94c9-c031-467d-8103-6bd6e0a432f2`。 |

### 使用平台API

有關如何成功調用平台API的資訊，請參見上的指南 [平台API入門](../../../../../landing/api-guide.md)。

## 建立基本連接

基本連接將保留源和平台之間的資訊，包括源的驗證憑據、連接的當前狀態和唯一的基本連接ID。 基本連接ID允許您從源中瀏覽和導航檔案，並標識要攝取的特定項目，包括有關其資料類型和格式的資訊。

要建立基本連接ID，請向 `/connections` 提供端點 [!DNL FTP] 身份驗證憑據作為請求參數的一部分。

**API格式**

```http
POST /connections
```

**要求**

以下請求為 [!DNL FTP]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `auth.params.host` | FTP伺服器的主機名。 |
| `auth.params.username` | 與FTP伺服器關聯的用戶名。 |
| `auth.params.password` | 與FTP伺服器關聯的密碼。 |
| `connectionSpec.id` | FTP伺服器連接規範ID: `fb2e94c9-c031-467d-8103-6bd6e0a432f2` |

**回應**

成功的響應返回唯一標識符(`id`)。 在下一教程中瀏覽FTP伺服器時需要此ID。

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## 後續步驟

按照本教程，您已使用 [!DNL Flow Service] API，並已獲取連接的唯一ID值。 您可以使用此連接ID [使用流服務API瀏覽雲儲存](../../explore/cloud-storage.md)。
