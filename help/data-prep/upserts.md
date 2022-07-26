---
keywords: Experience Platform；首頁；熱門主題；資料準備；資料準備；流式處理；upsert；流式處理；upsert
title: 使用資料準備將部分行更新發送到配置檔案服務
description: 本文檔提供有關如何使用資料準備將部分行更新發送到配置檔案服務的資訊。
exl-id: f9f9e855-0f72-4555-a4c5-598818fc01c2
source-git-commit: cc3ecbd8544839246d54f72b894ad27e850c0c90
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 1%

---

# 將部分行更新發送到 [!DNL Profile Service] 使用 [!DNL Data Prep]

流上插頁 [!DNL Data Prep] 允許您將部分行更新發送到 [!DNL Profile Service] 資料，同時使用單個API請求建立和建立新的標識連結。

通過流補插頁，您可以保留資料的格式，同時將資料轉換為 [!DNL Profile Service] PATCH請求。 根據你提供的資料， [!DNL Data Prep] 允許您發送單個API負載並將資料轉換為兩者 [!DNL Profile Service] PATCH [!DNL Identity Service] CREATE請求。

此文檔提供了有關如何流式處理上插頁的資訊 [!DNL Data Prep]。

## 快速入門

本概述要求對Adobe Experience Platform的下列組成部分進行工作理解：

* [[!DNL Data Prep]](./home.md): [!DNL Data Prep] 允許資料工程師將資料映射到體驗資料模型(XDM)並驗證資料。
* [[!DNL Identity Service]](../identity-service/home.md):通過跨設備和系統橋接身份，更好地瞭解單個客戶及其行為。
* [即時客戶概要資訊](../profile/home.md):根據來自多個來源的聚合資料即時提供統一的客戶配置檔案。
* [源](../sources/home.md):Experience Platform允許從各種源接收資料，同時讓您能夠使用平台服務構建、標籤和增強傳入資料。

## 在中使用流上插頁 [!DNL Data Prep] {#streaming-upserts-in-data-prep}

>[!NOTE]
>
>以下源支援使用流補插頁：<ul><li>[[!DNL Amazon Kinesis]](../sources/connectors/cloud-storage/kinesis.md)</li><li>[[!DNL Azure Event Hubs]](../sources/connectors/cloud-storage/eventhub.md)</li><li>[[!DNL HTTP API]](../sources/connectors/streaming/http.md)</li></ul>

### 流式上插高級工作流

流上插頁 [!DNL Data Prep] 如下：

* 您必須首先為 [!DNL Profile] 消費。 請參閱上的指南 [啟用資料集 [!DNL Profile]](../catalog/datasets/enable-for-profile.md) 的下界；
* 如果必須連結新標識，則還必須建立其他資料集 **使用同一架構** 作為 [!DNL Profile] 資料集；
* 準備好資料集後，必須建立資料流，將傳入的請求映射到 [!DNL Profile] 資料集；
* 接下來，必須更新傳入請求以包含必要的標頭。 這些標題定義：
   * 需要使用執行的資料操作 [!DNL Profile]: `create`。 `merge`, `delete`;
   * 要使用執行的可選標識操作 [!DNL Identity Service]: `create`。

### 配置標識資料集

如果必須連結新標識，則必須在傳入負載中建立並傳遞附加資料集。 建立標識資料集時，必須確保滿足以下要求：

* 標識資料集必須具有其關聯的架構 [!DNL Profile] 資料集。 模式不匹配可能導致系統行為不一致；
* 但是，必須確保標識資料集與 [!DNL Profile] 資料集。 如果資料集相同，則資料將被覆蓋而不是更新；
* 當初始資料集必須為 [!DNL Profile]，標識資料集 **不應** 啟用 [!DNL Profile]。 否則，資料也將被覆蓋而不是更新。

#### 與標識資料集關聯的架構中的必填欄位 {#identity-dataset-required-fileds}

如果您的架構包含必填欄位，則必須禁止驗證資料集才能啟用 [!DNL Identity Service] 只接收身份。 通過應用 `disabled` 值 `acp_validationContext` 的下界。 請參閱以下示例：

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
>如果與標識資料集關聯的架構沒有任何必需欄位，則無需執行任何其他配置。

## 傳入負載結構

下面顯示了建立新標識連結的傳入負載結構的示例。

