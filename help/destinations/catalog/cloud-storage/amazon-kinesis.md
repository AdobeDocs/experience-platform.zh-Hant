---
keywords: Amazon Kinesis；kinesis目的地；kinesis
title: Amazon Kinesis連線
description: 建立與您的Amazon Kinesis儲存空間的即時輸出連線，以從Adobe Experience Platform串流資料。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: b40117ef-6ad0-48a9-bbcb-97c6f6d1dce3
source-git-commit: c3ef732ee82f6c0d56e89e421da0efc4fbea2c17
workflow-type: tm+mt
source-wordcount: '1984'
ht-degree: 5%

---

# [!DNL Amazon Kinesis] 連線

## 概觀 {#overview}

>[!IMPORTANT]
>
> 此目的地僅適用於 [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/jp/legal/product-descriptions/real-time-customer-data-platform.html) 客戶。

此 [!DNL Kinesis Data Streams] 服務者 [!DNL Amazon Web Services] 可讓您即時收集和處理大型資料記錄串流。

您可以建立與您的的即時輸出連線 [!DNL Amazon Kinesis] 從Adobe Experience Platform串流資料的儲存空間。

* 有關詳細資訊 [!DNL Amazon Kinesis]，請參閱 [Amazon檔案](https://docs.aws.amazon.com/streams/latest/dev/introduction.html).
* 若要連線到 [!DNL Amazon Kinesis] 以程式設計方式參閱 [串流目的地API教學課程](../../api/streaming-destinations.md).
* 若要連線到 [!DNL Amazon Kinesis] 使用Platform使用者介面，請參閱下列章節。

![UI中的Amazon Kinesis](../../assets/catalog/cloud-storage/amazon-kinesis/catalog.png)

## 使用案例 {#use-cases}

使用串流目的地，例如 [!DNL Amazon Kinesis]，您就能輕鬆將高價值分段事件和相關設定檔屬性饋送至您選擇的系統。

例如，潛在客戶下載了白皮書，將其歸類為「高轉換傾向」區段。 將潛在客戶所屬的受眾對應至 [!DNL Amazon Kinesis] 目的地，您會在以下位置收到此事件： [!DNL Amazon Kinesis]. 在這裡，您可以採用DIY（自己動手）方式，並在事件上方描述商業邏輯，因為您認為這種方式最適合企業IT系統。

## 支援的對象 {#supported-audiences}

本節說明您可以將哪些型別的對象匯出至此目的地。

| 對象來源 | 支援 | 說明 |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ (A) | 透過Experience Platform產生的對象 [分段服務](../../../segmentation/home.md). |
| 自訂上傳 | ✓ | 受眾 [已匯入](../../../segmentation/ui/overview.md#import-audience) 從CSV檔案Experience Platform為。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出型別 | **[!UICONTROL 以設定檔為基礎]** | 您正在匯出區段的所有成員，以及所需的結構描述欄位（例如：電子郵件地址、電話號碼、姓氏），如 [目的地啟用工作流程](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 一旦根據對象評估在Experience Platform中更新了設定檔，聯結器就會將更新傳送至下游的目的地平台。 深入瞭解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## IP位址允許清單 {#ip-address-allowlist}

為了滿足客戶的安全性和合規性要求，Experience Platform提供您可以允許清單中的靜態IP [!DNL Amazon Kinesis] 目的地。 請參閱 [串流目的地的IP位址允許清單](/help/destinations/catalog/streaming/ip-address-allow-list.md) 以取得加入允許清單的IP完整清單。

## 必填 [!DNL Amazon Kinesis] 許可權 {#required-kinesis-permission}

若要成功連線並匯出資料至 [!DNL Amazon Kinesis] 串流，Experience Platform需要許可權才能執行下列動作：

* `kinesis:ListStreams`
* `kinesis:PutRecord`
* `kinesis:PutRecords`

這些許可權是透過 [!DNL Kinesis] 主控台，以及在Platform使用者介面中設定Kinesis目的地後由Platform檢查。

下列範例顯示成功將資料匯出至所需的最低存取許可權 [!DNL Kinesis] 目的地。

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "kinesis:ListStreams",
                "kinesis:PutRecord",
                "kinesis:PutRecords"
            ],
            "Resource": [
                "arn:aws:kinesis:us-east-2:901341027596:stream/*"
            ]
        }
    ]
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `kinesis:ListStreams` | 此動作會列出您的Amazon Kinesis資料串流。 |
| `kinesis:PutRecord` | 此動作會將單一資料記錄寫入Kinesis資料串流。 |
| `kinesis:PutRecords` | 此動作可透過單一呼叫，將多筆資料記錄寫入Kinesis資料流中。 |

{style="table-layout:auto"}

