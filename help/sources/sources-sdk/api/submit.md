---
keywords: Experience Platform；首頁；熱門主題；來源；聯結器；來源聯結器；來源sdk；sdk；SDK
title: 提交您的Source
description: 以下檔案提供如何使用「流量服務API」測試及驗證新來源，以及透過「自助來源」(批次SDK)整合新來源的步驟。
exl-id: 9e945ba1-51b6-40a9-b92f-e0a52b3f92fa
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 0%

---

# 提交您的來源

使用自助式來源(批次SDK)將新來源整合到Adobe Experience Platform的最後一步是測試來源以進行驗證。 一旦成功，您就可以連絡您的Adobe代表來提交新的來源。

以下檔案提供如何使用[[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)測試及偵錯來源的步驟。

## 快速入門

* 如需如何成功呼叫Experience Platform API的詳細資訊，請參閱[Experience Platform API快速入門](../../../landing/api-guide.md)指南。
* 如需如何產生Experience Platform API認證的詳細資訊，請參閱[驗證及存取Experience Platform API](../../../landing/api-authentication.md)教學課程。
* 如需如何為Experience Platform API設定[!DNL Postman]的詳細資訊，請參閱[設定開發人員主控台和 [!DNL Postman]](../../../landing/postman.md)上的教學課程。
* 若要協助您的測試和偵錯程式，請在此下載[自助來源驗證集合和環境](../assets/sdk-verification.zip)，並遵循下列步驟。

## 測試您的來源

若要測試您的來源，您必須在[!DNL Postman]上執行[自助來源驗證集合和環境](../assets/sdk-verification.zip)，同時提供與您的來源相關的適當環境變數。

若要開始測試，您必須先在[!DNL Postman]上設定集合和環境。 接著，指定您要測試的連線規格ID。

### 指定`authSpecName`

輸入連線規格ID後，您必須指定用於基礎連線的`authSpecName`。 根據您的選擇，這可能是`OAuth 2 Refresh Code`或`Basic Authentication`。 指定`authSpecName`後，您必須在環境中加入其必要的認證。 例如，若您指定`authSpecName`為`OAuth 2 Refresh Code`，則必須提供OAuth 2的必要認證，即`host`和`accessToken`。

### 指定`sourceSpec`

在新增驗證規格引數後，您必須接著從來源規格中新增必要屬性。 您可以在`sourceSpec.spec.properties`中找到必要的屬性。 在以下[!DNL MailChimp Members]範例中，唯一需要的屬性是`listId`，這表示`listId`且其對應至您[!DNL Postman]環境的ID值。

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

提供驗證和來源規格引數後，您就可以開始填入其餘的環境變數，請參閱下表以供參考：

>[!NOTE]
>
>以下所有範例變數都是您必須更新的預留位置值，`flowSpecificationId`和`targetConnectionSpecId`除外，它們是固定值。

| 參數 | 說明 | 範例 |
| --- | --- | --- |
| `x-api-key` | 用於驗證Experience Platform API呼叫的唯一識別碼。 如需如何擷取`x-api-key`的詳細資訊，請參閱有關[驗證及存取Experience Platform API](../../../landing/api-authentication.md)的教學課程。 | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `x-gw-ims-org-id` | 企業實體，可以擁有或授權產品及服務並允許存取其成員。 如需如何擷取`x-gw-ims-org-id`資訊的說明，請參閱[設定開發人員主控台和 [!DNL Postman]](../../../landing/postman.md)的教學課程。 | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `authorizationToken` | 完成對Experience Platform API的呼叫所需的授權權杖。 如需如何擷取`authorizationToken`的詳細資訊，請參閱有關[驗證及存取Experience Platform API](../../../landing/api-authentication.md)的教學課程。 | `Bearer authorizationToken` |
| `schemaId` | 為了在Experience Platform中使用來源資料，必須建立目標結構描述，以根據您的需求建構來源資料。 如需有關如何建立目標XDM結構描述的詳細步驟，請參閱有關使用API [建立結構描述的教學課程](../../../xdm/api/schemas.md)。 | `https://ns.adobe.com/{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `schemaVersion` | 與您的結構描述對應的唯一版本。 | `application/vnd.adobe.xed-full-notext+json; version=1` |
| `schemaAltId` | 建立新結構描述時與`schemaId`一併傳回的`meta:altId`。 | `_{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `dataSetId` | 如需有關如何建立目標資料集的詳細步驟，請參閱有關[使用API建立資料集](../../../catalog/api/create-dataset.md)的教學課程。 | `5f3c3cedb2805c194ff0b69a` |
| `mappings` | 對應集可用來定義來源結構描述中的資料如何對應到目的地結構描述的資料。 如需有關如何建立對應的詳細步驟，請參閱有關[使用API建立對應集的教學課程](../../../data-prep/api/mapping-set.md)。 | `[{"destinationXdmPath":"person.name.firstName","sourceAttribute":"email.email_id","identity":false,"version":0},{"destinationXdmPath":"person.name.lastName","sourceAttribute":"email.activity.action","identity":false,"version":0}]` |
| `mappingId` | 與對應集對應的唯一ID。 | `bf5286a9c1ad4266baca76ba3adc9366` |
| `connectionSpecId` | 與您的來源對應的連線規格ID。 這是您在[建立新連線規格](./create.md)後產生的ID。 | `2e8580db-6489-4726-96de-e33f5f60295f` |
| `flowSpecificationId` | `RestStorageToAEP`的流程規格識別碼。 **這是固定值**。 | `6499120c-0b15-42dc-936e-847ea3c24d72` |
| `targetConnectionSpecId` | 擷取的資料著陸所在資料湖的目標連線ID。 **這是固定值**。 | `c604ff05-7f1a-43c0-8e18-33bf874cb11c` |
| `verifyWatTimeInSecond` | 檢查流程執行的完成時要遵循的指定時間間隔。 | `40` |
| `startTime` | 為資料流指定的開始時間。 開始時間的格式必須是unix時間。 | `1597784298` |

提供所有環境變數後，您就可以使用[!DNL Postman]介面開始執行集合。 在[!DNL Postman]介面中，選取[!DNL Sources SSSs Verification Collection]旁的省略符號(**...**)，然後選取&#x200B;**執行集合**。

![執行者](../assets/runner.png)

[!DNL Runner]介面會出現，可讓您設定資料流的執行順序。 選取&#x200B;**執行SSS驗證集合**&#x200B;以執行集合。

>[!NOTE]
>
>如果您偏好使用Experience Platform UI中的來源監視儀表板，可以停用執行訂單檢查清單中的&#x200B;**刪除流程**。 不過，一旦完成測試，您必須確保已刪除測試流程。

![run-collection](../assets/run-collection.png)

## 提交您的來源

當您的來源能夠完成整個工作流程後，您可以繼續聯絡您的Adobe代表並提交來源以進行整合。
