---
title: 串流SDK API的檔案自助範本
description: 了解如何使用流量服務API將串流資料從來源帶入Adobe Experience Platform。
hide: true
hidefromtoc: true
source-git-commit: 7744fef9751212a40f8f20df52812d38130c42fc
workflow-type: tm+mt
source-wordcount: '1775'
ht-degree: 1%

---

# 建立源連接和要流的資料流 *您的來源* 資料使用 [!DNL Flow Service] API

*瀏覽此模板時，替換或刪除所有斜體段落（從此模板開始）。*

*首先，請更新頁面頂端的中繼資料（標題和說明）。 請忽略此頁面上的所有DNL實例。 這個標籤可協助我們的機器翻譯程式將頁面正確翻譯成我們支援的多種語言。 在您提交檔案後，我們會為其新增標籤。*

## 總覽

*提供您公司的簡短概觀，包括為客戶提供的價值。 加入產品檔案首頁的連結，以供進一步閱讀。*

>[!IMPORTANT]
>
>本檔案頁面由 *您的來源* 團隊。 如有任何查詢或更新請求，請直接與他們聯繫，地址為 *插入可以聯繫您獲取更新的連結或電子郵件地址*.

## 先決條件

*在本節中新增客戶開始在Adobe Experience Platform使用者介面中設定來源之前，需注意之事項的相關資訊。 這可以是：*

* *需要添加到允許清單*
* *電子郵件雜湊要求*
* *任何你方的賬戶細節*
* *如何取得API金鑰以連線至您的平台*

### 收集所需憑據

為了連接 *您的來源* 要Experience Platform，必須為以下連接屬性提供值：

| 憑據 | 說明 | 範例 |
| --- | --- | --- |
| *憑據* | *請在此處向源的身份驗證憑據添加簡短描述* | *請在此處添加源的驗證憑據示例* |
| *憑證* | *請在此處向源的身份驗證憑據添加簡短描述* | *請在此處添加源的驗證憑據示例* |
| *憑據三* | *請在此處向源的身份驗證憑據添加簡短描述* | *請在此處添加源的驗證憑據示例* |

如需這些憑證的詳細資訊，請參閱 *您的來源* 驗證檔案。 *請在此處將連結新增至您平台的驗證檔案*.

### 整合 *您的來源* 你的網鈎

*串流SDK需要您的來源能夠支援WebHook，以便與Experience Platform通訊。 在本節中，您必須提供使用者必須遵循的步驟，才能將YOURSOURCE與網頁連結整合。*

## Connect *您的來源* 到使用 [!DNL Flow Service] API

以下教學課程會逐步引導您完成建立 *您的來源* 源連接和建立資料流，以便 *您的來源* 使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

### 建立源連接 {#source-connection}

若要為串流來源建立來源連線，請向 `/sourceConnections` 端點 [!DNL Flow Service] 提供連線名稱、來源的連線規格ID和資料格式時的API。

**API格式**

```https
POST /sourceConnections
```

**要求**

以下請求將建立源連接 *您的來源*:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Streaming Source Connection for a Streaming SDK source",
      "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
      "description": "Streaming Source Connection for a Streaming SDK source",
      "connectionSpec": {
          "id": "e77fd9d2-22a8-11ed-861d-0242ac120002",
          "version": "1.0"
      },
      "data": {
          "format": "json"
      }
    }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 源連接的名稱。 請確保源連接的名稱是描述性的，因為您可以使用此名稱查找有關源連接的資訊。 |
| `description` | 可包含的選用值，用於提供來源連線的詳細資訊。 |
| `connectionSpec.id` | 與源對應的連接規範ID。 |
| `data.format` | 格式 *您的來源* 您要擷取的資料。 目前，唯一支援的資料格式是 `json`. |

**回應**

成功的回應會傳回唯一識別碼(`id`)。 在後續步驟中需要此ID才能建立資料流。

```json
{
     "id": "246d052c-da4a-494a-937f-a0d17b1c6cf5",
     "etag": "\"712a8c08-fda7-41c2-984b-187f823293d8\""
}
```

