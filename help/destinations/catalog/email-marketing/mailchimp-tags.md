---
title: Mailchimp標籤
description: Mailchimp標籤目的地可讓您匯出帳戶資料，並在Mailchimp中將其啟用，以便與聯絡人互動。
last-substantial-update: 2024-02-20T00:00:00Z
exl-id: 0f278ca8-4fcf-4c47-b538-9cffa45a3d90
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1646'
ht-degree: 2%

---

# [!DNL Mailchimp Tags]個連線

[[!DNL Mailchimp]](https://mailchimp.com) *（也稱為[!DNL Intuit Mailchimp]）*&#x200B;是一種熱門的行銷自動化平台和電子郵件行銷服務，企業使用它來管理與聯絡人&#x200B;*（客戶、客戶或其他感興趣的當事方）*&#x200B;的交談，使用郵寄清單和電子郵件行銷活動。

[!DNL Mailchimp Tags]使用[對象](https://mailchimp.com/help/getting-started-audience/)和[標籤](https://mailchimp.com/help/getting-started-tags/)來管理您的連絡資訊。 標籤是標籤，您可以使用這些標籤來組織您的連絡人，並在[!DNL Mailchimp]中將其標示為內部分類。

相較於您根據連絡人的興趣和喜好來排序連絡人的[!DNL Mailchimp Interest Categories]，[!DNL Mailchimp Tags]旨在管理您的連絡人可能感興趣的主題訂閱。 *請注意，Experience Platform也有[!DNL Mailchimp Interest Categories]的連線，您可以在[[!DNL Mailchimp Interest Categories]](/help/destinations/catalog/email-marketing/mailchimp-interest-categories.md)頁面上檢視。*

此[!DNL Adobe Experience Platform] [目的地](/help/destinations/home.md)利用[[!DNL Mailchimp batch subscribe or unsubscribe API]](https://mailchimp.com/developer/marketing/api/lists/batch-subscribe-or-unsubscribe/)端點。 在新對象中啟用現有[!DNL Mailchimp]對象中的現有[!DNL Mailchimp]連絡人&#x200B;**後，您可以**&#x200B;新增連絡人&#x200B;**或**&#x200B;更新這些連絡人的標籤。 [!DNL Mailchimp Tags]使用從Platform選取的對象名稱做為[!DNL Mailchimp]內的標籤名稱。

## 使用案例 {#use-cases}

為協助您更清楚瞭解您應如何及何時使用[!DNL Mailchimp Tags]目的地，以下是Adobe Experience Platform客戶可藉由使用此目的地解決的範例使用案例。

### 傳送電子郵件給行銷活動的連絡人 {#use-case-send-emails}

組織的銷售部門想要將電子郵件行銷活動廣播至已組織的聯絡人清單。 連絡人清單是從不同的離線來源以批次方式收到，因此需要加以追蹤。 團隊會識別現有[!DNL Mailchimp]對象，並開始建置將每個清單中的連絡人加入其中的Experience Platform對象。 將這些對象傳送至[!DNL Mailchimp Tags]後，如果所選[!DNL Mailchimp]對象中不存在任何連絡人，則會新增連絡人並附上相關標籤，其中包含連絡人所屬的對象名稱。 如果[!DNL Mailchimp]對象中已存在任何連絡人，則會新增一個具有對象名稱的新標籤。 由於標籤會顯示在[!DNL Mailchimp]中，因此可輕鬆識別離線來源。 資料傳送至[!DNL Mailchimp]後，他們會傳送行銷活動電子郵件給對象。

## 先決條件 {#prerequisites}

請參閱以下各節，瞭解在Experience Platform和[!DNL Mailchimp]中需要設定的任何先決條件，以及使用[!DNL Mailchimp Tags]目的地之前需要收集的資訊。

### Experience Platform的必要條件 {#prerequisites-in-experience-platform}

在啟用資料至[!DNL Mailchimp Tags]目的地之前，您必須在[!DNL Experience Platform]中建立[結構描述](/help/xdm/schema/composition.md)、[資料集](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en)和[對象](https://experienceleague.adobe.com/docs/platform-learn/tutorials/audiences/create-audiences.html)。

### [!DNL Mailchimp Tags]目的地的先決條件 {#prerequisites-destination}

若要將資料從Platform匯出至您的[!DNL Mailchimp Tags]帳戶，請注意下列必要條件：

#### 您必須擁有[!DNL Mailchimp]帳戶 {#prerequisites-account}

建立[!DNL Mailchimp Tags]目的地之前，您必須先確定您有[!DNL Mailchimp]帳戶。 如果您還沒有帳號，請造訪[[!DNL Mailchimp] 註冊頁面](https://login.mailchimp.com/signup/)來註冊並建立您的帳號。

#### 收集[!DNL Mailchimp] API金鑰 {#gather-credentials}

您需要您的[!DNL Mailchimp] **API金鑰**，以針對您的[!DNL Mailchimp]帳戶驗證[!DNL Mailchimp Interest Categories]目的地。 當您[驗證目的地](#authenticate)時，**API金鑰**&#x200B;將用作&#x200B;**密碼**。

如果您沒有&#x200B;**API金鑰**，請登入您的[!DNL Mailchimp]帳戶，並參閱[!DNL Mailchimp]有關[如何產生API金鑰](https://mailchimp.com/developer/marketing/guides/quick-start/#generate-your-api-key)的檔案。

API金鑰的範例為`0123456789abcdef0123456789abcde-us14`。

>[!IMPORTANT]
>
>如果您產生&#x200B;**API金鑰**，請將其記下，因為您無法在產生後存取它。

#### 識別您的[!DNL Mailchimp]資料中心 {#identify-data-center}

接下來，您必須識別您的[!DNL Mailchimp]資料中心。 若要這麼做，請登入您的[!DNL Mailchimp]帳戶，並導覽至您帳戶的&#x200B;**API金鑰區段**。

資料中心ID是您在瀏覽器中看到的URL的第一部分。 如果URL是&#x200B;*https://`us14`.mailchimp.com/account/api/*，則資料中心是`us14`。

資料中心ID也會以&#x200B;*key-dc*&#x200B;的格式附加至您的API金鑰；例如，若您的API金鑰為`0123456789abcdef0123456789abcde-us14`，則資料中心為`us14`。

寫下資料中心值&#x200B;*（`us14`在此範例中）*。 當您[填寫目的地詳細資料](#destination-details)時，將需要此值。

若您需要進一步的指引，請參閱[[!DNL Mailchimp] 基礎檔案](https://mailchimp.com/developer/marketing/docs/fundamentals/#api-structure)。

### 護欄 {#guardrails}

請參閱[!DNL Mailchimp] [速率限制](https://mailchimp.com/developer/marketing/docs/fundamentals/#api-limits)，以取得[!DNL Mailchimp] API所設限制的詳細資訊。

## 支援的身分 {#supported-identities}

[!DNL Mailchimp]支援下表所述的身分啟用。 深入瞭解[身分](/help/identity-service/features/namespaces.md)。

| 目標身分 | 說明 | 考量事項 |
|---|---|---|
| 電子郵件 | 連絡人的電子郵件地址。 | 強制 |

{style="table-layout:auto"}

## 支援的對象 {#supported-audiences}

本節說明您可以將哪些型別的對象匯出至此目的地。

| 對象來源 | 支援 | 說明 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ (A) | 透過Experience Platform[細分服務](../../../segmentation/home.md)產生的對象。 |
| 自訂上傳 | ✓ (A) | 對象[從CSV檔案匯入](../../../segmentation/ui/audience-portal.md#import-audience)至Experience Platform。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 以設定檔為基礎]** | <ul><li>您正在匯出對象的所有成員，以及所需的結構描述欄位&#x200B;*（例如：電子郵件地址、電話號碼、姓氏）* （根據您的欄位對應）。</li><li> 對於在Platform中選取的每個對象，相對應的[!DNL Mailchimp Tags]區段狀態會以Platform中的對象狀態更新。</li></ul> |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 一旦根據對象評估在Experience Platform中更新了設定檔，聯結器就會將更新傳送至下游的目的地平台。 深入瞭解[串流目的地](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## 連線到目標 {#connect}

>[!IMPORTANT]
>
>若要連線到目的地，您需要&#x200B;**[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要連線到此目的地，請依照[目的地組態教學課程](../../ui/connect-destination.md)中所述的步驟進行。 在設定目標工作流程中，填寫以下兩個區段中列出的欄位。

在&#x200B;**[!UICONTROL 目的地]** > **[!UICONTROL 目錄]**&#x200B;內，搜尋[!DNL Mailchimp Tags]。 或者，您可以在&#x200B;**[!UICONTROL 電子郵件行銷]**&#x200B;類別下找到它。

### 驗證目標 {#authenticate}

若要驗證到目的地，請填寫下列必填欄位，然後選取&#x200B;**[!UICONTROL 連線到目的地]**。

| 欄位 | 說明 |
| --- | --- |
| **[!UICONTROL 使用者名稱]** | 您的[!DNL Mailchimp]使用者名稱。 |
| **[!UICONTROL 密碼]** | 您的[!DNL Mailchimp] **API金鑰**&#x200B;已在[收集 [!DNL Mailchimp] 認證](#gather-credentials)區段中記下。<br>您的API金鑰採用`{KEY}-{DC}`的形式，其中`{KEY}`部分參考在[[!DNL Mailchimp] API金鑰](#gather-credentials)部分中記下的值，而`{DC}`部分參考[[!DNL Mailchimp] 資料中心](#identify-data-center)。 <br>您可以提供`{KEY}`部分或整個表單。<br>例如，若您的API金鑰是&#x200B;<br>*`0123456789abcdef0123456789abcde-us14`*，<br>，您可以提供&#x200B;*`0123456789abcdef0123456789abcde`*或&#x200B;*`0123456789abcdef0123456789abcde-us14`*作為值。 |

{style="table-layout:auto"}

![平台UI熒幕擷圖顯示如何驗證。](../../assets/catalog/email-marketing/mailchimp-tags/authenticate-destination.png)

如果提供的詳細資料有效，UI會顯示帶有綠色勾號的&#x200B;**[!UICONTROL 已連線]**&#x200B;狀態。 然後您可以繼續下一步驟。

### 填寫目標詳細資訊 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。

![顯示目的地詳細資訊的平台UI熒幕擷取畫面。](../../assets/catalog/email-marketing/mailchimp-tags/destination-details.png)

| 欄位 | 說明 |
| --- | --- |
| **[!UICONTROL 名稱]** | 您日後可辨識此目的地的名稱。 |
| **[!UICONTROL 說明]** | 可協助您日後識別此目的地的說明。 |
| **[!UICONTROL 資料中心]** | 您的[!DNL Mailchimp]帳戶`data center`。 如需任何指引，請參閱[識別 [!DNL Mailchimp] 資料中心](#identify-data-center)區段。 |
| **[!UICONTROL 對象名稱（請先輸入資料中心）]** | 在您輸入&#x200B;**[!UICONTROL 資料中心]**&#x200B;後，此下拉式清單會自動填入您[!DNL Mailchimp]帳戶中的對象名稱。 選取您要以Platform資料更新的對象。 |

{style="table-layout:auto"}

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱[使用UI訂閱目的地警示](../../ui/alerts.md)的指南。

當您完成提供目的地連線的詳細資訊後，請選取&#x200B;**[!UICONTROL 下一步]**。

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要&#x200B;**[!UICONTROL 檢視目的地]**、**[!UICONTROL 啟用目的地]**、**[!UICONTROL 檢視設定檔]**&#x200B;和&#x200B;**[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。
>* 若要匯出&#x200B;*身分*，您需要&#x200B;**[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions)。<br> ![選取工作流程中反白的身分名稱空間，以啟用目的地的對象。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以啟用目的地的對象。"){width="100" zoomable="yes"}

閱讀[啟用串流目的地的對象](/help/destinations/ui/activate-segment-streaming-destinations.md)，以取得啟用此目的地對象的指示。

### 對應考量事項和範例 {#mapping-considerations-example}

若要將對象資料從Adobe Experience Platform正確傳送至[!DNL Mailchimp Tags]目的地，您必須完成欄位對應步驟。 對應包括在Platform帳戶中的Experience Data Model (XDM)結構描述欄位與來自目標目的地的對應對應專案之間建立連結。

若要將您的XDM欄位正確對應到[!DNL Mailchimp Tags]目的地欄位，請遵循下列步驟：

1. 在&#x200B;**[!UICONTROL 對應]**&#x200B;步驟中，選取&#x200B;**[!UICONTROL 新增對應]**。 您會在畫面上看到新的對應列。
1. 在&#x200B;**[!UICONTROL 選取來源欄位]**&#x200B;視窗中，選擇&#x200B;**[!UICONTROL 選取身分名稱空間]**&#x200B;並選取`Email`身分名稱空間。

   ![Platform UI熒幕擷取畫面顯示Source欄位，作為來自身分名稱空間的電子郵件。](../../assets/catalog/email-marketing/mailchimp-tags/source-field.png)

1. 在&#x200B;**[!UICONTROL 選取目標欄位]**&#x200B;視窗中，選擇&#x200B;**[!UICONTROL 選取身分名稱空間]**&#x200B;並選取`Email`身分名稱空間。

   ![Platform UI熒幕擷取畫面，將Target欄位作為來自身分名稱空間的電子郵件。](../../assets/catalog/email-marketing/mailchimp-tags/target-field.png)

   您的XDM設定檔結構描述與[!DNL Mailchimp Tags]之間的對應將會如下所示：
| Source欄位 | 目標欄位 | 強制 |
| — | — | — |
|`IdentityMap: Email`|`Identity: Email`| 是 |

   具有已完成對應的範例如下所示：
   ![顯示欄位對應的平台UI熒幕擷圖範例。](../../assets/catalog/email-marketing/mailchimp-tags/mappings.png)

當您完成提供目的地連線的對應時，請選取&#x200B;**[!UICONTROL 下一步]**。

## 驗證資料匯出 {#exported-data}

若要驗證您是否已正確設定目的地，請遵循下列步驟：

1. 登入您的[[!DNL Mailchimp]](https://login.mailchimp.com/)帳戶。 然後導覽至&#x200B;**[!DNL Audience]** > **[!DNL All Contacts]**頁面，並檢查對象中的連絡人是否已新增，以及對象中的連絡人是否已使用對象名稱進行更新。
   ![顯示「對象」頁面的Mailchimp UI熒幕擷圖。](../../assets/catalog/email-marketing/mailchimp-tags/contacts.png)

## 資料使用與控管 {#data-usage-governance}

處理您的資料時，所有[!DNL Adobe Experience Platform]目的地都符合資料使用原則。 如需[!DNL Adobe Experience Platform]如何強制資料控管的詳細資訊，請參閱[資料控管概觀](/help/data-governance/home.md)。

## 錯誤與疑難排解 {#errors-and-troubleshooting}

請參閱[[!DNL Mailchimp] 錯誤頁面](https://mailchimp.com/developer/marketing/docs/errors/)，以取得包含說明的狀態和錯誤碼完整清單。

## 其他資源 {#additional-resources}

[!DNL Mailchimp]檔案中的其他實用資訊如下：
* [開始使用 [!DNL Mailchimp]](https://mailchimp.com/help/getting-started-with-mailchimp/)
* [開始使用對象](https://mailchimp.com/help/getting-started-audience/)
* [建立對象](https://mailchimp.com/help/create-audience/)
* [開始使用標籤](https://mailchimp.com/help/getting-started-tags/)
* [行銷API](https://mailchimp.com/developer/marketing/api/)
