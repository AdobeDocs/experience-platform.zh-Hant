---
title: Twitter自訂對象連線
description: 在Twitter中鎖定您現有的追隨者和客戶，並透過啟用您在Adobe Experience Platform中建立的對象來建立相關的再行銷活動
exl-id: fd244e58-cd94-4de7-81e4-c321eb673b65
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 5%

---

# [!DNL Twitter Custom Audiences]個連線

## 概觀 {#overview}

在Twitter中鎖定您現有的追隨者和客戶，並透過啟用您在Adobe Experience Platform中建立的對象來建立相關的再行銷活動。

## 先決條件 {#prerequisites}

設定[!DNL Twitter Custom Audiences]目的地之前，請務必檢閱下列需要符合的Twitter必要條件。

1. 您的[!DNL Twitter Ads]帳戶必須符合廣告資格。 新[!DNL Twitter Ads]帳戶在建立後的前2週內不符合廣告資格。
2. 您在[!DNL Twitter Audience Manager]中授權存取的Twitter使用者帳戶必須啟用&#x200B;*[!DNL Partner Audience Manager]*&#x200B;許可權。

## 支援的身分 {#supported-identities}

[!DNL Twitter Custom Audiences]支援下表所述的身分啟用。 深入瞭解[身分](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=zh-Hant#getting-started)。

| 目標身分 | 說明 | 考量事項 |
|---|---|---|
| device_id | IDFA/AdID/Android ID | Adobe Experience Platform支援廣告商適用的Google Advertising ID (GAID)和Apple ID (IDFA)。 請在目的地啟用工作流程的[對應步驟](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping)中，對應來源結構描述的這些名稱空間和/或屬性。 |
| 電子郵件 | 使用者的電子郵件地址 | 請將純文字電子郵件地址和SHA256雜湊電子郵件地址對應至此欄位。 當您的來源欄位包含未雜湊的屬性時，請核取&#x200B;**[!UICONTROL 套用轉換]**&#x200B;選項，讓[!DNL Experience Platform]在啟用時自動雜湊資料。 如果您將客戶電子郵件地址雜湊再上傳至Adobe Experience Platform，請注意，這些身分必須使用SHA256進行雜湊處理，不可使用Salt。 |

{style="table-layout:auto"}

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
| 匯出類型 | **[!UICONTROL 對象匯出]** | 您正使用Twitter自訂對象目的地中使用的識別碼匯出對象的所有成員。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 根據對象評估在Experience Platform中更新設定檔後，聯結器會立即將更新傳送至下游的目標平台。 深入瞭解[串流目的地](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## 使用案例 {#use-cases}

為協助您更清楚瞭解您應如何及何時使用[!DNL Twitter Custom Audiences]目的地，以下是Adobe Experience Platform客戶可藉由使用此目的地解決的範例使用案例。

### 使用案例#1

在Twitter中鎖定您現有的追隨者和客戶，並在Twitter中啟用您在Adobe Experience Platform中建立的對象作為[!DNL List Custom Audiences]，以建立相關的再行銷活動。

## 連線到目的地 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要&#x200B;**[!UICONTROL 檢視目的地]**&#x200B;和&#x200B;**[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要連線到此目的地，請依照[目的地組態教學課程](../../ui/connect-destination.md)中所述的步驟進行。 在設定目標工作流程中，填寫以下兩個區段中列出的欄位。

### 驗證目標 {#authenticate}

1. 在目的地目錄中尋找[!DNL Twitter Custom Audiences]目的地，並選取&#x200B;**[!UICONTROL 設定]**。
2. 選取&#x200B;**[!UICONTROL 連線到目的地]**。
   ![驗證LinkedIn](/help/destinations/assets/catalog/social/twitter/authenticate-twitter-destination.png)
3. 輸入您的Twitter認證，並選取&#x200B;**登入**。

### 填寫目標詳細資訊 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_twitter_accountid"
>title="帳戶 ID"
>abstract="您的 Twitter 廣告帳戶 ID。這可以在您的 Twitter 廣告設定中找到。"

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。

* **[!UICONTROL 名稱]**：您日後可辨識此目的地的名稱。
* **[!UICONTROL 描述]**：可協助您日後識別此目的地的描述。
* **[!UICONTROL 帳戶識別碼]**：您的[!DNL Twitter Ads]帳戶識別碼。 您可以在您的[!DNL Twitter Ads]設定中找到此專案。

>[!IMPORTANT]
>
>請勿使用特殊字元(+ &amp; ， % ： ； @ / = ？ $ \n)在對象、說明和對象對應名稱中。 如果您的Experience Platform對象名稱包含這些字元，請先移除這些字元，然後再將對象對應至Twitter目的地。

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱[使用UI訂閱目的地警示](../../ui/alerts.md)的指南。

當您完成提供目的地連線的詳細資訊後，請選取&#x200B;**[!UICONTROL 下一步]**。

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要&#x200B;**[!UICONTROL 檢視目的地]**、**[!UICONTROL 啟用目的地]**、**[!UICONTROL 檢視設定檔]**&#x200B;和&#x200B;**[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。
>* 若要匯出&#x200B;*身分*，您需要&#x200B;**[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions)。<br> ![選取工作流程中反白的身分名稱空間，以啟用目的地的對象。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以啟用目的地的對象。"){width="100" zoomable="yes"}

閱讀[將設定檔和對象啟用至串流對象匯出目的地](/help/destinations/ui/activate-segment-streaming-destinations.md)，以瞭解啟用此目的地對象的指示。

### 對應考量事項 {#mapping-considerations}

將受眾對應至Twitter時，請提供人類看得懂的受眾對應名稱。 建議您使用與Experience Platform區段相同的名稱。

## 資料使用與控管 {#data-usage-governance}

處理您的資料時，所有[!DNL Adobe Experience Platform]目的地都符合資料使用原則。 如需[!DNL Adobe Experience Platform]如何強制資料控管的詳細資訊，請參閱[資料控管概觀](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=zh-Hant)。

## 其他資源 {#additional-resources}

有關Twitter中[!DNL List Custom Audiences]的詳細資訊，請參閱[Twitter檔案](https://business.twitter.com/en/help/campaign-setup/campaign-targeting/custom-audiences/lists.html)。