### 具有標識配置的負載

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
| `flowId` | 標識資料流的唯一ID。 此資料流ID應與建立的源連接對應 [!DNL Amazon Kinesis]。 [!DNL Azure Event Hubs]或 [!DNL HTTP API]。 此資料流還應具有 [!DNL Profile]-enabled dataset作為目標資料集。 **注釋**:的ID [!DNL Profile]-enabled目標資料集也用作 `datasetId` 的下界。 |
| `imsOrgId` | 與您的組織對應的ID。 |
| `datasetId` | 的ID [!DNL Profile]已啟用資料流的目標資料集。 **注釋**:這與 [!DNL Profile]在資料流中找到 — enabled目標資料集ID。 |
| `operations` | 此參數概述了 [!DNL Data Prep] 將基於傳入的請求。 |
| `operations.data` | 定義必須在 [!DNL Profile Service]。 |
| `operations.identity` | 定義資料允許的操作 [!DNL Identity Service]。 |
| `operations.identityDatasetId` | （可選）只有在必須連結新標識時才需要的標識資料集的ID。 |

#### 支援的操作

支援以下操作 [!DNL Profile Service]:

| 運作 | 說明 |
| --- | --- | 
| `create` | 預設操作。 這將生成XDM實體建立方法 [!DNL Profile Service]。 |
| `merge` | 這將生成XDM實體更新方法 [!DNL Profile Service]。 |
| `delete` | 這將生成XDM實體刪除方法 [!DNL Profile Service] 並從 [!DNL Profile Store]。 |

支援以下操作 [!DNL Identity Service]:

| 運作 | 說明 |
| --- | --- |
| `create` | 此參數唯一允許的操作。 如果 `create` 作為 `operations.identity`，則 [!DNL Data Prep] 生成XDM實體建立請求 [!DNL Identity Service]。 如果標識已存在，則忽略該標識。 **注：** 如果 `operations.identity` 設定為 `create`，則 `identityDatasetId` 也必須指定。 XDM實體建立由 [!DNL Data Prep] 將為此資料集ID生成元件。 |

### 無標識配置的負載

如果不需要連結新身份，則可以忽略 `identity` 和 `identityDatasetId` 操作中的參數。 這樣做只將資料發送到 [!DNL Profile Service] 跳過 [!DNL Identity Service]。 有關示例，請參見下面的負載：

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

## 動態傳遞主標識

對於XDM更新，必須為 [!DNL Profile] 並包含主身份。 可以通過兩種方式指定XDM架構的主標識：

* 在XDM模式中指定靜態欄位作為主標識；
* 通過XDM架構中的標識映射欄位組將其中一個標識欄位指定為主標識。

### 在XDM架構中將靜態欄位指定為主標識欄位

在下面的示例中， `state`。 `homePhone.number` 而其它屬性則使用它們各自的給定值更新到 [!DNL Profile] 主要身份為 `sampleEmail@gmail.com`。 然後由流生成XDM實體更新消息 [!DNL Data Prep] 元件。 [!DNL Profile Service] 然後確認XDM更新消息以更新配置檔案記錄。

>[!NOTE]
>
>在本示例中，身份將不會連結在一起，因為沒有為身份定義任何操作。

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

### 通過XDM架構中的標識映射欄位組將其中一個標識欄位指定為主標識

在此示例中，標題包含 `operations` 屬性 `identity` 和 `identityDatasetId` 屬性。 這允許資料與 [!DNL Profile Service] 還有把身份傳給 [!DNL Identity Service]。

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

## 已知限制和關鍵注意事項

以下概述了在上插頁流時要考慮的已知限制清單 [!DNL Data Prep]:

* 只有在將部分行更新發送到 [!DNL Profile Service]。 部分行更新是 **不** 由資料湖消耗。
* 流式Upserts方法不支援更新、替換和刪除身份。 如果不存在新標識，則建立新標識。 因此 `identity` 必須始終將操作設定為建立。 如果標識已存在，則操作為no-op。
* 流upsreats方法當前僅支援基元單值屬性（如整數、日期、時間戳和字串）和對象。
* 流補插頁方法當前不支援 [Adobe Experience PlatformWeb SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=zh-Hant) 和 [Adobe Experience Platform移動SDK](https://aep-sdks.gitbook.io/docs/)。

## 後續步驟

通過閱讀此文檔，您應該瞭解如何在 [!DNL Data Prep] 將部分行更新發送到 [!DNL Profile Service] 資料，同時還使用單個API請求建立和連結標識。 有關其他資訊的詳細資訊 [!DNL Data Prep] 功能，請閱讀 [[!DNL Data Prep] 概述](./home.md)。 瞭解如何在 [!DNL Data Prep] API，請閱讀 [[!DNL Data Prep] 開發者指南](./api/overview.md)。
