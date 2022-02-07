---
keywords: Azure事件中心目標；azure事件中心；azure事件thub
title: (Beta) [!DNL Azure Event Hubs] 連接
description: 建立到您的 [!DNL Azure Event Hubs] 儲存以從Experience Platform流資料。
exl-id: f98a389a-bce3-4a80-9452-6c7293d01de3
source-git-commit: 577b42eef9d4b44b5b556ee31d22276d72c609ea
workflow-type: tm+mt
source-wordcount: '1149'
ht-degree: 1%

---

# (Beta) [!DNL Azure Event Hubs] 連接

## 總覽 {#overview}

>[!IMPORTANT]
>
>的 [!DNL Azure Event Hubs] 平台中的目標當前處於beta中。 文件和功能可能會有所變更。

[!DNL Azure Event Hubs] 是大資料流平台和事件接收服務。 它每秒可以接收和處理數百萬個事件。 通過使用任何即時分析提供程式或批處理/儲存適配器，可以轉換和儲存發送到事件中心的資料。

您可以建立到您的 [!DNL Azure Event Hubs] 儲存以從Adobe Experience Platform傳輸資料。

* 有關 [!DNL Azure Event Hubs]，請參見 [Microsoft文檔](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about)。
* 連接到 [!DNL Azure Event Hubs] 以寫程式方式，請參見 [流目標API教程](../../api/streaming-destinations.md)。
* 連接到 [!DNL Azure Event Hubs] 使用平台用戶介面，請參閱以下各節。

![AWSKinesis在用戶介面](../../assets/catalog/cloud-storage/event-hubs/catalog.png)

## 使用案例 {#use-cases}

使用流目標，如 [!DNL Azure Event Hubs]，您可以輕鬆地將高價值分段事件和關聯的配置檔案屬性輸入到您選擇的系統中。

例如，潛在客戶下載了一份白皮書，確認他們屬於「高傾向轉換」段。 通過映射目標客戶所在的段 [!DNL Azure Event Hubs] 目標，您將在 [!DNL Azure Event Hubs]。 在這裡，您可以採用自行動手的方法，並在活動之前描述業務邏輯，因為您認為最適合您的企業IT系統。

## 導出類型 {#export-type}