如需控制存取許可權的詳細資訊， [!DNL Kinesis] 資料串流，請閱讀下列內容 [[!DNL Kinesis] 檔案](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html).

## 連線到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要 **[!UICONTROL 檢視目的地]** 和 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md). 連線到這個目的地時，您必須提供下列資訊：

### 驗證資訊 {#authentication-information}

輸入以下欄位並選取 **[!UICONTROL 連線到目的地]**：

![顯示Amazon Kinesis驗證詳細資料已完成欄位的UI畫面影像](../../assets/catalog/cloud-storage/amazon-kinesis/kinesis-authentication-fields.png)

* **[!DNL Amazon Web Services]存取金鑰與秘密金鑰**：在 [!DNL Amazon Web Services]，產生 `access key - secret access key` 配對，授予Platform存取權給您的 [!DNL Amazon Kinesis] 帳戶。 進一步瞭解 [Amazon Web Services檔案](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).
* **[!UICONTROL 地區]**：指示哪個 [!DNL Amazon Web Services] 串流資料的目標區域。

### 填寫目標詳細資訊 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_kinesis_includesegmentnames"
>title="包括區段名稱"
>abstract="切換是否希望資料匯出包括您正在匯出的對象的名稱。檢視選取此選項時的資料匯出範例的文件。"

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_kinesis_includesegmenttimestamps"
>title="包括區段時間戳記"
>abstract="切換是否希望資料匯出包括建立和更新對象時的 UNIX 時間戳記，以及對象對應至啟動目的地時的 UNIX 時間戳記。檢視選取此選項時的資料匯出範例的文件。"

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。

![顯示Amazon Kinesis目的地詳細資訊的已完成欄位的UI畫面影像](../../assets/catalog/cloud-storage/amazon-kinesis/kinesis-destination-details.png)

