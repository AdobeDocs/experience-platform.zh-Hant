---
keywords: facebook擴充功能；facebook擴充功能；facebook目的地；facebook;instagram;messenger;facebook Messenger
title: Facebook延伸功能目的地
description: 根據雜湊的電子郵件，啟用您Facebook宣傳的個人檔案，以鎖定受眾、個人化和抑制受眾。
translation-type: tm+mt
source-git-commit: aa2088d30716f56ac2909214badbb39c0ae97855
workflow-type: tm+mt
source-wordcount: '952'
ht-degree: 3%

---


# [!DNL Facebook] 擴充功能

>[!IMPORTANT]
>
>客戶目前正在向新目標版本遷移。 在遷移完成之前，您只會看到此目標的[!UICONTROL EMAIL]和[!UICONTROL EMAIL_LC_SHA_256]可用身份。

啟用[!DNL Facebook]促銷活動的設定檔，根據雜湊的電子郵件鎖定受眾、個人化和抑制受眾。

您可以將此目標用於[!DNL Facebook’s]系列應用程式（包括[!DNL Facebook]、[!DNL Instagram]、[!DNL Audience Network]和[!DNL Messenger]）中的受眾定位。 [!DNL Custom Audiences]在 [!DNL Facebook Ads Manager] 中的廣告版位層級會指出您選擇針對哪個應用程式執行行銷活動。

![Adobe Experience Platform UI中的Facebook目標](../../assets/catalog/social/facebook/catalog.png)

## 使用案例

為協助您進一步瞭解應如何及何時使用[!DNL Facebook]目標，以下是Adobe Experience Platform客戶可使用此功能解決的兩個範例使用案例。

### 使用案例#1

線上零售商想透過社交平台接觸現有客戶，並根據先前的訂單向他們展示個人化優惠。 線上零售商可將其CRM的電子郵件位址內嵌至Adobe Experience Platform，從其線下資料建立細分，並將這些細分傳送至[!DNL Facebook]社交平台，以最佳化其廣告支出。

### 使用案例#2

航空公司有不同的客戶層級（銅、銀和金），並希望透過社交平台為每個層級提供個人化優惠。 不過，並非所有客戶都使用該航空公司的行動應用程式，其中有些客戶尚未登入該公司網站。 公司對於這些客戶的唯一識別碼是會籍ID和電子郵件地址。

若要跨社交媒體鎖定客戶，他們可以將客戶資料從CRM載入Adobe Experience Platform，使用電子郵件地址做為識別碼。

接著，他們可以使用離線資料（包括相關的會籍ID和客戶層級）來建立新的受眾細分，以便透過[!DNL Facebook]目標鎖定。

## 目標詳細資訊{#destination-specs}

### [!DNL Facebook]目標{#data-governance}的資料控管

>[!IMPORTANT]
>
>傳送至[!DNL Facebook]的資料不應包含銜接身分。 您有責任履行此義務，並可確保選定進行啟動的區段不會在其合併政策中使用拼接選項來履行此義務。 進一步瞭解[合併策略](/help/profile/ui/merge-policies.md)。

### 導出類型{#export-type}

**區段匯出** -您正匯出區段（對象）的所有成員，並包含識別碼（名稱、電話號碼等）用於Facebook目的地。

### Facebook帳戶先決條件{#facebook-account-prerequisites}

在將對象區段傳送至[!DNL Facebook]之前，請確定您符合下列需求：

- 您的[!DNL Facebook]使用者帳戶必須已針對您計畫使用的廣告帳戶啟用&#x200B;**[!DNL Manage campaigns]**&#x200B;權限。
- **Adobe Experience Cloud**&#x200B;商業帳戶必須新增為[!DNL Facebook Ad Account]的廣告合作夥伴。 使用 `business ID=206617933627973`。如需詳細資訊，請參閱Facebook檔案中的[將合作夥伴新增至您的業務經理](https://www.facebook.com/business/help/1717412048538897)。
   >[!IMPORTANT]
   >
   > 設定Adobe Experience Cloud的權限時，您必須啟用「管理促銷活動&#x200B;**」權限。**&#x200B;這是進行 [!DNL Adobe Experience Platform] 整合的必要權限。
