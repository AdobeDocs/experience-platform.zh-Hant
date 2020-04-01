---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 評估區段
topic: tutorial
translation-type: tm+mt
source-git-commit: 7f61cee8fb5160d0f393f8392b4ce2462d602981

---


# 評估並存取區段結果

本檔案提供使用區段API評估區段及存取區段結果的 [教學課程](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml)。

## 快速入門

本教學課程需要有效瞭解建立受眾細分所涉及的各種Adobe Experience Platform服務。 在開始本教學課程之前，請先閱讀下列服務的檔案：

- [即時客戶個人檔案](../../profile/home.md):根據來自多個來源的匯整資料，即時提供統一的客戶個人檔案。
- [Adobe Experience Platform細分服務](../home.md):可讓您從即時客戶個人檔案資料建立受眾細分。
- [體驗資料模型(XDM)](../../xdm/home.md):平台組織客戶體驗資料的標準化架構。
- [沙盒](../../sandboxes/home.md):Experience Platform提供虛擬沙盒，可將單一Platform實例分割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

### 必要的標題

本教學課程也要求您完成驗證教 [學課程](../../tutorials/authentication.md) ，才能成功呼叫平台API。 完成驗證教學課程後，所有Experience Platform API呼叫中每個必要標題的值都會顯示在下方：

- 授權：生產者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Experience Platform中的所有資源都隔離至特定的虛擬沙盒。 對平台API的請求需要一個標題，該標題指定要在中執行操作的沙盒名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

> [!NOTE] 如需平台中沙盒的詳細資訊，請參閱沙盒 [概觀檔案](../../sandboxes/home.md)。

所有POST、PUT和PATCH請求都需要附加標題：

- 內容類型：application/json

## 評估區段

開發、測試和儲存區段定義後，您就可以透過排程評估或隨選評估來評估區段。

[排程評估](#scheduled-evaluation)[](#on-demand-evaluation) （也稱為「排程的區段」）可讓您建立在特定時間執行匯出工作的循環排程，而隨選評估則涉及建立區段工作以立即建立觀眾。 以下列出各步驟。

如果您尚未完成「使用即時客戶描述檔 [API建立區段」教學課程，或是使用「區段產生器」建立區段定義](./create-a-segment.md)[](../ui/overview.md)，請在繼續本教學課程之前先執行此動作。

## 排程的評估

透過排程評估，您的IMS組織可以建立循環排程，以自動執行匯出工作。

> [!NOTE] XDM個別設定檔的合併原則上限為五(5)個沙盒，可啟用排程的評估。 如果貴組織在單一沙盒環境中有5種以上的XDM個人設定檔合併原則，您將無法使用排程的評估。

### 建立排程

通過向端點發出POST請 `/config/schedules` 求，您可以建立調度並包括應觸發該調度的特定時間。

**API格式**

```http
POST /config/schedules
```

**請求**

以下請求會根據裝載中提供的規格建立新的排程。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/schedules \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "{SCHEDULE_NAME}",
        "type": "batch_segmentation",
        "properties": {
            "segments": ["*"]
        },
        "schedule": "0 0 1 * * ?",
        "state": "inactive"
        }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `name` | **（必要）** ，排程名稱。 必須是字串。 |
| `type` | **（必要）** ，字串格式的工作類型。 支援的類型 `batch_segmentation` 為和 `export`。 |
| `properties` | **（必要）** ，包含與計畫相關的其他屬性的物件。 |
| `properties.segments` | **(等於時需`type`要`batch_segmentation`)** ：使用 `["*"]` 可確保包含所有區段。 |
| `schedule` | **（必要）** ，包含工作排程的字串。 作業只能排程為每天執行一次，這表示您無法排程作業在24小時期間執行多次。 顯示的範例(`0 0 1 * * ?`)意指每天在UTC 1:00:00觸發工作。 如需詳細資訊，請參閱 [cron運算式格式檔案](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) 。 |
| `state` | *（可選）包含排程狀態的字串* 。 可用值： `active` 和 `inactive`。 預設值為 `inactive`. IMS組織只能建立一個排程。 本教學課程稍後將提供更新排程的步驟。 |

