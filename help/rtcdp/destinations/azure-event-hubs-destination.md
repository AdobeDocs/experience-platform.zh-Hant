---
title: Azure事件集線器目標
seo-title: Azure事件集線器目標
description: 建立Azure事件中樞儲存空間的即時出站連線，以從Experience Platform串流資料。
seo-description: 建立Azure事件中樞儲存空間的即時出站連線，以從Experience Platform串流資料。
translation-type: tm+mt
source-git-commit: a18f89531cf024f61b054b47a660bd26766bebf6
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 0%

---


# Azure事件集線器目標

## 概述 {#overview}

[!DNL Azure Event Hubs] 是大型資料串流平台和事件擷取服務。 它每秒可接收和處理數百萬個事件。 可使用任何即時分析提供者或批次處理／儲存適配器來轉換和儲存傳送至事件中樞的資料。

您可以建立儲存的即時出站連線， [!DNL Azure Event Hubs] 以從Adobe Experience Platform串流資料。

* 如需詳細資訊 [!DNL Azure Event Hubs]，請參閱 [Microsoft檔案](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about)。
* 若要連線至使 [!DNL Azure Event Hubs] 用API呼叫，請參閱串 [流目標API教學課程]。
* 若要使用 [!DNL Azure Event Hubs] Adobe即時CDP使用者介面連線，請參閱以下各節。

![UI中的AWS Kinesis](/help/rtcdp/destinations/assets/azure-event-hubs-destination.png)

## 使用案例 {#use-cases}

透過使用串流目的地（例如Azure事件中樞），您可以輕鬆地將高價值區段事件和相關的描述檔屬性饋送到您選擇的系統中。

例如，潛在客戶下載了白皮書，使其符合「高轉換傾向」區段的資格。 通過將潛在客戶所屬的段映射到Azure事件集線器目標，您將在Azure事件集線器中接收此事件。 在這裡，您可以採用自行動手的方法，並在活動之上描述業務邏輯，因為您認為最適合企業IT系統。

## 連接目標 {#connect-destination}

如需如 [何連線至您的雲端儲 ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)存目的地的指示，請參閱雲端儲存目的地工作流程，包括 [!DNL Azure Event Hubs]:

對於目 [!DNL Azure Event Hubs] 標，請在建立目標工作流中輸入以下資訊：

### 在帳戶步驟中 {#account-step}

* **[!UICONTROL SAS密鑰名]** 和 **[!UICONTROL SAS密鑰]**: 填寫您的SAS密鑰名稱和密鑰。 瞭解 [!DNL Azure Event Hubs] Microsoft文檔中 [如何使用SAS密鑰驗證](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)。
* **[!UICONTROL 命名空間]**: 填寫您的命名 [!DNL Azure Event Hubs] 空間。 在 [!DNL Azure Event Hubs] Microsoft [檔案中瞭解命名](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace)空間。

![驗證步驟中需要的輸入](/help/rtcdp/destinations/assets/event-hubs-account-step.png)

### 在驗證步驟中 {#authentication-step}

* **[!UICONTROL 名稱]**: 填寫連接的名稱 [!DNL Azure Event Hubs]。
* **[!UICONTROL 說明]**: 提供連接的說明。  範例： 「Premium tier customers」、「Males intered to kitesurfing」。
* **[!UICONTROL eventHubName]**: 提供串流至您目的地的名 [!DNL Azure Event Hubs] 稱。

![設定步驟中所需的資料](/help/rtcdp/destinations/assets/event-hubs-authentication-step.png)

## 啟用區段 {#activate-segments}

如需 [區段啟動工作流程的相關資訊](/help/rtcdp/destinations/activate-destinations.md) ，請參閱啟用設定檔和區段至目的地。


## 匯出的資料 {#exported-data}

您匯出的Experience Platform資料會以JSON [!DNL Azure Event Hubs] 格式登入。 例如，包含退出特定區段之對象之雜湊電子郵件身分的事件串流可能如下所示：

```
{
   "segmentMembership":{
      "ups":{
         "7841ba61-23c1-4bb3-a495-00d695fe1e93":{
            "lastQualificationTime":"2020-03-03T21:24:39Z",
            "status":"exited"
         }
      }
   }
},
"identityMap":{
   "email_lc_sha256":[
      {
         "id":"655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
         "id":"66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
   ]
},
```



>[!MORELIKETHIS]
>
>* 連結至Azure事件中樞API教學課程
>* [AWS Kinesis目標](/help/rtcdp/destinations/amazon-kinesis-destination.md)
>* [目標類型和類別](/help/rtcdp/destinations/destination-types.md)