---
title: 使用流量服務API建立Phoenix基本連線
description: 瞭解如何使用流量服務API將Phoenix資料庫連線至Adobe Experience Platform。
exl-id: b69d9593-06fe-4fff-88a9-7860e4e45eb7
source-git-commit: efffd6ce1ed541ce20ee6500e42165465f2fa6a0
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 4%

---

# 建立 [!DNL Phoenix] 基礎連線使用 [!DNL Flow Service] API

基礎連線代表來源和Adobe Experience Platform之間的已驗證連線。

本教學課程提供如何建立基礎連線及連線您的 [!DNL Phoenix] Adobe Experience Platform帳戶使用 [!DNL Flow Service] API。

## 快速入門

本指南需要您深入了解下列 Experience Platform 元件：

* [來源](../../../../home.md)：Experience Platform可讓您從各種來源擷取資料，同時使用Experience Platform服務來建構、加標籤及增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md)：Experience Platform提供的虛擬沙箱可將單一Experience Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

以下小節提供成功連線所需的其他資訊 [!DNL Phoenix] 使用 [!DNL Flow Service] API。

### 收集必要的認證

您必須提供下列驗證認證，才能連線您的 [!DNL Phoenix] 要Experience Platform的帳戶。

| 認證 | 說明 |
| ---------- | ----------- |
| `host` | 的IP位址或主機名稱 [!DNL Phoenix] 伺服器。 |
| `username` | 您用來存取的使用者名稱 [!DNL Phoenix] 伺服器。 |
| `password` | 與使用者對應的密碼。 |
| `port` | TCP連線埠， [!DNL Phoenix] 伺服器使用來監聽使用者端連線。 如果您要連線到 [!DNL Azure HDInsights]，然後將連線埠指定為443。 如果未提供此引數，則值預設為8765。 |
| `httpPath` | 與對應的部分URL [!DNL Phoenix] 伺服器。 指定/hbasephoenix0 （如果使用） [!DNL Azure] HDInsights群集。 |
| `enableSsl` | 布林值。 指定是否使用SSL加密伺服器連線。 |
| `connectionSpec.id` | 連線規格會傳回來源的聯結器屬性，包括與建立基礎連線和來源連線相關的驗證規格。 的連線規格ID [!DNL Phoenix] 為： `102706fb-a5cd-42ee-afe0-bc42f017ff43` |

如需開始使用的詳細資訊，請參閱 [這份Phoenix檔案](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱以下指南： [Platform API快速入門](../../../../../landing/api-guide.md).

## 建立基礎連線

基礎連線會保留您的來源和平台之間的資訊，包括來源的驗證認證、連線的目前狀態，以及您唯一的基本連線ID。 基礎連線ID可讓您從來源內部探索及導覽檔案，並識別您要擷取的特定專案，包括其資料型別和格式的資訊。

若要建立基礎連線，請向以下連線發出POST請求： `/connections` 端點，同時提供 [!DNL Phoenix] 要求內文中的驗證認證。

**API格式**

```https
POST /connections
```

**要求**

下列要求會建立 [!DNL Phoenix]：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Phoenix test connection",
      "description": "Phoenix test connection",
      "auth": {
          "specName": "Basic Authentication",
      "params": {
          "host":  "{HOST}",
          "username": "{USERNAME}",
          "password":"{PASSWORD}",
          "port": {PORT},
          "httpPath": "{PATH}",
          "enableSsl": {SSL}
          }
      },
      "connectionSpec": {
          "id": "102706fb-a5cd-42ee-afe0-bc42f017ff43",
          "version": "1.0"
      }
  }'
```

| 屬性 | 說明 |
| --------- | ----------- |
| `auth.params.host` | 的主機 [!DNL Phoenix] 伺服器。 |
| `auth.params.username` | 與您的相關聯的使用者名稱 [!DNL Phoenix] 連線。 |
| `auth.params.password` | 與您的關聯的密碼 [!DNL Phoenix] 連線。 |
| `auth.params.port` | 您的TCP連線埠 [!DNL Phoenix] 連線。 |
| `auth.params.httpPath` | 您的專案的部分http路徑 [!DNL Phoenix] 連線。 |
| `auth.params.enableSsl` | 指定是否使用SSL加密伺服器連線的布林值。 |
| `connectionSpec.id` | 此 [!DNL Phoenix] 連線規格ID： `102706fb-a5cd-42ee-afe0-bc42f017ff43`. |

**回應**

成功的回應會傳回新建立連線的詳細資料，包括其唯一識別碼(`id`)。 在下個教學課程中探索您的資料時，需要此ID。

```json
{
    "id": "0d982fff-c443-403e-982f-ffc443f03e37",
    "etag": "\"830082dc-0000-0200-0000-5e84ee560000\""
}
```

## 後續步驟

依照本教學課程，您已建立 [!DNL Phoenix] 基礎連線使用 [!DNL Flow Service] API。 您可以在下列教學課程中使用此基本連線ID：

* [使用瀏覽資料表的結構和內容 [!DNL Flow Service] API](../../explore/tabular.md)
* [建立資料流以使用將資料庫資料帶入Platform [!DNL Flow Service] API](../../collect/database-nosql.md)
