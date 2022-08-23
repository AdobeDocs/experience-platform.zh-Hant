---
keywords: Experience Platform；首頁；熱門主題；Teradata
title: 使用流服務API建立TeradataVantage基連接
description: 瞭解如何使用流服務API將Adobe Experience Platform連接到Vantage。
source-git-commit: f140dac67ccd09ec1e6cab794f53e0090af55442
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 1%

---

# (Beta)建立 [!DNL Teradata Vantage] 基本連接使用 [!DNL Flow Service] API

>[!NOTE]
>
>的 [!DNL Teradata Vantage] 源為beta。 查看 [源概述](../../../../home.md#terms-and-conditions) 的子菜單。

基連接表示源和Adobe Experience Platform之間經過驗證的連接。

本教程將指導您完成建立基本連接的步驟 [!DNL Teradata Vantage] 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)。

## 快速入門

本指南要求對Adobe Experience Platform的下列組成部分有工作上的理解：

* [源](../../../../home.md): [!DNL Experience Platform] 允許從各種源接收資料，同時讓您能夠使用 [!DNL Platform] 服務。
* [沙箱](../../../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙箱，將單個沙箱 [!DNL Platform] 實例到獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

### 使用平台API

有關如何成功調用平台API的資訊，請參見上的指南 [平台API入門](../../../../../landing/api-guide.md)。

以下部分提供了成功連接到所需的其他資訊 [!DNL Teradata Vantage] 使用 [!DNL Flow Service] API。

### 收集所需憑據

為了 [!DNL Flow Service] 連接 [!DNL Teradata Vantage]，必須提供以下連接屬性：

| 憑據 | 說明 |
| --- | --- |
| `connectionString` | 連接字串是提供有關資料源以及如何連接到資料源的資訊的字串。 的連接字串模式 [!DNL Teradata Vantage] 是 `DBCName={SERVER};Uid={USERNAME};Pwd={PASSWORD}`。 |
| `connectionSpec.id` | 連接規範返回源的連接器屬性，包括與建立基連接和源連接相關的驗證規範。 連接規範ID [!DNL Teradata Vantage] 為： `2fa8af9c-2d1a-43ea-a253-f00a00c74412` |

有關入門的詳細資訊，請參閱此 [[!DNL Teradata Vantage] 文檔](https://docs.teradata.com/r/Teradata-VantageTM-Advanced-SQL-Engine-Security-Administration/July-2021/Setting-Up-the-Administrative-Infrastructure/Controlling-Access-to-the-Operating-System/Working-with-OS-Level-Security-Options)。

## 建立基本連接

基本連接將保留源和平台之間的資訊，包括源的驗證憑據、連接的當前狀態和唯一的基本連接ID。 基本連接ID允許您從源中瀏覽和導航檔案，並標識要攝取的特定項目，包括有關其資料類型和格式的資訊。

要建立基本連接ID，請向 `/connections` 提供端點 [!DNL Teradata Vantage] 身份驗證憑據作為請求正文的一部分。

**API格式**

```https
POST /connections
```

**要求**

以下請求為 [!DNL Teradata Vantage]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Teradata Vantage base connection",
      "description": "Teradata Vantage base connection",
      "auth": {
          "specName": "ConnectionString,
          "params": {
              "connectionString": "DBCName={SERVER};Uid={USERNAME};Pwd={PASSWORD}"
          }
      },
      "connectionSpec": {
          "id": "2fa8af9c-2d1a-43ea-a253-f00a00c74412",
          "version": "1.0"
      }
  }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `auth.params.connectionString` | 用於連接到您的 [!DNL Teradata Vantage] 實例。 的連接字串模式 [!DNL Teradata Vantage] 是 `DBCName={SERVER};Uid={USERNAME};Pwd={PASSWORD}`。 |
| `connectionSpec.id` | 的 [!DNL Teradata Vantage] 連接規範ID: `2fa8af9c-2d1a-43ea-a253-f00a00c74412`。 |

**回應**

成功的響應返回新建立的連接，包括其唯一連接標識符(`id`)。 在下一教程中瀏覽資料時需要此ID。

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

按照本教程，您建立了 [!DNL Teradata Vantage] 基本連接使用 [!DNL Flow Service] API。 您可以在以下教程中使用此基本連接ID:

* [使用 [!DNL Flow Service] API](../../explore/tabular.md)
* [建立資料流，使用 [!DNL Flow Service] API](../../collect/database-nosql.md)
