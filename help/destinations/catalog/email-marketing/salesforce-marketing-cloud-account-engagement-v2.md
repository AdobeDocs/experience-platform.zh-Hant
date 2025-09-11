---
title: (V2) Salesforce Marketing Cloud帳戶參與度
description: 瞭解如何使用(V2) Salesforce Marketing Cloud Account Engagement （先前稱為Pardot）目的地匯出您的設定檔資料，並使用批次處理來滿足您的業務需求在Salesforce Marketing Cloud Account Engagement中啟用資料。
badge: label="Alpha" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 21ca268d3ade99cf46b6c511360084297e8163d3
workflow-type: tm+mt
source-wordcount: '1809'
ht-degree: 3%

---

# [!DNL (V2) Salesforce Marketing Cloud Account Engagement] 連線

[[!DNL Salesforce Marketing Cloud Account Engagement]](https://www.salesforce.com/products/marketing-cloud/marketing-automation/) （先前稱為[!DNL Pardot]）目的地可讓您將您的Adobe Experience Platform設定檔資料匯出至Salesforce的B2B行銷自動化平台。

此整合可讓您在Adobe Experience Platform中的客戶設定檔與[!DNL Salesforce Marketing Cloud Account Engagement]中的行銷活動之間無縫同步資料。

此目的地使用[[!DNL Salesforce Import API v5]](https://developer.salesforce.com/docs/marketing/pardot/guide/import-v5.html)有效地處理批次資料匯出。


>[!IMPORTANT]
> 
> 這是[Salesforce Marketing Cloud帳戶參與](help/destinations/catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md)目的地的V2版本。 此版本會取代先前的目的地，目前是在Alpha版本中。
> > <br>
> > 如果您目前正在使用舊版[Salesforce Marketing Cloud帳戶參與](help/destinations/catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md)目的地，您必須在&#x200B;**2026年1月**&#x200B;前移轉至此V2版本。 2026年1月後，Adobe將淘汰舊版，不再提供使用。


## 使用案例 {#use-cases}

為協助您更清楚瞭解您應如何及何時使用[!DNL (V2) Marketing Cloud Account Engagement]目的地，以下是Adobe Experience Platform客戶可藉由使用此目的地解決的範例使用案例。

### B2B銷售機會管理 {#use-case-lead-management}

將來自Adobe Experience Platform的潛在客戶資料同步至[!DNL Salesforce Marketing Cloud Account Engagement]，以進行全面潛在客戶培養和評分。 您的行銷團隊可以在Experience Platform中建立豐富的對象設定檔，並將其匯出至[!DNL Salesforce Marketing Cloud Account Engagement]，以自動化B2B行銷活動。

### Campaign 自動化 {#use-case-campaign-automation}

您可以使用在Adobe Experience Platform中定義的對象，在[!DNL Salesforce Marketing Cloud Account Engagement]中觸發行銷活動。 將目標對象匯出至[!DNL Salesforce]後，您可以使用這些對象執行電子郵件行銷活動，並透過培養、評分和行銷活動細分來管理您的銷售機會。

### 輪廓擴充 {#use-case-profile-enrichment}

使用Adobe Experience Platform的豐富客戶資料增強您的[!DNL Salesforce Marketing Cloud Account Engagement]潛在客戶設定檔。 匯出完整的設定檔屬性，以在[!DNL Salesforce Marketing Cloud Account Engagement]中建立更詳細的潛在客戶記錄，以改善目標定位和個人化。

## 先決條件 {#prerequisites}

請參閱以下各節，瞭解在Experience Platform和[!DNL Salesforce]中設定所需的任何先決條件，以及使用[!DNL (V2) Marketing Cloud Account Engagement]目的地之前需要收集的資訊。

### Experience Platform必要條件 {#prerequisites-in-experience-platform}

在啟用資料至[!DNL (V2) Marketing Cloud Account Engagement]目的地之前，您必須在[中建立](/help/xdm/schema/composition.md)結構描述[、](../../../catalog/datasets/overview.md)資料集[和](../../../segmentation/types/overview.md)對象[!DNL Experience Platform]。

### [!DNL Salesforce Marketing Cloud Account Engagement]必要條件 {#prerequisites-destination}

若要將資料從Experience Platform匯出至您的[!DNL Marketing Cloud Account Engagement]帳戶，請注意下列必要條件：

#### 您必須擁有[!DNL Marketing Cloud Account Engagement]帳戶 {#prerequisites-account}

訂閱[!DNL Marketing Cloud Account Engagement]Marketing Cloud帳戶參與[產品的](https://www.salesforce.com/products/marketing-cloud/marketing-automation/)帳戶是繼續的必要專案。

#### 收集[!DNL Marketing Cloud Account Engagement]認證 {#gather-credentials}

在驗證[!DNL (V2) Marketing Cloud Account Engagement]目的地之前，請先寫下以下專案。

| 認證 | 說明 |
| --- | --- |
| **[!UICONTROL 帳戶參與業務單位識別碼]** | 您的[!DNL Salesforce]帳戶參與業務單位識別碼。 請參閱Salesforce [檔案](https://help.salesforce.com/s/articleView?id=000381973&type=1)以瞭解如何尋找ID。 |

{style="table-layout:auto"}

## 支援的身分 {#supported-identities}

[!DNL (V2) Marketing Cloud Account Engagement]支援下表所述的身分啟用。 深入瞭解[身分](/help/identity-service/features/namespaces.md)。

如果使用其中一個識別碼找到相符專案，則將使用Adobe Experience Platform的資料更新現有的帳戶參與潛在客戶記錄。 如果找不到相符專案，系統會在帳戶參與中建立新的潛在客戶記錄。

| 目標身分 | 說明 | 考量事項 |
|---|---|---|
| `matchId` | 帳戶參與中的潛在客戶ID | 這三個身分中至少需要一個身分 |
| `matchSalesforceId` | 潛在客戶的Salesforce銷售機會/聯絡人ID | 這三個身分中至少需要一個身分 |
| `matchEmail` | 潛在客戶的電子郵件地址 | 這三個身分中至少需要一個身分 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 以設定檔為基礎]** | <ul><li>您正在匯出對象的所有成員，以及所需的結構描述欄位&#x200B;*（例如：電子郵件地址、電話號碼、姓氏）* （根據您的欄位對應）。</li><li>此目的地支援使用Salesforce Import API v5批次匯出設定檔資料。</li></ul> |
| 匯出頻率 | **[!UICONTROL 批次]** | <ul><li>**初始匯出**：對應後立即完整匯出</li><li>**後續匯出**：每3小時遞增匯出一次</li><li>此排程已修正，無法在Alpha中自訂</li></ul> |

{style="table-layout:auto"}

## 連線到目標 {#connect}

>[!IMPORTANT]
>
>若要連線到目的地，您需要&#x200B;**[!UICONTROL 檢視目的地]**&#x200B;和&#x200B;**[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。

若要連線到此目的地，請依照[目的地組態教學課程](../../ui/connect-destination.md)中所述的步驟進行。 在設定目標工作流程中，填寫以下兩個區段中列出的欄位。

### 驗證目標 {#authenticate}

若要驗證到目的地，請選取&#x200B;**[!UICONTROL 連線到目的地]**。

![Salesforce Marketing Cloud帳戶參與V2目的地連線工作流程](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement-v2/connect-to-destination.png "Salesforce Marketing Cloud帳戶參與V2目的地連線工作流程")

系統會將您重新導向至[!DNL Salesforce]登入頁面。 輸入您的[!DNL Marketing Cloud Account Engagement]帳戶認證，並選取&#x200B;**[!UICONTROL 登入]**。

![Salesforce登入頁面](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement-v2/salesforce-auth.png "Salesforce登入頁面。")

接著，選取「**[!UICONTROL 允許]**」以授與&#x200B;**Adobe Experience Platform**&#x200B;應用程式的許可權以存取您的[!DNL Salesforce Marketing Cloud Account Engagement]帳戶。 *您只需要執行此動作一次*。

![Salesforce應用程式熒幕擷取畫面確認快顯視窗，可授予Experience Platform應用程式存取Marketing Cloud帳戶參與專案的許可權。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement-v2/allow-app.png)

如果提供的詳細資料有效，UI會顯示訊息： *您已成功連線至(V2) Salesforce Marketing Cloud帳戶參與帳戶*&#x200B;以及帶有綠色勾號的&#x200B;**[!UICONTROL 已連線]**&#x200B;狀態。

### 填寫目標詳細資料 {#destination-details}

若要設定目的地的詳細資訊，請填寫下方的必填和選用欄位。 UI中欄位旁的星號表示該欄位為必填欄位。

* **[!UICONTROL 名稱]**：您日後可辨識此目的地的名稱。
* **[!UICONTROL 描述]**：可協助您日後識別此目的地的描述。
* **[!UICONTROL 帳戶參與業務單位識別碼]**：您的[!DNL Salesforce] `Account Engagement Business Unit ID`。
* **[!UICONTROL 帳戶參與API]**：選取您要使用Account Engagement API的生產端點(`https://pi.pardot.com`)或示範端點(`https://pi.demo.pardot.com`)。
* **[!UICONTROL 帳戶參與行銷活動ID]**：每個[!DNL Account Engagement]潛在客戶都必須與行銷活動建立關聯。 如果您未設定行銷活動ID，則當您的Salesforce帳戶中存在預設值時，帳戶參與將嘗試自動指派一個ID。

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱[使用UI訂閱目的地警示](../../ui/alerts.md)的指南。

當您完成提供目的地連線的詳細資訊後，請選取&#x200B;**[!UICONTROL 下一步]**。

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要&#x200B;**[!UICONTROL 檢視目的地]**、**[!UICONTROL 啟用目的地]**、**[!UICONTROL 檢視設定檔]**&#x200B;和&#x200B;**[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions)。 閱讀[存取控制總覽](/help/access-control/ui/overview.md)或連絡您的產品管理員以取得必要的許可權。
>* 若要匯出&#x200B;*身分*，您需要&#x200B;**[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions)。<br> ![選取工作流程中反白的身分名稱空間，以啟用目的地的對象。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以啟用目的地的對象。"){width="100" zoomable="yes"}

讀取[啟用批次設定檔匯出目的地的對象資料](/help/destinations/ui/activate-batch-profile-destinations.md)，以取得啟用此目的地對象的指示。

### 對應考量事項和範例 {#mapping-considerations-example}

若要將對象資料從Adobe Experience Platform傳送到[!DNL (V2) Marketing Cloud Account Engagement]目的地，您必須將體驗資料模型(XDM)結構描述欄位對應到目的地中的對應欄位。

如需支援欄位的完整清單，請參閱[Salesforce Prospect API v5檔案](https://developer.salesforce.com/docs/marketing/pardot/guide/prospect-v5.html)。 請注意，Alpha版本不支援[自訂欄位](https://developer.salesforce.com/docs/marketing/pardot/guide/custom-field-v5.html)。

#### 支援的屬性 {#supported-attributes}

Salesforce Marketing Cloud帳戶參與目的地支援下表描述的目標屬性。

| 屬性 | 類型 | 說明 |
|---------|----------|----------|
| `salesforceId` | 字串 | 潛在客戶的Salesforce ID |
| `salesforceOwnerId` | 整數 | 潛在客戶擁有者的Salesforce使用者ID |
| `salutation` | 字串 | 潛在客戶的問候語（例如，先生、女士、博士） |
| `score` | 整數 | 帳戶參與中的潛在客戶分數 |
| `source` | 字串 | 潛在客戶記錄的來源 |
| `state` | 字串 | 潛在客戶的州/省 |
| `territory` | 字串 | 指派給潛在客戶的區域 |
| `userId` | 整數 | 與潛在客戶相關聯的使用者ID |
| `website` | 字串 | 潛在客戶的網站URL |
| `yearsInBusiness` | 字串 | 潛在客戶在業務上已執行的年數 |
| `zip` | 字串 | 潛在客戶的郵遞區號 |

#### 必要的對應 {#required-mappings}

開始對應資料之前，請檢閱下列必要的欄位對應。

| 目標欄位 | 類型 | 必要 | 何時使用 |
|---|---|---|---|
| `email` | 屬性 | 永遠必要 | 潛在客戶的電子郵件地址。 這是當您沒有`matchId`或`matchSalesforceId`時，在帳戶參與中尋找及比對潛在客戶記錄的主要識別碼。<br> **注意：**&#x200B;如果帳戶參與有「允許多個潛在客戶使用相同的電子郵件地址」功能，僅依賴電子郵件可能會導致模稜兩可，因為同一電子郵件中有多個潛在客戶。 在這種情況下，「帳戶參與」通常預設為使用最近的活動來更新潛在客戶。 |
| `matchId` | 身分識別 | 這三個身分中至少需要一個身分 | 「帳戶參與」為每個潛在客戶記錄產生的唯一識別碼。 若您已有帳戶參與潛在客戶ID，且想確保將更新套用至正確潛在客戶，尤其是有多個潛在客戶共用相同電子郵件地址時，請使用此選項。 |
| `matchSalesforceId` | 身分識別 | 這三個身分中至少需要一個身分 | Salesforce中潛在客戶或連絡人的Salesforce ID。 當潛在客戶已與Salesforce同步時，請使用此專案，以維持帳戶參與和Salesforce之間的資料一致性。 |
| `matchEmail` | 身分識別 | 這三個身分中至少需要一個身分 | 用於比對的潛在客戶電子郵件地址。 如果您沒有特定的帳戶參與潛在客戶ID或Salesforce ID，可使用此作為替代識別碼。 備註：如果多個潛在客戶共用相同的電子郵件地址，「帳戶參與」通常會預設為使用最近的活動更新潛在客戶。 |

請依照下列步驟對應正確的欄位。

1. 在&#x200B;**[!UICONTROL 對應]**&#x200B;步驟中，選取&#x200B;**[!UICONTROL 新增對應]**。 您會在畫面上看到新的對應列。
1. 在&#x200B;**[!UICONTROL 選取來源欄位]**&#x200B;視窗中，選擇&#x200B;**[!UICONTROL 選取屬性]**&#x200B;類別並選取XDM屬性，或選擇&#x200B;**[!UICONTROL 選取身分名稱空間]**&#x200B;並選取身分。
1. 在&#x200B;**[!UICONTROL 選取目標欄位]**&#x200B;視窗中，選擇&#x200B;**[!UICONTROL 選取身分名稱空間]**&#x200B;並選取身分，或選擇&#x200B;**[!UICONTROL 選取自訂屬性]**&#x200B;類別，並從標準帳戶參與潛在客戶欄位清單中指定。

![將XDM欄位和身分對應到Salesforce Marketing Cloud帳戶參與V2欄位](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement-v2/mapping.png "將XDM欄位和身分對應到Salesforce Marketing Cloud帳戶參與V2欄位的範例")

## 驗證資料匯出 {#exported-data}

若要驗證您是否已正確設定目的地，請遵循下列步驟：

1. 導覽至您選取的其中一個對象。 選取 **[!DNL Activation data]** 索引標籤。**[!UICONTROL 對應ID]**&#x200B;欄會顯示在[!DNL Marketing Cloud Account Engagement Prospects]頁面中產生的自訂欄位名稱。
   ![Experience Platform UI熒幕擷圖範例，顯示所選區段的對應ID。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement-v2/selected-segment-mapping-id.png)

1. 登入[[!DNL Salesforce]](https://login.salesforce.com/)網站。 然後導覽至「**[!DNL Account Engagement]** > **[!DNL Prospects]** > **[!DNL Pardot Prospects]**」頁面，並檢查是否新增/更新了對象中的潛在客戶。 或者，您也可以存取[[!DNL Account Engagement]](https://pi.pardot.com/)並存取&#x200B;**[!DNL Prospects]**頁面。
   ![顯示[潛在客戶]頁面的Salesforce UI熒幕擷圖。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement-v2/prospects.png)

1. 若要檢查潛在客戶是否已更新，請選取潛在客戶並驗證自訂潛在客戶欄位是否已使用Experience Platform對象狀態進行更新。
   ![Salesforce UI熒幕擷圖顯示選取的潛在客戶頁面，自訂潛在客戶欄位已更新為對象狀態。](../../assets/catalog/email-marketing/salesforce-marketing-cloud-account-engagement-v2/prospect.png)

## 資料使用與控管 {#data-usage-governance}

處理您的資料時，所有[!DNL Adobe Experience Platform]目的地都符合資料使用原則。 如需[!DNL Adobe Experience Platform]如何強制資料控管的詳細資訊，請參閱[資料控管概觀](/help/data-governance/home.md)。

## 其他資源 {#additional-resources}

* [!DNL Marketing Cloud Account Engagement] [API檔案](https://developer.salesforce.com/docs/marketing/pardot/guide/overview.html)
* [Salesforce匯入API v5檔案](https://developer.salesforce.com/docs/marketing/pardot/guide/import-v5.html)
* [Salesforce Prospect API v5檔案](https://developer.salesforce.com/docs/marketing/pardot/guide/prospect-v5.html)