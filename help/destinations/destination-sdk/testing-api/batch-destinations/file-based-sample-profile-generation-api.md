---
description: 本頁說明如何從Destination SDK使用/sample-profiles API端點，根據來源架構產生範例設定檔。 您可以使用這些範例設定檔來測試您的檔案式目的地設定。
title: 根據來源結構產生範例設定檔
exl-id: aea50d2e-e916-4ef0-8864-9333a4eafe80
source-git-commit: adf75720f3e13c066b5c244d6749dd0939865a6f
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 1%

---


# 根據來源結構產生範例設定檔

測試檔案式目的地的第一步，是使用 `/sample-profiles` 端點，根據您現有的來源架構產生範例設定檔。

範例設定檔可協助您了解設定檔的JSON結構。 此外，它們也提供您預設值，您可以使用自己的設定檔資料加以自訂，以進一步進行目的地測試。

## 快速入門 {#getting-started}

繼續之前，請檢閱 [快速入門手冊](../../getting-started.md) 若要成功呼叫API，需知的重要資訊，包括如何取得必要的目的地編寫權限和必要的標題。

## 先決條件 {#prerequisites}

您可以使用 `/sample-profiles` 端點，確定您符合下列條件：

* 您已透過Destination SDK建立現有的檔案型目的地，並可在 [目的地目錄](../../../ui/destinations-workspace.md).
* 您已在Experience PlatformUI中為您的目的地建立至少一個啟用流程。 此 `/sample-profiles` 端點會根據您在啟動流程中定義的來源架構來建立設定檔。 請參閱 [啟用教學課程](../../../ui/activate-batch-profile-destinations.md) 了解如何建立啟動流程。
* 若要成功提出API請求，您需要與要測試的目的地執行個體對應的目的地執行個體ID。 在Platform UI中瀏覽與目的地的連線時，從URL取得應用於API呼叫的目的地執行個體ID。

   ![顯示如何從URL取得目的地執行個體ID的UI影像。](../../assets/testing-api/get-destination-instance-id.png)

## 產生用於目的地測試的範例設定檔 {#generate-sample-profiles}

您可以向發出GET要求，以根據來源結構產生範例設定檔 `/sample-profiles` 端點，包含您要測試之目的地的目的地執行個體ID。

**API格式**

```http
GET /authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}&count={NUMBER_OF_GENERATED_PROFILES}
```

| 查詢參數 | 說明 |
| -------- | ----------- |
| `destinationInstanceId` | 您要產生範例設定檔的目的地例項ID。 請參閱 [必要條件](#prerequisites) 一節，以取得此ID的詳細資訊。 |
| `count` | *可選*. 您要產生的範例設定檔數目。 參數可以取用 `1 - 1000`. 如果此屬性未定義，則API會產生單一範例設定檔。 |

**要求**

下列請求會根據目標例項中定義的來源結構，以及對應的來源結構，產生範例設定檔 `destinationInstanceId`.

```shell
curl -X GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}' \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

成功的回應會傳回HTTP狀態200，包含指定數量的範例設定檔，以及對應至來源XDM架構的區段成員資格、身分和設定檔屬性。

>[!NOTE]
>
> 回應只會傳回目的地例項中使用的區段成員資格、身分和設定檔屬性。 即使您的源架構有其他欄位，這些欄位也會被忽略。

```json
[
   {
      "segmentMembership":{
         "ups":{
            "fea8d394-5a8c-4cea-bebc-df020ce37f5c":{
               "lastQualificationTime":"2022-01-13T11:33:28.211895Z",
               "status":"realized"
            },
            "5fa55d3a-18e1-4f65-95ed-ac8fdb03b45b":{
               "lastQualificationTime":"2022-01-13T11:33:28.211893Z",
               "status":"realized"
            }
         }
      },
      "personalEmail":{
         "address":"john.smith@abc.com"
      },
      "identityMap":{
         "crmid":[
            {
               "id":"crmid-P1A7l"
            }
         ]
      },
      "person":{
         "name":{
            "firstName":"string",
            "lastName":"string"
         }
      }
   }
]
```

![顯示從UI對應至API回應之欄位的影像。](../../assets/testing-api/batch-destinations/sample-api-response-mapping.png)

| 屬性 | 說明 |
| -------- | ----------- |
| `segmentMembership` | 描述個人區段成員資格的映射物件。 如需 `segmentMembership`，讀取 [區段成員資格詳細資料](../../../../xdm/field-groups/profile/segmentation.md). |
| `lastQualificationTime` | 此設定檔符合區段資格的上次時間時間戳記。 |
| `status` | 字串欄位，指出區段成員資格是否已在目前請求中實現。 接受下列值： <ul><li>`realized`:設定檔是區段的一部分。</li><li>`exited`:設定檔會隨著目前請求退出區段。</li></ul> |
| `identityMap` | 一種地圖類型欄位，說明個人的各種身分值及其相關聯的命名空間。 如需 `identityMap`，請參閱 [綱要組合的基礎](../../../../xdm/schema/composition.md#identityMap). |

{style="table-layout:auto"}

## API錯誤處理 {#api-error-handling}

Destination SDKAPI端點遵循一般Experience PlatformAPI錯誤訊息原則。 請參閱 [API狀態代碼](../../../../landing/troubleshooting.md#api-status-codes) 和 [請求標題錯誤](../../../../landing/troubleshooting.md#request-header-errors) （位於平台疑難排解指南中）。

## 後續步驟

閱讀本檔案後，您現在知道如何根據您在目的地中設定的來源架構產生範例設定檔 [啟動流程](../../../ui/activate-batch-profile-destinations.md).

您現在可以自訂這些設定檔，或在API傳回時使用這些設定檔， [測試基於檔案的目標配置](file-based-destination-testing-api.md).