**回應**

成功的回應會傳回新建立之排程的詳細資料。

```json
{
    "id": "cd585edf-962d-420d-94ad-3be03e619ac2",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "e7e17720-c5bb-11e9-aafb-87c71c35cac8",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "{SCHEDULE_NAME}",
    "state": "inactive",
    "type": "batch_segmentation",
    "schedule": "0 0 1 * * ?",
    "properties": {
        "segments": [
            "*"
        ]
    },
    "createEpoch": 1568267948,
    "updateEpoch": 1568267948
}
```

### 啟用排程

預設情況下，建立計畫時，除非將屬 `state` 性設定為建立(POST) `active` 請求主體中，否則該計畫處於非活動狀態。 通過向端點發出PATCH請求並在路徑中包 `state``active``/config/schedules` 括調度的ID，可以啟用調度（將設定為）。

**API格式**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**請求**

下列請求會使 [用JSON修補程式格式](http://jsonpatch.com/) ，以便將排程 `state` 更新為 `active`。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/schedules/cd585edf-962d-420d-94ad-3be03e619ac2 \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        {
          "op": "add",
          "path": "/state",
          "value": "active"
        }
      ]'
```

**回應**

成功的更新會傳回空回應主體和HTTP狀態204（無內容）。

使用相同的操作可以禁用調度，方法是將上一個請求中的&quot;value&quot;替換為&quot;inactive&quot;。

### 更新計畫時間

通過向端點發出PATCH請求並在路徑中包 `/config/schedules` 含調度的ID，可以更新調度時間。

**API格式**

```http
POST /config/schedules/{SCHEDULE_ID}
```

**請求**

下列請求使用 [JSON修補程式格式](http://jsonpatch.com/) ，以更新 [cron運算式](http://www.quartz-scheduler.org/documentation/quartz-2.3.0/tutorials/crontrigger.html) 。 在此範例中，排程現在會在UTC 10:15:00觸發。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/schedules/cd585edf-962d-420d-94ad-3be03e619ac2 \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        {
          "op": "add",
          "path": "/schedule",
          "value": "0 15 10 * * ?"
        }
      ]'
```

**回應**

成功的更新會傳回空回應主體和HTTP狀態204（無內容）。

## 隨選評估

隨選評估可讓您建立區段工作，以便在需要時產生對象區段。 與排程評估不同，這只會在要求時發生，且不會重複發生。

### 建立區段工作

區段工作是建立新讀者區段的非同步程式。 它參考區段定義，以及控制即時客戶描述檔如何合併描述檔片段中重疊屬性的任何合併原則。 當區段工作成功完成時，您可以收集區段的各種資訊，例如處理期間可能發生的任何錯誤，以及您的受眾的最終規模。

您可以透過對即時客戶描述檔API中的端點提出POST `/segment/jobs` 要求來建立新的區段工作。

**API格式**

```http
POST /segment/jobs
```

**請求**

下列請求會根據裝載中提供的兩個區段定義，建立新的區段工作。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/segment/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        {
          "segmentId" : "42f49f2d-edb0-474f-b29d-2799d89cd5a6"
        },
        {
          "segmentId" : "54a20f19-9a0w-293a-9b82-409b1p3v0192"
        }
    ]'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `segmentId` | 建立觀眾的區段定義識別碼。 裝載陣列中必須至少提供一個區段ID。 |

**回應**

成功的回應會傳回新建立之區段工作的詳細資料，包括其唯一 `id`的唯讀系統產生值，此值是此區段工作所獨有的。

