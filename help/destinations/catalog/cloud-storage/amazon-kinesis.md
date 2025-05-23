---
keywords: Amazon Kinesis；kinesis目的地；kinesis
title: Amazon Kinesis連線
description: 建立與您的Amazon Kinesis儲存空間的即時輸出連線，以從Adobe Experience Platform串流資料。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: b40117ef-6ad0-48a9-bbcb-97c6f6d1dce3
source-git-commit: 678f80445212edc1edd3f4799999990ddcc2a039
workflow-type: tm+mt
source-wordcount: '1985'
ht-degree: 5%

---

# [!DNL Amazon Kinesis]個連線

## 概觀 {#overview}

>[!IMPORTANT]
>
> 此目的地僅供[Adobe Real-Time Customer Data Platform Ultimate](https://helpx.adobe.com/jp/legal/product-descriptions/real-time-customer-data-platform.html)客戶使用。

[!DNL Amazon Web Services]的[!DNL Kinesis Data Streams]服務可讓您即時收集和處理大型資料記錄串流。

您可以建立與[!DNL Amazon Kinesis]儲存裝置的即時輸出連線，以從Adobe Experience Platform串流資料。

* 如需[!DNL Amazon Kinesis]的詳細資訊，請參閱[Amazon檔案](https://docs.aws.amazon.com/streams/latest/dev/introduction.html)。
* 若要以程式設計方式連線到[!DNL Amazon Kinesis]，請參閱[串流目的地API教學課程](../../api/streaming-destinations.md)。
* 若要使用Experience Platform使用者介面連線至[!DNL Amazon Kinesis]，請參閱下列章節。

UI中的![Amazon Kinesis](../../assets/catalog/cloud-storage/amazon-kinesis/catalog.png)

## 使用案例 {#use-cases}

透過使用串流目的地（例如[!DNL Amazon Kinesis]），您可以輕鬆將高價值分段事件和相關設定檔屬性饋送至您選擇的系統。

例如，潛在客戶下載了白皮書，將其歸類為「高轉換傾向」區段。 將潛在客戶所在對象對應至[!DNL Amazon Kinesis]目的地後，您將在[!DNL Amazon Kinesis]中收到此事件。 在這裡，您可以採用DIY（自己動手）方式，並在事件上方描述商業邏輯，因為您認為這種方式最適合企業IT系統。

## 支援的對象 {#supported-audiences}

本節說明您可以將哪些型別的對象匯出至此目的地。

| 對象來源 | 支援 | 說明 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | 透過Experience Platform [細分服務](../../../segmentation/home.md)產生的對象。 |
| 自訂上傳 | ✓ | 對象[從CSV檔案匯入](../../../segmentation/ui/audience-portal.md#import-audience)至Experience Platform。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 以設定檔為基礎]** | 您正在匯出區段的所有成員，以及所需的結構描述欄位（例如：電子郵件地址、電話號碼、姓氏），如[目的地啟用工作流程](../../ui/activate-batch-profile-destinations.md#select-attributes)的選取設定檔屬性畫面中所選。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 根據對象評估在Experience Platform中更新設定檔後，聯結器會立即將更新傳送至下游的目標平台。 深入瞭解[串流目的地](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## IP位址允許清單 {#ip-address-allowlist}

為了滿足客戶的安全性和合規性要求，Experience Platform提供您可以為[!DNL Amazon Kinesis]目的地加入允許清單的靜態IP清單。 如需允許清單的完整IP清單，請參閱串流目的地的[IP位址允許清單](/help/destinations/catalog/streaming/ip-address-allow-list.md)。

## 必要的[!DNL Amazon Kinesis]許可權 {#required-kinesis-permission}

若要成功連線並匯出資料至您的[!DNL Amazon Kinesis]串流，Experience Platform需要下列動作的許可權：

* `kinesis:ListStreams`
* `kinesis:PutRecord`
* `kinesis:PutRecords`

這些許可權是透過[!DNL Kinesis]主控台排列，當您在Experience Platform使用者介面中設定Kinesis目的地後，Experience Platform會檢查這些許可權。

下列範例顯示成功匯出資料至[!DNL Kinesis]目的地所需的最低存取許可權。

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
| `kinesis:PutRecords` | 此動作可透過單一呼叫，將多筆資料記錄寫入Kinesis資料串流。 |

{style="table-layout:auto"}

如需控制[!DNL Kinesis]資料串流存取權的詳細資訊，請閱讀下列[[!DNL Kinesis] 檔案](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html)。

## 連線到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要&#x200B;**[!UICONTROL 檢視目的地]**&#x200B;和&#x200B;**[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要連線到此目的地，請依照[目的地組態教學課程](../../ui/connect-destination.md)中所述的步驟進行。 連線到這個目的地時，您必須提供下列資訊：

### 驗證資訊 {#authentication-information}

輸入下列欄位並選取&#x200B;**[!UICONTROL 連線到目的地]**：

![顯示Amazon Kinesis驗證詳細資訊已完成欄位的UI畫面影像](../../assets/catalog/cloud-storage/amazon-kinesis/kinesis-authentication-fields.png)

* **[!DNL Amazon Web Services]存取金鑰和秘密金鑰**：在[!DNL Amazon Web Services]中，產生`access key - secret access key`配對，以授予Experience Platform存取您的[!DNL Amazon Kinesis]帳戶。 在[Amazon Web Services檔案](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)中進一步瞭解。
* **[!UICONTROL 區域]**：指出資料流要傳送到哪個[!DNL Amazon Web Services]區域。

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

![顯示Amazon Kinesis目的地詳細資訊已完成欄位的UI畫面影像](../../assets/catalog/cloud-storage/amazon-kinesis/kinesis-destination-details.png)

* **[!UICONTROL 名稱]**：提供您與[!DNL Amazon Kinesis]的連線名稱
* **[!UICONTROL 描述]**：提供您與[!DNL Amazon Kinesis]的連線描述。
* **[!UICONTROL 資料流]**：提供您[!DNL Amazon Kinesis]帳戶中現有資料流的名稱。 Experience Platform會將資料匯出至此資料流。
* **[!UICONTROL 包含區段名稱]**：如果要讓資料匯出包含您匯出的對象名稱，請切換選項。 如需選取此選項的資料匯出範例，請參閱下方的[匯出的資料](#exported-data)區段。
* **[!UICONTROL 包含區段時間戳記]**：若要讓資料匯出包含建立和更新對象時的UNIX時間戳記，以及對象對應至啟用目的地時的UNIX時間戳記，請切換此專案。 如需選取此選項的資料匯出範例，請參閱下方的[匯出的資料](#exported-data)區段。

<!--

>[!IMPORTANT]
>
>Experience Platform needs `write` permissions on the bucket object where the export files will be delivered.

-->

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱[使用UI訂閱目的地警示](../../ui/alerts.md)的指南。

當您完成提供目的地連線的詳細資訊後，請選取&#x200B;**[!UICONTROL 下一步]**。

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要&#x200B;**[!UICONTROL 檢視目的地]**、**[!UICONTROL 啟用目的地]**、**[!UICONTROL 檢視設定檔]**&#x200B;和&#x200B;**[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。
>* 目前匯出至Amazon Kinesis目的地時不支援[同意原則評估](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation)。 [閱讀全文](/help/destinations/ui/activate-streaming-profile-destinations.md#consent-policy-evaluation)。

如需啟用此目的地對象的指示，請參閱[啟用串流設定檔匯出目的地的對象資料](../../ui/activate-streaming-profile-destinations.md)。

## 設定檔匯出行為 {#profile-export-behavior}

Experience Platform會最佳化[!DNL Amazon Kinesis]目的地的設定檔匯出行為，只會在符合對象資格或其他重大事件後發生設定檔的相關更新時，將資料匯出至目的地。 在下列情況下，設定檔會匯出至您的目的地：

* 設定檔更新是由對應至目的地的至少一個對象的對象成員資格變更所決定。 例如，設定檔已符合對應至目的地的其中一個對象的資格，或已退出對應至目的地的其中一個對象。
* 設定檔更新是由[身分對應](/help/xdm/field-groups/profile/identitymap.md)中的變更所決定。 例如，已符合對應至目的地之其中一個對象資格的設定檔，已在身分對應屬性中新增身分。
* 設定檔更新是由對應到目的地的至少一個屬性的變更所決定。 例如，會將對應步驟中對應至目的地的其中一個屬性新增至設定檔。

在上述所有情況下，只有已發生相關更新的設定檔才會匯出至您的目的地。 例如，如果對應至目的地流程的受眾有一百個成員，且有五個新設定檔符合區段的資格，則匯出至您的目的地的作業將以漸進方式進行，且僅包含五個新設定檔。

請注意，無論變更位於何處，所有對映屬性都會匯出為設定檔。 因此，在上述範例中，將會匯出這五個新設定檔的所有對應屬性，即使屬性本身並未變更亦然。

### 決定資料匯出的因素及匯出中包含的因素 {#what-determines-export-what-is-included}

關於為特定設定檔匯出的資料，瞭解&#x200B;*決定匯出至您[!DNL Amazon Kinesis]目的地*&#x200B;的資料以及&#x200B;*匯出中包含哪些資料的兩個不同概念*&#x200B;很重要。

| 決定目的地匯出的因素 | 目的地匯出包含的內容 |
|---------|----------|
| <ul><li>對應的屬性和區段可作為目的地匯出的提示。 這表示如果設定檔的`segmentMembership`狀態變更為`realized`或`exiting`，或任何對應的屬性已更新，將會啟動目的地匯出。</li><li>由於身分目前無法對應至[!DNL Amazon Kinesis]目的地，因此特定設定檔上任何身分的變更也會決定目的地匯出。</li><li>屬性的變更定義為屬性上的任何更新，無論其是否為相同的值。 這表示即使值本身並未變更，屬性上的覆寫也會視為變更。</li></ul> | <ul><li>`segmentMembership`物件包含對映在啟動資料流中的區段，在資格或區段退出事件後，設定檔的狀態已針對該區段變更。 請注意，如果其他符合設定檔資格的未對應區段與啟動資料流中所對應的區段屬於同一個[合併原則](/help/profile/merge-policies/overview.md)，則這些區段可以是目的地匯出的一部分。 </li><li>`identityMap`物件中的所有身分也包括在內(Experience Platform目前不支援[!DNL Amazon Kinesis]目的地中的身分對應)。</li><li>目的地匯出僅包含對應的屬性。</li></ul> |

{style="table-layout:fixed"}

例如，將此資料流視為在[!DNL Amazon Kinesis]目的地中選取了三個對象，且四個屬性對應至該目的地。

![Amazon Kinesis目的地資料流](../../assets/catalog/http/profile-export-example-dataflow.png)

設定檔匯出至目的地的方式，可由符合或結束&#x200B;*三個對應區段*&#x200B;之一的設定檔來決定。 不過，在資料匯出中，`segmentMembership`物件（請參閱下方的[匯出的資料](#exported-data)區段）可能會顯示其他未對應的對象，如果該特定設定檔為其成員，且這些對象與觸發匯出的對象共用相同的合併原則。 如果設定檔符合&#x200B;**擁有DeLorean Cars的客戶**&#x200B;對象的資格，但同時也是&#x200B;**觀看的「回到未來」**&#x200B;電影和&#x200B;**科幻迷**&#x200B;對象的成員，則其他這兩個對象也將出現在資料匯出的`segmentMembership`物件中，即使這些對象未對應到資料流中，前提是這些對象與&#x200B;**擁有DeLorean Cars的客戶**&#x200B;區段共用相同的合併原則。

從設定檔屬性的角度來看，對上述四個對應屬性所做的任何變更將決定目的地匯出，而且設定檔上存在的四個對應屬性中的任何一個都會出現在資料匯出中。

## 歷史資料回填 {#historical-data-backfill}

當您新增對象至現有目的地，或當您建立新目的地並將對象對應至該目的地時，Experience Platform會將歷史對象資格資料匯出至該目的地。 在&#x200B;*之前新增了對象到目的地的符合對象*&#x200B;資格的設定檔，大約會在一小時內匯出到目的地。

## 匯出的資料 {#exported-data}

您匯出的[!DNL Experience Platform]資料以JSON格式登陸您的[!DNL Amazon Kinesis]目的地。 例如，下列匯出包含符合特定區段資格的設定檔、是另一個兩個區段的成員，且已退出另一個區段。 匯出也包含設定檔屬性的名字、姓氏、出生日期和個人電子郵件地址。 此設定檔的身分識別為ECID和電子郵件。

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

根據您在&#x200B;**[!UICONTROL 包含區段名稱]**&#x200B;和&#x200B;**[!UICONTROL 包含區段時間戳記]**&#x200B;選項的連線目的地流程中選取的UI設定，以下是匯出資料的更多範例：

+++ 下列資料匯出範例包含`segmentMembership`區段中的對象名稱

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

+++ 以下資料匯出範例包含`segmentMembership`區段中的對象時間戳記

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
>* [使用Flow Service API連線至Amazon Kinesis並啟用資料](../../api/streaming-destinations.md)
>* [Azure事件中樞目的地](./azure-event-hubs.md)
>* [目的地型別和類別](../../destination-types.md)
