---
keywords: google customer match;Google customer match;Google Customer Match
title: Google客戶符合目的地
seo-title: Google客戶符合目的地
description: Google Customer Match可讓您使用您的線上和離線資料，透過Google的自有和營運資產（例如搜尋、購物、Gmail和YouTube）觸及客戶並與其重新互動。
seo-description: Google Customer Match可讓您使用您的線上和離線資料，透過Google的自有和營運資產（例如搜尋、購物、Gmail和YouTube）觸及客戶並與其重新互動。
translation-type: tm+mt
source-git-commit: 2dfa46906374151628d46c309df724a59f8dc50e
workflow-type: tm+mt
source-wordcount: '1555'
ht-degree: 0%

---


# Google客戶符合目的地

## 概述 {#overview}

[Google Customer Match](https://support.google.com/google-ads/answer/6379332?hl=en) 可讓您使用您的線上和離線資料，透過Google擁有和營運的資產觸及客戶並與其重新互動，例如： [!DNL Search]、 [!DNL Shopping]、 [!DNL Gmail]和 [!DNL YouTube]。

![即時CDP UI中的Google客戶符合目標](/help/rtcdp/destinations/assets/google-customer-match-catalog.png)

## 使用案例

為協助您更清楚瞭解您應如何及何時使用目的地，以下是Adobe即時客戶資料平台客戶可運用此功能解決的範例使用案例。 [!DNL Google Customer Match]


### 使用案例#1

運動服裝品牌希望透過現有客戶，並根據 [!DNL Google Search] 其過去 [!DNL Google Shopping] 的購買和瀏覽記錄，將優惠和項目個人化。 服裝品牌可將其CRM的電子郵件地址內嵌至Adobe即時CDP、從其離線資料建立細分，並傳送這些細分以用於各 [!DNL Google Customer Match] 個 [!DNL Search] 和 [!DNL Shopping]最佳化廣告支出。

### 使用案例#2

一家知名科技公司剛剛發佈了一部新手機。 為了推廣這款新手機機型，他們希望讓擁有舊款手機的客戶對手機的新功能和特性有所瞭解。

為了推廣此版本，他們會將電子郵件地址從其CRM資料庫上傳至Adobe即時CDP，並使用電子郵件地址做為識別碼。 區段是根據擁有舊款手機機型並傳送給客戶而建立，以便 [!DNL Google Customer Match] 鎖定目前客戶、擁有舊款手機機型的客戶，以及類似客戶 [!DNL YouTube]。

## 目的地的資料管 [!DNL Google Customer Match] 理 {#data-governance}

Adobe即時CDP中的目標可能具有傳送至目標平台或從目標平台接收資料的特定規則和義務。 您有責任瞭解資料的限制和義務，以及您在Adobe Experience Platform和目標平台中如何使用該資料。 Adobe Experience Platform提供資料治理工具，可協助您管理部分資料使用義務。 [進一步瞭解](/help/data-governance/labels/overview.md) 資料治理工具和政策。

## 啟動類型與身分 {#activation-type}

**區段匯出** -您正匯出區段（對象）的所有成員，並包含識別碼（名稱、電話號碼等） 用於目的 [!DNL Google Customer Match] 地。

**身分** -您可以在Google中使用原始或雜湊的電子郵件做為客戶ID

## [!DNL Google Customer Match] 帳戶先決條件 {#google-account-prerequisites}

在Adobe即時CDP [!DNL Google Customer Match] 中設定目標之前，請務必閱讀並遵守 [!DNL Customer Match]Google支援檔案中概述的Google使用 [政策](https://support.google.com/google-ads/answer/6299717)。

### 允許清單 {#allowlist}

>[!NOTE]
>
>在Adobe即時CDP中設定您的第一個目的地之前，必須先將它新 [!DNL Google Customer Match] 增至Google的允許清單。 請確定Google在建立目標之前已完成下列說明的允許清單程式。

在Adobe即時 [!DNL Google Customer Match] CDP中建立目標之前，您必須聯絡Google，並依照「使用客戶符合」合作夥伴中的允許清單指示，在 [Google檔案中上傳您的資料](https://support.google.com/google-ads/answer/7361372?hl=en&amp;ref_topic=6296507) 。


### 電子郵件雜湊要求 {#hashing-requirements}

<!--

>[!IMPORTANT]
>
> When using mobile device IDs as identifiers, an AppId must be provided in the activation flow. For more information, see step 6 in the [Activate segments](#activate-segments) section of this page.

-->

Google要求不要傳送任何個人識別資訊(PII)。 因此，啟動的觀眾必須 [!DNL Google Customer Match] 鎖定雜湊的 *電子郵件* 位址。 您可以選擇先對電子郵件地址進行雜湊處理，然後再將它們匯入Adobe Experience Platform，或者選擇在Experience Platform中清楚處理電子郵件地址，並讓我們的演算法在啟動時對它們進行雜湊處理。

如需有關Google雜湊要求和其他啟動限制的詳細資訊，請參閱Google檔案中的下列章節：

* [[!DNL Customer Match] 包含電子郵件地址、地址或使用者ID](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_email_address_address_or_user_id)
* [[!DNL Customer Match] 注意事項](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_considerations)

<!--

Links to be added when activation based on phone number and device IDs becomes available.

* [Customer Match with phone number](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_phone_number)
* [Customer Match with mobile device IDs](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_mobile_device_ids)

-->

若要瞭解如何在Experience Platform中擷取電子郵件地址，請參閱批次 [擷取概觀](/help/ingestion/batch-ingestion/overview.md) ，以 [及快速擷取概觀](/help/ingestion/streaming-ingestion/overview.md)。

如果您選擇自行排列電子郵件地址，請務必符合上述連結中概述的Google要求。


>[!IMPORTANT]
>
>如果您選擇不散列電子郵件地址，Adobe Real-time CDP會在您啟用區段至時為您執行此動作 [!DNL Google Customer Match]。 在啟動 [工作流程](/help/rtcdp/destinations/google-customer-match-destination.md#activate-segments) （請參閱步驟5）中，針對純文字電子郵件位址選取 `Email` 如下所示的選項 *，並針對雜湊的電子郵*`Email_LC_SHA256`**&#x200B;件位址選取。


![啟動時雜湊](/help/rtcdp/destinations/assets/identity-mapping.png)

## 連接到目標 {#connect-destination}

1. 在「 **[!UICONTROL 目標]** >目錄 **[!UICONTROL 」中，捲動至「]**&#x200B;廣告 **** 」類別。 選擇 [!DNL Google Customer Match]，然後選擇 **[!UICONTROL 配置]**。

   ![連線至Google客戶符合目的地](/help/rtcdp/destinations/assets/connect-google-customer-match.png)

   >[!NOTE]
   >
   >如果此目標已存在連接，您可以在目標卡上看到 **[!UICONTROL 「激活]** 」按鈕。 有關「激活」( **[!UICONTROL Activate]** )和「配置」( **[!UICONTROL Configure]**)之間差異的詳細資訊，請參 [閱目標工作區文檔的「目錄](/help/rtcdp/destinations/destinations-workspace.md#catalog) 」(Catalog)部分。

2. 在「 **Account** 」（帳戶）步驟中 [!DNL Google Customer Match] ，如果您先前已設定連線至您的目的地，請選取「 **** Existing Account」（現有帳戶）並選取您現有的連線。 或者，您可以選 **[!UICONTROL 擇「新帳戶]** 」來設定新連線 [!DNL Google Customer Match]。 選 **[!UICONTROL 擇「連線至目的地]** 」以登入，並將Adobe Experience Cloud連線至您的 [!DNL Google Ad] 帳戶。

   >[!NOTE]
   >
   >Adobe Real-time CDP支援驗證程式中的認證驗證，如果您在帳戶中輸入錯誤的認證，則會顯示錯誤 [!DNL Google Ad] 訊息。 這可確保您不會以不正確的憑證完成工作流程。

   ![連線至Google客戶符合目的地——驗證步驟](/help/rtcdp/destinations/assets/google-customer-match-pre-connect-view.png)

3. 一旦您的認證獲得確認，而Adobe Experience Cloud已連線至您的Google帳戶，您就可以選取「 **[!UICONTROL Next]** 」（下一步），繼 **[!UICONTROL 續設定]** 。

   ![認證已確認](/help/rtcdp/destinations/assets/google-customer-match-connection-success.png)

4. 在「驗 **[!UICONTROL 證]** 」步驟中，輸入啟動流程的「名稱 **[!UICONTROL 」和「說明]** 」，然後填寫Google帳戶 ******** ID。 <br> 此外，您也可以在此步驟中，選取 **[!UICONTROL 任何應套用至此目的地的Marketing]** 使用案例。 行銷使用案例會指出將資料匯出至目的地的方式。 您可以從Adobe定義的行銷使用案例中選擇，也可以建立自己的行銷使用案例。 有關行銷使用案例的詳細資訊，請參 [閱即時CDP中的資料治理頁](/help/rtcdp/privacy/data-governance-overview.md#destinations) 。 如需個別Adobe定義之行銷使用案例的詳細資訊，請參閱「資 [料使用政策」概觀](/help/data-governance/policies/overview.md#core-actions)。 <br> 在填 **[!UICONTROL 入上述欄位後]** ，選取「建立目標」。

   >[!IMPORTANT]
   >
   > * 依預 **[!UICONTROL 設，「與PII結合]** 」行銷使用案例會針對目的地 [!DNL Google Customer Match] 選取，且無法移除。
   > * 適用於 [!DNL Google Customer Match] 目的地。 **[!UICONTROL 帳戶ID]** 是您使用Google的客戶用戶端ID。 ID的格式為xxx-xxx-xxxx。


   ![連線Google客戶符合——驗證步驟](/help/rtcdp/destinations/assets/google-customer-match-authentication-step.png)

5. 您的目標現在已建立。 如果您想 **[!UICONTROL 稍後啟動區段]** ，可以選取「儲存並退出」，或選取「下一步 **** 」以繼續工作流程，並選取要啟動的區段。 在這兩種情況下，請參閱下一 [節「啟動區段 [!DNL Google Customer Match]](#activate-segments)」，以瞭解其餘的工作流程。


## 啟用區段至 [!DNL Google Customer Match] {#activate-segments}

若要啟用區段 [!DNL Google Customer Match]至，請遵循下列步驟：

1. 在「 **[!UICONTROL 目標>瀏覽]**」中，選 [!DNL Google Customer Match] 取您要啟用區段的目標。
2. 按一下目標的名稱。 這會帶您進入「啟動」流程。
   ![activate-flow](/help/rtcdp/destinations/assets/google-customer-match-activate-flow.png)請注意，如果目的地已有啟動流程，您可以看到目前傳送至目的地的區段。 選取 **[!UICONTROL 右側邊欄]** 「編輯啟動」，然後依照下列步驟修改啟動詳細資訊。
3. 選擇 **[!UICONTROL 激活]**;
4. 在「啟 **[!UICONTROL 動目標]** 」工作流程的「選 **[!UICONTROL 取區段」頁面上，選取要傳送的區段]**[!DNL Google Customer Match]。
   ![區段到目的地](/help/rtcdp/destinations/assets/activate-segments-google-customer-match.png)
5. 在「身 **[!UICONTROL 份映射]** 」步驟中，選擇要作為身份包括在此目標中的屬性。 選擇 **[!UICONTROL 新增對應]** ，並瀏覽您的架構，選擇電子郵件和／或雜湊電子郵件，然後將它們對應至對應的目標識別
   ![身份映射初始螢幕](/help/rtcdp/destinations/assets/gcm-identity-mapping.png) <br> 
   *純文字檔案電子郵件地址作為主要身份*:如果您的架構中有純文字（未雜湊）電子郵件地址作為主要身分識別，請選取「來源屬性」中的電子郵件欄位，並對應至「目標身分」下方右欄中的「電子郵件」欄位 ********，如下所示：
   ![選擇純文字檔案電子郵件身份](/help/rtcdp/destinations/assets/gcm-raw-email.gif) <br> 
   *雜湊的電子郵件地址作為主要身份*:如果您在架構中已將電子郵件地址雜湊為主要身份，請在「來源屬性」中選擇雜湊的電子郵件欄位，並映射至「目標身份」下方右欄中的「 **[!UICONTROL Email_LC_SHA256」欄位]******，如下所示：
   ![選擇雜湊電子郵件身份](/help/rtcdp/destinations/assets/gcm-hashed-emails.gif) <br> 
6. 在「區 **[!UICONTROL 段排程]** 」頁面上，您可以設定傳送資料至目的地的開始日期。
7. 在「審 **[!UICONTROL 閱]** 」頁面上，您可以看到您所選項目的摘要。 選擇 **[!UICONTROL 取消]** ，以劃分流程，選擇 **[!UICONTROL 返回]** ，修改設定，或選擇完 **[!UICONTROL 成]** ，確認選擇並開始向目標發送資料。

>[!IMPORTANT]
>
>在此步驟中，即時CDP檢查資料使用策略違規。 以下是違反原則的範例。 除非您解決違規問題，否則無法完成區段啟動工作流程。 有關如何解決違反策略的資訊，請參 [閱資料治理文檔部分](/help/rtcdp/privacy/data-governance-overview.md#enforcement) 中的策略實施。

![確認選擇](/help/rtcdp/destinations/assets/data-policy-violation.png)

如果未檢測到任何違反策略的情況，請選擇 **[!UICONTROL 完成]** ，確認您的選擇並開始向目標發送資料。

![確認選擇](/help/rtcdp/destinations/assets/gcm-review.png)


<!--

Insert in Step 6 when mobile device ID activation is available

    >[!IMPORTANT]
    >
    >If you select mobile device IDs (GAID or IDFA) as primary identity in the Identity mapping step, you must also provide an Application Id in this step. If you selected GAID as identity, see [Set the Application ID](https://developer.android.com/studio/build/application-id) in the Android developer documentation. IF you selected IDFA as identity, see [App ID](https://developer.android.com/studio/build/application-id) in the Apple developer documentation.

    ![segment schedule page](/help/rtcdp/destinations/assets/gcm-segment-schedule.png) 

-->

## 確認區段啟動成功 {#verify-activation}

完成啟動流程後，請切換至您的 **[!UICONTROL Google Ads帳戶]** 。 啟用的區段現在會以客戶清單的形式顯示在您的Google帳戶中。 請注意，視您的區段大小而定，除非有超過100位使用中使用者可供服務，否則不會填入某些對象。

## 其他資源 {#additional-resources}

* [整合Google客戶符合——教學課程影片](https://docs.adobe.com/content/help/en/platform-learn/tutorials/rtcdp/integrate-with-google-customer-match.html)