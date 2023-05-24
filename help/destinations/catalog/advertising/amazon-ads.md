---
title: Amazon廣告
description: Amazon廣告為註冊銷售商、銷售商、圖書銷售商、Kindle Direct Publishing(KDP)作者、應用程式開發商和/或代理提供了一系列選項來幫助您實現廣告目標。 Amazon廣告與Adobe Experience Platform的整合為Amazon廣告產品，包括Amazon(ADSP)提供DSP了轉鍵整合。 使用Adobe Experience Platform的Amazon廣告目的地，用戶能夠定義廣告客戶受眾，以在Amazon進行定位和激DSP活。
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 724f3d32-65e0-4612-a882-33333e07c5af
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '1277'
ht-degree: 1%

---

# (Beta)Amazon廣告連接 {#amazon-ads}

## 總覽 {#overview}

Amazon廣告為註冊銷售商、銷售商、圖書銷售商、Kindle Direct Publishing(KDP)作者、應用程式開發商和/或代理提供了一系列選項來幫助您實現廣告目標。

Amazon廣告與Adobe Experience Platform的整合為Amazon廣告產品，包括Amazon(ADSP)提供DSP了轉鍵整合。 使用Adobe Experience Platform的Amazon廣告目的地，用戶能夠定義廣告客戶受眾，以在Amazon進行定位和激DSP活。

此連接支援以下Amazon市場中的受眾建立： `US`。 `CA`。 `MX`。 `BR`。

>[!IMPORTANT]
>
>此文檔頁面由 *Amazon廣告* 團隊。 這是當前的試用版產品，功能可能會更改。 如有任何查詢或更新請求，請直接聯繫他們，地址為： *`amc-support@amazon.com`。*

## 使用案例 {#use-cases}

幫助您更好地瞭解您應如何以及何時使用 *Amazon廣告* 目的地，以下是Adobe Experience Platform客戶可通過使用此目的地解決的示例使用案例。

### 激活和定向 {#activation-and-targeting}

與Amazon的DSP整合使Amazon廣告商能夠將廣告商的CDP片段從Adobe Experience Platform傳遞到Amazon,DSP以創造廣告商受眾以進行廣告定位。 可以在Amazon內選DSP擇觀眾進行正面瞄準和負面瞄準（壓制）。 此外，利用通過AmazonMarketing Cloud產生的信號，廣告商可以優化其廣告商受眾，從而使受眾變化與Amazon同DSP步。

## 先決條件 {#prerequisites}

為了使用Amazon廣告與Adobe Experience Platform的連接，用戶必須首先能夠訪問AmazonDSP廣告商帳戶。  要提供這些實例，請訪問Amazon廣告網站的以下頁面：

