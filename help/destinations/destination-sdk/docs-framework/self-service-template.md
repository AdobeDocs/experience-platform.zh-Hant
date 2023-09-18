---
title: 檔案自助範本//將取代為您的目的地名稱
description: 使用此範本為Adobe Experience Platform目錄中的目的地建立公開檔案。//以總覽區段中的段落取代
exl-id: 99700474-8bf6-4176-acc1-38814e17c995
source-git-commit: afcb5f80edaa4d68ba167123feb2ba9060469243
workflow-type: tm+mt
source-wordcount: '1640'
ht-degree: 1%

---

# 您的目的地連線 {#your-destination}

*瀏覽此範本時，取代或刪除所有斜體段落（從此段落開始）。*

*首先在頁面頂端更新中繼資料（標題和說明）。 請忽略此頁面上的所有UICONTROL執行個體。 此標籤可協助我們的機器翻譯流程將頁面正確翻譯為我們支援的多種語言。 我們會在您提交檔案後，新增標籤至檔案。*

>[!IMPORTANT]
>
>* 依照範本中列出的順序，填入此範本中的所有區段。
>* 此範本很少根據合作夥伴意見更新。 開始編寫目的地的檔案之前，請確定您已下載 [最新版本的範本](../assets/docs-framework/yourdestination-template.zip).

## 概觀 {#overview}

*提供貴公司的簡短概觀，包括其對客戶的價值。 加入產品檔案首頁的連結，以進一步閱讀。*

>[!IMPORTANT]
>
>此目的地聯結器和檔案頁面是由 *您的目的地* 團隊。 如有任何查詢或更新要求，請直接聯絡他們： *插入連結，或是連絡您取得更新的電子郵件地址，例如 `support@YourDestination.com`.*

## 使用案例 {#use-cases}

為了協助您更清楚瞭解您應如何及何時使用 *您的目的地* 目的地，以下是Adobe Experience Platform客戶可以使用此目的地解決的範例使用案例。

### 使用案例#1 {#use-case-1}

*若為行動訊息平台：*

*一個家用出租與銷售平台想要將行動通知推播到客戶的Android和iOS裝置，以便通知他們之前搜尋租用的區域有100個更新的清單。*

### 使用案例#2 {#use-case-2}

*若為社交網路平台：*

*運動服裝品牌想要透過其社群媒體帳戶觸及現有客戶。 服飾品牌可以從他們自己的CRM擷取電子郵件地址到Adobe Experience Platform，從他們自己的離線資料建立對象，並將這些對象傳送到YourDestination，以在其客戶的社群媒體摘要中顯示廣告。*

## 先決條件 {#prerequisites}

*在本節新增客戶在Adobe Experience Platform使用者介面中開始設定目的地之前需要注意的任何相關資訊。 這可能為：*

* *需要新增至允許清單*
* *電子郵件雜湊的需求*
* *任何您這邊的帳戶細節*
* *如何取得API金鑰以連線至您的平台*

*如果對客戶有幫助，您可以連結至相關檔案。*

## 支援的身分 {#supported-identities}

*在此區段中新增目的地支援之身分的相關資訊。 我們已在表格中預先填入了一些標準值。 刪除未套用至您的目的地的值和任何未預先填入的值。*

*您的目的地* 支援下表所述的身分啟用。 進一步瞭解 [身分](/help/identity-service/namespaces.md).

| 目標身分 | 說明 | 考量事項 |
|---|---|---|
| GAID | Google廣告ID | 當您的來源身分是GAID名稱空間時，請選取GAID目標身分。 |
| IDFA | 廣告商適用的Apple ID | 當您的來源身分是IDFA名稱空間時，請選取IDFA目標身分。 |
| ECID | Experience Cloud ID | 代表ECID的名稱空間。 此名稱空間也可以以下列别名表示：「Adobe Marketing Cloud ID」、「Adobe Experience Cloud ID」、「Adobe Experience Platform ID」。 請閱讀以下檔案： [ECID](/help/identity-service/ecid.md) 以取得詳細資訊。 |
| phone_sha256 | 使用SHA256演演算法雜湊的電話號碼 | Adobe Experience Platform同時支援純文字和SHA256雜湊電話號碼。 當來源欄位包含未雜湊屬性時，請核取 **[!UICONTROL 套用轉換]** 選項，擁有 [!DNL Platform] 啟動時自動雜湊資料。 |
| email_lc_sha256 | 使用SHA256演演算法雜湊的電子郵件地址 | Adobe Experience Platform同時支援純文字和SHA256雜湊電子郵件地址。 當來源欄位包含未雜湊屬性時，請核取 **[!UICONTROL 套用轉換]** 選項，擁有 [!DNL Platform] 啟動時自動雜湊資料。 |
| extern_id | 自訂使用者ID | 當您的來源身分是自訂名稱空間時，請選取此目標身分。 |

{style="table-layout:auto"}

## 支援的對象 {#supported-audiences}

*在此區段中新增目的地所支援對象的相關資訊。 我們已在表格中預先填入了一些標準值。 使用 `✓` 和 `X` 標示此目的地是否支援您的對象型別的字元。*

本節說明您可以將哪些型別的對象匯出至此目的地。

