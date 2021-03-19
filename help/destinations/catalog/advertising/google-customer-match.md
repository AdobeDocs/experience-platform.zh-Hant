---
keywords: google客戶符合；Google客戶符合；Google客戶符合
title: Google客戶符合連線
description: Google Customer Match可讓您使用您的線上和離線資料，透過Google的自有和營運資產（例如搜尋、購物、Gmail和YouTube）觸及客戶並與其重新互動。
translation-type: tm+mt
source-git-commit: 950dc24e44a32cfd3e0cdde0fee967cb687c572e
workflow-type: tm+mt
source-wordcount: '1565'
ht-degree: 0%

---


# [!DNL Google Customer Match] 連接

[Google Customer ](https://support.google.com/google-ads/answer/6379332?hl=en) Matchet可讓您使用您的線上和離線資料，透過Google擁有和營運的資產觸及並重新與客戶互動，例如： [!DNL Search]、 [!DNL Shopping]、 [!DNL Gmail]和 [!DNL YouTube]。

![Adobe Experience PlatformUI中的Google客戶符合目標](../../assets/catalog/advertising/google-customer-match/catalog.png)

## 使用案例

為協助您進一步瞭解應如何及何時使用[!DNL Google Customer Match]目標，以下是Adobe Experience Platform客戶可使用此功能解決的範例使用案例。

### 使用案例#1

運動服裝品牌希望透過[!DNL Google Search]和[!DNL Google Shopping]觸及現有客戶，根據他們過去的購買和瀏覽記錄個人化優惠和項目。 服裝品牌可將電子郵件地址從自己的CRM內嵌至Experience Platform，從自己的離線資料建立區段，並將這些區段傳送至[!DNL Google Customer Match]以用於[!DNL Search]和[!DNL Shopping]，最佳化其廣告支出。

### 使用案例#2

一家知名科技公司剛剛發佈了一部新手機。 為了推廣這款新手機機型，他們希望讓擁有舊款手機的客戶對手機的新功能和特性有所瞭解。

為了促銷此版本，他們會使用電子郵件地址做為識別碼，從其CRM資料庫將電子郵件地址上傳至Experience Platform。 區段是根據擁有舊款手機機型並傳送至[!DNL Google Customer Match]的客戶而建立，以便鎖定目前客戶、擁有舊款手機機型的客戶，以及[!DNL YouTube]上的類似客戶。

## [!DNL Google Customer Match]目標{#data-governance}的資料控管

Experience Platform中的目的地對於發送到目的地平台或從目的地平台接收的資料可能具有某些規則和義務。 您有責任瞭解資料的限制和義務，以及您在Adobe Experience Platform和目的地平台中使用資料的方式。 Adobe Experience Platform公司提供資料治理工具，幫助您管理部分資料使用義務。 [進一](../../..//data-governance/labels/overview.md) 步瞭解資料治理工具和政策。

## 支援的身份{#supported-identities}

[!DNL Google Customer Match] 支援啟用下表所述的身分。進一步瞭解[identities](/help/identity-service/namespaces.md)。

| 目標識別 | 說明 | 考量事項 |
|---|---|---|
| GAID | Google廣告ID | 當您的來源識別為GAID命名空間時，請選取此目標識別。 |
| IDFA | 廣告商的Apple ID | 當您的來源識別為IDFA命名空間時，請選取此目標識別。 |
| phone_sha256_e.164 | E164格式的電話號碼，使用SHA256演算法雜湊 | Adobe Experience Platform支援純文字和SHA256雜湊電話號碼。 按照[ID匹配要求](#id-matching-requirements-id-matching-requirements)部分中的說明，分別為純文字檔案和雜湊電話號碼使用適當的命名空間。 當來源欄位包含未雜湊屬性時，請勾選&#x200B;**[!UICONTROL Apply transformation]**&#x200B;選項，讓[!DNL Platform]在啟動時自動雜湊資料。 |
| email_lc_sha256 | 使用SHA256演算法雜湊的電子郵件地址 | Adobe Experience Platform支援純文字和SHA256雜湊電子郵件地址。 請依照[ID符合要求](#id-matching-requirements-id-matching-requirements)區段中的指示，並分別針對純文字和雜湊電子郵件地址使用適當的名稱空間。 當來源欄位包含未雜湊屬性時，請勾選&#x200B;**[!UICONTROL Apply transformation]**&#x200B;選項，讓[!DNL Platform]在啟動時自動雜湊資料。 |
| user_id | 自訂使用者ID | 當您的來源識別為自訂命名空間時，請選取此目標識別。 |

## 導出類型{#export-type}

**區段匯出** -您正匯出區段（對象）的所有成員，並包含識別碼（名稱、電話號碼等）用於[!DNL Google Customer Match]目標。

## [!DNL Google Customer Match] 帳戶先決條件  {#google-account-prerequisites}

在Experience Platform中設定[!DNL Google Customer Match]目標之前，請務必閱讀並遵守Google的[!DNL Customer Match]使用政策，如[ Google支援檔案](https://support.google.com/google-ads/answer/6299717)所述。

### 允許清單{#allowlist}

>[!NOTE]
>
>在Experience Platform中設定您的第一個[!DNL Google Customer Match]目標之前，必須先將它新增至Google的允許清單。 請確定Google在建立目標之前已完成下列說明的允許清單程式。

在Experience Platform中建立[!DNL Google Customer Match]目標之前，您必須聯繫Google並遵循[使用客戶匹配合作夥伴中的允許清單說明，以上傳Google文檔中的資料](https://support.google.com/google-ads/answer/7361372?hl=en&amp;ref_topic=6296507)。

此外，如果您打算使用Google的[User_ID](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_email_address_address_or_user_id)上傳資料，則還有第二個Google允許清單您必須將帳戶新增至。 請連絡您的Google帳戶管理員，確定您已新增至允許清單。

### ID匹配要求{#id-matching-requirements}

[!DNL Google] 要求不會傳送任何個人識別資訊(PII)。因此，激活至[!DNL Google Customer Match]的觀眾可以鍵入&#x200B;*雜湊*&#x200B;標識符，如電子郵件地址或電話號碼。

根據您收錄至Adobe Experience Platform的ID類型，您必須符合其相應需求。

#### 電話號碼雜湊要求{#phone-number-hashing-requirements}

在[!DNL Google Customer Match]中啟用電話號碼有兩種方法：

* **接收原始電話號碼**:您可以將原始電話號碼以格 [!DNL E.164] 式內嵌 [!DNL Platform]至，在啟動時會自動雜湊。如果您選擇此選項，請務必將原始電話號碼永遠收錄到`Phone_E.164`命名空間中。
* **接收雜湊電話號碼**:您可先將電話號碼雜湊，再將其擷取 [!DNL Platform]。如果您選擇此選項，請務必將雜湊電話號碼永遠收錄到`PHONE_SHA256_E.164`命名空間中。

>[!NOTE]
>
>不能在[!DNL Google Customer Match]中激活包含在`Phone`名稱空間中的電話號碼。

#### 電子郵件散列要求{#hashing-requirements}

您可以選擇先將電子郵件地址雜湊，再將其匯入Adobe Experience Platform，或選擇以清楚的Experience Platform方式處理電子郵件地址，並讓我們的演算法在啟動時雜湊這些地址。

如需Google雜湊要求和其他啟動限制的詳細資訊，請參閱Google檔案中的下列章節：

* [[!DNL Customer Match] 包含電子郵件地址、地址或使用者ID](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_email_address_address_or_user_id)
* [[!DNL Customer Match] 注意事項](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_considerations)
* [客戶與電話號碼相符](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_phone_number)
* [客戶與行動裝置ID相符](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_mobile_device_ids)


若要瞭解如何在Experience Platform中擷取電子郵件地址，請參閱[批次擷取概觀](../../../ingestion/batch-ingestion/overview.md)和[串流擷取概觀](../../../ingestion/streaming-ingestion/overview.md)。

如果您選擇自行排列電子郵件地址，請務必符合上述連結中概述的Google要求。

#### 使用自訂名稱空間{#custom-namespaces}

在使用`User_ID`命名空間將資料傳送至Google之前，請務必使用[!DNL gTag]同步您自己的識別碼。 如需詳細資訊，請參閱[Google官方檔案](https://support.google.com/google-ads/answer/9199250)。

<!-- Data from unhashed namespaces is automatically hashed by [!DNL Platform] upon activation.

Attribute source data is not automatically hashed. When your source field contains unhashed attributes, check the **[!UICONTROL Apply transformation]** option, to have [!DNL Platform] automatically hash the data on activation.
![Identity mapping transformation](../../assets/ui/activate-destinations/identity-mapping-transformation.png) -->

## 連接到目標{#connect-destination}

在&#x200B;**[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**&#x200B;中，滾動到&#x200B;**[!UICONTROL Advertising]**&#x200B;類別。 選擇[!DNL Google Customer Match]，然後選擇&#x200B;**[!UICONTROL Configure]**。

![連線至Google客戶符合目的地](../../assets/catalog/advertising/google-customer-match/connect.png)

>[!NOTE]
>
>如果已存在與此目標的連接，則可以在目標卡上看到&#x200B;**[!UICONTROL Activate]**&#x200B;按鈕。 有關&#x200B;**[!UICONTROL Activate]**&#x200B;和&#x200B;**[!UICONTROL Configure]**&#x200B;之間差異的詳細資訊，請參閱目標工作區文檔的[目錄](../../ui/destinations-workspace.md#catalog)部分。

在&#x200B;**Account**&#x200B;步驟中，如果您先前已設定到[!DNL Google Customer Match]目標的連接，請選擇&#x200B;**[!UICONTROL Existing Account]**&#x200B;並選擇現有連接。 或者，您可以選擇&#x200B;**[!UICONTROL New Account]**&#x200B;來設定到[!DNL Google Customer Match]的新連接。 選擇&#x200B;**[!UICONTROL Connect to destination]**&#x200B;以登入並將Adobe Experience Cloud連接至您的[!DNL Google Ad]帳戶。

>[!NOTE]
>
>Experience Platform支援驗證程式中的認證驗證，如果您為[!DNL Google Ad]帳戶輸入錯誤的認證，則會顯示錯誤訊息。 這可確保您不會以不正確的憑證完成工作流程。

![連線至Google客戶符合目的地——驗證步驟](../../assets/catalog/advertising/google-customer-match/connection.png)

一旦確認您的認證，且Adobe Experience Cloud已連線至您的Google帳戶後，您可以選取&#x200B;**[!UICONTROL Next]**&#x200B;以繼續&#x200B;**[!UICONTROL Authentication]**&#x200B;步驟。

![認證已確認](../../assets/catalog/advertising/google-customer-match/connection-success.png)

在&#x200B;**[!UICONTROL Authentication]**&#x200B;步驟中，輸入&#x200B;**[!UICONTROL Name]**&#x200B;和&#x200B;**[!UICONTROL Description]**&#x200B;作為啟動流程，並填入您的Google **[!UICONTROL Account ID]**。

在此步驟中，您也可以選取任何應套用至此目的地的&#x200B;**[!UICONTROL Marketing actions]**。 行銷動作會指出將資料匯出至目的地的方式。 您可以從Adobe定義的行銷動作中選擇，也可以建立自己的行銷動作。 如需行銷動作的詳細資訊，請參閱[資料使用政策概述](../../../data-governance/policies/overview.md)。

在填入上述欄位後，請選取&#x200B;**[!UICONTROL Create Destination]**。

>[!IMPORTANT]
>
> * 預設會為[!DNL Google Customer Match]目標選取&#x200B;**[!UICONTROL Combine with PII]**&#x200B;行銷動作，且無法移除。
> * 對於[!DNL Google Customer Match]目標。 **[!UICONTROL Account ID]** 是您使用Google的客戶用戶端ID。ID的格式為xxx-xxx-xxxx。


![連線Google客戶符合——驗證步驟](../../assets/catalog/advertising/google-customer-match/authentication.png)

您的目標現在已建立。 如果您想稍後啟動區段，可以選取&#x200B;**[!UICONTROL Save & Exit]**，或選取&#x200B;**[!UICONTROL Next]**&#x200B;以繼續工作流程，並選取要啟動的區段。 在這兩種情況下，請參閱工作流程的下一節「啟動區段至 [!DNL Google Customer Match]](#activate-segments)」。[

## 啟用區段至[!DNL Google Customer Match] {#activate-segments}

如需如何啟用區段至[!DNL Google Customer Match]的指示，請參閱[啟用資料至目標](../../ui/activate-destinations.md)。


在&#x200B;**[!UICONTROL Segment schedule]**&#x200B;步驟中，將[!DNL IDFA]或[!DNL GAID]區段傳送至[!DNL Google Customer Match]時，您必須提供[!UICONTROL App ID]。

![Google客戶符合應用程式ID](../../assets/catalog/advertising/google-customer-match/gcm-destination-appid.png)

有關如何查找[!DNL App ID]的詳細資訊，請參閱[ Google官方文檔](https://developers.google.com/adwords/api/docs/reference/v201809/AdwordsUserListService.CrmBasedUserList#appid)。







<!-- 
To activate segments to [!DNL Google Customer Match], follow the steps below: 

In **[!UICONTROL Destinations > Browse]**, select the [!DNL Google Customer Match] destination where you want to activate your segments.

Click the name of the destination. This takes you to the Activate flow.

![activate-flow](../../assets/catalog/advertising/google-customer-match/activate-flow.png)

Note that if an activation flow already exists for a destination, you can see the segments that are currently being sent to the destination. Select **[!UICONTROL Edit activation]** in the right rail and follow the steps below to modify the activation details.

Select **[!UICONTROL Activate]**. In the **[!UICONTROL Activate destination]** workflow, on the **[!UICONTROL Select Segments]** page, select which segments to send to [!DNL Google Customer Match].

![segments-to-destination](../../assets/catalog/advertising/google-customer-match/activate-segments.png)

In the **[!UICONTROL Identity mapping]** step, select which attributes to be included as an identity in this destination. Select **[!UICONTROL Add new mapping]** and browse your schema, select email and/or hashed email, and map them to the corresponding target identity.

![identity mapping initial screen](../../assets/catalog/advertising/google-customer-match/identity-mapping.png) 

**Plain text email address as primary identity**: If you have plain text (unhashed) email addresses as primary identity in your schema, select the email field in your **[!UICONTROL Source Attributes]** and map to the Email field in the right column under **[!UICONTROL Target Identities]**, as shown below:

![select plain text emails identity](../../assets/catalog/advertising/google-customer-match/raw-email.gif) 

**Hashed email address as primary identity**: If you have hashed email addresses as primary identity in your schema, select the hashed email field in your **[!UICONTROL Source Attributes]** and map to the Email_LC_SHA256 field in the right column under **[!UICONTROL Target Identities]**, as shown below:

![select hashed emails identity](../../assets/catalog/advertising/google-customer-match/hashed-emails.gif)

On the **[!UICONTROL Segment schedule]** page, you can set the start date for sending data to the destination.

On the **[!UICONTROL Review]** page, you can see a summary of your selection. Select **[!UICONTROL Cancel]** to break up the flow, **[!UICONTROL Back]** to modify your settings, or **[!UICONTROL Finish]** to confirm your selection and start sending data to the destination.

>[!IMPORTANT]
>
>In this step, Real-time CDP checks for data usage policy violations. Shown below is an example where a policy is violated. You cannot complete the segment activation workflow until you have resolved the violation. For information on how to resolve policy violations, see [Policy enforcement](../../../rtcdp/privacy/data-governance-overview.md#enforcement) in the data governance documentation section.
 
![confirm-selection](../../assets/common/data-policy-violation.png)

If no policy violations have been detected, select **[!UICONTROL Finish]** to confirm your selection and start sending data to the destination.

![confirm-selection](../../assets/catalog/advertising/google-customer-match/review.png) -->

## 確認區段啟動成功{#verify-activation}

完成啟動流程後，請切換至您的&#x200B;**[!UICONTROL Google Ads]**&#x200B;帳戶。 啟用的區段現在會以客戶清單的形式顯示在您的Google帳戶中。 請注意，視您的區段大小而定，除非有超過100位使用中使用者可供服務，否則不會填入某些對象。

將區段同時對應至[!DNL IDFA]和[!DNL GAID]行動ID時，[!DNL Google Customer Match]會為每個ID對應建立個別的區段。 您的[!DNL Google Ads]帳戶將顯示兩個不同的區段，一個用於[!DNL IDFA]，另一個用於[!DNL GAID]映射。

## 其他資源 {#additional-resources}

* [整合Google客戶符合——教學課程影片](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/integrate-with-google-customer-match.html)