* [開始使用AmazonDSP](https://advertising.amazon.com/solutions/products/amazon-dsp?ref_=a20m_us_hnav_p_dsp_adtech)

## 支援的身份 {#supported-identities}

的 *Amazon廣告* 連接支援激活下表中描述的身份。 瞭解有關 [身份](/help/identity-service/namespaces.md)。 有關Amazon廣告支援的身份的詳細資訊，請訪問 [AmazonDSP支援中心](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE)。

| 目標標識 | 說明 | 考量事項 |
|---|---|---|
| phone_sha256 | 使用SHA256算法散列的電話號碼 | 純文字檔案和SHA256散列電話號碼都受Adobe Experience Platform支援。 如果源欄位包含未散列的屬性，請檢查 **[!UICONTROL 應用轉換]** 選項 [!DNL Platform] 激活時自動對資料進行散列。 |
| email_lc_sha256 | 使用SHA256算法散列的電子郵件地址 | 純文字檔案和SHA256散列電子郵件地址都受Adobe Experience Platform支援。 如果源欄位包含未散列的屬性，請檢查 **[!UICONTROL 應用轉換]** 選項 [!DNL Platform] 激活時自動對資料進行散列。 |

{style="table-layout:auto"}

## 導出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 導出類型 | **[!UICONTROL 區段匯出]** | 您正在導出段（受眾）的所有成員，其中使用的標識符（名稱、電話號碼或其他） *Amazon廣告* 目標。 |
| 導出頻率 | **[!UICONTROL 流]** | 流目標是基於API的「始終開啟」連接。 一旦基於段評估在Experience Platform中更新配置檔案，連接器就將更新下游發送到目標平台。 閱讀有關 [流目標](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>要連接到目標，您需要 **[!UICONTROL 管理目標]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

要連接到此目標，請按照 [目標配置教程](../../ui/connect-destination.md)。 在配置目標工作流中，填寫下面兩節中列出的欄位。

### 驗證到目標 {#authenticate}

要驗證到目標，請填寫必填欄位並選擇 **[!UICONTROL 連接到目標]**。

您將被帶到Amazon廣告連接介面，在該介面中，您將首先選擇要連接到的廣告商帳戶。  連接後，您將重定向回Adobe Experience Platform，並帶有您選擇的廣告商帳戶的ID。 在目標配置螢幕上選擇相應的廣告商帳戶以繼續。

* **[!UICONTROL 持有者令牌]**:填寫承載令牌以驗證到目標。

### 填寫目標詳細資訊 {#destination-details}

要配置目標的詳細資訊，請填寫以下必需欄位和可選欄位。 UI中某個欄位旁邊的星號表示該欄位是必需的。

* **[!UICONTROL 名稱]**:您將來識別此目標的名稱。
* **[!UICONTROL 說明]**:將幫助您在將來確定此目標的說明。
* **[!UICONTROL Amazon廣告商ID]**:選擇用於目標的目標Amazon廣告帳戶的ID。

注：選擇此Amazon廣告商ID後，您需要建立新目標來更改此項。 如果您重新驗證OAuth憑據並選擇新的廣告商ID，則您所做的更改將不適用。

![配置新目標](../../assets/catalog/advertising/amazon_ads_image_1.png)

### 啟用警報 {#enable-alerts}

您可以啟用警報來接收有關目標資料流狀態的通知。 從清單中選擇要訂閱的警報以接收有關資料流狀態的通知。 有關警報的詳細資訊，請參閱上的指南 [使用UI訂閱目標警報](../../ui/alerts.md)。

完成提供目標連接的詳細資訊後，選擇 **[!UICONTROL 下一個]**。

## 將段激活到此目標 {#activate}

>[!IMPORTANT]
> 
>要激活資料，您需要 **[!UICONTROL 管理目標]**。 **[!UICONTROL 激活目標]**。 **[!UICONTROL 查看配置檔案]**, **[!UICONTROL 查看段]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

閱讀 [激活配置檔案和段以流式處理段導出目標](/help/destinations/ui/activate-segment-streaming-destinations.md) 有關激活此目標受眾段的說明。

### 映射屬性和標識 {#map}

Amazon廣告連接支援散列電子郵件地址和散列電話號碼，以便進行身份匹配。  下面的螢幕截圖提供了一個與Amazon廣告連接相容的匹配示例：

![Adobe到Amazon廣告地圖](../../assets/catalog/advertising/amazon_ads_image_2.png)

* 要映射散列的電子郵件地址，請選擇 `Email_LC_SHA256` 標識名稱空間作為源欄位。
* 要映射散列電話號碼，請選擇 `Phone_SHA256` 標識名稱空間作為源欄位。
* 要映射未散列的電子郵件地址或電話號碼，請選擇相應的標識命名空間作為源欄位，然後檢查 `Apply Transformation` 選項，使平台在激活時散列標識。

強烈建議您映射可用的盡可能多的欄位。 如果只有一個源屬性可用，則可以映射一個欄位。  Amazon廣告目的地將利用所有映射的欄位進行映射，如果提供更多欄位，則可獲得更高的匹配率。 有關接受的標識符的詳細資訊，請訪問 [Amazon廣告散播了受眾幫助頁面](https://advertising.amazon.com/dsp/help/ss/en/audiences#GA6BC9BW52YFXBNE)。

## 導出的資料/驗證資料導出 {#exported-data}

上載受眾後，您可以使用以下步驟驗證您的受眾是否已建立並正確上載：

**為Amazon DSP**

導航到您的廣告商ID →觀眾→廣告商受眾。 如果您的受眾已成功建立並且滿足最小受眾成員數，則您將看到的狀態為 `Active`。  有關觀眾規模和訪問範圍的其他詳細資訊，可在Amazon用戶介面右側的「預測訪問」面DSP板中找到。

![AmazonDSP觀眾建立驗證](../../assets/catalog/advertising/amazon_ads_image_3.png)

## 資料使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目標在處理資料時符合資料使用策略。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料治理，讀取 [資料治理概述](/help/data-governance/home.md)。

## 其他資源 {#additional-resources}

有關其他幫助文檔，請訪問以下Amazon廣告幫助資源：

* [AmazonDSP幫助中心](https://advertising.amazon.com/dsp/help/ss/en/audiences#/)
