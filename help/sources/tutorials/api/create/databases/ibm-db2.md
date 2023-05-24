---
keywords: Experience Platform；首頁；熱門主題；IBM [!DNL IBM DB2];IBM [!DNL IBM DB2];[!DNL IBM DB2];[!DNL IBM DB2]
solution: Experience Platform
title: 建立IBM [!DNL IBM DB2] 使用流服務API的基連接
type: Tutorial
description: 瞭解如何連接IBM [!DNL IBM DB2] 到Adobe Experience Platform。
exl-id: 83c1dbe6-975f-4e3b-a7bf-166eb5106dd2
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 1%

---

# 建立IBM [!DNL IBM DB2] 基本連接使用 [!DNL Flow Service] API

>[!NOTE]
>
>IBM [!DNL IBM DB2] 連接器位於beta中。 查看 [源概述](../../../../home.md#terms-and-conditions) 的子菜單。

基連接表示源和Adobe Experience Platform之間經過驗證的連接。

本教程將指導您完成建立基本連接的步驟 [!DNL IBM DB2] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)。

## 快速入門

本指南要求對Adobe Experience Platform的下列組成部分有工作上的理解：

* [源](../../../../home.md): [!DNL Experience Platform] 允許從各種源接收資料，同時讓您能夠使用平台服務構建、標籤和增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙箱，將單個平台實例分區到單獨的虛擬環境中，以幫助開發和發展數字型驗應用程式。

以下各節提供了要成功連接到所需的其他資訊 [!DNL IBM DB2] 使用 [!DNL Flow Service] API。

| 憑據 | 說明 |
| ---------- | ----------- |
| `server` | 名稱 [!DNL IBM DB2] 伺服器。 可以在伺服器名稱后指定埠號（以冒號分隔）。 例如：伺服器：埠。 |
| `database` | 名稱 [!DNL IBM DB2] 資料庫。 |
| `username` | 用於連接到 [!DNL IBM DB2] 資料庫。 |
| `password` | 為用戶名指定的用戶帳戶的密碼。 |
| `connectionSpec.id` | 建立連接所需的唯一標識符。 連接規範ID [!DNL IBM DB2] 是 `09182899-b429-40c9-a15a-bf3ddbc8ced7`。 |

有關入門的詳細資訊，請參閱 [這個 [!DNL IBM DB2] 文檔](https://www.ibm.com/support/knowledgecenter/SSFMBX/com.ibm.swg.im.dashdb.doc/connecting/connect_credentials.html)。

### 使用平台API

有關如何成功調用平台API的資訊，請參見上的指南 [平台API入門](../../../../../landing/api-guide.md)。

## 建立基本連接

基本連接將保留源和平台之間的資訊，包括源的驗證憑據、連接的當前狀態和唯一的基本連接ID。 基本連接ID允許您從源中瀏覽和導航檔案，並標識要攝取的特定項目，包括有關其資料類型和格式的資訊。

要建立基本連接ID，請向 `/connections` 提供端點 [!DNL IBM DB2] 身份驗證憑據作為請求參數的一部分。

**API格式**

```https
POST /connections
```

**要求**

以下請求為 [!DNL IBM DB2]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "[!DNL IBM DB2] connection",
        "description": "[!DNL IBM DB2] test connection",
        "auth": {
            "specName": "Basic Authentication",
            "params": {
                    "server": "{SERVER}",
                    "database": "{DATABASE}",
                    "authenticationType": "{AUTHENTICATION_TYPE}",
                    "username": "{USERNAME}",
                    "password": "{PASSWORD}"
                }
        },
        "connectionSpec": {
            "id": "09182899-b429-40c9-a15a-bf3ddbc8ced7",
            "version": "1.0"
        }
    }'
```

| 參數 | 說明 |
| --------- | ----------- |
| `auth.params.connectionString` | 與您的 [!DNL IBM DB2] 帳戶。 |
| `connectionSpec.id` | 的 [!DNL IBM DB2] 連接規範ID: `09182899-b429-40c9-a15a-bf3ddbc8ced7`。 |

**回應**

成功的響應返回新建立的連接的詳細資訊，包括其唯一標識符(`id`)。 在下一教程中瀏覽資料時需要此ID。

```json
{
    "id": "575abae5-c99a-452c-9aba-e5c99ac52c4d",
    "etag": "\"e5012c89-0000-0200-0000-5eaa036b0000\""
}
```

## 後續步驟

按照本教程，您建立了 [!DNL IBM DB2] 基本連接使用 [!DNL Flow Service] API。 您可以在以下教程中使用此基本連接ID:

* [使用 [!DNL Flow Service] API](../../explore/tabular.md)
* [建立資料流，使用 [!DNL Flow Service] API](../../collect/database-nosql.md)