**基於配置檔案**  — 導出段的所有成員以及所需的架構欄位(例如：電子郵件地址、電話號碼、姓氏)，從的「選擇屬性」螢幕中選擇 [受眾激活工作流](../../ui/activate-streaming-profile-destinations.md#select-attributes)。

## 連接到目標 {#connect}

要連接到此目標，請按照 [目標配置教程](../../ui/connect-destination.md)。

### 連接參數 {#parameters}

同時 [設定](../../ui/connect-destination.md) 此目標，必須提供以下資訊：

* **[!UICONTROL SAS密鑰名稱]** 和 **[!UICONTROL SAS密鑰]**:填寫SAS密鑰名稱和密鑰。 瞭解身份驗證 [!DNL Azure Event Hubs] 在 [Microsoft文檔](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)。
* **[!UICONTROL 命名空間]**:填寫 [!DNL Azure Event Hubs] 命名空間。 瞭解 [!DNL Azure Event Hubs] 命名空間 [Microsoft文檔](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace)。
* **[!UICONTROL 名稱]**:填寫到的連接的名稱 [!DNL Azure Event Hubs]。
* **[!UICONTROL 說明]**:提供連接的說明。  示例：「高級客戶」、「男性對風箏衝浪感興趣」。
* **[!UICONTROL 事件集線器名稱]**:為流提供名稱 [!DNL Azure Event Hubs] 目標。

## 將段激活到此目標 {#activate}

請參閱 [激活受眾資料以流式處理配置檔案導出目標](../../ui/activate-streaming-profile-destinations.md) 有關激活此目標受眾段的說明。

## 配置檔案導出行為 {#profile-export-behavior}

Experience Platform優化配置檔案導出行為 [!DNL Azure Event Hubs] 目標：僅當在段鑑定或其他重要事件之後對配置檔案進行了相關更新時，才將資料導出到目標。 配置式在以下情況下導出到目標：

* 配置檔案更新由映射到目的地的至少一個段的段成員資格的改變確定。 例如，配置檔案已限定映射到目標的段之一或已退出映射到目標的段之一。
* 配置檔案更新由 [身份映射](/help/xdm/field-groups/profile/identitymap.md)。 例如，已為映射到目標的段之一限定的配置檔案已在標識映射屬性中添加了新標識。
* 配置檔案更新由映射到目的地的至少一個屬性的屬性的改變確定。 例如，映射步驟中映射到目標的屬性之一被添加到配置檔案。

在上述所有情況下，只將發生相關更新的配置檔案導出到目標。 例如，如果映射到目標流的段有100個成員，並且有5個新配置檔案符合該段的條件，則向目標的導出是增量的，並且只包括5個新配置檔案。

請注意，無論更改位於何處，都會為配置檔案導出所有映射的屬性。 因此，在上面的示例中，即使屬性本身沒有更改，也會導出這五個新配置檔案的所有映射屬性。

### 什麼決定資料導出以及導出中包含的內容 {#what-determines-export-what-is-included}

對於為給定配置檔案導出的資料，瞭解以下兩個不同概念非常重要 *決定將資料導出到 [!DNL Azure Event Hubs] 目標* 和 *資料包含在導出中*。

| 決定目標導出的因素 | 目標導出中包含的內容 |
|---------|----------|
| <ul><li>映射的屬性和段用作目標導出的提示。 這意味著，如果任何映射段更改狀態（從null更改為已實現或從已實現/現有更新為退出）或任何映射屬性被更新，則將啟動目標導出。</li><li>由於標識當前無法映射到 [!DNL Azure Event Hubs] 目標，給定配置檔案上任何身份的更改也會決定目標導出。</li><li>屬性的更改定義為屬性上的任何更新，無論其值是否相同。 這意味著，即使值本身未更改，屬性上的覆蓋也被視為更改。</li></ul> | <ul><li>所有段（具有最新成員身份狀態）都包含在 `segmentMembership` 的雙曲餘切值。</li><li>中的所有標識 `identityMap` 也包括對象(Experience Platform當前不支援在 [!DNL Azure Event Hubs] 目標)。</li><li>目標導出中只包含映射的屬性。</li></ul> |

{style=&quot;table-layout:fixed&quot;

例如，將此資料流視為 [!DNL Azure Event Hubs] 目標，其中在資料流中選擇了三個段，並將四個屬性映射到目標。

![AmazonKinesis目標資料流](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

導出到目標的配置檔案可由符合或退出其中一個配置檔案來確定 *三個映射段*。 但是，在資料導出中，在 `segmentMembership` 對象（請參見） [導出的資料](#exported-data) )中，如果特定配置檔案是其成員，則可能會顯示其他未映射的段。 如果配置檔案符合DeLorean Cars分部客戶的資格，但也是受觀看的「回到未來」電影和科幻片迷分部的成員，則另外兩個分部也將出現在 `segmentMembership` 資料導出的對象，即使這些對象未映射到資料流中。

從配置檔案屬性的視點來看，對上述四個屬性的任何更改都將確定目標導出，並且配置檔案上存在的四個映射屬性中的任何一個都將出現在資料導出中。

## 導出的資料 {#exported-data}

已導出 [!DNL Experience Platform] 資料到達 [!DNL Azure Event Hubs] JSON格式的目標。 例如，下面的導出包含符合特定段條件的配置檔案，是另兩個段的成員，並退出另一個段。 導出還包括配置檔案屬性的名字、姓氏、出生日期和個人電子郵件地址。 此配置檔案的標識為ECID和電子郵件。

```json
{
  "person": {
    "birthDate": "YYYY-MM-DD",
    "name": {
      "firstName": "John",
      "lastName": "Doe"
    }
  },
  "personalEmail": {
    "address": "john.doe@acme.com"
  },
  "segmentMembership": {
   "ups":{
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93":{
         "lastQualificationTime":"2022-01-11T21:24:39Z",
         "status":"exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae":{
         "lastQualificationTime":"2022-01-02T23:37:33Z",
         "status":"existing"
      },
      "947c1c46-008d-40b0-92ec-3af86eaf41c1":{
         "lastQualificationTime":"2021-08-25T23:37:33Z",
         "status":"existing"
      },
      "5114d758-ce71-43ba-b53e-e2a91d67b67f":{
         "lastQualificationTime":"2022-01-11T23:37:33Z",
         "status":"realized"
      }
   }
},
  "identityMap": {
    "ecid": [
      {
        "id": "14575006536349286404619648085736425115"
      },
      {
        "id": "66478888669296734530114754794777368480"
      }
    ],
    "email_lc_sha256": [
      {
        "id": "655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
        "id": "66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
    ]
  }
}
```


>[!MORELIKETHIS]
>
>* [連接到Azure事件中心並使用流服務API激活資料](../../api/streaming-destinations.md)
>* [AWSKinesis目的地](./amazon-kinesis.md)
>* [目標類型和類別](../../destination-types.md)

