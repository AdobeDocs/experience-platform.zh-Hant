---
keywords: Experience Platform；首頁；熱門主題；資料準備；資料準備；串流；更新插入；串流更新插入
title: 使用「資料準備」將部分列更新傳送到「即時客戶個人檔案」
description: 瞭解如何使用「資料準備」將部分列更新傳送至「即時客戶個人檔案」。
exl-id: f9f9e855-0f72-4555-a4c5-598818fc01c2
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '1241'
ht-degree: 0%

---

# 使用[!DNL Data Prep]傳送部分資料列更新至[!DNL Real-Time Customer Profile]

>[!WARNING]
>
>已棄用透過DCS入口針對設定檔更新擷取的Experience Data Model (XDM)實體更新訊息(含JSONPATCH作業)。 或者，您可以[將原始資料擷取至DCS入口](../sources/tutorials/api/create/streaming/http.md#sending-messages-to-an-authenticated-streaming-connection)，並指定必要的資料對應，將您的資料轉換為符合XDM規範的訊息，以進行設定檔更新。

[!DNL Data Prep]中的串流更新插入可讓您傳送部分資料列更新至[!DNL Real-Time Customer Profile]資料，同時使用單一API要求建立和建立新的身分連結。

透過串流更新插入，您可以在擷取期間將該資料轉譯為[!DNL Real-Time Customer Profile]個PATCH請求時保留資料格式。 根據您提供的輸入，[!DNL Data Prep]可讓您傳送單一API裝載，並將資料轉譯為[!DNL Real-Time Customer Profile]PATCH和[!DNL Identity Service]建立要求。

>[!NOTE]
>
>若要利用更新插入功能，建議您在資料擷取期間關閉XDM相容的設定，並使用[資料準備對應程式](./ui/mapping.md)重新對應傳入裝載。

本檔案提供如何在[!DNL Data Prep]中串流更新插入的資訊。

## 快速入門

此概覽需要深入瞭解下列Adobe Experience Platform元件：

* [[!DNL Data Prep]](./home.md)： [!DNL Data Prep]可讓資料工程師對應、轉換及驗證與Experience Data Model (XDM)之間的資料。
* [[!DNL Identity Service]](../identity-service/home.md)：跨裝置和系統橋接身分，以更清楚瞭解個別客戶及其行為。
* [即時客戶個人檔案](../profile/home.md)：根據來自多個來源的彙總資料，即時提供統一的客戶個人檔案。
* [來源](../sources/home.md)：Experience Platform允許從各種來源擷取資料，同時讓您能夠使用Platform服務來建構、加標籤以及增強傳入的資料。

## 在[!DNL Data Prep]中使用串流更新插入 {#streaming-upserts-in-data-prep}

>[!NOTE]
>
>下列來源支援使用串流更新插入：<ul><li>[[!DNL Amazon Kinesis]](../sources/connectors/cloud-storage/kinesis.md)</li><li>[[!DNL Azure Event Hubs]](../sources/connectors/cloud-storage/eventhub.md)</li><li>[[!DNL HTTP API]](../sources/connectors/streaming/http.md)</li></ul>

### 串流更新插入高階工作流程

[!DNL Data Prep]中的串流更新插入的運作方式如下：

* 您必須先建立並啟用[!DNL Profile]使用量的資料集。 如需詳細資訊，請參閱[啟用 [!DNL Profile]](../catalog/datasets/enable-for-profile.md)的資料集指南。
* 如果新身分必須連結，則您也必須建立其他資料集&#x200B;**，其結構描述**&#x200B;與您的[!DNL Profile]資料集相同。
* 準備好資料集後，您必須建立資料流，將傳入的請求對應至[!DNL Profile]資料集；
* 接下來，您必須更新傳入請求以包含必要的標頭。 這些標頭會定義：
   * 需要對[!DNL Profile]執行的資料操作： `create`、`merge`和`delete`。
   * 要與[!DNL Identity Service]一起執行的選擇性身分作業： `create`。

### 設定身分資料集

如果新身分必須連結，則您必須在傳入裝載中建立並傳遞額外的資料集。 建立身分資料集時，您必須確保符合下列需求：

* 身分資料集必須具有關聯的結構描述做為[!DNL Profile]資料集。 結構描述不相符可能會導致不一致的系統行為。
* 不過，您必須確保身分資料集與[!DNL Profile]資料集不同。 如果資料集相同，則會覆寫資料而非更新資料。
* 雖然必須為[!DNL Profile]啟用初始資料集，但身分資料集&#x200B;**不應為[!DNL Profile]啟用**。 否則，也會覆寫資料，而非更新資料。 但是，應該為[!DNL Identity Service]啟用身分資料集&#x200B;****。

#### 與身分資料集相關聯之結構描述中的必填欄位 {#identity-dataset-required-fileds}

如果您的結構描述包含必填欄位，則必須隱藏資料集的驗證，以允許[!DNL Identity Service]僅接收身分識別。 您可以將`disabled`值套用至`acp_validationContext`引數來隱藏驗證。 請參閱下列範例：

```shell
curl -X POST 'https://platform.adobe.io/data/foundation/catalog/dataSets/62257bef7a75461948ebcaaa' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "tags": {
        "acp_validationContext": [
            "disabled"
        ],
        "unifiedProfile": [
            "enabled:false"
        ],
        "unifiedIdentity": [
            "enabled:true"
        ]
    }
}'
```

>[!TIP]
>
>如果與身分資料集相關聯的結構描述沒有任何必填欄位，則不需要進行任何其他設定。

## 傳入裝載結構

以下顯示可建立新身分連結之傳入裝載結構的範例。

### 具有身分設定的裝載

```shell
{
  "header": {
    "flowId": "923e2ac3-3869-46ec-9e6f-7012c4e23f69",
    "imsOrgId": "{ORG_ID}",
    "datasetId": "621fc19ab33d941949af16c8",
    "operations": {
        "data": "create" (default)/"merge"/"delete",
        "identity": "create",
        "identityDatasetId": "621fc19ab33d941949af16d9"
    }
  }
... //The raw data attributes are included here as the key/value pairs of the "body" property.
}
```

| 參數 | 說明 |
| --- | --- |
| `flowId` | 用於識別資料流的唯一ID。 此資料流ID應該對應到使用[!DNL Amazon Kinesis]、[!DNL Azure Event Hubs]或[!DNL HTTP API]建立的來源連線。 此資料流也應該有[!DNL Profile]啟用的資料集作為目標資料集。 **注意**：已啟用[!DNL Profile]的目標資料集的識別碼也會當作您的`datasetId`引數使用。 |
| `imsOrgId` | 與您的組織相對應的ID。 |
| `datasetId` | 您的資料流已啟用[!DNL Profile]的目標資料集識別碼。 **注意**：此ID與您資料流中具有[!DNL Profile]功能的目標資料集ID相同。 |
| `operations` | 此引數概述[!DNL Data Prep]根據傳入的請求將採取的動作。 |
| `operations.data` | 定義必須在[!DNL Real-Time Customer Profile]中執行的動作。 |
| `operations.identity` | 定義[!DNL Identity Service]允許對資料執行的作業。 |
| `operations.identityDatasetId` | （選用）只有在必須連結新身分時才需要身分資料集的ID。 |

#### 支援的作業

[!DNL Real-Time Customer Profile]支援下列作業：

| 運作 | 說明 |
| --- | --- | 
| `create` | 預設操作。 這會為[!DNL Real-Time Customer Profile]產生XDM實體建立方法。 |
| `merge` | 這會產生[!DNL Real-Time Customer Profile]的XDM實體更新方法。 |
| `delete` | 這會產生[!DNL Real-Time Customer Profile]的XDM實體刪除方法，並從[!DNL Profile store]永久移除資料。 |

[!DNL Identity Service]支援下列作業：

| 運作 | 說明 |
| --- | --- |
| `create` | 此引數唯一允許的作業。 如果`create`傳遞為`operations.identity`的值，則[!DNL Data Prep]會產生[!DNL Identity Service]的XDM實體建立請求。 如果身分已經存在，則會忽略身分。 **注意：**&#x200B;如果`operations.identity`設定為`create`，則必須同時指定`identityDatasetId`。 將針對此資料集ID產生由[!DNL Data Prep]元件內部產生的XDM實體建立訊息。 |

### 沒有身分設定的裝載

如果新身分不需要連結，則您可以在操作中省略`identity`和`identityDatasetId`引數。 這樣做只會傳送資料給[!DNL Real-Time Customer Profile]並略過[!DNL Identity Service]。 如需範例，請參閱以下裝載：

```shell
{
  "header": {
    "flowId": "923e2ac3-3869-46ec-9e6f-7012c4e23f69",
    "imsOrgId": "{ORG_ID}",
    "datasetId": "621fc19ab33d941949af16c8",
    "operations": {
        "data": "create"/"merge"/"delete",
    }
  }
... //The raw data attributes are included here as the key/value pairs of the "body" property.
}
```

## 動態傳遞主要身分

針對XDM更新，結構描述必須啟用[!DNL Profile]並包含主要身分。 您可以透過兩種方式指定XDM結構描述的主要身分：

* 在XDM結構中指定一個靜態欄位作為主要身分；
* 透過XDM結構描述中的身分對應欄位群組，將其中一個身分欄位指定為主要身分。

### 將靜態欄位指定為XDM結構描述中的主要身分欄位

在下列範例中，`state`、`homePhone.number`和其他屬性會以其各自的指定值更新插入[!DNL Profile]，主要識別碼為`sampleEmail@gmail.com`。 然後，串流[!DNL Data Prep]元件會產生XDM實體更新訊息。 [!DNL Real-Time Customer Profile]接著確認XDM更新訊息以更新插入設定檔記錄。

>[!NOTE]
>
>在此範例中，身分將不會連結在一起，因為沒有定義身分的操作。

```shell
curl -X POST 'https://dcs.adobedc.net/collection/9aba816d350a69c4abbd283eb5818ec3583275ffce4880ffc482be5a9d810c4b' \
  -H 'Content-Type: application/json' \
  -H 'x-adobe-flow-id: d5262d48-0f47-4949-be6d-795f06933527' \
  -d '{
    "header": {
        "flowId" : "d5262d48-0f47-4949-be6d-795f06933527",
        "imsOrgId": "{ORG_ID}",
        "datasetId": "62259f817f62d71947929a7b",
        "operations": {
         "data": "create"
     }
    },
    {
        "body": {
        "homeAddress": {
            "country": "US",
            "state": "GA",
            "region": "va7"
        },
        "homePhone": {
            "number": "123.456.799"
        },
        "identityMap": {
            "Email": [{
                "id": "sampleEmail@gmail.com",
                "primary": true
            }]
        },
      "personalEmail": {
            "address": "sampleEmail@gmail.com",
            "primary": true
       },
      "personID": "346576345",
      "_id": "346576345",
      "timestamp": "2021-05-05T17:51:45.1880+02",
      "workEmail": "sampleWorkEmail@gmail.com"
  }
}'
```

### 透過XDM結構描述中的身分對應欄位群組，將其中一個身分欄位指定為主要身分

在此範例中，標頭包含具有`identity`和`identityDatasetId`屬性的`operations`屬性。 這允許資料與[!DNL Real-Time Customer Profile]合併，也允許將身分傳遞給[!DNL Identity Service]。

```shell
curl -X POST 'https://dcs.adobedc.net/collection/9aba816d350a69c4abbd283eb5818ec3583275ffce4880ffc482be5a9d810c4b' \
  -H 'Content-Type: application/json' \
  -H 'x-adobe-flow-id: d5262d48-0f47-4949-be6d-795f06933527' \
  -d '{
    "header": {
        "flowId" : "d5262d48-0f47-4949-be6d-795f06933527",
        "imsOrgId": "{ORG_ID}",
        "datasetId": "62259f817f62d71947929a7b",
        "operations": {          
            "data": "merge",
            "identity": "create",
            "identityDatasetId": "6254a93b851ecd194b64af9e"
      }
    },
    {        
       "body": {
        "homeAddress": {
            "country": "US",
            "state": "GA",
            "region": "va7"
        },
        "homePhone": {
            "number": "123.456.799"
        },
        "identityMap": {
            "Email": [{
                "id": "sampleEmail@gmail.com",
                "primary": true
            }]
        },
      "personalEmail": {
            "address": "sampleEmail@gmail.com",
            "primary": true
       },
      "personID": "346576345",
      "_id": "346576345",
      "timestamp": "2021-05-05T17:51:45.1880+02",
      "workEmail": "sampleWorkEmail@gmail.com"
  }
 }'
```

## 已知限制和主要考量事項

以下概述使用[!DNL Data Prep]串流更新插入時應考量的已知限制清單：

* 只有在傳送部分資料列更新至[!DNL Real-Time Customer Profile]時，才應該使用串流更新插入方法。 部分資料列更新&#x200B;**不是**&#x200B;由資料湖使用。
* 串流更新插入方法不支援更新、取代和移除身分。 如果新身分不存在，則會建立新身分。 因此，`identity`作業必須一律設定為建立。 如果身分已經存在，則操作是無操作。
* 串流更新插入方法目前不支援[Adobe Experience Platform Web SDK](/help/web-sdk/home.md)和[Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/documentation/)。

## 後續步驟

閱讀本檔案後，您現在應該瞭解如何在[!DNL Data Prep]中串流更新插入，以傳送您[!DNL Real-Time Customer Profile]資料的部分列更新，同時使用單一API請求建立和連結身分識別。 如需其他[!DNL Data Prep]功能的詳細資訊，請閱讀[[!DNL Data Prep] 概觀](./home.md)。 若要瞭解如何在[!DNL Data Prep] API中使用對應集，請閱讀[[!DNL Data Prep] 開發人員指南](./api/overview.md)。
