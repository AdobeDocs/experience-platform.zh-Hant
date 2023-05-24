---
keywords: Experience Platform；首頁；熱門主題；源；連接器；源連接器；源sdk;sdk;SDK
title: 提交源
description: 以下文檔提供了如何使用流服務APItest和驗證新源並通過自助源（批處理SDK）整合新源的步驟。
exl-id: 9e945ba1-51b6-40a9-b92f-e0a52b3f92fa
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 0%

---

# 提交源

使用自助源（批處理SDK）將新源整合到Adobe Experience Platform的最後一步是test源進行驗證。 成功後，您可以通過聯繫Adobe代表來提交新來源。

以下文檔提供了有關如何使用test和調試源的步驟 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)。

## 快速入門

* 有關如何成功調用平台API的資訊，請參見上的指南 [平台API入門](../../../landing/api-guide.md)。
* 有關如何為平台API生成憑據的資訊，請參見上的教程 [驗證和訪問Experience PlatformAPI](../../../landing/api-authentication.md)。
* 有關如何設定的資訊 [!DNL Postman] 有關平台API，請參見上的教程 [設定開發人員控制台和 [!DNL Postman]](../../../landing/postman.md)。
* 要幫助測試和調試過程，請下載 [此處的自助源驗證收集和環境](../assets/sdk-verification.zip) 並按照下面介紹的步驟操作。

## Test源

要test源，必須運行 [自助源驗證收集和環境](../assets/sdk-verification.zip) 上 [!DNL Postman] 同時提供與源相關的相應環境變數。

要開始測試，必須先在 [!DNL Postman]。 接下來，指定要test的連接規範ID。

### 指定 `authSpecName`

輸入連接規範ID後，必須指定 `authSpecName` 用於基礎連接。 根據你的選擇，這可能是 `OAuth 2 Refresh Code` 或  `Basic Authentication`。 一旦指定 `authSpecName`，然後必須在您的環境中包括其所需憑據。 例如，如果 `authSpecName` 如 `OAuth 2 Refresh Code`，則必須提供OAuth 2的所需憑據， `host` 和 `accessToken`。

### 指定 `sourceSpec`

添加驗證規範參數後，必須從源規範中添加所需的屬性。 您可以在 `sourceSpec.spec.properties`。 對於 [!DNL MailChimp Members] 示例如下，唯一的必需屬性是 `listId`，表示 `listId` 它與你的 [!DNL Postman] 環境。

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

一旦提供了驗證和源規範參數，您就可以開始填充其餘的環境變數，請參閱下表以獲取參考：

>[!NOTE]
>
>下面的所有示例變數都是必須更新的佔位符值， `flowSpecificationId` 和 `targetConnectionSpecId`，它們是固定值。

| 參數 | 說明 | 範例 |
| --- | --- | --- |
| `x-api-key` | 用於驗證對Experience PlatformAPI的調用的唯一標識符。 請參閱上的教程 [驗證和訪問Experience PlatformAPI](../../../landing/api-authentication.md) 有關如何檢索 `x-api-key`。 | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `x-gw-ims-org-id` | 擁有或許可產品和服務並允許訪問其成員的公司實體。 請參閱上的教程 [設定開發人員控制台和 [!DNL Postman]](../../../landing/postman.md) 有關如何檢索 `x-gw-ims-org-id` 的下界。 | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `authorizationToken` | 完成對Experience PlatformAPI的調用所需的授權令牌。 請參閱上的教程 [驗證和訪問Experience PlatformAPI](../../../landing/api-authentication.md) 有關如何檢索 `authorizationToken`。 | `Bearer authorizationToken` |
| `schemaId` | 為了在平台中使用源資料，必須建立目標架構以根據您的需要來構造源資料。 有關如何建立目標XDM架構的詳細步驟，請參見上的教程 [使用API建立架構](../../../xdm/api/schemas.md)。 | `https://ns.adobe.com/{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `schemaVersion` | 與架構對應的唯一版本。 | `application/vnd.adobe.xed-full-notext+json; version=1` |
| `schemaAltId` | 的 `meta:altId` 在它旁邊  `schemaId` 建立新架構時。 | `_{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `dataSetId` | 有關如何建立目標資料集的詳細步驟，請參見上的教程 [使用API建立資料集](../../../catalog/api/create-dataset.md)。 | `5f3c3cedb2805c194ff0b69a` |
| `mappings` | 映射集可用於定義源模式中的資料如何映射到目標模式的資料。 有關如何建立映射的詳細步驟，請參見上的教程 [使用API建立映射集](../../../data-prep/api/mapping-set.md)。 | `[{"destinationXdmPath":"person.name.firstName","sourceAttribute":"email.email_id","identity":false,"version":0},{"destinationXdmPath":"person.name.lastName","sourceAttribute":"email.activity.action","identity":false,"version":0}]` |
| `mappingId` | 與映射集對應的唯一ID。 | `bf5286a9c1ad4266baca76ba3adc9366` |
| `connectionSpecId` | 與源對應的連接規範ID。 這是您在 [建立新連接規範](./create.md)。 | `2e8580db-6489-4726-96de-e33f5f60295f` |
| `flowSpecificationId` | 流規範ID `RestStorageToAEP`。 **這是一個固定值**。 | `6499120c-0b15-42dc-936e-847ea3c24d72` |
| `targetConnectionSpecId` | 所接收資料到達的資料湖的目標連接ID。 **這是一個固定值**。 | `c604ff05-7f1a-43c0-8e18-33bf874cb11c` |
| `verifyWatTimeInSecond` | 檢查流運行是否完成時要遵循的指定時間間隔。 | `40` |
| `startTime` | 資料流的指定開始時間。 開始時間必須在unix時間中格式化。 | `1597784298` |

提供所有環境變數後，可以使用 [!DNL Postman] 。 在 [!DNL Postman] 介面，選取橢圓(**...**) [!DNL Sources SSSs Verification Collection] ，然後選擇 **運行集合**。

![跑](../assets/runner.png)

的 [!DNL Runner] 介面，允許您配置資料流的運行順序。 選擇 **運行SSS驗證收集** 以運行集合。

>[!NOTE]
>
>可以禁用 **刪除流** 從運行訂單核對清單中，如果您希望使用平台UI中的源監視面板。 但是，完成測試後，必須確保刪除test流。

![運行集合](../assets/run-collection.png)

## 提交源

在您的來源能夠完成整個工作流後，您可以繼續與Adobe代表聯繫，並提交您的來源以進行整合。
