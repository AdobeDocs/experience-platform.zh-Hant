---
title: （測試版）Azure事件集線器目標
seo-title: （測試版）Azure事件集線器目標
description: 建立Azure事件中樞儲存空間的即時出站連線，以從Experience Platform串流資料。
seo-description: 建立Azure事件中樞儲存空間的即時出站連線，以從Experience Platform串流資料。
translation-type: tm+mt
source-git-commit: e93bfc028d5e23c3add55677c4003ca549a902c6
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 2%

---


# （測試版）Azure事件集線器目標

>[!IMPORTANT]
>
>Adobe [!DNL Azure Event Hubs] 即時CDP的目的地目前為beta版。 文件和功能可能會有所變更。

## 概述 {#overview}

[!DNL Azure Event Hubs] 是大型資料串流平台和事件擷取服務。 它每秒可接收和處理數百萬個事件。 可使用任何即時分析提供者或批次處理／儲存適配器來轉換和儲存傳送至事件中樞的資料。

您可以建立儲存的即時出站連線， [!DNL Azure Event Hubs] 以從Adobe Experience Platform串流資料。

* 如需詳細資訊 [!DNL Azure Event Hubs]，請參閱 [Microsoft檔案](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about)。
* 若要連線至使 [!DNL Azure Event Hubs] 用API呼叫，請參閱串 [流目標API教學課程](/help/rtcdp/destinations/streaming-destinations-api-tutorial.md)。
* 若要使用 [!DNL Azure Event Hubs] Adobe即時CDP使用者介面連線，請參閱以下各節。

![UI中的AWS Kinesis](/help/rtcdp/destinations/assets/azure-event-hubs-destination.png)

## 使用案例 {#use-cases}

透過使用串流目的地（例如Azure事件中樞），您可以輕鬆地將高價值區段事件和相關的描述檔屬性饋送到您選擇的系統中。

例如，潛在客戶下載了白皮書，使其符合「高轉換傾向」區段的資格。 通過將潛在客戶所屬的段映射到Azure事件集線器目標，您將在Azure事件集線器中接收此事件。 在這裡，您可以採用自行動手的方法，並在活動之上描述業務邏輯，因為您認為最適合企業IT系統。

## 連接目標 {#connect-destination}

如需如 [何連線至您的雲端儲 ](/help/rtcdp/destinations/cloud-storage-destinations-workflow.md)存目的地的指示，請參閱雲端儲存目的地工作流程，包括 [!DNL Azure Event Hubs]:

對於目 [!DNL Azure Event Hubs] 標，請在建立目標工作流中輸入以下資訊：

### 在驗證步驟中 {#authentication-step}

* **[!UICONTROL SAS密鑰名]** 和 **[!UICONTROL SAS密鑰]**: 填寫您的SAS密鑰名稱和密鑰。 瞭解 [!DNL Azure Event Hubs] Microsoft文檔中 [如何使用SAS密鑰驗證](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)。
* **[!UICONTROL 命名空間]**: 填寫您的命名 [!DNL Azure Event Hubs] 空間。 在 [!DNL Azure Event Hubs] Microsoft [檔案中瞭解命名](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace)空間。

![驗證步驟中需要的輸入](/help/rtcdp/destinations/assets/event-hubs-authentication.png)

### 在設定步驟中 {#setup-step}

* **[!UICONTROL 名稱]**: 填寫連接的名稱 [!DNL Azure Event Hubs]。
* **[!UICONTROL 說明]**: 提供連接的說明。  範例： 「Premium tier customers」、「Males intered to kitesurfing」。
* **[!UICONTROL eventHubName]**: 提供串流至您目的地的名 [!DNL Azure Event Hubs] 稱。

![設定步驟中所需的資料](/help/rtcdp/destinations/assets/event-hubs-setup-step.png)

## 啟用區段 {#activate-segments}

如需 [區段啟動工作流程的相關資訊](/help/rtcdp/destinations/activate-destinations.md) ，請參閱啟用設定檔和區段至目的地。


## 匯出的資料 {#exported-data}

您匯出的Experience Platform資料會以JSON [!DNL Azure Event Hubs] 格式登入。 例如，以下事件包含符合特定區段資格並退出其他區段之對象的電子郵件地址設定檔屬性。 此潛在客戶的身分是ECID和電子郵件。

```
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
>* [連線至Azure事件中樞，並使用API呼叫啟用資料](/help/rtcdp/destinations/streaming-destinations-api-tutorial.md)
>* [AWS Kinesis目標](/help/rtcdp/destinations/amazon-kinesis-destination.md)
>* [目標類型和類別](/help/rtcdp/destinations/destination-types.md)