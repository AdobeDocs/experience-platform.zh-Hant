---
keywords: Azure事件中心目標；Azure事件中心；Azure eventhub
title: （測試版） [!DNL Azure Event Hubs] 連接
description: 建立與 [!DNL Azure Event Hubs] 儲存以從Experience Platform串流資料。
exl-id: f98a389a-bce3-4a80-9452-6c7293d01de3
source-git-commit: 0a45cb49f3eb2bbd6ac1b39962df88b2352eb121
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 1%

---

# （測試版） [!DNL Azure Event Hubs] 連接

## 總覽 {#overview}

>[!IMPORTANT]
>
>此 [!DNL Azure Event Hubs] Platform中的目的地目前為測試版。 文件和功能可能會有所變更。

[!DNL Azure Event Hubs] 是大資料串流平台和事件擷取服務。 它每秒可接收並處理數百萬個事件。 透過任何即時分析提供者或批次處理程式/儲存轉接器，即可轉換及儲存傳送至事件中樞的資料。

您可以建立與 [!DNL Azure Event Hubs] 儲存以從Adobe Experience Platform串流資料。

* 如需 [!DNL Azure Event Hubs]，請參閱 [Microsoft檔案](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about).
* 連線至 [!DNL Azure Event Hubs] 以程式設計方式，請參閱 [串流目的地API教學課程](../../api/streaming-destinations.md).
* 連線至 [!DNL Azure Event Hubs] 使用Platform使用者介面，請參閱以下各節。

![AWS Kinesis在UI中](../../assets/catalog/cloud-storage/event-hubs/catalog.png)

## 使用案例 {#use-cases}

使用串流目的地，例如 [!DNL Azure Event Hubs]，您可以輕鬆將高價值細分事件和相關設定檔屬性饋送至您所選擇的系統。

例如，潛在客戶下載了白皮書，將其歸類為「高傾向轉換」區段。 通過映射潛在客戶所在的段 [!DNL Azure Event Hubs] 目的地，您會在 [!DNL Azure Event Hubs]. 在那裡，您可以採用自己動手做的方法，在活動之上描述業務邏輯，因為您認為最適合您的企業IT系統。

## 匯出類型 {#export-type}

**設定檔**  — 您要匯出區段的所有成員，以及所需的架構欄位(例如：電子郵件地址、電話號碼、姓氏)，如「選取屬性」畫面中所選 [對象啟用工作流程](../../ui/activate-streaming-profile-destinations.md#select-attributes).

## 連接到目標 {#connect}

若要連線至此目的地，請依照 [目的地設定教學課程](../../ui/connect-destination.md).

### 連線參數 {#parameters}

同時 [設定](../../ui/connect-destination.md) 此目的地時，您必須提供下列資訊：

* **[!UICONTROL SAS密鑰名]** 和 **[!UICONTROL SAS密鑰]**:填寫SAS密鑰名和密鑰。 了解驗證 [!DNL Azure Event Hubs] 在 [Microsoft檔案](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* **[!UICONTROL 命名空間]**:填入 [!DNL Azure Event Hubs] 命名空間。 了解 [!DNL Azure Event Hubs] 中的命名空間 [Microsoft檔案](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace).
* **[!UICONTROL 名稱]**:填入連線的名稱 [!DNL Azure Event Hubs].
* **[!UICONTROL 說明]**:提供連線的說明。  範例：「高級顧客」、「男性對玩風箏衝浪感興趣」。
* **[!UICONTROL eventHubName]**:提供資料流的名稱給您的 [!DNL Azure Event Hubs] 目的地。

## 啟用此目的地的區段 {#activate}

請參閱 [對串流設定檔匯出目的地啟用受眾資料](../../ui/activate-streaming-profile-destinations.md) 以取得啟用受眾區段至此目的地的指示。

## 設定檔匯出行為 {#profile-export-behavior}

Experience Platform會最佳化設定檔匯出行為至您的Azure事件中樞目的地，以僅在區段資格或其他重要事件後發生設定檔的相關更新時，將資料匯出至您的目的地。 設定檔會在下列情況下匯出至您的目的地：

* 至少有一個區段對應至目的地，區段成員資格有所變更，便觸發設定檔更新。 例如，設定檔已符合對應至目的地的其中一個區段資格，或已退出對應至目的地的其中一個區段。
* 設定檔更新是由 [身分圖](/help/xdm/field-groups/profile/identitymap.md). 例如，已符合其中一個對應至目的地區段資格的設定檔，已在「身分對應」屬性中新增身分識別。
* 設定檔更新是由至少一個已對應至目的地之屬性的屬性變更所觸發。 例如，對應步驟中對應至目的地的其中一個屬性會新增至設定檔。

在上述所有情況中，只有發生相關更新的設定檔會匯出至您的目的地。 例如，如果對應至目的地流程的區段有100個成員，且有5個新設定檔符合該區段的資格，則匯出至目的地的作業會是增量的，且僅包含5個新設定檔。

請注意，無論變更在何處，所有對應屬性都會針對設定檔匯出。 因此，在上述範例中，即使屬性本身未變更，這五個新設定檔的所有對應屬性也會匯出。

## 匯出的資料 {#exported-data}

已導出 [!DNL Experience Platform] 資料登陸 [!DNL Azure Event Hubs] 格式。 例如，下列匯出包含符合特定區段資格且已退出另一個區段的設定檔，並包含設定檔屬性名、姓氏、出生日期和個人電子郵件地址。 此設定檔的身分為ECID和電子郵件。

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
>* [AWSKinesis目的地](./amazon-kinesis.md)
>* [目的地類型和類別](../../destination-types.md)

