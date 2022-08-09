---
keywords: facebook連接；facebook連接；facebook目標；facebook;instagram;facebook
title: Facebook
description: 激活您的Facebook市場活動的配置檔案，以便根據經過散列的電子郵件進行受眾目標、個性化和壓制。
exl-id: 51e8c8f0-5e79-45b9-afbc-110bae127f76
source-git-commit: 70670f7aec2ab6a5594f5e69672236c7bcc3ce81
workflow-type: tm+mt
source-wordcount: '1859'
ht-degree: 1%

---

# [!DNL Facebook] 連接

## 總覽 {#overview}

激活您的配置檔案 [!DNL Facebook] 針對受眾的營銷活動，根據散列的電子郵件進行定位、個性化和壓制。

您可以將此目標用於跨目標對象 [!DNL Facebook’s] 受支援的應用系列 [!DNL Custom Audiences]，包括 [!DNL Facebook]。 [!DNL Instagram]。 [!DNL Audience Network], [!DNL Messenger]。 在 [!DNL Facebook Ads Manager] 中的廣告版位層級會指出您選擇針對哪個應用程式執行行銷活動。

![Facebook目的地：Adobe Experience PlatformUI](../../assets/catalog/social/facebook/catalog.png)

## 使用案例

幫助您更好地瞭解如何和何時使用 [!DNL Facebook] 目的地，下面是Adobe Experience Platform客戶可通過使用此功能解決的兩個示例使用案例。

### 用例#1

一家線上零售商希望通過社交平台接觸現有客戶，並根據他們之前的訂單向他們展示個性化的優惠。 該線上零售商可以將電子郵件地址從自己的CRM接收到Adobe Experience Platform，從自己的離線資料構建段，並將這些段發送到 [!DNL Facebook] 社交平台，優化廣告支出。

### 用例#2

航空公司有不同的客戶層（銅牌、銀牌和金牌），希望通過社交平台為每個層提供個性化服務。 然而，並非所有客戶都使用該航空公司的移動應用，其中一些客戶還沒有登錄該公司的網站。 公司擁有的有關這些客戶的唯一標識符是成員資格ID和電子郵件地址。

為了在社交媒體上瞄準他們，他們可以將客戶資料從CRM載入Adobe Experience Platform，使用電子郵件地址作為標識符。

接下來，他們可以使用其離線資料（包括關聯的成員身份ID和客戶層）構建新的受眾群，通過 [!DNL Facebook] 目標。

## 支援的身份 {#supported-identities}

[!DNL Facebook Custom Audiences] 支援激活下表中描述的身份。 瞭解有關 [身份](/help/identity-service/namespaces.md)。