| 對象來源 | 支援 | 說明 |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ (A) | 透過Experience Platform產生的對象 [分段服務](../../../segmentation/home.md). |
| 自訂上傳 | X | 受眾 [已匯入](../../../segmentation/ui/overview.md#import-audience) 從CSV檔案Experience Platform為。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

*在表格中，只保留與目的地相對應的行。 您應該有一行用於匯出型別，另一行用於匯出頻率。 刪除不適用於目的地的值。*

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出型別 | **[!UICONTROL 對象匯出]** | 您正在匯出某個對象的所有成員，而這些成員中都有用於的識別碼（名稱、電話號碼或其他）。 *您的目的地* 目的地。 |
| 匯出型別 | **[!UICONTROL 以設定檔為基礎]** | 您正在匯出區段的所有成員，以及所需的結構描述欄位（例如：電子郵件地址、電話號碼、姓氏），如 [目的地啟用工作流程](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes). |
| 匯出型別 | **[!UICONTROL 資料集匯出]** | 您正在匯出原始資料集，這些資料集未依對象興趣或資格進行分組或建構。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 一旦根據對象評估在Experience Platform中更新了設定檔，聯結器就會將更新傳送至下游的目的地平台。 深入瞭解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |
| 匯出頻率 | **[!UICONTROL 批次]** | 批次目的地會以三、六、八、十二或二十四小時的增量將檔案匯出至下游平台。 深入瞭解 [批次檔案型目的地](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## 連線到目的地 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md). 在設定目標工作流程中，填寫以下兩個區段中列出的欄位。

### 驗證到目的地 {#authenticate}

*新增客戶在對您的目的地進行驗證時必須填寫的欄位。 這些欄位會因目的地而異，視您在Destination SDK中的設定而定。 目的地的欄位可能與下方所列的欄位不同。 請一併加入類似下列範例熒幕擷圖的熒幕擷圖。*

若要向目的地進行驗證，請填寫必填欄位並選取 **[!UICONTROL 連線到目的地]**.

![顯示如何驗證至目的地的範例熒幕擷圖](../assets/docs-framework/authenticate-destination.png)

* **[!UICONTROL 持有人權杖]**：填寫持有人權杖以對目的地進行驗證。

### 填寫目的地詳細資料 {#destination-details}

*新增客戶在設定新目的地時必須填寫的欄位。 這些欄位會因目的地而異，視您在Destination SDK中的設定而定。 目的地的欄位可能與下方所列的欄位不同。 請一併加入類似下列範例熒幕擷圖的熒幕擷圖。*

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。

![顯示如何填寫目的地詳細資料的熒幕擷取畫面範例](../assets/docs-framework/configure-destination-details.png)

* **[!UICONTROL 名稱]**：您日後可辨識此目的地的名稱。
* **[!UICONTROL 說明]**：可協助您日後識別此目的地的說明。
* **[!UICONTROL 帳戶ID]**：您的 *您的目的地* 帳戶ID。

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需有關警示的詳細資訊，請閱讀以下指南： [使用UI訂閱目的地警報](../../ui/alerts.md).

當您完成提供目的地連線的詳細資訊時，請選取「 」 **[!UICONTROL 下一個]**.

## 啟用此目的地的對象 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。
>* 要匯出 *身分*，您需要 **[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions). <br> ![選取工作流程中反白顯示的身分名稱空間，以將對象啟用至目的地。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以將對象啟用至目的地。"){width="100" zoomable="yes"}

*適當刪除 — 如果您正在記錄新的串流目的地，請保留下方第一段。 如果您要記錄以檔案為基礎的新目的地，請保留第二段。 如果您要記錄匯出資料集的目的地，請保留第三段。*

讀取 [將設定檔和受眾啟用至串流受眾匯出目標](/help/destinations/ui/activate-segment-streaming-destinations.md) 以取得啟用此目的地對象的指示。

讀取 [啟用對象資料至批次設定檔匯出目的地](/help/destinations/ui/activate-batch-profile-destinations.md) 以取得啟用此目的地對象的指示。

讀取 [(Beta)匯出資料集](/help/destinations/ui/export-datasets.md) 以取得將資料集匯出至此目的地的詳細指示。

### 對應屬性和身分 {#map}

*在啟動工作流程的「對應」步驟中，新增來源與目標欄位之間支援的對應相關資訊。 您的目的地可能支援匯出設定檔屬性、身分名稱空間或兩者。 部分欄位可能為必填欄位。 Target屬性可為預先定義或自訂。 指出重要警告並使用範例，最好搭配熒幕擷取畫面。 您可參考的兩個目的地頁面範例是：*

* *[Pega](/help/destinations/catalog/personalization/pega.md#mapping-example)*
* *[梅迪亞文](/help/destinations/catalog/voice/medallia-connector.md#map)*

## 匯出的資料/驗證資料匯出 {#exported-data}

*新增段落來說明如何將資料匯出至您的目的地。 這可協助客戶確保已正確與您的目的地整合。 例如，您可以提供類似以下的JSON範例。 或者，您可以提供目的地介面的熒幕擷取畫面和資訊，說明客戶應如何預期目標平台中的對象填入。*

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

全部 [!DNL Adobe Experience Platform] 處理您的資料時，目的地符合資料使用原則。 如需如何操作的詳細資訊 [!DNL Adobe Experience Platform] 強制執行資料控管，讀取 [資料控管概觀](/help/data-governance/home.md).

## 其他資源 {#additional-resources}

*您可以提供產品檔案的進一步連結，或您認為對客戶取得成功很重要的任何其他資源。*