---
description: 此頁面說明如何使用Destination SDK中的/sample-profiles API端點，根據來源結構描述產生範例設定檔。 您可以使用這些設定檔範例來測試以檔案為基礎的目的地組態。
title: 根據來源結構描述產生範例設定檔
exl-id: aea50d2e-e916-4ef0-8864-9333a4eafe80
source-git-commit: c1ba465a8a866bd8bdc9a2b294ec5d894db81e11
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 1%

---


# 根據來源結構描述產生範例設定檔

測試以檔案為基礎的目的地的第一個步驟是使用`/sample-profiles`端點根據您現有的來源結構描述產生範例設定檔。

設定檔範例可協助您瞭解設定檔的JSON結構。 此外，它們會提供預設值，您可以使用自己的設定檔資料來自訂，以進行進一步的目的地測試。

## 快速入門 {#getting-started}

繼續之前，請檢閱[快速入門手冊](../../getting-started.md)以取得重要資訊，您必須瞭解這些資訊才能成功呼叫API，包括如何取得必要的目的地撰寫許可權和必要的標頭。

## 先決條件 {#prerequisites}

在使用`/sample-profiles`端點之前，請確定您符合下列條件：

* 您有一個透過Destination SDK建立的檔案型目的地，且您可以在[目的地目錄](../../../ui/destinations-workspace.md)中看到它。
* 您已在Experience Platform UI中為您目的地建立至少一個啟用流程。 `/sample-profiles`端點會根據您在啟動流程中定義的來源結構描述建立設定檔。 請參閱[啟動教學課程](../../../ui/activate-batch-profile-destinations.md)，瞭解如何建立啟動流程。
* 若要成功提出API請求，您需要與要測試的目的地執行個體對應的目的地執行個體ID。 在Platform UI中瀏覽與目的地的連線時，從URL取得應在API呼叫中使用的目的地執行個體ID。

  ![UI影像顯示如何從URL取得目的地執行個體識別碼。](../../assets/testing-api/get-destination-instance-id.png)

## 產生用於目的地測試的範例設定檔 {#generate-sample-profiles}

您可以透過以您要測試之目的地的目的地執行個體識別碼向`/sample-profiles`端點發出GET要求，根據來源結構描述產生範例設定檔。

**API格式**

```http
GET /authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}&count={NUMBER_OF_GENERATED_PROFILES}
```

| 查詢參數 | 說明 |
| -------- | ----------- |
| `destinationInstanceId` | 您要產生範例設定檔之目的地執行個體的ID。 如需如何取得此ID的詳細資訊，請參閱[必要條件](#prerequisites)一節。 |
| `count` | *選擇性*。 您要產生的範例設定檔數目。 引數可以取用`1 - 1000`之間的值。 如果此屬性未定義，則API會產生單一範例設定檔。 |

**要求**

下列要求會根據目的地執行個體中定義的來源結構描述（具有對應的`destinationInstanceId`），產生範例設定檔。

```shell
curl -X GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}' \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

成功的回應會傳回HTTP狀態200，其中包含指定數量的範例設定檔，以及與來源XDM結構描述對應的對象成員資格、身分和設定檔屬性。

>[!NOTE]
>
> 回應只會傳回目標例項中使用的對象成員資格、身分和設定檔屬性。 即使您的來源結構描述有其他欄位，這些欄位仍會被忽略。

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

![顯示從UI對應到API回應之欄位的影像。](../../assets/testing-api/batch-destinations/sample-api-response-mapping.png)

| 屬性 | 說明 |
| -------- | ----------- |
| `segmentMembership` | 說明個人對象會籍的地圖物件。 如需`segmentMembership`的詳細資訊，請閱讀[對象成員資格詳細資料](../../../../xdm/field-groups/profile/segmentation.md)。 |
| `lastQualificationTime` | 此設定檔上次符合區段資格的時間戳記。 |
| `status` | 字串欄位，指出是否已在目前請求中實現對象成員資格。 接受下列值： <ul><li>`realized`：設定檔是區段的一部分。</li><li>`exited`：設定檔正在退出對象，做為目前請求的一部分。</li></ul> |
| `identityMap` | 描述個人各種身分值及其相關名稱空間的對應型別欄位。 如需`identityMap`的詳細資訊，請參閱[結構描述組合基礎](../../../../xdm/schema/composition.md#identityMap)。 |

{style="table-layout:auto"}

## API錯誤處理 {#api-error-handling}

Destination SDK API端點遵循一般Experience Platform API錯誤訊息原則。 請參閱Platform疑難排解指南中的[API狀態碼](../../../../landing/troubleshooting.md#api-status-codes)和[請求標頭錯誤](../../../../landing/troubleshooting.md#request-header-errors)。

## 後續步驟

閱讀本檔案後，您現在知道如何根據您在目的地[啟動流程](../../../ui/activate-batch-profile-destinations.md)中設定的來源結構描述產生範例設定檔。

您現在可以自訂這些設定檔，或在API傳回時加以使用，以[測試您的檔案型目的地組態](file-based-destination-testing-api.md)。
