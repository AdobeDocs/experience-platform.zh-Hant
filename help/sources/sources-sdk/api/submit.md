---
keywords: Experience Platform；首頁；熱門主題；來源；連接器；來源連接器；來源sdk;sdk; SDK
title: 提交您的源
description: 以下檔案提供如何使用流量服務API測試和驗證新來源，以及透過自助來源(Batch SDK)整合新來源的步驟。
exl-id: 9e945ba1-51b6-40a9-b92f-e0a52b3f92fa
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 0%

---

# 提交您的來源

使用自助來源（批次SDK）將新來源整合至Adobe Experience Platform的最後一步，就是測試您的來源以進行驗證。 成功後，您就可以聯絡Adobe代表，提交新來源。

以下檔案提供如何使用 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 快速入門

* 如需如何成功呼叫Platform API的詳細資訊，請參閱 [Platform API快速入門](../../../landing/api-guide.md).
* 如需如何產生Platform API認證的詳細資訊，請參閱 [驗證和存取Experience PlatformAPI](../../../landing/api-authentication.md).
* 有關如何設定的資訊 [!DNL Postman] 若為Platform API，請參閱以下的教學課程： [設定開發人員主控台和 [!DNL Postman]](../../../landing/postman.md).
* 若要協助您進行測試和偵錯程式，請下載 [此處的自助源驗證收集和環境](../assets/sdk-verification.zip) 並遵循下列步驟。

## 測試源

要測試源，必須運行 [自助源驗證收集和環境](../assets/sdk-verification.zip) on [!DNL Postman] 同時提供與源相關的適當環境變數。

若要開始測試，您必須先在上設定集合和環境 [!DNL Postman]. 接下來，指定要測試的連接規範ID。

### 指定 `authSpecName`

輸入連接規範ID後，必須指定 `authSpecName` 用於基礎連接。 視您的選擇而定，這可以是 `OAuth 2 Refresh Code` 或  `Basic Authentication`. 指定 `authSpecName`，則您必須在您的環境中包含其必要憑證。 例如，如果您指定 `authSpecName` as `OAuth 2 Refresh Code`，則您必須提供OAuth 2的必要憑證， `host` 和 `accessToken`.

### 指定 `sourceSpec`

添加身份驗證規範參數後，您必須從源規範中添加所需屬性。 您可以在 `sourceSpec.spec.properties`. 若 [!DNL MailChimp Members] 以下範例中，唯一需要的屬性為 `listId`，表示 `listId` 而且它是與 [!DNL Postman] 環境。

```json
"spec": {
  "$schema": "http://json-schema.org/draft-07/schema#",
  "type": "object",
  "description": "Define user input parameters to fetch resource values.",
  "properties": {
    "listId": {
      "type": "string",
      "description": "listId for which members need to fetch."
    }
  }
}
```

提供驗證和源規範參數後，您可以開始填入其餘的環境變數，請參閱下表以供參考：

>[!NOTE]
>
>下列所有範例變數都是您必須更新的預留位置值，但 `flowSpecificationId` 和 `targetConnectionSpecId`，即固定值。

| 參數 | 說明 | 範例 |
| --- | --- | --- |
| `x-api-key` | 用來驗證對Experience PlatformAPI呼叫的唯一識別碼。 請參閱 [驗證和存取Experience PlatformAPI](../../../landing/api-authentication.md) 以了解如何擷取 `x-api-key`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `x-gw-ims-org-id` | 擁有或許可產品和服務並允許訪問其成員的公司實體。 請參閱 [設定開發人員主控台和 [!DNL Postman]](../../../landing/postman.md) 有關如何檢索 `x-gw-ims-org-id` 資訊。 | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `authorizationToken` | 完成對Experience PlatformAPI的呼叫所需的授權Token。 請參閱 [驗證和存取Experience PlatformAPI](../../../landing/api-authentication.md) 以了解如何擷取 `authorizationToken`. | `Bearer authorizationToken` |
| `schemaId` | 為了在Platform中使用來源資料，必須建立目標架構，以根據您的需求來建構來源資料。 如需建立Target XDM結構的詳細步驟，請參閱 [使用API建立結構](../../../xdm/api/schemas.md). | `https://ns.adobe.com/{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `schemaVersion` | 與您的架構對應的唯一版本。 | `application/vnd.adobe.xed-full-notext+json; version=1` |
| `schemaAltId` | 此 `meta:altId` 與  `schemaId` 建立新結構時。 | `_{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `dataSetId` | 如需如何建立目標資料集的詳細步驟，請參閱 [使用API建立資料集](../../../catalog/api/create-dataset.md). | `5f3c3cedb2805c194ff0b69a` |
| `mappings` | 映射集可用於定義源架構中的資料如何映射到目標架構的資料。 如需如何建立對應的詳細步驟，請參閱 [使用API建立對應集](../../../data-prep/api/mapping-set.md). | `[{"destinationXdmPath":"person.name.firstName","sourceAttribute":"email.email_id","identity":false,"version":0},{"destinationXdmPath":"person.name.lastName","sourceAttribute":"email.activity.action","identity":false,"version":0}]` |
| `mappingId` | 與您的對應集對應的唯一ID。 | `bf5286a9c1ad4266baca76ba3adc9366` |
| `connectionSpecId` | 與源對應的連接規範ID。 這是您在 [建立新的連接規範](./create.md). | `2e8580db-6489-4726-96de-e33f5f60295f` |
| `flowSpecificationId` | 流規範ID為 `RestStorageToAEP`. **這是固定值**. | `6499120c-0b15-42dc-936e-847ea3c24d72` |
| `targetConnectionSpecId` | 擷取的資料登陸所在資料湖的目標連線ID。 **這是固定值**. | `c604ff05-7f1a-43c0-8e18-33bf874cb11c` |
| `verifyWatTimeInSecond` | 檢查流運行是否完成時要遵循的指定時間間隔。 | `40` |
| `startTime` | 資料流的指定開始時間。 開始時間必須採用unix時間格式。 | `1597784298` |

提供所有環境變數後，您就可以開始使用 [!DNL Postman] 介面。 在 [!DNL Postman] 介面，選取點(**...**)旁邊 [!DNL Sources SSSs Verification Collection] 然後選取 **執行集合**.

![跑道](../assets/runner.png)

此 [!DNL Runner] 介面出現，允許您配置資料流的運行順序。 選擇 **運行SSS驗證集合** 來執行集合。

>[!NOTE]
>
>您可以停用 **刪除流量** 如果您偏好在Platform UI中使用來源監控控制面板，請從執行順序檢查清單中選取。 不過，完成測試後，您必須確定已刪除測試流程。

![執行集合](../assets/run-collection.png)

## 提交您的來源

在您的來源能夠完成整個工作流程後，您可以繼續聯絡Adobe代表並提交來源以進行整合。
