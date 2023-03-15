---
keywords: Experience Platform；首頁；熱門主題；資料準備；資料準備；串流；上插；串流上插
title: 使用資料準備將部分行更新發送到配置檔案服務
description: 本檔案提供如何使用資料準備將部分列更新傳送至設定檔服務的資訊。
exl-id: f9f9e855-0f72-4555-a4c5-598818fc01c2
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1169'
ht-degree: 1%

---

# 將部分列更新傳送至 [!DNL Profile Service] 使用 [!DNL Data Prep]

流上插頁 [!DNL Data Prep] 可讓您將部分列更新傳送至 [!DNL Profile Service] 資料，同時使用單一API請求建立新身分連結。

通過流式插頁，您可以在將資料轉換為 [!DNL Profile Service] PATCH擷取期間的請求。 根據你提供的資料， [!DNL Data Prep] 可讓您傳送單一API裝載，並將資料轉譯為兩者 [!DNL Profile Service] PATCH和 [!DNL Identity Service] 建立請求。

本文檔提供了有關如何流式處理上插頁的資訊 [!DNL Data Prep].

## 快速入門

此概觀需要妥善了解下列Adobe Experience Platform元件：

* [[!DNL Data Prep]](./home.md): [!DNL Data Prep] 可讓資料工程師將資料對應、轉換及驗證至Experience Data Model(XDM)。
* [[!DNL Identity Service]](../identity-service/home.md):跨裝置和系統橋接身分，以更全面了解個別客戶及其行為。
* [即時客戶個人檔案](../profile/home.md):根據來自多個來源的匯總資料，即時提供統一的客戶設定檔。
* [來源](../sources/home.md):Experience Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。

## 在中使用流插頁 [!DNL Data Prep] {#streaming-upserts-in-data-prep}

>[!NOTE]
>
>以下源支援使用流上插頁：<ul><li>[[!DNL Amazon Kinesis]](../sources/connectors/cloud-storage/kinesis.md)</li><li>[[!DNL Azure Event Hubs]](../sources/connectors/cloud-storage/eventhub.md)</li><li>[[!DNL HTTP API]](../sources/connectors/streaming/http.md)</li></ul>

### 流式處理上插頁高級工作流

流上插頁 [!DNL Data Prep] 如下所示：

* 您必須先為 [!DNL Profile] 消耗。 請參閱 [啟用資料集 [!DNL Profile]](../catalog/datasets/enable-for-profile.md) 以取得更多資訊；
* 如果必須連結新身分，您也必須建立其他資料集 **具有相同架構** 作為 [!DNL Profile] 資料集；
* 準備好資料集後，您必須建立資料流，將傳入的請求對應至 [!DNL Profile] 資料集；
* 接下來，您必須更新傳入的請求以包含必要的標題。 這些標題會定義：
   * 需要使用執行的資料操作 [!DNL Profile]: `create`, `merge`，和 `delete`;
   * 要使用執行的可選身份操作 [!DNL Identity Service]: `create`.

### 設定身分資料集

如果必須連結新身分，則您必須在傳入的裝載中建立並傳遞其他資料集。 建立身分資料集時，您必須確保符合下列要求：

* 身分資料集的關聯結構必須為 [!DNL Profile] 資料集。 架構的不匹配可能導致系統行為不一致；
* 不過，您必須確定身分資料集與 [!DNL Profile] 資料集。 如果資料集相同，資料會遭到覆寫，而非更新；
* 初始資料集必須為 [!DNL Profile]，身分資料集 **不應** 為 [!DNL Profile]. 否則，資料也會遭到覆寫，而非更新。

#### 與身分資料集相關聯的結構中的必填欄位 {#identity-dataset-required-fileds}

如果您的結構包含必要欄位，則必須隱藏資料集的驗證才能啟用 [!DNL Identity Service] 只接收身份。 通過應用 `disabled` 值 `acp_validationContext` 參數。 請參閱下列範例：

```shell
curl -X POST 'https://platform.adobe.io/data/foundation/catalog/dataSets/62257bef7a75461948ebcaaa' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "tags":{
        "acp_validationContext": ["disabled"]
        }
}'
```

>[!TIP]
>
>如果與身分資料集相關聯的結構沒有任何必要欄位，則您不需要進行任何額外設定。

## 傳入的裝載結構

以下顯示了建立新標識連結的傳入有效負載結構的示例。

