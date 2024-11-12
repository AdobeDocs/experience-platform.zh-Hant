---
title: 檔案自助範本//將取代為您的目的地名稱
description: 使用此範本為Adobe Experience Platform目錄中的目的地建立公開檔案。//以總覽區段中的段落取代
exl-id: 99700474-8bf6-4176-acc1-38814e17c995
source-git-commit: 10521602a5871419c0c49d54c8ed250af39a78a4
workflow-type: tm+mt
source-wordcount: '1645'
ht-degree: 2%

---

# 您的目的地連線 {#your-destination}

*當您瀏覽此範本時，請取代或刪除所有斜體字的段落（從此段落開始）。*

*從更新頁面頂端的中繼資料（標題和說明）開始。 請忽略此頁面上的所有UICONTROL執行個體。 此標籤可協助我們的機器翻譯流程將頁面正確翻譯為我們支援的多種語言。 我們會在您提交檔案後新增標籤。*

>[!IMPORTANT]
>
>* 依照範本中列出的順序，填入此範本中的所有區段。
>* 此範本很少根據合作夥伴意見更新。 在您開始編寫目的地的檔案之前，請確定您已下載範本的[最新版本](../assets/docs-framework/yourdestination-template.zip)。

## 概觀 {#overview}

*提供您公司的簡短概觀，包括它提供給客戶的價值。 加入產品檔案首頁的連結，以便進一步閱讀。*

>[!IMPORTANT]
>
>此目的地聯結器和檔案頁面是由&#x200B;*YourDestination*&#x200B;團隊建立和維護。 若有任何查詢或更新要求，請直接連絡他們： *插入連結或電子郵件地址，您可以連絡此處取得更新，例如`support@YourDestination.com`。*

## 使用案例 {#use-cases}

為協助您更清楚瞭解您應如何及何時使用&#x200B;*YourDestination*&#x200B;目的地，以下是Adobe Experience Platform客戶可藉由使用此目的地解決的範例使用案例。

### 使用案例#1 {#use-case-1}

*針對行動訊息平台：*

*住家租賃與銷售平台想要將行動通知推播到客戶的Android和iOS裝置，以告知他們之前搜尋租賃的區域中有100個更新的清單。*

### 使用案例#2 {#use-case-2}

*若為社交網路平台：*

*運動服裝品牌想要透過其社群媒體帳戶觸及現有客戶。 服飾品牌可以從自己的CRM擷取電子郵件地址至Adobe Experience Platform、從自己的離線資料建立對象，並將這些對象傳送至YourDestination，以便在客戶的社群媒體摘要中顯示廣告。*

## 先決條件 {#prerequisites}

*在本節中新增客戶在Adobe Experience Platform使用者介面中開始設定目的地之前需要注意的任何相關資訊。 這可能約：*

* *需要新增至允許清單*
* *電子郵件雜湊需求*
* *您這邊的任何帳戶細節*
* *如何取得API金鑰以連線至您的平台*

*如果對客戶有幫助，您可以連結至相關檔案。*

## 支援的身分 {#supported-identities}

*在此區段中新增目的地支援的身分的相關資訊。 我們已在表格中預先填入了一些標準值。 刪除未套用至您的目的地的值和/或新增任何未預先填入的值。*

*YourDestination*&#x200B;支援啟用下表所述的身分。 深入瞭解[身分](/help/identity-service/features/namespaces.md)。