```json
{
    "profileInstanceId": "ups",
    "computeJobId": 1,
    "id": "b0f99dde-6d3b-4d92-aa92-28072ded71a0",
    "status": "PROCESSING",
    "segments": [
        {
            "segmentId": "42f49f2d-edb0-474f-b29d-2799d89cd5a6",
            "segment": {
                "id": "42f49f2d-edb0-474f-b29d-2799d89cd5a6",
                "version": 1,
                "expression": {
                    "type": "PQL",
                    "format": "pql/text",
                    "value": "homeAddress.country = \"US\""
                },
                "mergePolicy": {
                    "id": "mpid1",
                    "version": 1
                }
            }
        },
        {
            "segmentId": "54a20f19-9a0w-293a-9b82-409b1p3v0192",
            "segment": {
                "id": "54a20f19-9a0w-293a-9b82-409b1p3v0192",
                "version": 1,
                "expression": {
                    "type": "PQL",
                    "format": "pql/text",
                    "value": "homeAddress.country = \"US\""
                },
                "mergePolicy": {
                    "id": "mpid1",
                    "version": 1
                }
            }
        }
    ],
    "updateTime": 1533581808162,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1533581808162,
    "_links": {
        "cancel": {
            "href": "/segment/jobs/b0f99dde-6d3b-4d92-aa92-28072ded71a0",
            "method": "DELETE"
        },
        "checkStatus": {
            "href": "/segment/jobs/b0f99dde-6d3b-4d92-aa92-28072ded71a0",
            "method": "GET"
        }
    }
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `id` | 新區段工作的識別碼，用於查閱。 |
| `status` | 區段工作的目前狀態。 在處理完成之前，將為「處理」，此時會變成「成功」或「失敗」。 |

### 查找段作業狀態

您可以使用 `id` 特定區段工作來執行查閱請求(GET)，以檢視工作的目前狀態。

**API格式**

```http
GET /segment/jobs/{SEGMENT_JOB_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{SEGMENT_JOB_ID}` | 您 `id` 要存取的區段工作。 |

**請求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/segment/jobs/80388706-29fa-40d3-81cf-a297d0224ad9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

成功的回應會傳回分段工作的詳細資料，並根據工作的目前狀態提供不同的資訊。 您可以重複查閱請求，直 `status` 到達「SUCCEEDED」（成功），此時您可將區段匯出至資料集。


```json
{
    "profileInstanceId": "ups",
    "errors": [],
    "computeJobId": 13377,
    "modelName": "_xdm.context.profile",
    "id": "80388706-29fa-40d3-81cf-a297d0224ad9",
    "status": "SUCCEEDED",
    "segments": [
        {
            "segmentId": "b560a09a-de85-4a1c-8477-2f3da1d9e86b",
            "segment": {
                "id": "b560a09a-de85-4a1c-8477-2f3da1d9e86b",
                "version": 1,
                "expression": {
                    "type": "PQL",
                    "format": "pql/json",
                    "value": "homeAddress.country = \"US\""
                },
                "mergePolicy": {
                    "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
                    "version": 1
                }
            }
        }
    ],
    "requestId": "prgu92v4VNvsGuuXticcsqX96UXGjXtS",
    "computeGatewayJobId": "a7c33b77-3aeb-497f-bc88-807915c57b5f",
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1547063631503,
            "endTimeInMs": 1547063731181,
            "totalTimeInMs": 99678
        },
        "profileSegmentationTime": {
            "startTimeInMs": 1547063669001,
            "endTimeInMs": 1547063720887,
            "totalTimeInMs": 51886
        },
        "segmentedProfileCounter": {
            "ca763983-5572-4ea4-809c-b7dff7e0d79b": 4195,
            "251e3a1f-645c-4444-836b-18e6b668bdf8": 0,
            "3da8bad9-29fb-40e0-b39e-f80322e964de": 0,
            "30230300-ccf1-48ad-8012-c5563a007069": 0
        },
        "segmentedProfileByNamespaceCounter": {
            "ca763983-5572-4ea4-809c-b7dff7e0d79b": {
                "email": 4195
            },
            "251e3a1f-645c-4444-836b-18e6b668bdf8": {},
            "3da8bad9-29fb-40e0-b39e-f80322e964de": {},
            "30230300-ccf1-48ad-8012-c5563a007069": {}
        }     
    },
    "updateTime": 1547063731181,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1547063631503,
    "_links": {
        "cancel": {
            "href": "/segment/jobs/80388706-29fa-40d3-81cf-a297d0224ad9",
            "method": "DELETE"
        },
        "checkStatus": {
            "href": "/segment/jobs/80388706-29fa-40d3-81cf-a297d0224ad9",
            "method": "GET"
        }
    }
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `segmentedProfileCounter` | 符合區段資格的合併描述檔總數。 |
| `segmentedProfileByNamespaceCounter` | 依身分命名空間代碼劃分符合區段資格的描述檔。 您可在識別名稱空間概述中找到識別名稱空間 [代碼清單](../../identity-service/namespaces.md)。 |

