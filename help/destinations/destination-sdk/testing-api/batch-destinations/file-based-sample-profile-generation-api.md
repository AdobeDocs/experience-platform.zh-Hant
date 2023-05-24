---
description: 本頁說明如何使用Destination SDK中的/sample-profiles API終結點來基於源架構生成示例配置檔案。 您可以使用這些示例配置檔案來test基於檔案的目標配置。
title: 基於源架構生成示例配置檔案
exl-id: aea50d2e-e916-4ef0-8864-9333a4eafe80
source-git-commit: adf75720f3e13c066b5c244d6749dd0939865a6f
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 1%

---


# 基於源架構生成示例配置檔案

測試基於檔案的目標的第一步是使用 `/sample-profiles` 終結點，以基於現有源架構生成示例配置檔案。

示例配置檔案可幫助您瞭解配置檔案的JSON結構。 此外，它們還為您提供了一個預設值，您可以使用自己的配置檔案資料進行自定義，以便進行進一步的目標測試。

## 快速入門 {#getting-started}

在繼續之前，請查看 [入門指南](../../getting-started.md) 瞭解成功調用API所需的重要資訊，包括如何獲得所需的目標創作權限和所需的標題。

## 先決條件 {#prerequisites}

在使用 `/sample-profiles` 端點，確保滿足以下條件：

* 您通過Destination SDK建立了一個現有的基於檔案的目標，您可以在 [目標目錄](../../../ui/destinations-workspace.md)。
* 您在Experience PlatformUI中至少為目標建立了一個激活流。 的 `/sample-profiles` 終結點根據您在激活流中定義的源架構建立配置檔案。 查看 [激活教程](../../../ui/activate-batch-profile-destinations.md) 瞭解如何建立激活流。
* 要成功發出API請求，您需要與要測試的目標實例對應的目標實例ID。 在平台UI中瀏覽與目標的連接時，從URL獲取在API調用中應使用的目標實例ID。

   ![顯示如何從URL獲取目標實例ID的UI影像。](../../assets/testing-api/get-destination-instance-id.png)

## 生成目標測試的示例配置檔案 {#generate-sample-profiles}

通過向Web站點發出GET請求，可以根據源架構生成示例配置檔案 `/sample-profiles` 包含要test的目標的目標實例ID的終結點。

**API格式**

```http
GET /authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}&count={NUMBER_OF_GENERATED_PROFILES}
```

| 查詢參數 | 說明 |
| -------- | ----------- |
| `destinationInstanceId` | 要為其生成示例配置檔案的目標實例的ID。 查看 [先決條件](#prerequisites) 的子菜單。 |
| `count` | *可選*. 要生成的示例配置檔案數。 參數可以取值 `1 - 1000`。 如果未定義此屬性，則API將生成單個示例配置檔案。 |

**要求**

以下請求基於在目標實例中定義的源模式生成示例配置檔案，其中 `destinationInstanceId`。

```shell
curl -X GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}' \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

成功的響應返回HTTP狀態200，其中包含指定數量的示例配置檔案，以及與源XDM架構對應的段成員資格、標識和配置檔案屬性。

>[!NOTE]
>
> 響應僅返回目標實例中使用的段成員身份、標識和配置檔案屬性。 即使源架構有其他欄位，也會忽略這些欄位。

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

![顯示從UI到API響應欄位的映射的影像。](../../assets/testing-api/batch-destinations/sample-api-response-mapping.png)

| 屬性 | 說明 |
| -------- | ----------- |
| `segmentMembership` | 描述個人段成員身份的映射對象。 有關 `segmentMembership`，閱讀 [段成員身份詳細資訊](../../../../xdm/field-groups/profile/segmentation.md)。 |
| `lastQualificationTime` | 此配置檔案上次限定段的時間的時間戳。 |
| `status` | 一個字串欄位，指示是否已將段成員資格作為當前請求的一部分實現。 接受以下值： <ul><li>`realized`:輪廓是段的一部分。</li><li>`exited`:配置檔案作為當前請求的一部分退出段。</li></ul> |
| `identityMap` | 映射類型欄位，它描述個人的各種標識值及其關聯的命名空間。 有關 `identityMap`，請參閱 [模式組合基礎](../../../../xdm/schema/composition.md#identityMap)。 |

{style="table-layout:auto"}

## API錯誤處理 {#api-error-handling}

Destination SDKAPI端點遵循常規Experience PlatformAPI錯誤消息原則。 請參閱 [API狀態代碼](../../../../landing/troubleshooting.md#api-status-codes) 和 [請求標頭錯誤](../../../../landing/troubleshooting.md#request-header-errors) 中。

## 後續步驟

閱讀此文檔後，您現在知道如何根據在目標中配置的源架構生成示例配置檔案 [激活流](../../../ui/activate-batch-profile-destinations.md)。

您現在可以自定義這些配置檔案，或在API返回時使用它們， [test基於檔案的目標配置](file-based-destination-testing-api.md)。
