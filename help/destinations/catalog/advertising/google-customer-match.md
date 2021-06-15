---
keywords: Google客戶比對；Google客戶比對；Google客戶比對
title: Google Customer Match連線
description: Google Customer Match可讓您使用您的線上和離線資料，透過Google擁有且運作的屬性(例如Search、Shopping、Gmail及YouTube)，觸及客戶並與其重新互動。
exl-id: 8209b5eb-b05c-4ef7-9fdc-22a528d5f020
source-git-commit: da069c6c931bfd2af38b40fc061d5eb633aba9ea
workflow-type: tm+mt
source-wordcount: '1521'
ht-degree: 0%

---

# [!DNL Google Customer Match] 連接

## 概覽 {#overview}

[Google Customer ](https://support.google.com/google-ads/answer/6379332?hl=en) Match可讓您使用您的線上和離線資料，在Google擁有且運作的屬性中觸及客戶並與其重新互動，例如： [!DNL Search]、  [!DNL Shopping]、  [!DNL Gmail]和 [!DNL YouTube]。

![Adobe Experience Platform UI中的Google Customer Match目的地](../../assets/catalog/advertising/google-customer-match/catalog.png)

## 使用個案

為協助您更清楚了解使用[!DNL Google Customer Match]目的地的方式和時機，以下是Adobe Experience Platform客戶可透過此功能解決的範例使用案例。

### 使用案例#1

運動服飾品牌想要透過[!DNL Google Search]和[!DNL Google Shopping]觸及現有客戶，以根據其過去的購買和瀏覽記錄來個人化選件和項目。 服飾品牌可從自己的CRM擷取電子郵件地址至Experience Platform，並從自己的離線資料建立區段。 接著，他們可以將這些區段傳送至[!DNL Google Customer Match]以用於[!DNL Search]和[!DNL Shopping]，最佳化其廣告支出。

### 使用案例#2

一家知名科技公司推出了一款新手機。 為了推廣這種新手機型號，他們希望讓擁有舊款手機的客戶了解這款手機的新功能。

為了促銷此版本，他們使用電子郵件地址做為識別碼，從其CRM資料庫上傳電子郵件地址至Experience Platform。 會根據擁有舊款手機型號的客戶來建立區段。 然後，區段會傳送至[!DNL Google Customer Match]，以便公司可鎖定目前的客戶、擁有舊手機型號的客戶，以及[!DNL YouTube]上的類似客戶。

## [!DNL Google Customer Match]目的地{#data-governance}的資料控管

Experience Platform中的某些目的地對於傳送至目的地平台或從目的地平台接收的資料，有特定的規則和義務。 您有責任了解資料的限制和義務，以及如何在Adobe Experience Platform和目的地平台中使用該資料。 Adobe Experience Platform提供資料控管工具，可協助您管理其中部分資料使用義務。 [進一步](../../../data-governance/labels/overview.md) 了解資料控管工具和原則。

## 支援的身分{#supported-identities}

[!DNL Google Customer Match] 支援啟用下表所述的身分。深入了解[identities](/help/identity-service/namespaces.md)。

| Target身分 | 說明 | 考量事項 |
|---|---|---|
| GAID | Google廣告ID | 當源標識為GAID命名空間時，選擇此目標標識。 |
| IDFA | 廣告商專用的Apple ID | 當您的來源識別為IDFA命名空間時，請選取此目標識別。 |
| phone_sha256_e.164 | E164格式的電話號碼，使用SHA256演算法雜湊 | Adobe Experience Platform支援純文字和SHA256雜湊電話號碼。 請依照[ID匹配要求](#id-matching-requirements-id-matching-requirements)一節中的指示，並分別將適當的命名空間用於純文字和雜湊電話號碼。 當源欄位包含未雜湊屬性時，請核取&#x200B;**[!UICONTROL Apply transformation]**&#x200B;選項，讓[!DNL Platform]在啟動時自動雜湊資料。 |
| email_lc_sha256 | 使用SHA256演算法雜湊的電子郵件地址 | Adobe Experience Platform支援純文字和SHA256雜湊電子郵件地址。 請依照[ID符合需求](#id-matching-requirements-id-matching-requirements)一節中的指示，並分別將適當的命名空間用於純文字和雜湊電子郵件地址。 當源欄位包含未雜湊屬性時，請核取&#x200B;**[!UICONTROL Apply transformation]**&#x200B;選項，讓[!DNL Platform]在啟動時自動雜湊資料。 |
| user_id | 自訂使用者ID | 當源標識為自定義命名空間時，選擇此目標標識。 |

## 導出類型{#export-type}

**區段匯出**  — 您會匯出區段（對象）的所有成員，以及目的地中使用的識別碼(名稱、電話號碼及其他 [!DNL Google Customer Match] )。

## [!DNL Google Customer Match] 帳戶必要條件  {#google-account-prerequisites}

在Experience Platform中設定[!DNL Google Customer Match]目的地之前，請務必閱讀並遵循[!DNL Customer Match]中概述的Google支援檔案](https://support.google.com/google-ads/answer/6299717)中的使用[原則。

### 允許清單 {#allowlist}

在Experience Platform中建立[!DNL Google Customer Match]目的地之前，請確定您的[!DNL Google Ads]帳戶符合[Google客戶比對原則](https://support.google.com/google-ads/answer/6299717/customer-match-policy)。

Google會自動允許帳戶符合規範的客戶列出。

## ID匹配要求{#id-matching-requirements}

[!DNL Google] 需要清楚傳送任何個人識別資訊(PII)。因此，對[!DNL Google Customer Match]啟動的對象可以被去除&#x200B;*雜湊*&#x200B;識別碼，例如電子郵件地址或電話號碼。

視您擷取至Adobe Experience Platform的ID類型而定，您必須遵守其對應要求。

## 電話號碼雜湊要求{#phone-number-hashing-requirements}

在[!DNL Google Customer Match]中激活電話號碼有兩種方法：

* **擷取原始電話號碼**:您可以將原始電話號碼以格式內 [!DNL E.164] 嵌至， [!DNL Platform]這些電話號碼一經啟用就會自動雜湊。如果選擇此選項，請務必始終將原始電話號碼嵌入`Phone_E.164`命名空間。
* **擷取雜湊電話號碼**:您可以先預先雜湊電話號碼，再擷取至 [!DNL Platform]中。如果選擇此選項，請務必始終將雜湊電話號碼內嵌到`PHONE_SHA256_E.164`命名空間中。

>[!NOTE]
>
>無法在[!DNL Google Customer Match]中激活被錄入`Phone`命名空間的電話號碼。

## 電子郵件雜湊要求{#hashing-requirements}

您可以在將電子郵件地址擷取至Adobe Experience Platform之前先雜湊電子郵件地址，或在Experience Platform中清楚使用電子郵件地址，並在啟用時讓[!DNL Platform]雜湊這些地址。

如需Google雜湊要求和其他啟用限制的詳細資訊，請參閱Google檔案中的下列章節：

* [[!DNL Customer Match] 包含電子郵件地址、地址或使用者ID](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_email_address_address_or_user_id)
* [[!DNL Customer Match] 考量事項](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_considerations)
* [客戶與電話號碼匹配](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_phone_number)
* [與行動裝置ID的客戶比對](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_mobile_device_ids)


若要了解如何以Experience Platform擷取電子郵件地址，請參閱[批次擷取概述](../../../ingestion/batch-ingestion/overview.md)和[串流擷取概述](../../../ingestion/streaming-ingestion/overview.md)。

如果您選擇自行雜湊電子郵件地址，請務必遵守上述連結中概述的Google要求。

## 使用自訂命名空間{#custom-namespaces}

使用`User_ID`命名空間將資料傳送至Google之前，請務必使用[!DNL gTag]同步您自己的識別碼。 如需詳細資訊，請參閱[Google官方檔案](https://support.google.com/google-ads/answer/9199250)。

<!-- Data from unhashed namespaces is automatically hashed by [!DNL Platform] upon activation.

Attribute source data is not automatically hashed. When your source field contains unhashed attributes, check the **[!UICONTROL Apply transformation]** option, to have [!DNL Platform] automatically hash the data on activation.
![Identity mapping transformation](../../assets/ui/activate-destinations/identity-mapping-transformation.png) -->

## 設定目的地 — 視訊逐步說明 {#video}

以下影片示範設定[!DNL Google Customer Match]目的地和啟用區段的步驟。 步驟也按順序排列在下幾節中。

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

## 連接到目標{#connect-destination}

在&#x200B;**[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**&#x200B;中，捲動至&#x200B;**[!UICONTROL Advertising]**&#x200B;類別。 選擇[!DNL Google Customer Match]，然後選擇&#x200B;**[!UICONTROL 配置]**。

![連線至Google Customer Match目的地](../../assets/catalog/advertising/google-customer-match/connect.png)

>[!NOTE]
>
>如果與此目的地的連線存在，您可以在目的地卡片上看到&#x200B;**[!UICONTROL 啟動]**&#x200B;按鈕。 有關&#x200B;**[!UICONTROL Activate]**&#x200B;和&#x200B;**[!UICONTROL Configure]**&#x200B;之間差異的詳細資訊，請參閱目標工作區檔案的[Catalog](../../ui/destinations-workspace.md#catalog)區段。

在&#x200B;**帳戶**&#x200B;步驟中，如果您先前已設定到[!DNL Google Customer Match]目的地的連線，請選擇&#x200B;**[!UICONTROL 現有帳戶]**&#x200B;並選擇您的現有連線。 或者，您可以選擇&#x200B;**[!UICONTROL 新帳戶]**&#x200B;以設定與[!DNL Google Customer Match]的新連接。 若要登入Adobe Experience Cloud並將其連線至您的[!DNL Google Ad]帳戶，請選取「**[!UICONTROL 連線至目的地]**」。

>[!NOTE]
>
>Experience Platform支援驗證過程中的憑據驗證。 如果您為[!DNL Google Ad]帳戶輸入了錯誤的憑證，以確保您沒有使用錯誤的憑證完成工作流程，則會顯示錯誤訊息。

![連線至Google Customer Match目的地 — 驗證步驟](../../assets/catalog/advertising/google-customer-match/connection.png)

確認憑證並將Adobe Experience Cloud連線至您的Google帳戶後，您可以選取&#x200B;**[!UICONTROL Next]**&#x200B;以繼續&#x200B;**[!UICONTROL Authentication]**&#x200B;步驟。

![確認憑據](../../assets/catalog/advertising/google-customer-match/connection-success.png)

在&#x200B;**[!UICONTROL Authentication]**&#x200B;步驟中，輸入激活流的&#x200B;**[!UICONTROL Name]**&#x200B;和&#x200B;**[!UICONTROL Description]**，並填寫Google **[!UICONTROL Account ID]**。

在此步驟中，您也可以選取套用至此目的地的任何&#x200B;**[!UICONTROL 行銷動作]**。 行銷動作會指出資料匯出至目的地的目的。 您可以從Adobe定義的行銷動作中選取，或者您可以建立自己的行銷動作。 如需行銷動作的詳細資訊，請參閱[資料使用原則概述](../../../data-governance/policies/overview.md)。

在填寫上述欄位後，選擇&#x200B;**[!UICONTROL 建立目標]**。

>[!IMPORTANT]
>
> * 預設會為[!DNL Google Customer Match]目的地選取&#x200B;**[!UICONTROL 結合PII]**&#x200B;行銷動作，且無法移除。
> * 針對[!DNL Google Customer Match]目的地。 **[!UICONTROL 帳]** 戶ID是您使用Google的客戶用戶端ID。ID的格式為xxx-xxx-xxxx。


![連接Google Customer Match — 驗證步驟](../../assets/catalog/advertising/google-customer-match/authentication.png)

您的目的地現在已建立。 如果您想稍後啟動區段，可以選取&#x200B;**[!UICONTROL 儲存並退出]**，或選取&#x200B;**[!UICONTROL 下一步]**&#x200B;以繼續工作流程並選取要啟動的區段。 無論是哪種情況，請參閱工作流程其餘部分的下一節「將區段啟用至 [!DNL Google Customer Match]](#activate-segments)」。[

## 將區段啟用至[!DNL Google Customer Match] {#activate-segments}

如需如何將區段啟用至[!DNL Google Customer Match]的指示，請參閱[將資料啟用至目的地](../../ui/activate-destinations.md)。


在&#x200B;**[!UICONTROL 區段排程]**&#x200B;步驟中，傳送[!DNL IDFA]或[!DNL GAID]區段至[!DNL Google Customer Match]時，您必須提供[!UICONTROL 應用程式ID]。

![Google客戶比對應用程式ID](../../assets/catalog/advertising/google-customer-match/gcm-destination-appid.png)

有關如何查找[!DNL App ID]的詳細資訊，請參閱[Google官方檔案](https://developers.google.com/adwords/api/docs/reference/v201809/AdwordsUserListService.CrmBasedUserList#appid)。

## 確認區段啟動成功{#verify-activation}

完成啟動流程後，切換至您的&#x200B;**[!UICONTROL Google Ads]**&#x200B;帳戶。 已啟動的區段會在您的Google帳戶中顯示為客戶清單。 請注意，除非有超過100個使用中使用者提供服務，否則不會填入部分對象（視您的區段大小而定）。

將區段對應至[!DNL IDFA]和[!DNL GAID]行動ID時， [!DNL Google Customer Match]會為每個ID對應建立個別的區段。 您的[!DNL Google Ads]帳戶會顯示兩個不同的區段，一個用於[!DNL IDFA]，另一個用於[!DNL GAID]對應。

## 額外資源{#additional-resources}

* [整合Google Customer Match — 教學課程影片](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/integrate-with-google-customer-match.html)