| 目標標識 | 說明 | 考量事項 |
|---|---|---|
| GAID | Google廣告ID | 當源標識為GAID命名空間時，選擇GAID目標標識。 |
| IDFA | Apple廣告商ID | 當源標識為IDFA命名空間時，選擇IDFA目標標識。 |
| phone_sha256 | 使用SHA256算法散列的電話號碼 | 純文字檔案和SHA256散列電話號碼都受Adobe Experience Platform支援。 按照 [ID匹配要求](#id-matching-requirements-id-matching-requirements) 部分，並分別為純文字檔案和散列電話號碼使用相應的命名空間。 如果源欄位包含未散列的屬性，請檢查 **[!UICONTROL 應用轉換]** 選項 [!DNL Platform] 激活時自動對資料進行散列。 |
| email_lc_sha256 | 使用SHA256算法散列的電子郵件地址 | 純文字檔案和SHA256散列電子郵件地址都受Adobe Experience Platform支援。 按照 [ID匹配要求](#id-matching-requirements-id-matching-requirements) 中，分別使用純文字檔案和散列電子郵件地址的相應命名空間。 如果源欄位包含未散列的屬性，請檢查 **[!UICONTROL 應用轉換]** 選項 [!DNL Platform] 激活時自動對資料進行散列。 |
| 外部ID | 自定義用戶ID | 如果源標識是自定義命名空間，請選擇此目標標識。 |

## 導出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 導出類型 | **[!UICONTROL 區段匯出]** | 您正在導出段（受眾）的所有成員，其中包含在Facebook目標中使用的標識符（名稱、電話號碼或其他）。 |
| 導出頻率 | **[!UICONTROL 流]** | 流目標是基於API的「始終開啟」連接。 一旦基於段評估在Experience Platform中更新配置檔案，連接器就將更新下游發送到目標平台。 閱讀有關 [流目標](/help/destinations/destination-types.md#streaming-destinations)。 |

{style=&quot;table-layout:auto&quot;}

## Facebook帳戶先決條件 {#facebook-account-prerequisites}

在將受眾段發送到 [!DNL Facebook]，確保滿足以下要求：

* 您 [!DNL Facebook] 用戶帳戶必須具有 **[!DNL Manage campaigns]** 已為您計畫使用的Ad帳戶啟用權限。
* 的 **Adobe Experience Cloud** 必須將業務帳戶添加為廣告合作夥伴 [!DNL Facebook Ad Account]。 使用 `business ID=206617933627973`. 請參閱 [將合作夥伴添加到您的業務經理](https://www.facebook.com/business/help/1717412048538897) 在Facebook文檔中。
   >[!IMPORTANT]
   >
   > 為Adobe Experience Cloud配置權限時，必須啟用 **管理市場活動** 權限。 需要權限 [!DNL Adobe Experience Platform] 整合。
* 閱讀並簽名 [!DNL Facebook Custom Audiences] 服務條款。 要執行此操作，請轉至 `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`，也請參見Wiki頁。 `accountID` 你 [!DNL Facebook Ad Account ID]。
   >[!IMPORTANT]
   >
   >簽名時 [!DNL Facebook Custom Audiences] 服務條款，確保使用您在FacebookAPI中進行身份驗證時使用的相同用戶帳戶。

## ID匹配要求 {#id-matching-requirements}

[!DNL Facebook] 要求未清除發送個人身份資訊(PII)。 因此，觀眾被激活 [!DNL Facebook] 可以鎖住 *散* 標識符，如電子郵件地址或電話號碼。

根據您在Adobe Experience Platform接收的ID類型，您必須遵守其相應要求。

## 電話號碼散列要求 {#phone-number-hashing-requirements}

在中激活電話號碼有兩種方法 [!DNL Facebook]:

* **正在接收原始電話號碼**:你可以錄下原始電話號碼 [!DNL E.164] 格式 [!DNL Platform]。 它們在激活時自動散列。 如果選擇此選項，請確保始終將原始電話號碼插入 `Phone_E.164` 命名空間。
* **正在攝取散列電話號碼**:你可以先對電話號碼進行散列，然後才能接收 [!DNL Platform]。 如果選擇此選項，請確保始終將散列電話號碼輸入到 `Phone_SHA256` 命名空間。

>[!NOTE]
>
>接收到的電話號碼 `Phone` 無法在中激活命名空間 [!DNL Facebook]。

## 電子郵件散列要求 {#email-hashing-requirements}

您可以在將電子郵件地址插入Adobe Experience Platform之前對它們進行散列，或在Experience Platform中使用明確的電子郵件地址，並且 [!DNL Platform] 在激活時對它們進行散列。

要瞭解在Experience Platform中插入電子郵件地址的資訊，請參閱 [批處理接收概述](/help/ingestion/batch-ingestion/overview.md) 和 [流式處理概述](/help/ingestion/streaming-ingestion/overview.md)。

如果您選擇自己對電子郵件地址進行散列，請確保符合以下要求：

* 從電子郵件字串中裁切所有前導空格和尾隨空格；示例： `johndoe@example.com`不 `<space>johndoe@example.com<space>`;
* 散列電子郵件字串時，確保散列小寫字串；
   * 示例： `example@email.com`不 `EXAMPLE@EMAIL.COM`;
* 確保散列字串全部為小寫
   * 示例： `55e79200c1635b37ad31a378c39feb12f120f116625093a19bc32fff15041149`不 `55E79200C1635B37AD31A378C39FEB12F120F116625093A19bC32FFF15041149`;
* 別用鹽把繩子撒了。

>[!NOTE]
>
>來自未哈希命名空間的資料自動哈希由 [!DNL Platform] 激活後。
> 屬性源資料不會自動散列。 如果源欄位包含未散列的屬性，請檢查 **[!UICONTROL 應用轉換]** 選項 [!DNL Platform] 激活時自動對資料進行散列。
> 的 **[!UICONTROL 應用轉換]** 選項。 選擇命名空間時不顯示它。

![身份映射轉換](../../assets/ui/activate-destinations/identity-mapping-transformation.png)

## 使用自定義命名空間 {#custom-namespaces}

在使用 `Extern_ID` 將資料發送到的命名空間 [!DNL Facebook]，確保您使用 [!DNL Facebook Pixel]。 查看 [Facebook官方檔案](https://developers.facebook.com/docs/marketing-api/audiences/guides/custom-audiences/#external_identifiers) 的上界。

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>要連接到目標，您需要 **[!UICONTROL 管理目標]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

要連接到此目標，請按照 [目標配置教程](../../ui/connect-destination.md)。 在配置目標工作流中，填寫下面兩節中列出的欄位。

下面的視頻還演示了配置 [!DNL Facebook] 目標和激活段。

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng)

>[!NOTE]
>
>Experience Platform用戶介面頻繁更新，自此視頻記錄後可能已更改。 有關最新資訊，請參閱 [目標配置教程](../../ui/connect-destination.md)。

### 驗證到目標 {#authenticate}

1. 在目標目錄中查找Facebook目標，然後選擇 **[!UICONTROL 設定]**。
2. 選擇 **[!UICONTROL 連接到目標]**。
   ![驗證到Facebook](/help/destinations/assets/catalog/social/facebook/authenticate-facebook-destination.png)
3. 輸入您的Facebook憑據並選擇 **登錄**。

### 填寫目標詳細資訊 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_facebook_accountid"
>title="帳戶 ID"
>abstract="你的Facebook廣告帳戶ID。 您可以在Facebook廣告經理帳戶中找到此ID。 輸入此ID時，請始終將其前置詞 `act_`。"

要配置目標的詳細資訊，請填寫以下必需欄位和可選欄位。 UI中某個欄位旁邊的星號表示該欄位是必需的。

* **[!UICONTROL 名稱]**:您將來識別此目標的名稱。
* **[!UICONTROL 說明]**:將幫助您在將來確定此目標的說明。
* **[!UICONTROL 帳戶ID]**:您 [!DNL Facebook Ad Account ID]。 您可以在 [!DNL Facebook Ads Manager] 帳戶。 輸入此ID時，請始終將其前置詞 `act_`。

### 啟用警報 {#enable-alerts}

您可以啟用警報來接收有關目標資料流狀態的通知。 從清單中選擇要訂閱的警報以接收有關資料流狀態的通知。 有關警報的詳細資訊，請參閱上的指南 [使用UI訂閱目標警報](../../ui/alerts.md)。

完成提供目標連接的詳細資訊後，選擇 **[!UICONTROL 下一個]**。

## 將段激活到此目標 {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience"
>title="受眾來源"
>abstract="選擇最初收集段中客戶資料的方式。 當用戶被段鎖定時，資料將顯示在Facebook"

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience_customers"
>title="受眾來源"
>abstract="廣告商直接從客戶那裡收集資料。"

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience_partners"
>title="受眾來源"
>abstract="廣告商直接從合作夥伴那裡收集資料。"

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_facebook_originofaudience_customersandpartners"
>title="受眾來源"
>abstract="廣告商直接從客戶和合作夥伴那裡收集資料。"

>[!IMPORTANT]
> 
>要激活資料，您需要 **[!UICONTROL 管理目標]**。 **[!UICONTROL 激活目標]**。 **[!UICONTROL 查看配置檔案]**, **[!UICONTROL 查看段]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

請參閱 [將受眾資料激活到流段導出目標](../../ui/activate-segment-streaming-destinations.md) 有關激活此目標受眾段的說明。

在 **[!UICONTROL 段計畫]** 步驟，必須提供 [!UICONTROL 受眾來源] 將段發送到 [!DNL Facebook Custom Audiences]。

![Facebook觀眾起源](../../assets/catalog/social/facebook/facebook-origin-audience.png)

### 映射示例：激活受眾資料 [!DNL Facebook Custom Audience] {#example-facebook}

下面是激活以下內容中的受眾資料時正確身份映射的示例 [!DNL Facebook Custom Audience]。

選擇源欄位：

* 選擇 `Email` 命名空間（如果您使用的電子郵件地址沒有散列）。
* 選擇 `Email_LC_SHA256` 命名空間作為源標識(如果在資料接收時已將客戶電子郵件地址插入到 [!DNL Platform]，根據 [!DNL Facebook] [電子郵件散列要求](#email-hashing-requirements)。
* 選擇 `PHONE_E.164` 命名空間作為源標識（如果資料包含非散列電話號碼）。 [!DNL Platform] 將散列電話號碼以符合 [!DNL Facebook] 要求。
* 選擇 `Phone_SHA256` 命名空間：源標識（如果對資料接收進行了電話號碼處理） [!DNL Platform]，根據 [!DNL Facebook] [電話號碼散列要求](#phone-number-hashing-requirements)。
* 選擇 `IDFA` 命名空間(如果資料包含 [!DNL Apple] 設備ID。
* 選擇 `GAID` 命名空間(如果資料包含 [!DNL Android] 設備ID。
* 選擇 `Custom` 命名空間，如果資料包含其他類型的標識符，則作為源標識。

選擇目標欄位：

* 選擇 `Email_LC_SHA256` 作為目標標識的命名空間 `Email` 或 `Email_LC_SHA256`。
* 選擇 `Phone_SHA256` 作為目標標識的命名空間 `PHONE_E.164` 或 `Phone_SHA256`。
* 選擇 `IDFA` 或 `GAID` 在源命名空間時作為目標標識的命名空間 `IDFA` 或 `GAID`。
* 選擇 `Extern_ID` 當源命名空間是自定義命名空間時，將命名空間作為目標標識。

>[!IMPORTANT]
>
>來自未哈希命名空間的資料自動哈希由 [!DNL Platform] 激活後。
> 
>屬性源資料不會自動散列。 如果源欄位包含未散列的屬性，請檢查 **[!UICONTROL 應用轉換]** 選項 [!DNL Platform] 激活時自動對資料進行散列。

![標識映射](../../assets/ui/activate-segment-streaming-destinations/mapping-summary.png)

## 導出的資料 {#exported-data}

對於 [!DNL Facebook]，成功激活表示 [!DNL Facebook] 自定義訪問群體將以寫程式方式在 [[!DNL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/)。 當用戶符合激活的段的條件或取消其資格時，將添加和刪除在受眾中的段成員資格。

>[!TIP]
>
>Adobe Experience Platform與 [!DNL Facebook] 支援歷史受眾回填。 所有歷史段資格均發送至 [!DNL Facebook] 將段激活到目標。

## 疑難排解 {#troubleshooting}

### 400錯誤請求錯誤消息 {#bad-request}

配置此目標時，可能會收到以下錯誤：

`{"message":"Facebook Error: Permission error","code":"400 BAD_REQUEST"}`

當客戶使用新建立的帳戶時， [!DNL Facebook] 權限尚未激活。

如果您收到 `400 Bad Request` 執行中的步驟後出現錯誤消息 [Facebook帳戶先決條件](#facebook-account-prerequisites)，請允許幾天 [!DNL Facebook] 權限生效。