### 建立目標XDM結構 {#target-schema}

為了在Platform中使用來源資料，必須建立目標架構，以根據您的需求來建構來源資料。 然後，目標架構會用來建立包含來源資料的Platform資料集。

您可以透過執行POST要求來建立目標XDM結構 [結構註冊表API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/).

如需建立Target XDM結構的詳細步驟，請參閱 [使用API建立結構](https://experienceleague.adobe.com/docs/experience-platform/xdm/api/schemas.html?lang=en#create).

### 建立目標資料集 {#target-dataset}

目標資料集的建立方式，是透過對 [目錄服務API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)，提供裝載中目標架構的ID。

如需如何建立目標資料集的詳細步驟，請參閱 [使用API建立資料集](https://experienceleague.adobe.com/docs/experience-platform/catalog/api/create-dataset.html?lang=en).

### 建立目標連線 {#target-connection}

目標連線代表要儲存所擷取資料的目的地連線。 要建立目標連接，必須提供與資料庫對應的固定連接規範ID。 此ID為： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

您現在擁有目標架構、目標資料集以及資料湖的連線規格ID的唯一識別碼。 使用這些識別碼，您可以使用 [!DNL Flow Service] API，指定包含傳入來源資料的資料集。

**API格式**

```https
POST /targetConnections
```

**要求**

下列請求會為 *您的來源*:


```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Streaming Target Connection for a Streaming SDK source",
      "description": "Streaming Target Connection for a Streaming SDK source",
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      },
      "data": {
          "format": "json",
          "schema": {
              "id": "{TARGET_XDM_SCHEMA}",
              "version": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "params": {
          "dataSetId": "{TARGET_DATASET}"
      }
  }'
```


| 屬性 | 說明 |
| -------- | ----------- |
| `name` | 目標連接的名稱。 請確定目標連線的名稱是描述性的，因為您可以使用此名稱來查詢目標連線的資訊。 |
| `description` | 可包含的選用值，用於提供目標連線的詳細資訊。 |
| `connectionSpec.id` | 與資料湖對應的連接規範ID。 此固定ID為： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`. |
| `data.format` | 格式 *您的來源* 要帶入Platform的資料。 |
| `params.dataSetId` | 上一步驟中擷取的目標資料集ID。 |


**回應**

成功的回應會傳回新目標連線的唯一識別碼(`id`)。 後續步驟需要此ID。

```json
{
     "id": "7c96c827-3ffd-460c-a573-e9558f72f263",
     "etag": "\"a196f685-f5e8-4c4c-bfbd-136141bb0c6d\""
}
```

### 建立對應 {#mapping}

若要將來源資料內嵌至目標資料集，必須先將其對應至目標資料集所遵守的目標架構。 這是透過執行POST要求來達成 [[!DNL Data Prep] API](https://www.adobe.io/experience-platform-apis/references/data-prep/) 在要求裝載中定義的資料對應。

**API格式**

```http
POST /conversion/mappingSets
```

**要求**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/mappingSets' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "version": 0,
      "xdmSchema": "{TARGET_XDM_SCHEMA}",
      "xdmVersion": "1.0",
      "mappings": [
          {
              "destinationXdmPath": "person.name.firstName",
              "sourceAttribute": "firstName",
              "identity": false,
              "version": 0
          },
          {
              "destinationXdmPath": "person.name.lastName",
              "sourceAttribute": "lastName",
              "identity": false,
              "version": 0
          }
      ]
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `xdmSchema` | 的ID [target XDM結構](#target-schema) 在先前的步驟中產生。 |
| `mappings.destinationXdmPath` | 要映射源屬性的目標XDM路徑。 |
| `mappings.sourceAttribute` | 需要對應至目標XDM路徑的來源屬性。 |
| `mappings.identity` | 一個布林值，用於指定是否要為標籤映射集 [!DNL Identity Service]. |

**回應**

成功的回應會傳回新建立之對應的詳細資訊，包括其唯一識別碼(`id`)。 在以後的步驟中需要此值才能建立資料流。

```json
{
    "id": "bf5286a9c1ad4266baca76ba3adc9366",
    "version": 0,
    "createdDate": 1597784069368,
    "modifiedDate": 1597784069368,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}"
}
```

### 建立流程 {#flow}

將資料從 *您的來源* 到平台是建立資料流。 您現在已準備下列必要值：

* [源連接ID](#source-connection)
* [Target連線ID](#target-connection)
* [對應ID](#mapping)

資料流負責從源中調度和收集資料。 您可以在裝載中提供先前提及的值時，執行POST要求來建立資料流。

若要排程擷取，您必須先將開始時間值設為紀元時間（以秒為單位）。 然後，您必須將頻率值設定為以下五個選項之一： `once`, `minute`, `hour`, `day`，或 `week`. 間隔值會指定兩個連續擷取之間的期間，但建立一次性擷取不需要設定間隔。 對於所有其他頻率，間隔值必須設定為等於或大於 `15`.


**API格式**

```http
POST /flows
```

**要求**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Streaming Dataflow for a Streaming SDK source",
      "description": "Streaming Dataflow for a Streaming SDK source",
      "flowSpec": {
          "id": "e77fde5a-22a8-11ed-861d-0242ac120002",
          "version": "1.0"
      },
      "sourceConnectionIds": [
          "246d052c-da4a-494a-937f-a0d17b1c6cf5"
      ],
      "targetConnectionIds": [
          "7c96c827-3ffd-460c-a573-e9558f72f263"
      ],
      "transformations": [
      {
        "name": "Mapping",
        "params": {
          "mappingId": "bf5286a9c1ad4266baca76ba3adc9366",
          "mappingVersion": 0
        }
      }
    ]
  }'
```

| 屬性 | 說明 |
| --- | --- |
| `name` | 資料流的名稱。 請確保資料流的名稱具有描述性，因為您可以使用此名稱查找資料流的資訊。 |
| `description` | 一個可選值，可以包括該值以提供有關資料流的詳細資訊。 |
| `flowSpec.id` | 建立資料流所需的流規範ID。 此固定ID為： `e77fde5a-22a8-11ed-861d-0242ac120002`. |
| `flowSpec.version` | 流規範ID的相應版本。 此值預設為 `1.0`. |
| `sourceConnectionIds` | 此 [源連接ID](#source-connection) 在先前的步驟中產生。 |
| `targetConnectionIds` | 此 [目標連線ID](#target-connection) 在先前的步驟中產生。 |
| `transformations` | 此屬性包含需要套用至資料的各種轉換。 將不符合XDM的資料帶入Platform時，此屬性為必要屬性。 |
| `transformations.name` | 指派給轉換的名稱。 |
| `transformations.params.mappingId` | 此 [對應ID](#mapping) 在先前的步驟中產生。 |
| `transformations.params.mappingVersion` | 對應ID的對應版本。 此值預設為 `0`. |

**回應**

成功的回應會傳回ID(`id`)。 您可以使用此ID監視、更新或刪除資料流。

```json
{
     "id": "993f908f-3342-4d9c-9f3c-5aa9a189ca1a",
     "etag": "\"510bb1d4-8453-4034-b991-ab942e11dd8a\""
}
```

### 取得您的串流端點URL

建立資料流後，您現在可以檢索流終結點URL。 您將使用此端點URL將源訂閱到Webhook，從而允許源與Experience Platform通信。

若要擷取串流端點URL，請向 `/flows` 端點，並提供資料流的ID。

**API格式**

```http
GET /flows/{FLOW_ID}
```

**要求**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flows/993f908f-3342-4d9c-9f3c-5aa9a189ca1a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回有關資料流的資訊，包括終結點URL，標籤為 `inletUrl`.

```json
{
  "items": [
    {
      "id": "993f908f-3342-4d9c-9f3c-5aa9a189ca1a",
      "createdAt": 1669238699119,
      "updatedAt": 1669238699119,
      "createdBy": "acme@AdobeID",
      "updatedBy": "acme@AdobeID",
      "createdClient": "{CREATED_CLIENT}",
      "updatedClient": "{UPDATED_CLIENT}",
      "sandboxId": "{SANDBOX_ID}",
      "sandboxName": "{SANDBOX_NAME}",
      "imsOrgId": "{ORG_ID}",
      "name": "Streaming Dataflow for a Streaming SDK source",
      "description": "Streaming Dataflow for a Streaming SDK source",
      "flowSpec": {
        "id": "e77fde5a-22a8-11ed-861d-0242ac120002",
        "version": "1.0"
      },
      "state": "enabled",
      "version": "\"a1011225-0000-0200-0000-63c78ae60000\"",
      "etag": "\"a1011225-0000-0200-0000-63c78ae60000\"",
      "sourceConnectionIds": [
        "246d052c-da4a-494a-937f-a0d17b1c6cf5"
      ],
      "targetConnectionIds": [
        "7c96c827-3ffd-460c-a573-e9558f72f263"
      ],
      "inheritedAttributes": {
        "properties": {
          "isSourceFlow": true
        },
        "sourceConnections": [
          {
            "id": "246d052c-da4a-494a-937f-a0d17b1c6cf5",
            "connectionSpec": {
              "id": "bdb5b792-451b-42de-acf8-15f3195821de",
              "version": "1.0"
            }
          }
        ],
        "targetConnections": [
          {
            "id": "7c96c827-3ffd-460c-a573-e9558f72f263",
            "connectionSpec": {
              "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
              "version": "1.0"
            }
          }
        ]
      },
      "options": {
        "errorDiagnosticsEnabled": true,
        "inletUrl": "https://dcs-int.adobedc.net/collection/ab65636c31778fb0455c439ffb48a5433a34d443f4c83c4b5beda9c5688797c5"
      },
      "transformations": [
        {
          "name": "Mapping",
          "params": {
            "mappingVersion": 0,
            "mappingId": "bf5286a9c1ad4266baca76ba3adc9366"
          }
        }
      ],
      "runs": "/runs?property=flowId==e1514b79-f031-43b4-aab5-381a42f86ad4",
      "providerRefId": "c9809ab5-71e0-4c7f-887b-61c95e4e20b5",
      "lastOperation": {
        "started": 0,
        "updated": 0,
        "operation": "enable"
      }
    }
  ]
}
```

## 附錄

以下部分提供了可以監視、更新和刪除資料流的步驟資訊。

### 監視資料流

建立資料流後，您可以監視正在通過資料流進行內嵌的資料，以查看有關流運行、完成狀態和錯誤的資訊。 如需完整的API範例，請參閱 [使用API監控來源資料流](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/monitor.html).

### 更新資料流

通過向發出PATCH請求，更新資料流的詳細資訊（如其名稱和說明），以及其運行計畫和關聯的映射集 `/flows` 端點 [!DNL Flow Service] API，同時提供資料流的ID。 發出PATCH請求時，必須提供資料流的唯一 `etag` 在 `If-Match` 頁首。 如需完整的API範例，請參閱 [使用API更新源資料流](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update-dataflows.html)

### 更新您的帳戶

通過向執行PATCH請求，更新源帳戶的名稱、說明和憑據 [!DNL Flow Service] API，同時將基本連線ID設為查詢參數。 提出PATCH請求時，您必須提供來源帳戶的唯一 `etag` 在 `If-Match` 頁首。 如需完整的API範例，請參閱 [使用API更新您的來源帳戶](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/update.html).

### 刪除資料流

通過執行DELETE請求以刪除資料流 [!DNL Flow Service] API，同時提供您要在查詢參數中刪除之資料流的ID。 如需完整的API範例，請參閱 [使用API刪除資料流](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete-dataflows.html).

### 刪除您的帳戶

對執行DELETE請求以刪除帳戶 [!DNL Flow Service] API，同時提供您要刪除之帳戶的基本連線ID。 如需完整的API範例，請參閱 [使用API刪除您的來源帳戶](https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/delete.html).