| 目標身分 | 說明 | 考量事項 |
|---|---|---|
| GAID | GOOGLE ADVERTISING ID | 當您的來源身分是GAID名稱空間時，請選取GAID目標身分。 |
| IDFA | 廣告商適用的Apple ID | 當您的來源身分是IDFA名稱空間時，請選取IDFA目標身分。 |
| ECID | Experience Cloud ID | 代表ECID的名稱空間。 此名稱空間也可以以下列别名表示：「Adobe Marketing Cloud ID」、「Adobe Experience Cloud ID」、「Adobe Experience Platform ID」。 如需詳細資訊，請參閱[ECID](/help/identity-service/features/ecid.md)上的下列檔案。 |
| phone_sha256 | 使用SHA256演演算法雜湊的電話號碼 | Adobe Experience Platform同時支援純文字和SHA256雜湊電話號碼。 當您的來源欄位包含未雜湊的屬性時，請核取&#x200B;**[!UICONTROL 套用轉換]**&#x200B;選項，讓[!DNL Platform]在啟用時自動雜湊資料。 |
| email_lc_sha256 | 使用SHA256演演算法雜湊的電子郵件地址 | Adobe Experience Platform同時支援純文字和SHA256雜湊電子郵件地址。 當您的來源欄位包含未雜湊的屬性時，請核取&#x200B;**[!UICONTROL 套用轉換]**&#x200B;選項，讓[!DNL Platform]在啟用時自動雜湊資料。 |
| extern_id | 自訂使用者ID | 當您的來源身分是自訂名稱空間時，請選取此目標身分。 |

{style="table-layout:auto"}

## 支援的對象 {#supported-audiences}

*在此章節新增目的地所支援對象的相關資訊。 我們已在表格中預先填入了一些標準值。 使用`✓`和`X`字元來標示此目的地是否支援您的對象型別。*

本節說明您可以將哪些型別的對象匯出至此目的地。

