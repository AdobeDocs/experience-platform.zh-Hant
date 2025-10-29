---
title: Salesforce Marketing Cloud帳戶參與度
description: 瞭解如何使用Salesforce Marketing Cloud Account Engagement （先前稱為Pardot）目的地匯出您的帳戶資料，並在Salesforce Marketing Cloud Account Engagement中根據您的業務需求啟用資料。
last-substantial-update: 2023-04-14T00:00:00Z
exl-id: fca9d4f4-8717-4bfa-9992-5164ba98bea4
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1482'
ht-degree: 2%

---

# [!DNL Salesforce Marketing Cloud Account Engagement] 連線

使用[[!DNL Salesforce Marketing Cloud Account Engagement]](https://www.salesforce.com/products/marketing-cloud/marketing-automation/) *（先前稱為[!DNL Pardot]）*&#x200B;目的地來擷取、追蹤、評分和評等潛在客戶。 您還可以透過電子郵件滴答式行銷活動，使用培養、評分和行銷活動細分來針對目標市場對象和客戶群組設計管道所有階段的潛在客戶追蹤。

相較於[!DNL Salesforce Marketing Cloud Engagement]更傾向於&#x200B;**B2C**&#x200B;行銷，[!DNL Marketing Cloud Account Engagement]是涉及多個部門與決策者（需要較長的銷售和決策週期）的&#x200B;**B2B**&#x200B;使用案例的理想選擇。 此外，您也可以與CRM維持更緊密的鄰近度及整合度，以做出適當的銷售和行銷決策。 *請注意，Experience Platform也有[!DNL Salesforce Marketing Cloud Engagement]的連線，您可以在[[!DNL Salesforce Marketing Cloud]](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud.md)和[[!DNL (API) Salesforce Marketing Cloud]](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud-exact-target.md)頁面上檢視。*

此[!DNL Adobe Experience Platform] [目的地](/help/destinations/home.md)利用[[!DNL Salesforce Account Engagement API > Prospect Upsert by Email]](https://developer.salesforce.com/docs/marketing/pardot/guide/prospect-v5.html#prospect-upsert-by-email)端點，在新&#x200B;**區段中啟用潛在客戶**&#x200B;後，新增或更新您的潛在客戶[!DNL Marketing Cloud Account Engagement]。

[!DNL Marketing Cloud Account Engagement]使用OAuth 2搭配授權碼通訊協定來驗證[!DNL Account Engagement] API。 [!DNL Marketing Cloud Account Engagement]向目的地驗證[區段中進一步說明如何向您的](#authenticate)執行個體進行驗證。

## 使用案例 {#use-cases}

為協助您更清楚瞭解您應如何及何時使用[!DNL Marketing Cloud Account Engagement]目的地，以下是Adobe Experience Platform客戶可藉由使用此目的地解決的範例使用案例。

### 傳送電子郵件給行銷活動的連絡人 {#use-case-send-emails}

線上平台的行銷部門想要將電子郵件式行銷活動廣播給B2B潛在客戶的精選受眾。 平台的行銷團隊可以透過Adobe Experience Platform新增新的潛在客戶或更新現有的潛在客戶資訊、從自己的離線資料建立對象，並將這些對象傳送到[!DNL Marketing Cloud Account Engagement]，接著再使用這些對象來傳送行銷活動電子郵件。

## 先決條件 {#prerequisites}

請參閱以下各節，瞭解在Experience Platform和[!DNL Salesforce]中設定所需的任何先決條件，以及使用[!DNL Marketing Cloud Account Engagement]目的地之前需要收集的資訊。

### Experience Platform的必要條件 {#prerequisites-in-experience-platform}

在啟用資料到[!DNL Marketing Cloud Account Engagement]目的地之前，您必須在[中建立](/help/xdm/schema/composition.md)結構描述[、](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html)資料集[和](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html)區段[!DNL Experience Platform]。

### [!DNL Marketing Cloud Account Engagement]中的必要條件 {#prerequisites-destination}

若要將資料從Experience Platform匯出至您的[!DNL Marketing Cloud Account Engagement]帳戶，請注意下列必要條件：

#### 您必須擁有[!DNL Marketing Cloud Account Engagement]帳戶 {#prerequisites-account}

訂閱[!DNL Marketing Cloud Account Engagement]Marketing Cloud帳戶參與[產品的](https://www.salesforce.com/products/marketing-cloud/marketing-automation/)帳戶是繼續的必要專案。

您的[!DNL Salesforce]帳戶應該有[!DNL Salesforce] `Account Engagement Administrator role`。 這是[建立自訂潛在客戶欄位](https://help.salesforce.com/s/articleView?id=sf.pardot_fields_create_custom_field.htm&type=5)的必要專案。

最後，您的帳戶應該也能夠存取[[!DNL Account Engagement Lightning App]](https://help.salesforce.com/s/articleView?id=sf.pardot_lightning_enable.htm&type=5)。

如果您沒有帳戶，或帳戶缺少[[!DNL Salesforce] 訂閱或](https://www.salesforce.com/company/contact-us/?d=cta-glob-footer-10)，請連絡[!DNL Salesforce]支援[!DNL Marketing Cloud Account Engagement]或您的[!DNL Account Engagement Administrator role]帳戶管理員。

#### 收集[!DNL Marketing Cloud Account Engagement]認證 {#gather-credentials}

在驗證[!DNL Marketing Cloud Account Engagement]目的地之前，請記下以下專案。

| 認證 | 說明 |
| --- | --- |
| `Username` | 您的[!DNL Marketing Cloud Account Engagement]帳戶使用者名稱。 |
| `Password` | 您的[!DNL Marketing Cloud Account Engagement]帳戶密碼。 |
| `Account Engagement Business Unit ID` | 若要尋找Account Engagement Business Unit ID，請使用[!DNL Salesforce]中的設定。 從設定中，在[快速尋找]方塊中輸入&#x200B;*商務單位設定*。 您的帳戶參與業務單位識別碼以`0Uv`開頭，長度為18個字元。 如果您無法存取業務單位設定資訊，請要求您的[!DNL Salesforce]帳戶管理員提供`Account Engagement Business Unit ID`給您。 如果您需要其他指引，請參閱[[!DNL Salesforce] 驗證](https://developer.salesforce.com/docs/marketing/pardot/guide/authentication)指引頁面。 |

{style="table-layout:auto"}

### 護欄 {#guardrails}

請參閱[!DNL Marketing Cloud Account Engagement] [速率限制](https://developer.salesforce.com/docs/marketing/pardot/guide/overview.html#rate-limits)，其詳細說明您的計畫所強加的限制，並且也會套用至Experience Platform執行。

>[!IMPORTANT]
>
>如果您的[!DNL Salesforce]帳戶管理員已限制受信任IP範圍的存取權，您必須連絡他們，才能取得[Experience Platform IP的](/help/destinations/catalog/streaming/ip-address-allow-list.md)加入允許清單。 如需其他指引，請參閱[!DNL Salesforce] [限制連線應用程式的受信任IP範圍存取](https://help.salesforce.com/s/articleView?id=sf.connected_app_edit_ip_ranges.htm&type=5)檔案。

## 支援的身分 {#supported-identities}

[!DNL Marketing Cloud Account Engagement]支援下表所述的身分啟用。 深入瞭解[身分](/help/identity-service/features/namespaces.md)。

| 目標身分 | 說明 | 考量事項 |
|---|---|---|
| 電子郵件 | 潛在客戶電子郵件地址 | 強制 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
|---------|----------|---------|
| 匯出類型 | **[!UICONTROL Profile-based]** | <ul><li>您正在匯出區段的所有成員，以及所需的結構描述欄位&#x200B;*（例如：電子郵件地址、電話號碼、姓氏）* （根據您的欄位對應）。</li><li> 針對Experience Platform中每個選取的對象，相對應的[!DNL Salesforce Marketing Cloud Account Engagement]區段狀態會從Experience Platform更新其對象狀態。</li></ul> |
| 匯出頻率 | **[!UICONTROL Streaming]** | 串流目的地是「一律開啟」的API型連線。 根據對象評估在Experience Platform中更新設定檔後，聯結器會立即將更新傳送至下游的目標平台。 深入瞭解[串流目的地](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## 連線到目標 {#connect}

>[!IMPORTANT]
>
>若要連線到目的地，您需要&#x200B;**[!UICONTROL View Destinations]**&#x200B;和&#x200B;**[!UICONTROL Manage Destinations]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要連線到此目的地，請依照[目的地組態教學課程](../../ui/connect-destination.md)中所述的步驟進行。 在設定目標工作流程中，填寫以下兩個區段中列出的欄位。

在&#x200B;**[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**&#x200B;內，搜尋[!DNL Salesforce Marketing Cloud Account Engagement]。 或者，您可以在&#x200B;**[!UICONTROL Email marketing]**&#x200B;類別下找到它。

### 驗證目標 {#authenticate}

若要驗證到目的地，請選取&#x200B;**[!UICONTROL Connect to destination]**。 您將會被導覽至[!DNL Salesforce]登入頁面。 輸入您的[!DNL Marketing Cloud Account Engagement]帳戶認證並選取[!DNL Log In]。

![Experience Platform UI熒幕擷圖顯示如何驗證Marketing Cloud帳戶參與度。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/authenticate-destination.png)

接下來，在後續視窗中選取「[!UICONTROL Allow]」，授與&#x200B;**Adobe Experience Platform**&#x200B;應用程式的許可權以存取您的[!DNL Salesforce Marketing Cloud Account Engagement]帳戶。 *您只需要執行此動作一次*。

![Salesforce應用程式熒幕擷取畫面確認快顯視窗，可授予Experience Platform應用程式存取Marketing Cloud帳戶參與專案的許可權。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/allow-app.png)

如果提供的詳細資料有效，UI會顯示訊息： *您已成功連線至Salesforce Marketing Cloud帳戶參與帳戶*&#x200B;訊息，以及帶有綠色勾號的&#x200B;**[!UICONTROL Connected]**&#x200B;狀態，您就可以繼續下一個步驟。

### 填寫目標詳細資料 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。 如需任何指引，請參閱[收集 [!DNL Marketing Cloud Account Engagement] 認證](#gather-credentials)區段。

![Experience Platform UI熒幕擷圖顯示目的地詳細資料。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/destination-details.png)

| 欄位 | 說明 |
| --- | --- |
| **[!UICONTROL Name]** | 您日後可辨識此目的地的名稱。 |
| **[!UICONTROL Description]** | 可協助您日後識別此目的地的說明。 |
| **[!UICONTROL Account Engagement Business Unit ID]** | 您的[!DNL Salesforce] `Account Engagement Business Unit ID`。 |

{style="table-layout:auto"}

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱[使用UI訂閱目的地警示](../../ui/alerts.md)的指南。

當您完成提供目的地連線的詳細資訊時，請選取&#x200B;**[!UICONTROL Next]**。

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要&#x200B;**[!UICONTROL View Destinations]**、**[!UICONTROL Activate Destinations]**、**[!UICONTROL View Profiles]**&#x200B;和&#x200B;**[!UICONTROL View Segments]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。
>* 若要匯出&#x200B;*身分*，您需要&#x200B;**[!UICONTROL View Identity Graph]** [存取控制許可權](/help/access-control/home.md#permissions)。<br> ![選取工作流程中反白的身分名稱空間，以啟用目的地的對象。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以啟用目的地的對象。"){width="100" zoomable="yes"}

閱讀[將設定檔和對象啟用至串流對象匯出目的地](/help/destinations/ui/activate-segment-streaming-destinations.md)，以瞭解啟用此目的地對象的指示。

### 對應考量事項和範例 {#mapping-considerations-example}

若要將對象資料從Adobe Experience Platform正確傳送至[!DNL Marketing Cloud Account Engagement]目的地，您必須完成欄位對應步驟。 對應包括在Experience Platform帳戶中的Experience Data Model (XDM)結構描述欄位與來自目標目的地的對應對應專案之間建立連結。

若要將您的XDM欄位正確對應到[!DNL Marketing Cloud Account Engagement]目的地欄位，請遵循下列步驟。

1. 在&#x200B;**[!UICONTROL Mapping]**&#x200B;步驟中，選取&#x200B;**[!UICONTROL Add new mapping]**。 您會在畫面上看到新的對應列。
1. 在&#x200B;**[!UICONTROL Select source field]**&#x200B;視窗中，選擇&#x200B;**[!UICONTROL Select attributes]**&#x200B;類別並選取XDM屬性，或選擇&#x200B;**[!UICONTROL Select identity namespace]**&#x200B;並選取身分。
1. 在&#x200B;**[!UICONTROL Select target field]**&#x200B;視窗中，選擇&#x200B;**[!UICONTROL Select identity namespace]**&#x200B;並選取身分，或選擇&#x200B;**[!UICONTROL Select custom attributes]**&#x200B;類別並從可用結構描述的[[!DNL Prospect API fields]](https://developer.salesforce.com/docs/marketing/pardot/guide/prospect-v5.html#fields)清單中指定。

   * 重複這些步驟，在您的XDM設定檔結構描述與[!DNL Marketing Cloud Account Engagement]之間新增任何對應：

     | 來源欄位 | 目標欄位 | 強制 |
     | --- | --- | --- |
     | `IdentityMap: Email` | `Identity: email` | 是 |
     | `xdm: MailingAddress.city` | `xdm: city` | |
     | `xdm: person.name.firstName` | `Attribute: firstName` | |

   * 具有上述對應的範例如下所示：
     ![Experience Platform UI熒幕擷圖範例顯示Target對應。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/mappings.png)

當您完成提供目的地連線的對應時，請選取&#x200B;**[!UICONTROL Next]**。

## 驗證資料匯出 {#exported-data}

若要驗證您是否已正確設定目的地，請遵循下列步驟：

1. 導覽至您選取的其中一個對象。 選取 **[!DNL Activation data]** 索引標籤。**[!UICONTROL Mapping ID]**&#x200B;欄會顯示在[!DNL Marketing Cloud Account Engagement Prospects]頁面中產生的自訂欄位名稱。
   ![Experience Platform UI熒幕擷圖範例，顯示所選區段的對應ID。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/selected-segment-mapping-id.png)

1. 登入[[!DNL Salesforce]](https://login.salesforce.com/)網站。 然後導覽至「**[!DNL Account Engagement]** > **[!DNL Prospects]** > **[!DNL Pardot Prospects]**」頁面，並檢查是否已新增/更新對象中的潛在客戶。 或者，您也可以存取[[!DNL Salesforce Pardot]](https://pi.pardot.com/)並存取&#x200B;**[!DNL Prospects]**&#x200B;頁面。
   ![顯示[潛在客戶]頁面的Salesforce UI熒幕擷圖。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/prospects.png)

1. 若要檢查潛在客戶是否已更新，請選取潛在客戶並驗證自訂潛在客戶欄位是否已使用Experience Platform對象狀態進行更新。
   ![Salesforce UI熒幕擷圖顯示選取的潛在客戶頁面，自訂潛在客戶欄位已更新為對象狀態。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement/prospect.png)

## 資料使用與控管 {#data-usage-governance}

處理您的資料時，所有[!DNL Adobe Experience Platform]目的地都符合資料使用原則。 如需[!DNL Adobe Experience Platform]如何強制資料控管的詳細資訊，請參閱[資料控管概觀](/help/data-governance/home.md)。

## 其他資源 {#additional-resources}

* [!DNL Marketing Cloud Account Engagement] [API檔案](https://developer.salesforce.com/docs/marketing/pardot/guide/overview.html)。