## 解譯區段結果

當區段工作成功執行時，會針 `segmentMembership` 對區段內的每個描述檔更新地圖。 `segmentMembership` 此外，還會儲存任何預先評估的受眾細分，這些細分會納入Platform中，以便與其他解決方案（例如Adobe Audience Manager）整合。

以下範例顯示每個個 `segmentMembership` 別描述檔記錄的屬性外觀：

```json
{
  "segmentMembership": {
    "UPS": {
      "04a81716-43d6-4e7a-a49c-f1d8b3129ba9": {
        "timestamp": "2018-04-26T15:52:25+00:00",
        "status": "existing"
      },
      "53cba6b2-a23b-454a-8069-fc41308f1c0f": {
        "lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "status": "realized"
      }
    },
    "Email": {
      "abcd@adobe.com": {
        "lastQualificationTime": "2017-09-26T15:52:25+00:00",
        "status": "exited"
      }
    }
  }
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `lastQualificationTime` | 斷言區段成員資格及設定檔輸入或退出區段時的時間戳記。 |
| `status` | 目前請求中區段參與率的狀態。 必須等於下列其中一個已知值： <ul><li>`existing`:實體繼續在分部中。</li><li>`realized`:實體正在輸入區段。</li><li>`exited`:實體正在退出區段。</li></ul> |

## 存取區段結果

可以通過以下兩種方式之一訪問段作業的結果：您可以存取個別設定檔，或將整個對象匯出至資料集。

以下幾節將更詳細地概述這些選項。

## 查找配置檔案

如果您知道要存取的特定描述檔，則可使用即時客戶描述檔API進行存取。 使用「描述檔API」教學課程的「存取即時客戶描述檔」資料中，提供存取個 [別描述檔的完整步驟](../../profile/api/entities.md) 。

## 匯出區段

分段工作成功完成(屬性的值為 `status` 「成功」)後，您可將對象匯出至資料集，供您存取及操作。

匯出您的觀眾需要下列步驟：

- [建立目標資料集](#create-a-target-dataset) -建立資料集以容納對象成員。
- [在資料集中產生觀眾設定檔](#generate-profiles-for-audience-members) -根據區段工作的結果，以XDM個別設定檔填入資料集。
- [監視導出進度](#monitor-export-progress) -檢查導出進程的當前進度。
- [讀取觀眾資料](#next-steps) -擷取產生的XDM個人設定檔，代表觀眾的成員。

### 建立目標資料集

匯出對象時，必須先建立目標資料集。 請務必正確設定資料集，以確保匯出成功。

主要考量事項之一是資料集所依據的架構(在下`schemaRef.id` 面的API範例請求中)。 若要匯出區段，資料集必須以XDM個別描述檔結合架構(`https://ns.adobe.com/xdm/context/profile__union`)為基礎。 聯合模式是系統生成的只讀模式，它聚合共用相同類的模式的欄位（在本例中為XDM Individual Profile類）。 有關聯合視圖方案的詳細資訊，請參閱 [方案註冊開發人員指南的「即時客戶概要檔案」部分](../../xdm/api/getting-started.md)。

建立必要資料集有兩種方式：