* **[!UICONTROL 名稱]**：提供連線的名稱，並前往 [!DNL Amazon Kinesis]
* **[!UICONTROL 說明]**：提供連線至的說明 [!DNL Amazon Kinesis].
* **[!UICONTROL 串流]**：提供中現有資料串流的名稱， [!DNL Amazon Kinesis] 帳戶。 Platform會將資料匯出至此資料流。
* **[!UICONTROL 包含區段名稱]**：如果您希望資料匯出包含您正在匯出的對象名稱，請切換按鈕。 有關選取此選項的資料匯出範例，請參閱 [匯出的資料](#exported-data) 區段。
* **[!UICONTROL 包含區段時間戳記]**：如果您希望資料匯出包含建立和更新對象時的UNIX時間戳記，以及對象對應至啟用目的地時的UNIX時間戳記，請切換此按鈕。 有關選取此選項的資料匯出範例，請參閱 [匯出的資料](#exported-data) 區段。

<!--

>[!IMPORTANT]
>
>Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱以下指南： [使用UI訂閱目的地警報](../../ui/alerts.md).

當您完成提供目的地連線的詳細資訊時，請選取「 」 **[!UICONTROL 下一個]**.

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要 **[!UICONTROL 檢視目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。
>* [同意原則評估](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) 目前不支援匯出至Amazon Kinesis目的地。 [閱讀全文](/help/destinations/ui/activate-streaming-profile-destinations.md#consent-policy-evaluation)。

另請參閱 [啟用受眾資料至串流設定檔匯出目的地](../../ui/activate-streaming-profile-destinations.md) 以取得啟用此目的地對象的指示。

## 設定檔匯出行為 {#profile-export-behavior}

Experience Platform會將設定檔匯出行為最佳化至 [!DNL Amazon Kinesis] 目的地，目的是在對象資格或其他重大事件後發生設定檔的相關更新時，僅將資料匯出至您的目的地。 在下列情況下，設定檔會匯出至您的目的地：

* 設定檔更新是由對應至目的地的至少一個對象的對象成員資格變更所決定。 例如，設定檔已符合對應至目的地的其中一個對象的資格，或已退出對應至目的地的其中一個對象。
* 設定檔更新是由 [身分對應](/help/xdm/field-groups/profile/identitymap.md). 例如，已符合對應至目的地之其中一個對象資格的設定檔，已在身分對應屬性中新增身分。
* 設定檔更新是由對應到目的地的至少一個屬性的變更所決定。 例如，會將對應步驟中對應至目的地的其中一個屬性新增至設定檔。

在上述所有情況下，只有已發生相關更新的設定檔才會匯出至您的目的地。 例如，如果對應至目的地流程的受眾有一百個成員，且有五個新設定檔符合區段的資格，則匯出至您的目的地的作業將以漸進方式進行，且僅包含五個新設定檔。

請注意，無論變更位於何處，所有對映屬性都會匯出為設定檔。 因此，在上述範例中，將會匯出這五個新設定檔的所有對應屬性，即使屬性本身並未變更亦然。

### 決定資料匯出的因素及匯出中包含的因素 {#what-determines-export-what-is-included}

針對針對指定設定檔匯出的資料，瞭解以下兩個不同的概念是很重要的 *決定匯出至您的資料的 [!DNL Amazon Kinesis] 目的地* 和 *哪些資料包含在匯出中*.

| 決定目的地匯出的因素 | 目的地匯出包含的內容 |
|---------|----------|
| <ul><li>對應的屬性和受眾可作為目的地匯出的提示。 這表示如果任何對應的對象變更狀態(從 `null` 至 `realized` 或從 `realized` 至 `exiting`)或更新任何對應的屬性，就會開始匯出目的地。</li><li>由於身分目前無法對應至 [!DNL Amazon Kinesis] 目的地，指定設定檔上任何身分的變更也會決定目的地匯出。</li><li>屬性的變更定義為屬性上的任何更新，無論其是否為相同的值。 這表示即使值本身並未變更，屬性上的覆寫也會視為變更。</li></ul> | <ul><li>此 `segmentMembership` 物件包含啟動資料流中對應的對象，其設定檔的狀態已隨著資格或對象退出事件而變更。 請注意，如果其他未對應對象屬於相同對象，則設定檔符合資格的對象可以屬於目的地匯出的一部分 [合併原則](/help/profile/merge-policies/overview.md) 對象在啟動資料流中的對應方式。 </li><li>中的所有身分 `identityMap` 也包括物件(Experience Platform目前不支援中的身分對應) [!DNL Amazon Kinesis] 目的地)。</li><li>目的地匯出僅包含對應的屬性。</li></ul> |

{style="table-layout:fixed"}

例如，將此資料流視為 [!DNL Amazon Kinesis] 在資料流中選取三個對象，且四個屬性對應至目的地的目的地。

![Amazon Kinesis目的地資料流](../../assets/catalog/http/profile-export-example-dataflow.png)

要判斷匯出至目的地的設定檔是否符合「 」或「 」其中之一， *三個對應的區段*. 不過，在資料匯出中，在 `segmentMembership` 物件(請參閱 [匯出的資料](#exported-data) 區段底下)，其他未對應的對象可能會出現，如果該特定設定檔為其成員，且這些對象與觸發匯出的對象共用相同的合併原則。 如果設定檔符合 **擁有DeLorean Cars的客戶** 對象，但也是 **觀看「回到未來」** 影片和 **科幻迷** 受眾，則其他這兩個受眾也會出現在 `segmentMembership` 匯出的物件，即使這些物件未在資料流中對映，只要它們與共用相同的合併原則 **擁有DeLorean Cars的客戶** 區段。

從設定檔屬性的角度來看，對上述四個對應屬性所做的任何變更將決定目的地匯出，而且設定檔上存在的四個對應屬性中的任何一個都會出現在資料匯出中。

## 歷史資料回填 {#historical-data-backfill}

當您新增對象至現有目的地，或當您建立新目的地並將對象對應至該目的地時，Experience Platform會將歷史對象資格資料匯出至該目的地。 符合對象資格的設定檔 *早於* 新增至目的地的對象會在約一小時內匯出至目的地。

## 匯出的資料 {#exported-data}

您的匯出 [!DNL Experience Platform] 資料進入您的 [!DNL Amazon Kinesis] JSON格式的目的地。 例如，下列匯出包含符合特定區段資格的設定檔、是另一個兩個區段的成員，且已退出另一個區段。 匯出也包含設定檔屬性的名字、姓氏、出生日期和個人電子郵件地址。 此設定檔的身分識別為ECID和電子郵件。

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

以下為更多匯出資料範例，視您在連線目的地流程中選取的UI設定而定 **[!UICONTROL 包含區段名稱]** 和 **[!UICONTROL 包含區段時間戳記]** 選項：

+++ 以下資料匯出範例包含 `segmentMembership` 區段

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

+++ 以下資料匯出範例包含 `segmentMembership` 區段

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

## 限制和重試原則 {#limits-retry-policy}

在95%的時間中，Experience Platform會嘗試針對每個資料流向HTTP目的地的成功傳送訊息，以每秒少於10,000個要求的速率，提供少於10分鐘的輸送量延遲。

如果對您的HTTP API目的地的請求失敗，Experience Platform會儲存失敗的請求並重試兩次，以將請求傳送至您的端點。

>[!MORELIKETHIS]
>
>* [連線至Amazon Kinesis並使用流量服務API啟用資料](../../api/streaming-destinations.md)
>* [Azure事件中樞目的地](./azure-event-hubs.md)
>* [目的地型別和類別](../../destination-types.md)