- 閱讀並簽署[!DNL Facebook Custom Audiences]服務條款。 若要完成此操作，請前往 `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`，其中 `accountID` 是您的 [!DNL Facebook Ad Account ID]。

### ID匹配要求{#id-matching-requirements}

[!DNL Facebook] 要求不會傳送任何個人識別資訊(PII)。因此，激活至[!DNL Facebook]的觀眾可以鍵入&#x200B;*雜湊*&#x200B;標識符，如電子郵件地址或電話號碼。

視您將ID收錄至Adobe Experience Platform的類型而定，您必須符合其相應的需求。

#### 電話號碼雜湊要求{#phone-number-hashing-requirements}

在[!DNL Facebook]中啟用電話號碼有兩種方法：

- **接收原始電話號碼**:您可以將原始電話號碼以格 [!DNL E.164] 式內嵌 [!DNL Platform]至，在啟動時會自動雜湊。如果您選擇此選項，請務必將原始電話號碼永遠收錄到`Phone_E.164`命名空間中。
- **接收雜湊電話號碼**:您可先將電話號碼雜湊，再將其擷取 [!DNL Platform]。如果您選擇此選項，請務必將雜湊電話號碼永遠收錄到`Phone_SHA256`命名空間中。

>[!NOTE]
>
>不能在[!DNL Facebook]中激活包含在`Phone`名稱空間中的電話號碼。


#### 電子郵件散列要求{#email-hashing-requirements}

您可以選擇先對電子郵件地址進行雜湊處理，然後再將它們匯入Adobe Experience Platform，或者選擇在Experience Platform中清楚處理電子郵件地址，並讓我們的演算法在啟動時對它們進行雜湊處理。

若要瞭解如何在Experience Platform中擷取電子郵件地址，請參閱[批次擷取概觀](/help/ingestion/batch-ingestion/overview.md)和[蒸發擷取概觀](/help/ingestion/streaming-ingestion/overview.md)。

如果您選擇自行排列電子郵件地址，請務必符合下列要求：

- 從電子郵件字串中修剪所有前導和尾隨空格；範例：`johndoe@example.com`，而非`<space>johndoe@example.com<space>`;
- 在對電子郵件字串進行散列時，請務必對小寫字串進行散列；
   - 範例：`example@email.com`，而非`EXAMPLE@EMAIL.COM`;
- 請確定雜湊字串全部為小寫
   - 範例：`55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`，而非`55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
- 別用鹽鹽。

啟動後，[!DNL Platform]會自動雜湊來自未雜湊名稱空間的資料。

屬性來源資料不會自動雜湊。 當您的來源欄位包含未雜湊的屬性時，請勾選「套用轉換&#x200B;]**」選項，讓[!DNL Platform]在啟動時自動雜湊資料。**[!UICONTROL ![身份映射轉換](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

#### 使用自訂名稱空間{#custom-namespaces}

在使用`Extern_ID`命名空間將資料傳送至[!DNL Facebook]之前，請務必使用[!DNL Facebook Pixel]同步您自己的識別碼。 如需詳細資訊，請參閱[官方檔案](https://developers.facebook.com/docs/marketing-api/audiences/guides/custom-audiences/#external_identifiers)。

## 連接到目標{#connect-destination}

若要連線至[!DNL Facebook]目的地，請參閱[社交網路目的地驗證工作流程](./workflow.md)。

## 啟用區段至[!DNL Facebook] {#activate-segments}

如需如何啟用區段至[!DNL Facebook]的指示，請參閱[啟用資料至目標](../../ui/activate-destinations.md)。

在&#x200B;**[!UICONTROL 區段排程]**&#x200B;步驟中，傳送區段至[!DNL Facebook Custom Audiences]時，您必須提供[!UICONTROL 觀眾來源]。

![Facebook對象來源](../../assets/catalog/social/facebook/facebook-origin-audience.png)

## 導出資料{#exported-data}

對於[!DNL Facebook]，成功啟動表示[!DNL Facebook]自訂觀眾將以程式設計方式建立在[[!DNL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/)中。 當使用者符合已啟用區段的資格或被取消資格時，會新增及移除觀眾中的區段成員資格。

>[!TIP]
>
>Adobe Experience Platform與[!DNL Facebook]的整合可支援歷史觀眾回填。 當您將區段啟動至目標時，所有歷史區段資格都會傳送至[!DNL Facebook]。