### 具有身分配置的裝載

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
| `flowId` | 標識資料流的唯一ID。 此資料流ID應對應於使用建立的源連接 [!DNL Amazon Kinesis], [!DNL Azure Event Hubs]，或 [!DNL HTTP API]. 此資料流也應具有 [!DNL Profile] — 啟用資料集作為目標資料集。 **附註**:的ID [!DNL Profile]-enabled target dataset也用作 `datasetId` 參數。 |
| `imsOrgId` | 與您的組織對應的ID。 |
| `datasetId` | 的ID [!DNL Profile] — 啟用資料流的目標資料集。 **附註**:這是與 [!DNL Profile] — 啟用在資料流中找到的目標資料集ID。 |
| `operations` | 此參數會概述 [!DNL Data Prep] 會根據傳入的要求進行。 |
| `operations.data` | 定義必須在 [!DNL Profile Service]. |
| `operations.identity` | 定義資料允許的操作 [!DNL Identity Service]. |
| `operations.identityDatasetId` | （選用）只有在必須連結新身分時才需要的身分資料集ID。 |

#### 支援的操作

支援下列操作 [!DNL Profile Service]:

| 運作 | 說明 |
| --- | --- | 
| `create` | 預設操作。 這會為產生XDM實體建立方法 [!DNL Profile Service]. |
| `merge` | 這會為產生XDM實體更新方法 [!DNL Profile Service]. |
| `delete` | 這會為產生XDM實體刪除方法 [!DNL Profile Service] 並從 [!DNL Profile Store]. |

支援下列操作 [!DNL Identity Service]:

| 運作 | 說明 |
| --- | --- |
| `create` | 此參數唯一允許的操作。 若 `create` 會以 `operations.identity`，然後 [!DNL Data Prep] 為產生XDM實體建立請求 [!DNL Identity Service]. 如果身分已存在，則會忽略該身分。 **注意：** 若 `operations.identity` 設為 `create`，則 `identityDatasetId` 也必須指定。 XDM實體會建立由內部產生的訊息 [!DNL Data Prep] 會為此資料集id產生元件。 |

### 無身份配置的裝載

如果不需要連結新身分，您可以忽略 `identity` 和 `identityDatasetId` 參數。 這麼做只會將資料傳送至 [!DNL Profile Service] 然後跳 [!DNL Identity Service]. 如需範例，請參閱下方的裝載：

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

若是XDM更新，必須為 [!DNL Profile] 並包含主要身分。 您可以透過兩種方式指定XDM架構的主要身分：

* 指定靜態欄位作為XDM架構中的主要身分；
* 在XDM架構中，透過身分對應欄位群組，指定其中一個身分欄位作為主要身分。

### 指定靜態欄位作為XDM架構中的主要身分欄位

在以下範例中， `state`, `homePhone.number` 而其他屬性則會以其各自的指定值更新至 [!DNL Profile] 與 `sampleEmail@gmail.com`. 然後由流產生XDM實體更新消息 [!DNL Data Prep] 元件。 [!DNL Profile Service] 然後確認XDM更新訊息以更新設定檔記錄。

>[!NOTE]
>
>在此範例中，身分不會連結在一起，因為沒有為身分定義任何操作。

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

### 在XDM架構中，透過「身分對應」欄位群組，指定其中一個身分欄位作為主要身分

在此範例中，標題包含 `operations` 屬性 `identity` 和 `identityDatasetId` 屬性。 這可讓資料與 [!DNL Profile Service] 還要傳遞給 [!DNL Identity Service].

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

## 已知限制和主要考量

以下概述了流上插頁時要考慮的已知限制清單 [!DNL Data Prep]:

* 只有在將部分列更新傳送至 [!DNL Profile Service]. 部分列更新為 **not** 被資料湖消耗。
* 流上插頁方法不支援更新、替換和刪除身份。 如果新身分不存在，則會建立這些身分。 因此， `identity` 操作必須始終設定為建立。 如果身分已存在，則操作為無操作。
* 流插頁方法當前不支援 [Adobe Experience Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=zh-Hant) 和 [Adobe Experience Platform Mobile SDK](https://aep-sdks.gitbook.io/docs/).

## 後續步驟

通過閱讀此文檔，您現在應該了解如何在 [!DNL Data Prep] 若要將部分列更新傳送至 [!DNL Profile Service] 資料，同時使用單一API請求建立和連結身分。 如需其他項目的詳細資訊 [!DNL Data Prep] 功能，請閱讀 [[!DNL Data Prep] 概述](./home.md). 若要了解如何在 [!DNL Data Prep] API，請閱讀 [[!DNL Data Prep] 開發人員指南](./api/overview.md).