- **使用API:** 本教學課程中的後續步驟概述如何使用目錄API建立參照XDM個別描述檔結合架構的資料集。
- **使用UI:** 若要使用Adobe Experience Platform使用者介面來建立參照聯合架構的資料集，請依照 [UI教學課程中的步驟](../ui/overview.md) ，然後返回本教學課程，繼續產生觀眾設定檔 [的步驟](#generate-xdm-profiles-for-audience-members)。

如果您已擁有相容的資料集並知道其ID，則可直接執行步驟，以產生觀 [眾設定檔](#generate-xdm-profiles-for-audience-members)。

**API格式**

```http
POST /dataSets
```

**請求**

下列請求會建立新資料集，提供裝載中的設定參數。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "name": "Segment Export",
    "schemaRef": {
        "id": "https://ns.adobe.com/xdm/context/profile__union",
        "contentType": "application/vnd.adobe.xed+json;version=1"
    },
    "fileDescription": {
        "persisted": true,
        "containerFormat": "parquet",
        "format": "parquet"
    },
    "aspect": "production"
}'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `name` | 資料集的描述性名稱。 |
| `schemaRef.id` | 資料集將與之關聯的聯合檢視（結構）ID。 |
| `fileDescription.persisted` | 布爾值，設定為 `true`時，可讓資料集在聯合檢視中持續存在。 |

**回應**

成功的回應會傳回包含新建立資料集之唯讀、系統產生之唯一ID的陣列。 若要成功匯出觀眾成員，需要正確設定的資料集ID。

```json
[
  "@/datasets/5b020a27e7040801dedba61b"
] 
```

### 為觀眾成員產生個人檔案

在您擁有持續合併的資料集後，您可以建立匯出工作，透過對即時客戶描述檔API中的端點提出POST要求，並提供資料集ID和您要匯出之區段的區段資訊，將觀眾成員持續存留至資料集。 `/export/jobs`

**API格式**

```http
POST /export/jobs
```

**請求**

下列請求會建立新的匯出工作，提供裝載中的設定參數。

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/export/jobs \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "fields": "identities.id,personalEmail.address",
    "mergePolicy": {
      "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
      "version": 1
    },
    "filter": {
      "segments": [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"]
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"]
        }
      ],
      "segmentQualificationTime": {
            "startTime": "2019-09-01T00:00:00Z",
            "endTime": "2019-09-02T00:00:00Z"
        },
      "fromIngestTimestamp": "2018-10-25T13:22:04-07:00",
      "emptyProfiles": false
    },
    "additionalFields" : {
      "eventList": {
        "fields": "environment.browserDetails.name,environment.browserDetails.version",
        "filter": {
          "fromIngestTimestamp": "2018-10-25T13:22:04-07:00"
        }
      }
    },
    "destination": {
      "datasetId": "5b020a27e7040801dedba61b",
      "segmentPerBatch": true
    },
    "schema": {
      "name": "_xdm.context.profile"
    }
  }'