| 對象來源 | 支援 | 說明 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ (A) | 透過Experience Platform[細分服務](../../../segmentation/home.md)產生的對象。 |
| 自訂上傳 | X | 對象[從CSV檔案匯入](../../../segmentation/ui/audience-portal.md#import-audience)至Experience Platform。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

*在表格中，只保留與目的地相對應的行。 您應該有一行用於匯出型別，另一行用於匯出頻率。 刪除未套用至您的目的地的值。*

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 對象匯出]** | 您正在匯出具有&#x200B;*YourDestination*&#x200B;目的地中所使用之識別碼（名稱、電話號碼或其他）的對象的所有成員。 |
| 匯出類型 | **[!UICONTROL 以設定檔為基礎]** | 您正在匯出對象的所有成員，以及所需的結構描述欄位（例如：電子郵件地址、電話號碼、姓氏），如[目的地啟用工作流程](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes)的選取設定檔屬性畫面中所選。 |
| 匯出類型 | **[!UICONTROL 資料集匯出]** | 您正在匯出原始資料集，這些資料集未依對象興趣或資格進行分組或建構。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 一旦根據對象評估在Experience Platform中更新了設定檔，聯結器就會將更新傳送至下游的目的地平台。 深入瞭解[串流目的地](/help/destinations/destination-types.md#streaming-destinations)。 |
| 匯出頻率 | **[!UICONTROL 批次]** | 批次目的地會以三、六、八、十二或二十四小時的增量將檔案匯出至下游平台。 深入瞭解[批次檔案型目的地](/help/destinations/destination-types.md#file-based)。 |

{style="table-layout:auto"}

## 連線到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要&#x200B;**[!UICONTROL 檢視目的地]**&#x200B;和&#x200B;**[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要連線到此目的地，請依照[目的地組態教學課程](../../ui/connect-destination.md)中所述的步驟進行。 在設定目標工作流程中，填寫以下兩個區段中列出的欄位。

### 驗證目標 {#authenticate}

*新增客戶在對您的目的地進行驗證時必須填寫的欄位。 這些欄位會因目的地而異，視您在Destination SDK中的設定而定。 目的地的欄位可能與下方所列的欄位不同。 請一併加入類似下列範例熒幕擷圖的熒幕擷圖。*

若要驗證到目的地，請填入必填欄位，然後選取&#x200B;**[!UICONTROL 連線到目的地]**。

![顯示如何驗證目的地](../assets/docs-framework/authenticate-destination.png)的範例熒幕擷圖

* **[!UICONTROL 持有人權杖]**：填入持有人權杖以驗證目的地。

### 填寫目標詳細資訊 {#destination-details}

*新增客戶在設定新目的地時必須填寫的欄位。 這些欄位會因目的地而異，視您在Destination SDK中的設定而定。 目的地的欄位可能與下方所列的欄位不同。 請一併加入類似下列範例熒幕擷圖的熒幕擷圖。*

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。

![顯示如何填寫目的地詳細資料的熒幕擷圖範例](../assets/docs-framework/configure-destination-details.png)

* **[!UICONTROL 名稱]**：您日後可辨識此目的地的名稱。
* **[!UICONTROL 描述]**：可協助您日後識別此目的地的描述。
* **[!UICONTROL 帳戶識別碼]**：您的&#x200B;*YourDestination*&#x200B;帳戶識別碼。

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱[使用UI訂閱目的地警示](../../ui/alerts.md)的指南。

當您完成提供目的地連線的詳細資訊後，請選取&#x200B;**[!UICONTROL 下一步]**。

## 啟動此目標的客群 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要&#x200B;**[!UICONTROL 檢視目的地]**、**[!UICONTROL 啟用目的地]**、**[!UICONTROL 檢視設定檔]**&#x200B;和&#x200B;**[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。
>* 若要匯出&#x200B;*身分*，您需要&#x200B;**[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions)。<br> ![選取工作流程中反白的身分名稱空間，以啟用目的地的對象。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以啟用目的地的對象。"){width="100" zoomable="yes"}

*視需要刪除 — 如果您要記錄新的串流目的地，請保留下方第一段。 如果您要記錄以檔案為基礎的新目的地，請保留第二段。 如果您要記錄匯出資料集的目的地，請保留第三段。*

閱讀[將設定檔和對象啟用至串流對象匯出目的地](/help/destinations/ui/activate-segment-streaming-destinations.md)，以瞭解啟用此目的地對象的指示。

讀取[啟用批次設定檔匯出目的地的對象資料](/help/destinations/ui/activate-batch-profile-destinations.md)，以取得啟用此目的地對象的指示。

閱讀[(Beta)匯出資料集](/help/destinations/ui/export-datasets.md)，以取得將資料集匯出至此目的地的詳細指示。

### 對應屬性和身分 {#map}

*在啟動工作流程的[對應]步驟中，新增來源與目標欄位之間支援的對應。 您的目的地可能支援匯出設定檔屬性、身分名稱空間或兩者。 部分欄位可能為必填欄位。 Target屬性可為預先定義或自訂。 指出重要警告並使用範例，最好搭配熒幕擷取畫面。 您可以做為參考的兩個目的地頁面範例是：*

* *[Pega](/help/destinations/catalog/personalization/pega.md#mapping-example)*
* *[Medallia](/help/destinations/catalog/voice/medallia-connector.md#map)*

## 匯出的資料/驗證資料匯出 {#exported-data}

*新增有關資料如何匯出至目的地的段落。 這可協助客戶確保已正確與您的目的地整合。 例如，您可以提供類似以下的JSON範例。 或者，您可以從目的地介面提供熒幕擷取畫面與資訊，顯示客戶預期目標平台中會如何填入對象。*

```
{
  "person": {
    "email": "yourstruly@adobe.com"
  },
  "segmentMembership": {
    "ups": {
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93": {
        "lastQualificationTime": "2020-05-25T21:24:39Z",
        "status": "exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae": {
        "lastQualificationTime": "2020-05-25T23:37:33Z",
        "status": "realized"
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

## 資料使用與控管 {#data-usage-governance}

處理您的資料時，所有[!DNL Adobe Experience Platform]目的地都符合資料使用原則。 如需[!DNL Adobe Experience Platform]如何強制資料控管的詳細資訊，請閱讀[資料控管概觀](/help/data-governance/home.md)。

## 其他資源 {#additional-resources}

*您可以提供產品檔案的進一步連結，或您認為對客戶成功很重要的任何其他資源。*
