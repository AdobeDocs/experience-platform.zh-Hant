---
keywords: Azure事件中心目標；Azure事件中心；Azure eventhub
title: （測試版）!DNL Azure Event Hubs]連接
description: 建立到！DNL Azure Event Hubs]儲存的即時出站連接，以便從Experience Platform流資料。
exl-id: f98a389a-bce3-4a80-9452-6c7293d01de3
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 2%

---

# (Beta)[!DNL Azure Event Hubs]連接

## 概覽 {#overview}

>[!IMPORTANT]
>
>Platform中的[!DNL Azure Event Hubs]目標目前為測試版。 文件和功能可能會有所變更。

[!DNL Azure Event Hubs] 是大資料串流平台和事件擷取服務。它每秒可接收並處理數百萬個事件。 透過任何即時分析提供者或批次處理程式/儲存轉接器，即可轉換及儲存傳送至事件中樞的資料。

您可以建立與[!DNL Azure Event Hubs]儲存的即時傳出連線，以便串流來自Adobe Experience Platform的資料。

* 有關[!DNL Azure Event Hubs]的詳細資訊，請參閱[Microsoft文檔](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about)。
* 若要以程式設計方式連線至[!DNL Azure Event Hubs]，請參閱[串流目的地API教學課程](../../api/streaming-destinations.md)。
* 若要使用Platform使用者介面連線至[!DNL Azure Event Hubs]，請參閱以下各節。

![UI中的AWS Kinesis](../../assets/catalog/cloud-storage/event-hubs/catalog.png)

## 使用案例 {#use-cases}

透過使用[!DNL Azure Event Hubs]等串流目的地，您可以輕鬆將高價值分段事件和相關設定檔屬性饋送至您所選擇的系統。

例如，潛在客戶下載了白皮書，將其歸類為「高傾向轉換」區段。 將潛在客戶所屬的區段對應至[!DNL Azure Event Hubs]目的地後，您會在[!DNL Azure Event Hubs]中收到此事件。 在那裡，您可以採用自己動手做的方法，在活動之上描述業務邏輯，因為您認為最適合您的企業IT系統。

## 匯出類型 {#export-type}

**以設定檔為基礎**  — 您要匯出區段的所有成員，以及所需的結構欄位(例如：電子郵件地址、電話號碼、姓氏)，從對象啟用工作流程的「選取屬性」畫面 [中選取](../../ui/activate-streaming-profile-destinations.md#select-attributes)。

## 連接到目標 {#connect}

要連接到此目標，請按照[目標配置教程](../../ui/connect-destination.md)中所述的步驟操作。

### 連線參數 {#parameters}

在[設定](../../ui/connect-destination.md)此目標時，您必須提供下列資訊：

* **[!UICONTROL SAS密鑰]** 名和 **[!UICONTROL SAS密鑰]**:填寫SAS密鑰名和密鑰。了解[Microsoft文檔](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)中的SAS密鑰驗證[!DNL Azure Event Hubs]。
* **[!UICONTROL 命名空間]**:填入您的命名 [!DNL Azure Event Hubs] 空間。了解[Microsoft文檔](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace)中的[!DNL Azure Event Hubs]命名空間。
* **[!UICONTROL 名稱]**:填寫連線的名 [!DNL Azure Event Hubs]稱。
* **[!UICONTROL 說明]**:提供連線的說明。範例：「高級顧客」、「男性對玩風箏衝浪感興趣」。
* **[!UICONTROL eventHubName]**:提供目的地資料流的名 [!DNL Azure Event Hubs] 稱。

## 啟用此目的地的區段 {#activate}

請參閱[將受眾資料啟用至串流設定檔匯出目的地](../../ui/activate-streaming-profile-destinations.md) ，以取得關於將受眾區段啟用至此目的地的指示。

## 匯出的資料 {#exported-data}

您匯出的[!DNL Experience Platform]資料會以JSON格式連結至[!DNL Azure Event Hubs]。 例如，以下事件包含已符合特定區段資格並退出其他區段之對象的電子郵件地址設定檔屬性。 此潛在客戶的身分識別為ECID和電子郵件。

```json
{
  "person": {
    "email": "yourstruly@adobe.con"
  },
  "segmentMembership": {
    "ups": {
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93": {
        "lastQualificationTime": "2020-05-25T21:24:39Z",
        "status": "exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae": {
        "lastQualificationTime": "2020-05-25T23:37:33Z",
        "status": "existing"
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
>* [連接到Azure事件集線器，並使用流服務API激活資料](../../api/streaming-destinations.md)
* [AWS Kinesis目的地](./amazon-kinesis.md)
* [目的地類型和類別](../../destination-types.md)

