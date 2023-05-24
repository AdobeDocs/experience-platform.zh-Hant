---
keywords: Azure事件中心目標；azure事件中心；azure事件thub
title: Azure事件中心連接
description: 建立到您的 [!DNL Azure Event Hubs] 儲存以從Experience Platform流資料。
exl-id: f98a389a-bce3-4a80-9452-6c7293d01de3
source-git-commit: 4d1f9fa19bd35095e3ccbd8d83bcc33dcd4c45a8
workflow-type: tm+mt
source-wordcount: '2062'
ht-degree: 4%

---

# [!DNL Azure Event Hubs] 連接

## 總覽 {#overview}

>[!IMPORTANT]
>
> 此目標僅可用於 [Adobe Real-time Customer Data Platform旗艦](https://helpx.adobe.com/jp/legal/product-descriptions/real-time-customer-data-platform.html) 客戶。

[!DNL Azure Event Hubs] 是大資料流平台和事件接收服務。 它每秒可以接收和處理數百萬個事件。 通過使用任何即時分析提供程式或批處理/儲存適配器，可以轉換和儲存發送到事件中心的資料。

您可以建立到您的 [!DNL Azure Event Hubs] 儲存以從Adobe Experience Platform傳輸資料。

* 有關 [!DNL Azure Event Hubs]，請參見 [Microsoft文檔](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-about)。
* 連接到 [!DNL Azure Event Hubs] 以寫程式方式，請參見 [流目標API教程](../../api/streaming-destinations.md)。
* 連接到 [!DNL Azure Event Hubs] 使用平台用戶介面，請參閱以下各節。

![AWSKinesis在用戶介面](../../assets/catalog/cloud-storage/event-hubs/catalog.png)

## 使用案例 {#use-cases}

使用流目標，如 [!DNL Azure Event Hubs]，您可以輕鬆地將高價值分段事件和關聯的配置檔案屬性輸入到您選擇的系統中。

例如，潛在客戶下載了一份白皮書，確認他們屬於「高傾向轉換」段。 通過映射目標客戶所在的段 [!DNL Azure Event Hubs] 目標，您將在 [!DNL Azure Event Hubs]。 在這裡，您可以採用自行動手的方法，並在活動之前描述業務邏輯，因為您認為最適合您的企業IT系統。

## 導出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 導出類型 | **[!UICONTROL 基於配置檔案]** | 您正在導出段的所有成員以及所需的架構欄位(例如：電子郵件地址、電話號碼、姓氏)，在「選擇配置檔案屬性」螢幕中選擇 [目標激活工作流](../../ui/activate-batch-profile-destinations.md#select-attributes)。 |
| 導出頻率 | **[!UICONTROL 流]** | 流目標是基於API的「始終開啟」連接。 一旦基於段評估在Experience Platform中更新配置檔案，連接器就將更新下游發送到目標平台。 閱讀有關 [流目標](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## IP地址允許清單 {#ip-address-allowlist}

為滿足客戶的安全性和法規遵從性要求，Experience Platform提供了一個靜態IP清單，您可以為 [!DNL Azure Event Hubs] 目標。 請參閱 [流目標的IP地址允許清單](/help/destinations/catalog/streaming/ip-address-allow-list.md) 清單。

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>要連接到目標，您需要 **[!UICONTROL 管理目標]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

要連接到此目標，請按照 [目標配置教程](../../ui/connect-destination.md)。 連接到此目標時，必須提供以下資訊：

### 驗證資訊 {#authentication-information}

#### 標準驗證 {#standard-authentication}

![顯示Azure事件集線器標準身份驗證詳細資訊已完成欄位的UI螢幕影像](../../assets/catalog/cloud-storage/event-hubs/event-hubs-standard-authentication.png)

如果選擇 **[!UICONTROL 標準驗證]** 鍵入以連接到HTTP終結點，輸入下面的欄位並選擇 **[!UICONTROL 連接到目標]**:

* **[!UICONTROL SAS密鑰名稱]**:授權規則的名稱，也稱為SAS密鑰名稱。
* **[!UICONTROL SAS密鑰]**:事件集線器命名空間的主鍵。 的 `sasPolicy` 那個 `sasKey` 必須對應 **管理** 為填充事件中心清單而配置的權限。 瞭解身份驗證 [!DNL Azure Event Hubs] 在 [Microsoft文檔](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)。
* **[!UICONTROL 命名空間]**:填寫 [!DNL Azure Event Hubs] 命名空間。 瞭解 [!DNL Azure Event Hubs] 命名空間 [Microsoft文檔](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace)。

#### 共用訪問簽名(SAS)驗證 {#sas-authentication}

![顯示Azure事件集線器標準身份驗證詳細資訊已完成欄位的UI螢幕影像](../../assets/catalog/cloud-storage/event-hubs/event-hubs-sas-authentication.png)

如果選擇 **[!UICONTROL 標準驗證]** 鍵入以連接到HTTP終結點，輸入下面的欄位並選擇 **[!UICONTROL 連接到目標]**:

* **[!UICONTROL SAS密鑰名稱]**:授權規則的名稱，也稱為SAS密鑰名稱。
* **[!UICONTROL SAS密鑰]**:事件集線器命名空間的主鍵。 的 `sasPolicy` 那個 `sasKey` 必須對應 **管理** 為填充事件中心清單而配置的權限。 瞭解身份驗證 [!DNL Azure Event Hubs] 在 [Microsoft文檔](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)。
* **[!UICONTROL 命名空間]**:填寫 [!DNL Azure Event Hubs] 命名空間。 瞭解 [!DNL Azure Event Hubs] 命名空間 [Microsoft文檔](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace)。
* **[!UICONTROL 事件中心名稱]**:填寫 [!DNL Azure Event Hub] 名稱。 瞭解 [!DNL Azure Event Hubs] 名稱 [Microsoft文檔](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hub)。

### 填寫目標詳細資訊 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_eventhubs_includesegmentnames"
>title="包括區段名稱"
>abstract="切換是否希望資料匯出包括您正在匯出的區段的名稱。檢視選取此選項時的資料匯出範例的文件。"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_eventhubs_includesegmenttimestamps"
>title="包括區段時間戳記"
>abstract="切換是否希望資料匯出包括建立和更新區段時的 Unix 時間戳記，以及區段對應至啟動目的地時的 Unix 時間戳記。檢視選取此選項時的資料匯出範例的文件。"

要配置目標的詳細資訊，請填寫以下必需欄位和可選欄位。 UI中某個欄位旁邊的星號表示該欄位是必需的。

![顯示Azure事件中心目標詳細資訊已完成欄位的UI螢幕影像](../../assets/catalog/cloud-storage/event-hubs/event-hubs-destination-details.png)

* **[!UICONTROL 名稱]**:填寫到的連接的名稱 [!DNL Azure Event Hubs]。
* **[!UICONTROL 說明]**:提供連接的說明。  示例：「高級客戶」、「對風箏衝浪感興趣的客戶」。
* **[!UICONTROL 事件集線器名稱]**:為流提供名稱 [!DNL Azure Event Hubs] 目標。
* **[!UICONTROL 包括段名稱]**:如果希望資料導出包含要導出的段的名稱，則切換。 有關選擇此選項的資料導出示例，請參閱 [導出的資料](#exported-data) 的下一頁。
* **[!UICONTROL 包括段時間戳]**:如果希望資料導出包括建立和更新段時的UNIX時間戳，以及將段映射到要激活的目標時的UNIX時間戳，則切換。 有關選擇此選項的資料導出示例，請參閱 [導出的資料](#exported-data) 的下一頁。

### 啟用警報 {#enable-alerts}

您可以啟用警報來接收有關目標資料流狀態的通知。 從清單中選擇要訂閱的警報以接收有關資料流狀態的通知。 有關警報的詳細資訊，請參閱上的指南 [使用UI訂閱目標警報](../../ui/alerts.md)。

完成提供目標連接的詳細資訊後，選擇 **[!UICONTROL 下一個]**。

## 將段激活到此目標 {#activate}

>[!IMPORTANT]
> 
>要激活資料，您需要 **[!UICONTROL 管理目標]**。 **[!UICONTROL 激活目標]**。 **[!UICONTROL 查看配置檔案]**, **[!UICONTROL 查看段]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

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
| <ul><li>映射的屬性和段用作目標導出的提示。 這表示如果任何映射的段更改狀態(從 `null` 至 `realized` 或 `realized` 至 `exiting`)或更新任何映射屬性時，將啟動目標導出。</li><li>由於標識當前無法映射到 [!DNL Azure Event Hubs] 目標，給定配置檔案上任何身份的更改也會決定目標導出。</li><li>屬性的更改定義為屬性上的任何更新，無論其值是否相同。 這意味著，即使值本身未更改，屬性上的覆蓋也被視為更改。</li></ul> | <ul><li>的 `segmentMembership` 對象包括在激活資料流中映射的段，在限定或段退出事件後配置檔案的狀態已更改。 請注意，如果配置檔案限定用於的其他未映射段屬於相同的段，則這些段可以是目標導出的一部分 [合併策略](/help/profile/merge-policies/overview.md) 激活資料流中映射的段。 </li><li>中的所有標識 `identityMap` 也包括對象(Experience Platform當前不支援在 [!DNL Azure Event Hubs] 目標)。</li><li>目標導出中只包含映射的屬性。</li></ul> |

{style="table-layout:fixed"}

例如，將此資料流視為 [!DNL Azure Event Hubs] 目標，其中在資料流中選擇了三個段，並將四個屬性映射到目標。

![AmazonKinesis目標資料流](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

導出到目標的配置檔案可由符合或退出其中一個配置檔案來確定 *三個映射段*。 但是，在資料導出中，在 `segmentMembership` 對象（請參見） [導出的資料](#exported-data) )中，如果特定配置檔案是其成員，並且這些配置檔案與觸發導出的段共用相同的合併策略，則可能會出現其他未映射的段。 如果配置檔案符合 **DeLorean汽車的客戶** 部，但亦為 **觀看《回到未來》** 電影和 **科幻迷** 段，則這兩個段也將 `segmentMembership` 資料導出的對象，即使這些對象未在資料流中映射，如果它們與 **DeLorean汽車的客戶** 段。

從配置檔案屬性的視點來看，對上述四個屬性的任何更改都將確定目標導出，並且配置檔案上存在的四個映射屬性中的任何一個都將出現在資料導出中。

## 歷史資料回填 {#historical-data-backfill}

當您將新段添加到現有目標或建立新目標並將段映射到該目標時，Experience Platform會將歷史段限定資料導出到目標。 限定段的配置檔案 *先* 已添加到目標的段在大約一小時內導出到目標。

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
         "status":"realized"
      },
      "947c1c46-008d-40b0-92ec-3af86eaf41c1":{
         "lastQualificationTime":"2021-08-25T23:37:33Z",
         "status":"realized"
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

下面是導出資料的進一步示例，具體取決於您在連接目標流中為 **[!UICONTROL 包括段名稱]** 和 **[!UICONTROL 包括段時間戳]** 選項：

+++ 以下資料導出示例包括 `segmentMembership` 節

```json
"segmentMembership": {
        "ups": {
          "5b998cb9-9488-4ec3-8d95-fa8338ced490": {
            "lastQualificationTime": "2019-04-15T02:41:50+0000",
            "status": "realized",
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

+++ 以下資料導出示例包括 `segmentMembership` 節

```json
"segmentMembership": {
        "ups": {
          "5b998cb9-9488-4ec3-8d95-fa8338ced490": {
            "lastQualificationTime": "2019-04-15T02:41:50+0000",
            "status": "realized",
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

在95%的時間內，Experience Platform會嘗試為成功發送的消息提供少於10分鐘的吞吐量延遲，每個資料流的請求速率低於每秒10,000次，到HTTP目標。

如果向HTTP API目標發出失敗請求，Experience Platform將儲存失敗的請求並重試兩次，以將請求發送到終結點。

>[!MORELIKETHIS]
>
>* [連接到Azure事件中心並使用流服務API激活資料](../../api/streaming-destinations.md)
>* [AWSKinesis目的地](./amazon-kinesis.md)
>* [目標類型和類別](../../destination-types.md)