```

| 屬性 | 說明 |
| -------- | ----------- |
| `fields` | *（可選）* ，將要包含在導出中的資料欄位限制為僅限此參數中提供的資料欄位。 建立區段時也可使用相同的參數，因此區段中的欄位可能已經過篩選。 省略此值會導致所有欄位都包含在匯出的資料中 |
| `mergePolicy` | *（可選）* 指定用於管理導出資料的合併策略。 當有多個區段要匯出時，請加入此參數。 省略此值將導致Export Service使用區段提供的合併原則。 |
| `mergePolicy.id` | 合併策略的ID |
| `mergePolicy.version` | 要使用的合併策略的特定版本。 省略此值將預設為最新版本。 |
| `filter` | *（可選）* 指定在匯出前套用至區段的下列一或多個篩選： |
| `filter.segments` | *（選用）* ，指定要匯出的區段。 省略此值將導致導出所有配置檔案中的所有資料。 接受區段物件的陣列，每個物件都包含下列欄位： |
| `filter.segments.segmentId` | **（若使用）`segments`** 「區段ID」，則需要匯出描述檔。 |
| `filter.segments.segmentNs` | *（可選）* ，指定的區段名稱空間 `segmentID`。 |
| `filter.segments.status` | *（可選）* ，提供狀態篩選的字串陣列 `segmentID`。 依預設， `status` 將會有值， `["realized", "existing"]` 代表目前時段屬於區段的所有描述檔。 可能的值包括： `"realized"`、 `"existing"`和 `"exited"`。 |
| `filter.segmentQualificationTime` | *（選用）* ，根據區段限定時間篩選。 可以提供開始時間和／或結束時間。 |
| `filter.segmentQualificationTime.startTime` | *（可選）* ，指定狀態之區段ID的區段資格開始時間。 未提供，區段ID資格的開始時間將不會有篩選。 時間戳必須以 [RFC 3339格式提供](https://tools.ietf.org/html/rfc3339) 。 |
| `filter.segmentQualificationTime.endTime` | *（可選）* ，指定狀態之區段ID的區段資格結束時間。 未提供，區段ID資格的結束時間將不會有篩選。 時間戳必須以 [RFC 3339格式提供](https://tools.ietf.org/html/rfc3339) 。 |
| `filter.fromIngestTimestamp` | *（可選）* 「限制」匯出的描述檔僅包含在此時間戳記後更新的描述檔。 時間戳必須以 [RFC 3339格式提供](https://tools.ietf.org/html/rfc3339) 。 |
| `filter.fromIngestTimestamp` 如果 **提供**，則 | 包含所有合併的描述檔，其中合併的更新時間戳記大於指定的時間戳記。 支援操 `greater_than` 作數。 |
| `filter.fromTimestamp` 適用於事件 | 在此時間戳記之後收錄的所有事件都會匯出，以對應於產生的描述檔結果。 這不是事件時間本身，而是事件的擷取時間。 |
| `filter.emptyProfiles` | *（可選）* Boolean。 設定檔可以包含設定檔記錄、ExperienceEvent記錄或兩者。 沒有設定檔記錄且只有ExperienceEvent記錄的設定檔稱為「emptyProfiles」。 要導出配置檔案儲存中的所有配置檔案，包括「emptyProfiles」，請將值設 `emptyProfiles` 置為 `true`。 如果 `emptyProfiles` 設定為， `false`則只導出儲存中具有配置檔案記錄的配置檔案。 預設情況下，如果不包 `emptyProfiles` 含屬性，則僅導出包含配置檔案記錄的配置檔案。 |
| `additionalFields.eventList` | *（可選）* ，通過提供以下一個或多個設定來控制為子對象或關聯對象導出的時間系列事件欄位： |
| `additionalFields.eventList.fields` | 控制要匯出的欄位。 |
| `additionalFields.eventList.filter` | 指定限制關聯對象所包含結果的標準。 預期匯出所需的最低值，通常為日期。 |
| `additionalFields.eventList.filter.fromIngestTimestamp` | 將時間系列事件篩選為在提供時間戳記後所擷取的事件。 這不是事件時間本身，而是事件的擷取時間。 |
| `destination` | **（必要）** ，匯出資料的目標資訊 |
| `destination.datasetId` | **（必要）** ，要匯出資料的資料集ID。 |
| `destination.segmentPerBatch` | *（可選）* ，一個布爾值，如果未提供，則預設為 `false`。 值將所有 `false` 區段ID匯出為單一批次ID。 值將一個 `true` 區段ID匯出為一個批次ID。 請注意，將值設定為可能 `true` 會影響批導出效能。 |
| `schema.name` | **（必要）** ，與要匯出資料的資料集關聯的架構名稱。 |

**回應**

成功的回應會傳回資料集，其中填入符合區段工作上次完成執行的設定檔。 已移除任何先前可能存在於資料集中，但在上次完成區段工作執行期間不符合區段資格的設定檔。

```json
{
    "profileInstanceId": "ups",
    "jobType": "BATCH",
    "filter": {
      "segments": [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"]
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"]
        }
      ]
    },
    "id": 24115,
    "schema": {
        "name": "_xdm.context.profile"
    },
    "mergePolicy": {
        "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
        "version": 1
    },
    "status": "NEW",
    "requestId": "IwkVcD4RupdSmX376OBVORvcvTdA4ypN",
    "computeGatewayJobId": {},
    "metrics": {
        "totalTime": {
            "startTimeInMs": 1559674261657
        }
    },
    "destination": {
      "dataSetId" : "5cf6bcf79ecc7c14530fe436",
      "segmentPerBatch": true,
      "batches" : [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"],
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"],
          "batchId": "df4gssdfb93a09f7e37fa53ad52"
        }
      ]
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1559674261657
}
```

如 `destination.segmentPerBatch` 果請求中未包含(如果不存在，則預設為 `false`)或值已設為 `false`，則上述回應中的物件將不會包含陣列，而只會包含一個 `destination``batches``batchId`，如下所示。 該單一批次會包含所有區段ID，而上述回應則會針對每個批次ID顯示單一區段ID。

```json
  "destination": {
    "datasetId": "5cf6bcf79ecc7c14530fe436",
    "segmentPerBatch": false,
    "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
  }
