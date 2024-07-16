---
title: Mailchimp興趣類別
description: Mailchimp （也稱為Intuit Mailchimp）是一種流行的行銷自動化平台和電子郵件行銷服務，企業使用它來管理與聯絡人（客戶、客戶或其他感興趣的當事方）使用郵寄清單和電子郵件行銷活動。 可使用此連接器根據聯絡人的興趣和偏好將他們排序。
last-substantial-update: 2023-05-24T00:00:00Z
exl-id: bdce8295-7305-4d54-81c1-7fa3e580ce70
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '2299'
ht-degree: 2%

---

# [!DNL Mailchimp Interest Categories]個連線

[[!DNL Mailchimp]](https://mailchimp.com)是熱門的行銷自動化平台和電子郵件行銷服務，企業使用郵寄清單和電子郵件行銷活動，管理與連絡人&#x200B;*（客戶、客戶或其他感興趣的當事方）*&#x200B;的交談。 可使用此連接器根據聯絡人的興趣和偏好將他們排序。

[!DNL Mailchimp Interest Categories]使用[對象](https://mailchimp.com/help/getting-started-audience/)、[群組](https://mailchimp.com/help/getting-started-with-groups/)和興趣類別&#x200B;*（也稱為群組名稱或群組標題）*。 每個[!DNL Mailchimp]群組都是興趣類別的清單。 聯絡人透過您網站上的登錄檔單訂閱一或多個興趣類別時，就會與興趣類別相關聯。 在對象中，您還可以將聯絡人組織成群組，並將其與興趣類別建立關聯，然後可以使用這些群組來建立區段。 您可以使用這些受眾將目標行銷活動電子郵件廣播給訂閱的聯絡人。

<!--
Compared to [!DNL Mailchimp Tags] which you would use for internal classification, [!DNL Mailchimp Interest Categories] is meant to manage subscriptions to topics of interest that your contacts might be interested in. *Note, Experience Platform also has a connection for [!DNL Mailchimp Tags], you can check it out on the [[!DNL Mailchimp Tags]](/help/destinations/catalog/email-marketing/mailchimp-tags.md) page.*
-->

此[!DNL Adobe Experience Platform] [目的地](/help/destinations/home.md)使用[[!DNL Mailchimp batch subscribe or unsubscribe API]](https://mailchimp.com/developer/marketing/api/lists/batch-subscribe-or-unsubscribe/) API來建立[興趣類別](https://mailchimp.com/developer/marketing/api/interest-categories/)，然後將每個所選平台對象的連絡人新增至對應的興趣類別。 您可以&#x200B;**新增連絡人**&#x200B;或&#x200B;**更新現有[!DNL Mailchimp]連絡人的資訊**，然後在新的區段中啟用這些連絡人後，在現有[!DNL Mailchimp]對象中&#x200B;**新增或移除他們想要的群組**。 [!DNL Mailchimp Interest Groups]使用從Platform選取的對象名稱做為[!DNL Mailchimp]內的興趣類別。

## 使用案例 {#use-cases}

為協助您更清楚瞭解您應如何及何時使用[!DNL Mailchimp Interest Categories]目的地，以下是Adobe Experience Platform客戶可藉由使用此目的地解決的範例使用案例。

### 傳送電子郵件給行銷活動的連絡人 {#use-case-send-emails}

一家體育用品網站的銷售部門想要廣播電子郵件行銷活動，給已自我認定對足球感興趣的聯絡人清單。 聯絡人清單在從網站開發團隊收到的資料匯出中被分離為批次，因此需要被追蹤。 團隊會識別現有[!DNL Mailchimp]對象，並開始建置將每個清單中的連絡人加入其中的Experience Platform對象。 將這些對象傳送至[!DNL Mailchimp Interest Categories]後，如果所選[!DNL Mailchimp]對象中不存在任何連絡人，則會將其新增至具有連絡人所屬對象名稱的群組。 如果[!DNL Mailchimp]對象或群組中已有任何連絡人，則會更新其資訊。 資料傳送至[!DNL Mailchimp Interest Categories]後，銷售團隊可以選取行銷活動電子郵件，並傳送給[!DNL Mailchimp]對象中的足球興趣群組。

## 先決條件 {#prerequisites}

請參閱以下各節，瞭解在Experience Platform和[!DNL Mailchimp]中需要設定的任何先決條件，以及使用[!DNL Mailchimp Interest Categories]目的地之前必須收集的資訊。

### Experience Platform的必要條件 {#prerequisites-in-experience-platform}

在啟用資料到[!DNL Mailchimp Interest Categories]目的地之前，您必須在[!DNL Experience Platform]中建立[結構描述](/help/xdm/schema/composition.md)、[資料集](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html)和[區段](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html)。

### [!DNL Mailchimp Interest Categories]目的地的先決條件 {#prerequisites-destination}

若要將資料從Platform匯出至您的[!DNL Mailchimp]帳戶，請注意下列必要條件：

#### 您必須擁有[!DNL Mailchimp]帳戶 {#prerequisites-account}

建立[!DNL Mailchimp Interest Categories]目的地之前，您必須先確定您有[!DNL Mailchimp]帳戶。 如果您還沒有帳戶，請造訪[[!DNL Mailchimp] 註冊頁面](https://login.mailchimp.com/signup/)來註冊並建立您的帳戶。

#### 收集[!DNL Mailchimp] API金鑰 {#gather-credentials}

您需要您的[!DNL Mailchimp] **API金鑰**，以針對您的[!DNL Mailchimp]帳戶驗證[!DNL Mailchimp Interest Categories]目的地。 當您[驗證目的地](#authenticate)時，**API金鑰**&#x200B;將用作&#x200B;**密碼**。

如果您沒有&#x200B;**API金鑰**，請登入您的帳戶並參閱[[!DNL Mailchimp] 產生您的API金鑰](https://mailchimp.com/developer/marketing/guides/quick-start/#generate-your-api-key)檔案以建立金鑰。

API金鑰的範例為`0123456789abcdef0123456789abcde-us14`。

>[!IMPORTANT]
>
>如果您產生&#x200B;**API金鑰**，請將其記下，因為您無法在產生後存取它。

#### 識別[!DNL Mailchimp]資料中心 {#identify-data-center}

接下來，您必須識別您的[!DNL Mailchimp]資料中心。 若要這麼做，請登入您的[!DNL Mailchimp]帳戶，並導覽至您帳戶的&#x200B;**API金鑰區段**。

值是您在瀏覽器中看到的URL的第一部分。 如果URL是&#x200B;*https://`us14`.mailchimp.com/account/api/*，則資料中心是`us14`。

它還以&#x200B;*key-dc*&#x200B;的格式附加至您的API金鑰；如果您的API金鑰是`0123456789abcdef0123456789abcde-us14`，則資料中心是`us14`。

寫下資料中心值&#x200B;*（在此範例中為`us14`）*，當您[填寫目的地詳細資料](#destination-details)時，需要此值。

若您需要進一步的指引，請參閱[[!DNL Mailchimp] 基礎檔案](https://mailchimp.com/developer/marketing/docs/fundamentals/#api-structure)。

### 護欄 {#guardrails}

您的[!DNL Mailchimp]個對象中，每個對象都可以在單一群組或相同對象內數個群組間包含最多60個群組名稱（或興趣類別）。 如需任何必要的說明，請參考[!DNL Mailchimp] [群組](https://mailchimp.com/help/getting-started-with-groups/)。 當您達到此限制時，您會從[!DNL Mailchimp] API收到錯誤回應形式的`400 BAD_REQUEST Cannot have more than 60 interests per list (Across all categories)`訊息。

此外，請參閱[!DNL Mailchimp] [速率限制](https://mailchimp.com/developer/marketing/docs/fundamentals/#api-limits)，以取得有關[!DNL Mailchimp] API所設限制的詳細資訊。

## 支援的身分 {#supported-identities}

[!DNL Mailchimp]支援下表所述的身分啟用。 深入瞭解[身分](/help/identity-service/features/namespaces.md)。

| 目標身分 | 說明 | 考量事項 |
|---|---|---|
| 電子郵件 | 連絡人電子郵件地址 | 強制 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 以設定檔為基礎]** | <ul><li>您正在匯出區段的所有成員，以及所需的結構描述欄位&#x200B;*（例如：電子郵件地址、電話號碼、姓氏）* （根據您的欄位對應）。</li><li> 針對Platform中每個選取的對象，相對應的[!DNL Mailchimp Interest Categories]區段狀態會從Platform更新其對象狀態。</li></ul> |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 當根據對象評估在Experience Platform中更新設定檔時，聯結器會將更新傳送至下游的目標平台。 深入瞭解[串流目的地](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## 連線到目標 {#connect}

>[!IMPORTANT]
>
>若要連線到目的地，您需要&#x200B;**[!UICONTROL 檢視目的地]**&#x200B;和&#x200B;**[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要連線到此目的地，請依照[目的地組態教學課程](../../ui/connect-destination.md)中所述的步驟進行。 在設定目標工作流程中，填寫以下兩個區段中列出的欄位。

在&#x200B;**[!UICONTROL 目的地]** > **[!UICONTROL 目錄]**&#x200B;內，搜尋[!DNL Mailchimp Interest Categories]。 或者，您可以在&#x200B;**[!UICONTROL 電子郵件行銷]**&#x200B;類別下找到它。

### 驗證目標 {#authenticate}

若要驗證到目的地，請填寫下列必填欄位，然後選取&#x200B;**[!UICONTROL 連線到目的地]**。

| 欄位 | 說明 |
| --- | --- |
| **[!UICONTROL 使用者名稱]** | 您的[!DNL Mailchimp Interest Categories]使用者名稱。 |
| **[!UICONTROL 密碼]** | 您的[!DNL Mailchimp] **API金鑰**&#x200B;已在[收集 [!DNL Mailchimp] 認證](#gather-credentials)區段中記下。<br>您的API金鑰採用`{KEY}-{DC}`的形式，其中`{KEY}`部分參考在[[!DNL Mailchimp] API金鑰](#gather-credentials)部分中記下的值，而`{DC}`部分參考[[!DNL Mailchimp] 資料中心](#identify-data-center)。 <br>您可以提供`{KEY}`部分或整個表單。<br>例如，若您的API金鑰是&#x200B;<br>*`0123456789abcdef0123456789abcde-us14`*，<br>，您可以提供&#x200B;*`0123456789abcdef0123456789abcde`*或&#x200B;*`0123456789abcdef0123456789abcde-us14`*作為值。 |

{style="table-layout:auto"}

![平台UI熒幕擷圖顯示如何驗證。](../../assets/catalog/email-marketing/mailchimp-interest-categories/authenticate-destination.png)

如果提供的詳細資料有效，UI會顯示帶有綠色勾號的&#x200B;**[!UICONTROL 已連線]**&#x200B;狀態。 然後您可以繼續下一步驟。

### 填寫目標詳細資訊 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。

![顯示目的地詳細資訊的平台UI熒幕擷取畫面。](../../assets/catalog/email-marketing/mailchimp-interest-categories/destination-details.png)

| 欄位 | 說明 |
| --- | --- |
| **[!UICONTROL 名稱]** | 您日後可辨識此目的地的名稱。 |
| **[!UICONTROL 說明]** | 可協助您日後識別此目的地的說明。 |
| **[!UICONTROL 資料中心]** | 您的[!DNL Mailchimp]帳戶`data center`。 如需任何指引，請參閱[識別 [!DNL Mailchimp] 資料中心](#identify-data-center)區段。 |
| **[!UICONTROL 對象名稱（請先選取資料中心）]** | 選取您的&#x200B;**[!UICONTROL 資料中心]**&#x200B;後，此下拉式清單會自動填入您[!DNL Mailchimp]帳戶中的對象名稱。 選取您要以Platform資料更新的對象。 |
| **[!UICONTROL 興趣類別（請先選取資料中心和對象名稱）]** | 選取您的&#x200B;**[!UICONTROL 對象名稱]**&#x200B;後，此下拉式清單會自動填入您[!DNL Mailchimp]帳戶中的興趣群組類別名稱。 選取您要以Platform資料更新的類別名稱。 |

{style="table-layout:auto"}

>[!TIP]
>
> 如果您在&#x200B;**[!UICONTROL 密碼]**&#x200B;欄位中提供的API金鑰或&#x200B;**[!UICONTROL 資料中心]**&#x200B;值不正確，UI會顯示[!DNL Mailchimp] API錯誤回應： *`No options are available. Please verify the values selected for the following dependent fields: dataCenter`*，如下所示。 在此情況下，您無法從&#x200B;**[!UICONTROL 對象名稱（請先選取資料中心）]**&#x200B;欄位中選取值。 若要修正此錯誤，請提供正確的值。

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱[使用UI訂閱目的地警示](../../ui/alerts.md)的指南。

當您完成提供目的地連線的詳細資訊後，請選取&#x200B;**[!UICONTROL 下一步]**。

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要&#x200B;**[!UICONTROL 檢視目的地]**、**[!UICONTROL 啟用目的地]**、**[!UICONTROL 檢視設定檔]**&#x200B;和&#x200B;**[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。
>* 若要匯出&#x200B;*身分*，您需要&#x200B;**[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions)。<br> ![選取工作流程中反白的身分名稱空間，以啟用目的地的對象。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以啟用目的地的對象。"){width="100" zoomable="yes"}

閱讀[將設定檔和對象啟用至串流對象匯出目的地](/help/destinations/ui/activate-segment-streaming-destinations.md)，以瞭解啟用此目的地對象的指示。

### 對應考量事項和範例 {#mapping-considerations-example}

若要將對象資料從Adobe Experience Platform正確傳送至[!DNL Mailchimp Interest Categories]目的地，您必須完成欄位對應步驟。 對應包括在Platform帳戶中的Experience Data Model (XDM)結構描述欄位與來自目標目的地的對應對應專案之間建立連結。

若要將您的XDM欄位正確對應到[!DNL Mailchimp Interest Categories]目的地欄位，請遵循下列步驟：

1. 在&#x200B;**[!UICONTROL 對應]**&#x200B;步驟中，選取&#x200B;**[!UICONTROL 新增對應]**。 您現在可以在畫面上看到新的對應列。
1. 在&#x200B;**[!UICONTROL 選取來源欄位]**&#x200B;視窗中，選擇&#x200B;**[!UICONTROL 選取屬性]**&#x200B;類別並選取XDM屬性，或選擇&#x200B;**[!UICONTROL 選取身分名稱空間]**&#x200B;並選取身分。
1. 在&#x200B;**[!UICONTROL 選取目標欄位]**&#x200B;視窗中，選擇&#x200B;**[!UICONTROL 選取身分名稱空間]**&#x200B;並選取身分，或選擇&#x200B;**[!UICONTROL 選取屬性]**&#x200B;類別，並從[!DNL Mailchimp] API填入的屬性清單中選取。 *您新增至所選[!DNL Mailchimp]對象的自訂屬性也可供選擇為目標欄位。*

   您的XDM設定檔結構描述與[!DNL Mailchimp Interest Categories]之間可用的對應如下：
| Source欄位 | 目標欄位 | 附註 |
| — | — | — |
|`IdentityMap: Email`|`Identity: email`| 必要：是 |
|`xdm: person.name.firstName`|`Attribute: FNAME`| |
|`xdm: person.name.lastName`|`Attribute: LNAME`| |
|`xdm: person.birthDayAndMonth`|`Attribute: BIRTHDAY`| |

   此外，`ADDRESS`是特殊目標欄位，在您的[!DNL Mailchimp]對象中稱為`merge field`。 [[!DNL Mailchimp] 檔案](https://mailchimp.com/developer/marketing/docs/merge-fields/)將必要的金鑰定義為`addr1`、`city`、`state`和`zip`，以及選用金鑰`addr2`和`country`。 這些欄位的值必須是字串。 如果存在任何`ADDRESS`欄位對應，目的地會將`ADDRESS`物件傳遞至[!DNL Mailchimp] API以進行更新。 除了預設為`US`的國家/地區外，任何未對應的`ADDRESS`欄位的值預設為`NULL`。

   `ADDRESS`欄位可用的對應如下：

   | 來源欄位 | 目標欄位 |
   | --- | --- |
   | `xdm: workAddress.street1` | `Attribute: ADDRESS.addr1` |
   | `xdm: workAddress.street2` | `Attribute: ADDRESS.addr2` |
   | `xdm: workAddress.city` | `Attribute: ADDRESS.city` |
   | `xdm: workAddress.state` | `Attribute: ADDRESS.state` |
   | `xdm: workAddress.postalCode` | `Attribute: ADDRESS.zip` |
   | `xdm: workAddress.country` | `Attribute: ADDRESS.country` |

   例如，您想要以連絡人的現有位址列位`addr1`、`city`、`state`和`zip`的值更新`country`的值，例如`132, My Street, Kingston`、`New York`、`New York`和`12401`。 若要更新`country`，您必須傳遞變更&#x200B;*（若有的話）*&#x200B;的現有值，以及國家/地區的新值。 所以資料集中的值應該是`132, My Street, Kingston`、`New York`、`New York`、`12401`和`US`。 若要重申，如果您只傳遞`country`而未提供`addr1`、`city`、`state`和`zip`的值，則會被`NULL`覆寫。

   具有已完成對應的範例如下所示：
   ![顯示欄位對應的平台UI熒幕擷圖範例。](../../assets/catalog/email-marketing/mailchimp-interest-categories/mappings.png)

當您完成提供目的地連線的對應時，請選取&#x200B;**[!UICONTROL 下一步]**。

## 驗證資料匯出 {#exported-data}

若要驗證您是否已正確設定目的地，請遵循下列步驟：

* 登入您的[[!DNL Mailchimp]](https://login.mailchimp.com/)帳戶。 然後，導覽至&#x200B;**[!DNL Audience]**&#x200B;頁面。 接下來，展開&#x200B;**[!DNL Manage Contacts]**&#x200B;功能表並選取&#x200B;**[!DNL Groups]**。

![顯示「對象」群組頁面的Mailchimp UI熒幕擷圖。](../../assets/catalog/email-marketing/mailchimp-interest-categories/audience-groups.png)

* 選取群組，並檢查選取的對象是否以來自平台的對象名稱建立為類別，且後面可能會接著自動產生的尾碼。
   * 此目的地會使用[[!DNL Mailchimp] 新增興趣類別API](https://mailchimp.com/developer/marketing/api/interest-categories/add-interest-category/)，以選取的區段名稱來建立興趣類別。 如果您建立新目的地並再次啟用相同的對象，[!DNL Mailchimp]會新增尾碼以區分現有區段和新區段。
* 群組中不存在其電子郵件的連絡人會新增至新建立的類別。
* 對於群組中已存在的連絡人，會更新屬性欄位資料，並將連絡人新增至新建立的類別。

![顯示Audience群組類別的Mailchimp UI熒幕擷圖。](../../assets/catalog/email-marketing/mailchimp-interest-categories/audience-groups-category.png)

## 資料使用與控管 {#data-usage-governance}

處理您的資料時，所有[!DNL Adobe Experience Platform]目的地都符合資料使用原則。 如需[!DNL Adobe Experience Platform]如何強制資料控管的詳細資訊，請參閱[資料控管概觀](/help/data-governance/home.md)。

## 錯誤與疑難排解 {#errors-and-troubleshooting}

### 如果[!DNL Mailchimp] API金鑰或資料中心值不正確，便發生錯誤 {#incorrect-credentials-error}

如果您在&#x200B;**[!UICONTROL 密碼]**&#x200B;欄位中提供的API金鑰或&#x200B;**[!UICONTROL 資料中心]**&#x200B;值不正確，UI會顯示[!DNL Mailchimp] API錯誤回應： *`No options are available. Please verify the values selected for the following dependent fields: dataCenter`*，如下所示。 在此情況下，您無法從&#x200B;**[!UICONTROL 對象名稱（請先選取資料中心）]**&#x200B;欄位中選取值。

![若您的Mailchimp API金鑰或資料中心值不正確，則平台UI熒幕擷取畫面會顯示錯誤。](../../assets/catalog/email-marketing/mailchimp-interest-categories/error.png)

若要修正此錯誤並繼續進行下一個步驟，您必須提供正確的值。 請參閱[識別 [!DNL Mailchimp] 資料中心](#identify-data-center)和
如果您需要指引，請[收集 [!DNL Mailchimp] API金鑰](#gather-credentials)區段。

### 如果超過[!DNL Mailchimp]群組名稱限制，就會發生錯誤 {#group-name-limits-error}

建立目的地時，您可能會收到下列錯誤訊息： *`Cannot have more than 60 interests per list (Across all categories)`*&#x200B;或&#x200B;*`400 BAD_REQUEST`*。 如[護欄](#guardrails)區段所述，當您在單一群組或跨相同對象限制內的數個群組超過60個群組名稱（或興趣類別）時，就會發生這種情況。 若要修正此錯誤，請確定您在[!DNL Mailchimp]中未超過群組名稱限制。

### [!DNL Mailchimp]狀態與錯誤碼

請參閱[[!DNL Mailchimp] 錯誤頁面](https://mailchimp.com/developer/marketing/docs/errors/)，以取得包含說明的狀態和錯誤碼完整清單。

## 其他資源 {#additional-resources}

[!DNL Mailchimp]檔案中的其他實用資訊如下：
* [開始使用 [!DNL Mailchimp]](https://mailchimp.com/help/getting-started-with-mailchimp/)
* [開始使用對象](https://mailchimp.com/help/getting-started-audience/)
* [建立對象](https://mailchimp.com/help/create-audience/)
* [開始使用群組](https://mailchimp.com/help/getting-started-with-groups/)
* [建立新的對象群組](https://mailchimp.com/help/create-new-audience-group/)
* [興趣類別](https://mailchimp.com/developer/marketing/api/interest-categories/)
* [行銷API](https://mailchimp.com/developer/marketing/api/)
