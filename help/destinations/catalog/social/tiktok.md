---
title: TikTok
description: 利用您的資料在TikTok建立自定義受眾，以針對您的廣告活動。 這些觀眾可能是訪問您網站或與您的內容互動的人。 使用Adobe與TikTok廣告經理的即時整合，快速而安全地將所需的網段從Adobe Experience Platform推送到TikTok。
last-substantial-update: 2023-03-20T00:00:00Z
exl-id: 7b12d17f-7d9a-4615-9830-92bffe3f6927
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '980'
ht-degree: 2%

---

# TikTok

## 總覽 {#overview}

利用您的資料在TikTok建立自定義受眾，以針對您的廣告活動。 這些觀眾可能是訪問您網站或與您的內容互動的人。 使用Adobe與TikTok廣告經理的即時整合，快速而安全地將所需的網段從Adobe Experience Platform推送到TikTok。 訪問 [TikTok商務幫助中心](https://ads.tiktok.com/help/article/audiences?lang=en) 的子菜單。

>[!IMPORTANT]
>
>此文檔頁面由TikTok團隊建立。 如有任何查詢或更新請求，請直接聯繫他們，地址為： [https://ads.tiktok.com/help/](https://ads.tiktok.com/help/)。

## 使用案例 {#use-cases}

為了幫助您更好地瞭解您應如何以及何時使用TikTok目標，以下是Adobe Experience Platform客戶的示例使用案例。

### 使用案例 {#use-case-1}

一個運動服裝品牌希望通過社交媒體賬戶接觸現有客戶。 服裝品牌可以將自己的CRM中的電子郵件地址接收到Adobe Experience Platform，從自己的離線資料構建資料段，並將這些資料段發送到TikTok，以在客戶的社交媒體源中顯示廣告。

## 先決條件 {#prerequisites}

在將資料發送到 [!DNL TikTok Ads Manager] 帳戶，您需要授予Adobe Experience Platform權限才能訪問您的廣告帳戶 `Audience Management`。 可以通過在Experience Platform中輸入廣告商ID並遵循授予權限的重定向來提供此權限。 您可以在 [TikTokAPI文檔](https://ads.tiktok.com/marketing_api/docs?id=1738373141733378)。

## 支援的身份 {#supported-identities}

TikTok支援激活下表中描述的身份。 瞭解有關 [身份](/help/identity-service/namespaces.md)。

| 目標標識 | 說明 | 考量事項 |
|---|---|---|
| GAID | Google廣告ID | 當源標識為GAID命名空間時，選擇GAID目標標識。 |
| IDFA | Apple廣告商ID | 當源標識為IDFA命名空間時，選擇IDFA目標標識。 |
| 電話號碼 | 使用SHA256算法散列的電話號碼 | Adobe Experience Platform支援純文字檔案和SHA256散列電話號碼，並且它們必須採用E.164格式。 如果源欄位包含未散列的屬性，請檢查 **[!UICONTROL 應用轉換]** 選項 [!DNL Platform] 激活時自動對資料進行散列。 |
| 電子郵件 | 使用SHA256算法散列的電子郵件地址 | 純文字檔案和SHA256散列電子郵件地址都受Adobe Experience Platform支援。 如果源欄位包含未散列的屬性，請檢查 **[!UICONTROL 應用轉換]** 選項 [!DNL Platform] 激活時自動對資料進行散列。 |

{style="table-layout:auto"}

## 導出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 導出類型 | **[!UICONTROL 區段匯出]** | 您正在導出段（受眾）的所有成員，其中包含在TikTok目標中使用的標識符（名稱、電話號碼或其他）。 |
| 導出頻率 | **[!UICONTROL 流]** | 流目標是基於API的「始終開啟」連接。 一旦基於段評估在Experience Platform中更新配置檔案，連接器就將更新下游發送到目標平台。 閱讀有關 [流目標](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>要連接到目標，您需要 **[!UICONTROL 管理目標]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

要連接到此目標，請按照 [目標配置教程](../../ui/connect-destination.md)。 在配置目標工作流中，填寫下面兩節中列出的欄位。

### 驗證到目標 {#authenticate}

要向目標進行身份驗證，將重定向到登錄 [!DNL TikTok Ads Manager] 帳戶並授權Adobe代您管理受眾。

![TikTok權限選擇](/help/destinations/assets/catalog/social/tiktok/tiktok-authenticate-destination.png "用於選擇權限的TikTokUI映像")

### 填寫目標詳細資訊 {#destination-details}

要配置目標的詳細資訊，請填寫以下必需欄位和可選欄位。 UI中某個欄位旁邊的星號表示該欄位是必需的。

![目標連接詳細資訊](/help/destinations/assets/catalog/social/tiktok/tiktok-configure-destination-details.png "平台UI的影像，顯示要填充的目標連接詳細資訊")

* **[!UICONTROL 名稱]**:您將來識別此目標的名稱。
* **[!UICONTROL 說明]**:將幫助您在將來確定此目標的說明。
* **[!UICONTROL TikTok廣告經理ID]**:您 [!DNL TikTok Ads Manager ID]。 你可以在 [!DNL TikTok Ads manager] 帳戶。

![TikTok廣告經理ID](/help/destinations/assets/catalog/social/tiktok/tiktok-ads-manager-ID.png "TikTok廣告管理器UI的影像，顯示如何獲取TikTok廣告管理器ID")

### 啟用警報 {#enable-alerts}

您可以啟用警報來接收有關目標資料流狀態的通知。 從清單中選擇要訂閱的警報以接收有關資料流狀態的通知。 有關警報的詳細資訊，請參閱上的指南 [使用UI訂閱目標警報](../../ui/alerts.md)。

完成提供目標連接的詳細資訊後，選擇 **[!UICONTROL 下一個]**。

## 將段激活到此目標 {#activate}

>[!IMPORTANT]
> 
>要激活資料，您需要 **[!UICONTROL 管理目標]**。 **[!UICONTROL 激活目標]**。 **[!UICONTROL 查看配置檔案]**, **[!UICONTROL 查看段]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

閱讀 [激活配置檔案和段以流式處理段導出目標](/help/destinations/ui/activate-segment-streaming-destinations.md) 有關激活此目標受眾段的說明。

### 對應身分 {#map}

下面是將段導出到TikTok廣告管理器時正確標識映射的示例。

選擇源欄位：

* 選擇標識符(例如：` Email_LC_SHA256`)作為唯一標識Adobe Experience Platform和 [!DNL TikTok Ads Manager]。

選擇目標欄位：

* 選擇電子郵件命名空間作為目標標識。

![標識映射](/help/destinations/assets/catalog/social/tiktok/tiktok-map-identity.png "平台UI的映像，標識的映射")

## 導出的資料 {#exported-data}

檢查 [!DNL TikTok Ads Manager] 帳戶(在 **資產>受眾**)以驗證是否成功導出Experience Platform段。 受眾將被填充為受眾類型： `Partner Audience`。

## 資料使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目標在處理資料時符合資料使用策略。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料治理，讀取 [資料治理概述](/help/data-governance/home.md)。

## 其他資源 {#additional-resources}

請參閱 [TikTok幫助中心頁](https://ads.tiktok.com/help/article/audiences?lang=en) 的雙曲餘切值。