```

### 列出所有匯出工作

您可以執行GET請求至端點，傳回特定IMS組織所有匯出工作的清 `export/jobs` 單。 請求也支援查詢參 `limit` 數 `offset`和，如下所示。

**API格式**

```http
GET /export/jobs
GET /export/jobs?limit=4
GET /export/jobs?offset=2
```

| 屬性 | 說明 |
| -------- | ----------- |
| `limit` | 指定要傳回的記錄數。 |
| `offset` | 將要傳回的結果頁面偏移所提供的數字。 |


**請求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/export/jobs/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

回應包含包 `records` 含由IMS組織建立之匯出工作的物件。

```json
{
  "records": [
    {
      "profileInstanceId": "ups",
      "jobType": "BATCH",
      "filter": {
          "segments": [
              {
                  "segmentId": "52c26d0d-45f2-47a2-ab30-ed06abc981ff"
              }
          ]
      },
      "id": 726,
      "schema": {
          "name": "_xdm.context.profile"
      },
      "mergePolicy": {
          "id": "timestampOrdered-none-mp",
          "version": 1
      },
      "status": "SUCCEEDED",
      "requestId": "d995479c-8a08-4240-903b-af469c67be1f",
      "computeGatewayJobId": {
          "exportJob": "f3058161-7349-4ca9-807d-212cee2c2e94",
          "pushJob": "feaeca05-d137-4605-aa4e-21d19d801fc6"
      },
      "metrics": {
          "totalTime": {
              "startTimeInMs": 1538615973895,
              "endTimeInMs": 1538616233239,
              "totalTimeInMs": 259344
          },
          "profileExportTime": {
              "startTimeInMs": 1538616067445,
              "endTimeInMs": 1538616139576,
              "totalTimeInMs": 72131
          },
          "aCPDatasetWriteTime": {
              "startTimeInMs": 1538616195172,
              "endTimeInMs": 1538616195715,
              "totalTimeInMs": 543
          }
      },
      "destination": {
          "datasetId": "5b7c86968f7b6501e21ba9df",
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
      },
      "updateTime": 1538616233239,
      "imsOrgId": "{IMS_ORG}",
      "creationTime": 1538615973895
    },
    {
      "profileInstanceId": "test_xdm_latest_profile_20_e2e_1538573005395",
      "errors": [
        {
          "code": "0090000009",
          "msg": "Error writing profiles to output path 'adl://va7devprofilesnapshot.azuredatalakestore.net/snapshot/722'",
          "callStack": "com.adobe.aep.unifiedprofile.common.logging.Logger" 
        },
        {
          "code": "unknown",
          "msg": "Job aborted.",
          "callStack": "org.apache.spark.SparkException: Job aborted."
        }
      ],
      "jobType": "BATCH",
      "filter": {
        "segments": [
            {
                "segmentId": "7a93d2ff-a220-4bae-9a4e-5f3c35032be3"
            }
        ]
      },
      "id": 722,
      "schema": {
          "name": "_xdm.context.profile"
      },
      "mergePolicy": {
          "id": "7972e3d6-96ea-4ece-9627-cbfd62709c5d",
          "version": 1
      },
      "status": "FAILED",
      "requestId": "KbOAsV7HXmdg262lc4yZZhoml27UWXPZ",
      "computeGatewayJobId": {
          "exportJob": "15971e0f-317c-4390-9038-1a0498eb356f"
      },
      "metrics": {
          "totalTime": {
              "startTimeInMs": 1538573416687,
              "endTimeInMs": 1538573922551,
              "totalTimeInMs": 505864
          },
          "profileExportTime": {
              "startTimeInMs": 1538573872211,
              "endTimeInMs": 1538573918809,
              "totalTimeInMs": 46598
          }
      },
      "destination": {
          "datasetId": "5bb4c46757920712f924a3eb",
          "batchId": ""
      },
      "updateTime": 1538573922551,
      "imsOrgId": "{IMS_ORG}",
      "creationTime": 1538573416687
    }
  ],
  "page": {
      "sortField": "createdTime",
      "sort": "desc",
      "pageOffset": "1538573416687_722",
      "pageSize": 2
  },
  "link": {
      "next": "/export/jobs/?limit=2&offset=1538573416687_722"
  }
}
```

### 監視導出進度

作為導出作業進程，您可以通過向端點發出GET請求並在路徑中包 `/export/jobs` 括導出作 `id` 業來監視其狀態。 一旦欄位傳回值&quot;SUCCEEDED&quot;, `status` 匯出工作就會完成。

**API格式**

```http
GET /export/jobs/{EXPORT_JOB_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{EXPORT_JOB_ID}` | 您 `id` 要存取的匯出工作。 |

**請求**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/export/jobs/24115 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

```json
{
    "profileInstanceId": "ups",
    "jobType": "BATCH",
    "filter": {
      "segments": [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"]
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"]
        }
      ]
    },
    "id": 24115,
    "schema": {
        "name": "_xdm.context.profile"
    },
    "mergePolicy": {
        "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
        "version": 1
    },
    "status": "SUCCEEDED",
    "requestId": "YwMt1H8QbVlGT2pzyxgwFHTwzpMbHrTq",
    "computeGatewayJobId": {
      "exportJob": "305a2e5c-2cf3-4746-9b3d-3c5af0437754",
      "pushJob": "963f275e-91a3-4fa1-8417-d2ca00b16a8a"
    },
    "metrics": {
      "totalTime": {
        "startTimeInMs": 1547053539564,
        "endTimeInMs": 1547054743929,
        "totalTimeInMs": 1204365
      },
      "profileExportTime": {
        "startTimeInMs": 1547053667591,
        "endTimeInMs": 1547053778195,
        "totalTimeInMs": 110604
      },
      "aCPDatasetWriteTime": {
        "startTimeInMs": 1547054660416,
        "endTimeInMs": 1547054698918,
        "totalTimeInMs": 38502
      }
    },
    "destination": {
      "dataSetId" : "5cf6bcf79ecc7c14530fe436",
      "segmentPerBatch": true,
      "batches" : [
        {
          "segmentId": "4edc8488-2c35-4f6d-b4c6-9075c68d2df4",
          "segmentNs": "AAM",
          "status": ["realized"],
          "batchId": "da5cfb4de32c4b93a09f7e37fa53ad52"
        },
        {
          "segmentId": "1rfe8422-334d-12f4-3sd4-12cf6g990g51",
          "segmentNs": "UPS",
          "status": ["exited"],
          "batchId": "df4gssdfb93a09f7e37fa53ad52"
        }
      ]
    },
    "updateTime": 1559674261868,
    "imsOrgId": "{IMS_ORG}",
    "creationTime": 1559674261657
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `batchId` | 從成功匯出建立的批次識別碼，在讀取觀眾資料時用於查閱。 |

## 後續步驟

匯出成功後，您的資料就可在Experience Platform的資料湖中使用。 然後，您就可以使 [用「資料存取API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) 」，使用與匯出相 `batchId` 關的資料來存取資料。 視區段大小而定，資料可能以區塊為單位，而批次可能由數個檔案組成。

如需如何使用資料存取API存取和下載批次檔案的逐步指示，請依照資料存取教 [學課程](../../data-access/api.md)。

您也可以使用Adobe Experience Platform Query Service存取成功匯出的區段資料。 使用UI或REST風格的API，查詢服務可讓您在資料湖中寫入、驗證及執行資料查詢。

如需如何查詢觀眾資料的詳細資訊，請參閱查詢服 [務檔案](../../query-service/home.md)。
