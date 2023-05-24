---
keywords: google客戶匹配；Google客戶匹配；Google客戶匹配
title: Google客戶匹配連接
description: Google客戶匹配允許您使用線上和離線資料在Google擁有和運營的資產(如搜索、購物、Gmail和YouTube)中與客戶聯繫並重新聯繫。
exl-id: 8209b5eb-b05c-4ef7-9fdc-22a528d5f020
source-git-commit: d6b34f3bd3a432e1cf7d3dcce242934391b65d78
workflow-type: tm+mt
source-wordcount: '1763'
ht-degree: 1%

---

# [!DNL Google Customer Match] 連接

## 總覽 {#overview}

[[!DNL Google Customer Match]](https://support.google.com/google-ads/answer/6379332?hl=en) 允許您使用線上和離線資料在Google自有和運營的物業中與客戶聯繫和重新接觸，例如： [!DNL Search]。 [!DNL Shopping]。 [!DNL Gmail], [!DNL YouTube]。

![Google客戶在Adobe Experience PlatformUI中匹配目標。](../../assets/catalog/advertising/google-customer-match/catalog.png)

## 使用案例 {#use-cases}

幫助您更好地瞭解如何和何時使用 [!DNL Google Customer Match] 目的地，以下是Adobe Experience Platform客戶可使用此功能解決的示例使用案例。

### 用例#1

運動服裝品牌希望通過 [!DNL Google Search] 和 [!DNL Google Shopping] 根據過去的購買和瀏覽歷史記錄個性化優惠和項目。 服裝品牌可以將電子郵件地址從自己的CRM接收到Experience Platform，並從自己的離線資料構建資料段。 然後，他們可以將這些段發送到 [!DNL Google Customer Match] 用於 [!DNL Search] 和 [!DNL Shopping]優化廣告支出。

### 用例#2

一家知名科技公司推出了一款新手機。 為了推廣這種新型號的手機，他們希望能夠讓擁有以前型號手機的客戶瞭解這款手機的新特性和功能。

要升級此版本，他們將電子郵件地址從其CRM資料庫上載到Experience Platform中，使用電子郵件地址作為標識符。 段是根據擁有較舊手機型號的客戶建立的。 然後將段發送到 [!DNL Google Customer Match]因此，公司可以瞄準當前客戶、擁有較舊手機型號的客戶和類似客戶 [!DNL YouTube]。

## 資料管理 [!DNL Google Customer Match] 目的地 {#data-governance}

某些Experience Platform中的目的地對於發送到目標平台或從目標平台接收的資料具有某些規則和義務。 您負責瞭解資料的局限性和義務，以及您如何在Adobe Experience Platform和目標平台中使用該資料。 Adobe Experience Platform公司提供資料治理工具，幫助您管理其中一些資料使用義務。 [瞭解更多資訊](../../../data-governance/labels/overview.md) 關於資料治理工具和策略。

## 支援的身份 {#supported-identities}

[!DNL Google Customer Match] 支援激活下表中描述的身份。 瞭解有關 [身份](/help/identity-service/namespaces.md)。

| 目標標識 | 說明 | 考量事項 |
|---|---|---|
| GAID | Google廣告ID | 當源標識為GAID命名空間時，選擇此目標標識。 |
| IDFA | Apple廣告商ID | 當源標識為IDFA命名空間時，選擇此目標標識。 |
| phone_sha256_e.164 | E164格式的電話號碼，使用SHA256算法散列 | 純文字檔案和SHA256散列電話號碼都受Adobe Experience Platform支援。 按照 [ID匹配要求](#id-matching-requirements-id-matching-requirements) 部分，並分別為純文字檔案和散列電話號碼使用相應的命名空間。 如果源欄位包含未散列的屬性，請檢查 **[!UICONTROL 應用轉換]** 選項 [!DNL Platform] 激活時自動對資料進行散列。 |
| email_lc_sha256 | 使用SHA256算法散列的電子郵件地址 | 純文字檔案和SHA256散列電子郵件地址都受Adobe Experience Platform支援。 按照 [ID匹配要求](#id-matching-requirements-id-matching-requirements) 中，分別使用純文字檔案和散列電子郵件地址的相應命名空間。 如果源欄位包含未散列的屬性，請檢查 **[!UICONTROL 應用轉換]** 選項 [!DNL Platform] 激活時自動對資料進行散列。 |
| 用戶ID | 自定義用戶ID | 如果源標識是自定義命名空間，請選擇此目標標識。 |

{style="table-layout:auto"}

## 導出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 導出類型 | **[!UICONTROL 區段匯出]** | 您正在導出段（受眾）的所有成員，其中使用的標識符（名稱、電話號碼和其他） [!DNL Google Customer Match] 目標。 |
| 導出頻率 | **[!UICONTROL 流]** | 流目標是基於API的「始終開啟」連接。 一旦基於段評估在Experience Platform中更新配置檔案，連接器就將更新下游發送到目標平台。 閱讀有關 [流目標](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## [!DNL Google Customer Match] 帳戶先決條件 {#google-account-prerequisites}

設定之前 [!DNL Google Customer Match] 目標Experience Platform，確保閱讀並遵守Google的使用策略 [!DNL Customer Match]，在 [Google支援文檔](https://support.google.com/google-ads/answer/6299717)。

接下來，確保 [!DNL Google] 為 [!DNL Standard] 或更高權限級別。 查看 [Google廣告文檔](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1) 的雙曲餘切值。

### 允許清單 {#allowlist}

在建立 [!DNL Google Customer Match] 目標Experience Platform，確保 [!DNL Google Ads] 帳戶符合 [[!DNL Google Customer Match] 政策](https://support.google.com/google-ads/answer/6299717/customer-match-policy)。

擁有合規帳戶的客戶將自動獲得Google的許可。

## ID匹配要求 {#id-matching-requirements}

[!DNL Google] 要求未清除發送個人身份資訊(PII)。 因此，觀眾被激活 [!DNL Google Customer Match] 可以鎖住 *散* 標識符，如電子郵件地址或電話號碼。

根據您在Adobe Experience Platform接收的ID類型，您必須遵守其相應要求。

### 電話號碼散列要求 {#phone-number-hashing-requirements}

在中激活電話號碼有兩種方法 [!DNL Google Customer Match]:

* **正在接收原始電話號碼**:你可以錄下原始電話號碼 [!DNL E.164] 格式 [!DNL Platform]，並在激活時自動對它們進行散列。 如果選擇此選項，請確保始終將原始電話號碼插入 `Phone_E.164` 命名空間。
* **正在攝取散列電話號碼**:你可以先對電話號碼進行散列，然後才能接收 [!DNL Platform]。 如果選擇此選項，請確保始終將散列電話號碼輸入到 `PHONE_SHA256_E.164` 命名空間。

>[!NOTE]
>
>接收到的電話號碼 `Phone` 無法在中激活命名空間 [!DNL Google Customer Match]。

### 電子郵件散列要求 {#hashing-requirements}

您可以在將電子郵件地址插入Adobe Experience Platform之前對它們進行散列，或在Experience Platform中使用明確的電子郵件地址，並且 [!DNL Platform] 在激活時對它們進行散列。

有關Google散列要求和激活的其他限制的詳細資訊，請參閱Google文檔中的以下各節：

* [[!DNL Customer Match] 具有電子郵件地址、地址或用戶ID](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_email_address_address_or_user_id)
* [[!DNL Customer Match] 注意事項](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_considerations)
* [[!DNL Customer Match] 帶有電話號碼](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_phone_number)
* [[!DNL Customer Match] 具有移動設備ID](https://developers.google.com/google-ads/api/docs/remarketing/audience-types/customer-match#customer_match_with_mobile_device_ids)


要瞭解在Experience Platform中插入電子郵件地址的資訊，請參閱 [批處理接收概述](../../../ingestion/batch-ingestion/overview.md) 和 [流式處理概述](../../../ingestion/streaming-ingestion/overview.md)。

如果您選擇自己對電子郵件地址進行散列，請確保符合上面連結中概述的Google的要求。

### 使用自定義命名空間 {#custom-namespaces}

在使用 `User_ID` 命名空間將資料發送到Google，確保使用 [!DNL gTag]。 請參閱 [Google官方檔案](https://support.google.com/google-ads/answer/9199250) 的上界。

<!-- Data from unhashed namespaces is automatically hashed by [!DNL Platform] upon activation.

Attribute source data is not automatically hashed. When your source field contains unhashed attributes, check the **[!UICONTROL Apply transformation]** option, to have [!DNL Platform] automatically hash the data on activation.
![Identity mapping transformation](../../assets/ui/activate-destinations/identity-mapping-transformation.png) -->

<!-- ## Configure destination - video walkthrough {#video}

The video below demonstrates the steps to configure a [!DNL Google Customer Match] destination and activate segments. The steps are also laid out sequentially in the next sections.

>[!VIDEO](https://video.tv.adobe.com/v/332599/?quality=12&learn=on&captions=eng) -->

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>要連接到目標，您需要 **[!UICONTROL 管理目標]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

要連接到此目標，請按照 [目標配置教程](../../ui/connect-destination.md)。

### 連接參數 {#parameters}

同時 [設定](../../ui/connect-destination.md) 此目標，必須提供以下資訊：

* **[!UICONTROL 名稱]**:為此目標連接提供名稱
* **[!UICONTROL 說明]**:提供此目標連接的說明
* **[!UICONTROL 帳戶ID]**:你 [Google廣告客戶ID](https://support.google.com/google-ads/answer/1704344?hl=en)。 ID的格式為xxx-xxx-xxxx。 如果使用 [!DNL Google Ads Manager Account (My Client Center)]，不要使用Manager帳戶ID。 使用 [Google廣告客戶ID](https://support.google.com/google-ads/answer/1704344?hl=en) 的雙曲餘切值。

>[!IMPORTANT]
>
> * 的 **[!UICONTROL 與PII結合]** 預設情況下，為 [!DNL Google Customer Match] 目標，無法刪除。


### 啟用警報 {#enable-alerts}

您可以啟用警報來接收有關目標資料流狀態的通知。 從清單中選擇要訂閱的警報以接收有關資料流狀態的通知。 有關警報的詳細資訊，請參閱上的指南 [使用UI訂閱目標警報](../../ui/alerts.md)。

完成提供目標連接的詳細資訊後，選擇 **[!UICONTROL 下一個]**。

## 將段激活到此目標 {#activate}

>[!IMPORTANT]
> 
>要激活資料，您需要 **[!UICONTROL 管理目標]**。 **[!UICONTROL 激活目標]**。 **[!UICONTROL 查看配置檔案]**, **[!UICONTROL 查看段]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

請參閱 [將受眾資料激活到流段導出目標](../../ui/activate-segment-streaming-destinations.md) 有關激活此目標受眾段的說明。

在 **[!UICONTROL 段計畫]** 步驟，必須提供 [!UICONTROL 應用ID] 發送 [!DNL IDFA] 或 [!DNL GAID] 段 [!DNL Google Customer Match]。

![Google客戶匹配應用ID](../../assets/catalog/advertising/google-customer-match/gcm-destination-appid.png)

有關如何查找 [!DNL App ID]，請參閱 [Google官方檔案](https://developers.google.com/adwords/api/docs/reference/v201809/AdwordsUserListService.CrmBasedUserList#appid)。

### 映射示例：激活受眾資料 [!DNL Google Customer Match] {#example-gcm}

這是激活中的受眾資料時正確身份映射的示例 [!DNL Google Customer Match]。

選擇源欄位：

* 選擇 `Email` 命名空間（如果您使用的電子郵件地址沒有散列）。
* 選擇 `Email_LC_SHA256` 命名空間作為源標識(如果在資料接收時已將客戶電子郵件地址插入到 [!DNL Platform]，根據 [!DNL Google Customer Match] [電子郵件散列要求](#hashing-requirements)。
* 選擇 `PHONE_E.164` 命名空間作為源標識（如果資料包含非散列電話號碼）。 [!DNL Platform] 將散列電話號碼以符合 [!DNL Google Customer Match] 要求。
* 選擇 `Phone_SHA256_E.164` 命名空間：源標識（如果對資料接收進行了電話號碼處理） [!DNL Platform]，根據 [!DNL Facebook] [電話號碼散列要求](#phone-number-hashing-requirements)。
* 選擇 `IDFA` 命名空間(如果資料包含 [!DNL Apple] 設備ID。
* 選擇 `GAID` 命名空間(如果資料包含 [!DNL Android] 設備ID。
* 選擇 `Custom` 命名空間，如果資料包含其他類型的標識符，則作為源標識。

選擇目標欄位：

* 選擇 `Email_LC_SHA256` 作為目標標識的命名空間 `Email` 或 `Email_LC_SHA256`。
* 選擇 `Phone_SHA256_E.164` 作為目標標識的命名空間 `PHONE_E.164` 或 `Phone_SHA256_E.164`。
* 選擇 `IDFA` 或 `GAID` 在源命名空間時作為目標標識的命名空間 `IDFA` 或 `GAID`。
* 選擇 `User_ID` 當源命名空間是自定義命名空間時，將命名空間作為目標標識。

![標識映射](../../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm.png)

來自未哈希命名空間的資料自動哈希由 [!DNL Platform] 激活後。

屬性源資料不會自動散列。 如果源欄位包含未散列的屬性，請檢查 **[!UICONTROL 應用轉換]** 選項 [!DNL Platform] 激活時自動對資料進行散列。

![身份映射轉換](../../assets/ui/activate-segment-streaming-destinations/identity-mapping-gcm-transformation.png)

## 驗證段激活是否成功 {#verify-activation}

完成激活流後，切換到 **[!UICONTROL Google廣告]** 帳戶。 激活的段在您的Google帳戶中顯示為客戶清單。 請注意，根據您的網段大小，除非有100多個活動用戶提供服務，否則不會填充某些受眾。

將段映射到兩者時 [!DNL IDFA] 和 [!DNL GAID] 移動ID, [!DNL Google Customer Match] 為每個ID映射建立單獨的段。 您 [!DNL Google Ads] 帳戶顯示兩個不同的段，一個 [!DNL IDFA]，一個 [!DNL GAID] 映射。

## 疑難排解 {#troubleshooting}

### 400錯誤請求錯誤消息 {#bad-request}

配置此目標時，可能會收到以下錯誤：

`{"message":"Google Customer Match Error: OperationAccessDenied.ACTION_NOT_PERMITTED","code":"400 BAD_REQUEST"}`

當客戶帳戶不符合 [先決條件](#google-account-prerequisites)。 要解決此問題，請與Google聯繫，並確保您的帳戶已允許列出並配置為 [!DNL Standard] 或更高權限級別。 查看 [Google廣告文檔](https://support.google.com/google-ads/answer/9978556?visit_id=637611563637058259-4176462731&amp;rd=1) 的雙曲餘切值。

## 其他資源 {#additional-resources}

* [整合 [!DNL Google Customer Match]  — 視頻教程](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/integrate-with-google-customer-match.html)

