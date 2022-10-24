---
keywords: Azure事件中心目標；Azure事件中心；Azure eventhub
title: Azure事件集線器連接
description: 建立與 [!DNL Azure Event Hubs] 儲存以從Experience Platform串流資料。
exl-id: f98a389a-bce3-4a80-9452-6c7293d01de3
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '2004'
ht-degree: 0%

---

# [!DNL Azure Event Hubs] 連接

## 總覽 {#overview}

>[!IMPORTANT]
>
> 此目的地僅適用於 [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) 客戶。

[!DNL Azure Event Hubs] 是大資料串流平台和事件擷取服務。 它每秒可接收並處理數百萬個事件。 透過任何即時分析提供者或批次處理程式/儲存轉接器，即可轉換及儲存傳送至事件中樞的資料。

您可以建立與 [!DNL Azure Event Hubs] 儲存以從Adobe Experience Platform串流資料。

* 如需 [!DNL Azure Event Hubs]，請參閱 [Microsoft檔案](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about).
* 連線至 [!DNL Azure Event Hubs] 以程式設計方式，請參閱 [串流目的地API教學課程](../../api/streaming-destinations.md).
* 連線至 [!DNL Azure Event Hubs] 使用Platform使用者介面，請參閱以下各節。

![AWS Kinesis在UI中](../../assets/catalog/cloud-storage/event-hubs/catalog.png)

## 使用案例 {#use-cases}

使用串流目的地，例如 [!DNL Azure Event Hubs]，您可以輕鬆將高價值細分事件和相關設定檔屬性饋送至您所選擇的系統。

例如，潛在客戶下載了白皮書，將其歸類為「高傾向轉換」區段。 通過映射潛在客戶所在的段 [!DNL Azure Event Hubs] 目的地，您會在 [!DNL Azure Event Hubs]. 在那裡，您可以採用自己動手做的方法，在活動之上描述業務邏輯，因為您認為最適合您的企業IT系統。

## 匯出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 設定檔]** | 您要匯出區段的所有成員，以及所需的結構欄位(例如：電子郵件地址、電話號碼、姓氏)，如「選取設定檔屬性」畫面中所選 [目的地啟動工作流程](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」API型連線。 一旦根據區段評估在Experience Platform中更新設定檔，連接器就會將更新傳送至下游的目的地平台。 深入了解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## IP位址允許清單 {#ip-address-allowlist}

為滿足客戶的安全性和合規性要求，Experience Platform提供了靜態IP清單，您可以在 [!DNL Azure Event Hubs] 目的地。 請參閱 [串流目的地的IP位址允許清單](/help/destinations/catalog/streaming/ip-address-allow-list.md) 以取得允許清單的完整IP清單。

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線至目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

若要連線至此目的地，請依照 [目的地設定教學課程](../../ui/connect-destination.md). 連接到此目的地時，必須提供以下資訊：

### 驗證資訊 {#authentication-information}

#### 標準驗證 {#standard-authentication}

![UI螢幕的影像，顯示Azure事件集線器標準驗證詳細資訊的已完成欄位](../../assets/catalog/cloud-storage/event-hubs/event-hubs-standard-authentication.png)

如果您選取 **[!UICONTROL 標準驗證]** 輸入以連線至HTTP端點，輸入下方欄位並選取 **[!UICONTROL 連接到目標]**:

* **[!UICONTROL SAS密鑰名]**:授權規則的名稱，也稱為SAS密鑰名稱。
* **[!UICONTROL SAS密鑰]**:事件集線器命名空間的主鍵。 此 `sasPolicy` the `sasKey` 對應到必須有 **管理** 為填充事件中心清單而配置的權限。 了解驗證 [!DNL Azure Event Hubs] 在 [Microsoft檔案](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* **[!UICONTROL 命名空間]**:填入 [!DNL Azure Event Hubs] 命名空間。 了解 [!DNL Azure Event Hubs] 中的命名空間 [Microsoft檔案](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace).

#### 共用訪問簽名(SAS)驗證 {#sas-authentication}

![UI螢幕的影像，顯示Azure事件集線器標準驗證詳細資訊的已完成欄位](../../assets/catalog/cloud-storage/event-hubs/event-hubs-sas-authentication.png)

如果您選取 **[!UICONTROL 標準驗證]** 輸入以連線至HTTP端點，輸入下方欄位並選取 **[!UICONTROL 連接到目標]**:

* **[!UICONTROL SAS密鑰名]**:授權規則的名稱，也稱為SAS密鑰名稱。
* **[!UICONTROL SAS密鑰]**:事件集線器命名空間的主鍵。 此 `sasPolicy` the `sasKey` 對應到必須有 **管理** 為填充事件中心清單而配置的權限。 了解驗證 [!DNL Azure Event Hubs] 在 [Microsoft檔案](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature).
* **[!UICONTROL 命名空間]**:填入 [!DNL Azure Event Hubs] 命名空間。 了解 [!DNL Azure Event Hubs] 中的命名空間 [Microsoft檔案](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace).
* **[!UICONTROL 命名空間]**:填入 [!DNL Azure Event Hubs] 命名空間。 了解 [!DNL Azure Event Hubs] 中的命名空間 [Microsoft檔案](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace).

### 填寫目的地詳細資訊 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_eventhubs_includesegmentnames"
>title="包含區段名稱"
>abstract="如果要讓資料匯出包含要匯出的區段名稱，請切換。 檢視已選取此選項之資料匯出範例的檔案。"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_eventhubs_includesegmenttimestamps"
>title="包含區段時間戳記"
>abstract="如果您希望資料匯出包含建立和更新區段時的UNIX時間戳記，以及將區段對應至要啟用的目的地時的UNIX時間戳記，則切換。 檢視已選取此選項之資料匯出範例的檔案。"

若要設定目的地的詳細資訊，請填寫下方的必填和選填欄位。 UI中欄位旁的星號表示該欄位為必要欄位。

![UI螢幕的影像，顯示Azure事件中心目標詳細資訊的已完成欄位](../../assets/catalog/cloud-storage/event-hubs/event-hubs-destination-details.png)

* **[!UICONTROL 名稱]**:填入連線的名稱 [!DNL Azure Event Hubs].
* **[!UICONTROL 說明]**:提供連線的說明。  範例：「高端客戶」、「對玩風箏衝浪感興趣的客戶」。
* **[!UICONTROL eventHubName]**:提供資料流的名稱給您的 [!DNL Azure Event Hubs] 目的地。
* **[!UICONTROL 包含區段名稱]**:如果要讓資料匯出包含要匯出的區段名稱，請切換。 如需選取此選項的資料匯出範例，請參閱 [匯出的資料](#exported-data) 下文一節。
* **[!UICONTROL 包含區段時間戳記]**:如果您希望資料匯出包含建立和更新區段時的UNIX時間戳記，以及將區段對應至要啟用的目的地時的UNIX時間戳記，則切換。 如需選取此選項的資料匯出範例，請參閱 [匯出的資料](#exported-data) 下文一節。

### 啟用警報 {#enable-alerts}

您可以啟用警報，接收有關資料流到目標狀態的通知。 從清單中選擇要訂閱的警報，以接收有關資料流狀態的通知。 如需警報的詳細資訊，請參閱 [使用UI訂閱目的地警報](../../ui/alerts.md).

完成提供目標連接的詳細資訊後，請選擇 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**, **[!UICONTROL 啟動目的地]**, **[!UICONTROL 檢視設定檔]**，和 **[!UICONTROL 檢視區段]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

請參閱 [對串流設定檔匯出目的地啟用受眾資料](../../ui/activate-streaming-profile-destinations.md) 以取得啟用受眾區段至此目的地的指示。

## 設定檔匯出行為 {#profile-export-behavior}

Experience Platform會最佳化將設定檔匯出至您的 [!DNL Azure Event Hubs] 」，以僅在符合區段資格或其他重大事件後發生設定檔的相關更新時，將資料匯出至您的目的地。 設定檔會在下列情況下匯出至您的目的地：

* 設定檔更新是由對應至目的地的至少一個區段的區段成員資格變更所決定。 例如，設定檔已符合對應至目的地的其中一個區段資格，或已退出對應至目的地的其中一個區段。
* 設定檔更新是由 [身分圖](/help/xdm/field-groups/profile/identitymap.md). 例如，已符合其中一個對應至目的地區段資格的設定檔，已在「身分對應」屬性中新增身分識別。
* 配置檔案更新由至少一個映射到目標的屬性的屬性的屬性變化確定。 例如，對應步驟中對應至目的地的其中一個屬性會新增至設定檔。

在上述所有情況中，只有發生相關更新的設定檔會匯出至您的目的地。 例如，如果對應至目的地流程的區段有100個成員，且有5個新設定檔符合該區段的資格，則匯出至目的地的作業會是增量的，且僅包含5個新設定檔。

請注意，無論變更在何處，所有對應屬性都會針對設定檔匯出。 因此，在上述範例中，即使屬性本身未變更，這五個新設定檔的所有對應屬性也會匯出。

### 決定資料匯出的項目，以及匯出中包含的項目 {#what-determines-export-what-is-included}

對於針對指定設定檔匯出的資料，請務必了解 *決定將資料匯出至您的 [!DNL Azure Event Hubs] 目的地* 和 *匯出中包含的資料*.

| 決定目標匯出的因素 | 目的地匯出包含的項目 |
|---------|----------|
| <ul><li>對應的屬性和區段可作為目的地匯出的提示。 這表示，如果任何映射的段更改狀態（從null更改為已實現或從已實現/現有更新為正在退出）或任何映射的屬性被更新，則將啟動目標導出。</li><li>由於身分目前無法對應至 [!DNL Azure Event Hubs] 目的地、指定設定檔上任何身分的變更也會決定目的地匯出。</li><li>屬性的更改定義為對屬性的任何更新，無論其是否為相同值。 這表示即使值本身未變更，屬性的覆寫仍視為變更。</li></ul> | <ul><li>所有段（具有最新的成員資格狀態），無論它們是否映射到資料流中，都會包含在 `segmentMembership` 物件。</li><li>中的所有身分 `identityMap` 也包含物件(Experience Platform目前不支援 [!DNL Azure Event Hubs] 目的地)。</li><li>目標匯出中僅包含對應的屬性。</li></ul> |

{style=&quot;table-layout:fixed&quot;}

例如，將此資料流視為 [!DNL Azure Event Hubs] 目標中，在資料流中選擇了三個段，四個屬性映射到目標。

![Amazon Kinesis目的地資料流](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

匯出至目的地的設定檔可由符合以下條件之一或退出該條件的設定檔來決定 *三個已對應區段*. 不過，在資料匯出中， `segmentMembership` 物件(請參閱 [匯出的資料](#exported-data) )，則如果該特定設定檔是其成員，則可能會顯示其他未映射的區段。 如果設定檔符合「使用德羅林汽車」區段的客戶資格，但同時也是「已觀看的回到未來」電影和科幻影迷區段的成員，則另外兩個區段也會出現在 `segmentMembership` 對象，即使這些對象未映射到資料流中。

從設定檔屬性的觀點來看，對上述四個屬性所做的任何變更將決定目的地匯出，而設定檔上呈現的四個對應屬性中的任何一個將出現在資料匯出中。

## 歷史資料回填 {#historical-data-backfill}

將新區段新增至現有目的地，或建立新目的地並將區段對應至該目的地時，Experience Platform會將歷史區段資格資料匯出至目的地。 符合區段資格的設定檔 *befor* 區段已新增至目的地後，大約一小時內就會匯出至目的地。

## 匯出的資料 {#exported-data}

已導出 [!DNL Experience Platform] 資料登陸 [!DNL Azure Event Hubs] 目的地。 例如，以下匯出包含符合特定區段資格的設定檔、是其他兩個區段的成員，並退出另一個區段。 匯出內容也包含設定檔屬性名、姓氏、出生日期和個人電子郵件地址。 此設定檔的身分為ECID和電子郵件。

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

以下是匯出資料的進一步範例，具體取決於您在連線目的地流程中為 **[!UICONTROL 包含區段名稱]** 和 **[!UICONTROL 包含區段時間戳記]** 選項：

+++ 以下資料匯出範例包含 `segmentMembership` 節

```json
"segmentMembership": {
        "ups": {
          "5b998cb9-9488-4ec3-8d95-fa8338ced490": {
            "lastQualificationTime": "2019-04-15T02:41:50+0000",
            "status": "existing",
            "createdAt": 1648553325000,
            "updatedAt": 1648553330000,
            "mappingCreatedAt": 1649856570000,
            "mappingUpdatedAt": 1649856570000,
            "name": "First name equals John"
          }
        }
      }
```

+++

+++ 以下資料匯出範例包含 `segmentMembership` 節

```json
"segmentMembership": {
        "ups": {
          "5b998cb9-9488-4ec3-8d95-fa8338ced490": {
            "lastQualificationTime": "2019-04-15T02:41:50+0000",
            "status": "existing",
            "createdAt": 1648553325000,
            "updatedAt": 1648553330000,
            "mappingCreatedAt": 1649856570000,
            "mappingUpdatedAt": 1649856570000,
          }
        }
      }
```

+++

## 限制和重試策略 {#limits-retry-policy}

在95%的時間內，Experience Platform會嘗試為成功發送的消息提供少於10分鐘的吞吐量延遲，每個資料流每秒的請求速率小於10,000個，以到達HTTP目的地。

如果對您的HTTP API目的地提出失敗請求，Experience Platform會儲存失敗的請求並重試兩次，以將請求傳送至端點。

>[!MORELIKETHIS]
>
>* [連接到Azure事件集線器，並使用流服務API激活資料](../../api/streaming-destinations.md)
>* [AWSKinesis目的地](./amazon-kinesis.md)
>* [目的地類型和類別](../../destination-types.md)

