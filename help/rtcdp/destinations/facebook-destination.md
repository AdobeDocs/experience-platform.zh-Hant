---
title: Facebook目標
seo-title: Facebook目標
description: 根據雜湊的電子郵件，啟用您Facebook宣傳的個人檔案，以鎖定受眾、個人化和抑制受眾。
seo-description: 根據雜湊的電子郵件，啟用您Facebook宣傳的個人檔案，以鎖定受眾、個人化和抑制受眾。
translation-type: tm+mt
source-git-commit: faaa4eda5174bb8d27a76d767891df15df69e30a
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 0%

---


# Facebook目標

## 概述 {#overview}

根據雜湊的電子郵件，啟用您Facebook宣傳的個人檔案，以鎖定受眾、個人化和抑制受眾。

## 使用案例

為協助您更清楚瞭解您應如何及何時使用Facebook目標，以下是Adobe即時客戶資料平台客戶可使用此功能解決的兩個範例使用案例。


### 使用案例#1


線上零售商想透過社交平台接觸現有客戶，並根據先前的訂單向他們展示個人化優惠。 線上零售商可將其CRM的電子郵件位址內嵌至Adobe即時CDP，從其線下資料建立細分，並將這些細分傳送至Facebook社交平台，以最佳化其廣告支出。


### 使用案例#2


航空公司有不同的客戶層級（銅、銀和金），並希望透過社交平台為每個層級提供個人化優惠。 不過，並非所有客戶都使用該航空公司的行動應用程式，其中有些客戶尚未登入該公司網站。 公司對於這些客戶的唯一識別碼是會籍ID和電子郵件地址。
若要跨社交媒體鎖定客戶，他們可以將客戶資料從CRM載入Adobe即時CDP，並使用雜湊的電子郵件地址做為識別碼。
接下來，他們可以將離線資料與現有的線上活動資料結合，以建立新的受眾細分，以便透過Facebook目標進行鎖定。

## 目的地細節 {#destination-specs}

### Facebook目的地的資料管理 {#data-governance}

>[!IMPORTANT]
>
>傳送至Facebook的資料不應包含銜接身分。 您有責任履行此義務，並可確保選定進行啟動的區段不會在其合併政策中使用拼接選項來履行此義務。 進一步瞭解合 [並原則](/help/profile/ui/merge-policies.md)。

### 啟動類型 {#activation-type}

**區段匯出** -您正匯出區段（對象）的所有成員，並包含識別碼（名稱、電話號碼等） 用於Facebook目的地。

### Facebook帳戶先決條件 {#facebook-account-prerequisites}

在將受眾細分傳送至之前，請 [!DNL Facebook]確定您符合下列需求：

1. 您 [!DNL Facebook] 的使用者帳戶必須為您 **[!DNL Manage campaigns]** 計畫使用的廣告帳戶啟用權限。
2. 將 **Adobe Experience Cloud商業帳戶新增為廣告合作夥伴**[!DNL Facebook Ad Account]。 使用 `business ID=206617933627973`。 如需詳 [細資訊，請參閱Facebook檔案中的](https://www.facebook.com/business/help/1717412048538897) 「將合作夥伴新增至您的業務經理」。
   >[!IMPORTANT]
   > 設定Adobe Experience Cloud的權限時，您必須啟用「管理促銷 **活動** 」權限。 這是整合的必 [!DNL Adobe Real-time CDP] 要項。
3. 閱讀並簽署 [!DNL Facebook Custom Audiences] 服務條款。 若要這麼做，請前 `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`往您的 `accountID` 位置 [!DNL Facebook Ad Account ID]。

### 電子郵件雜湊要求 {#email-hashing-requirements}

Facebook要求不要求傳送任何個人識別資訊(PII)。 因此，啟動至Facebook的觀眾必須關閉雜湊的 *電子郵件* 位址。 您可以選擇先對電子郵件地址進行雜湊處理，然後再將它們匯入Adobe Experience Platform，或者選擇在Experience Platform中清楚處理電子郵件地址，並讓我們的演算法在啟動時對它們進行雜湊處理。

若要瞭解如何在Experience Platform中擷取電子郵件地址，請參閱批次 [擷取概觀](/help/ingestion/batch-ingestion/overview.md) ，以 [及快速擷取概觀](/help/ingestion/streaming-ingestion/overview.md)。

如果您選擇自行排列電子郵件地址，請務必符合下列要求：

* 從電子郵件字串中修剪所有前導和尾隨空格； 範例： `johndoe@example.com`，不是 `<space>johndoe@example.com<space>`;
* 在對電子郵件字串進行散列時，請務必對小寫字串進行散列；
   * 範例： `example@email.com`，不是 `EXAMPLE@EMAIL.COM`;
* 請確定雜湊字串全部為小寫
   * 範例： `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`，不是 `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
* 別用鹽鹽。


>[!IMPORTANT]
>
>如果您選擇不散列電子郵件地址，Adobe Real-time CDP會在您啟動區段至Facebook時為您執行此動作。 在啟動 [工作流程](/help/rtcdp/destinations/activate-destinations.md#activate-data) （請參閱步驟5）中，針對原始電子郵件位址選取如 `Email` 下所示的選項 *，並針對雜湊的電子郵件位址選*`Email_LC_SHA256`**&#x200B;取下列選項。


![啟動時雜湊](/help/rtcdp/destinations/assets/identity-mapping.png)

## 連接到目標 {#connect-destination}

若要連線至Facebook目的地，請參閱 [Social網路目的地驗證工作流程](/help/rtcdp/destinations/social-network-destinations-workflow.md)。


## 啟用區段至Facebook {#activate-segments}

如需如何啟用區段至Facebook的指示，請參閱啟 [用資料至目標](/help/rtcdp/destinations/activate-destinations.md)。