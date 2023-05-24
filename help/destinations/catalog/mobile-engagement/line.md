---
keywords: 移動；移動接洽目標；LINE;LINE移動接洽目標
title: 線路連接
description: LINE目標允許您將配置檔案添加到平台段，並為連接的用戶提供個性化體驗。
last-substantial-update: 2022-11-08T00:00:00Z
exl-id: 9981798a-61f2-4a09-9a33-57e63eb36d43
source-git-commit: 83778bc5d643f69e0393c0a7767fef8a4e8f66e9
workflow-type: tm+mt
source-wordcount: '1180'
ht-degree: 0%

---

# [!DNL LINE] 連接

## 總覽 {#overview}

[[!DNL LINE]](https://line.me/en/) 是一個熱門的溝通平台，它連接了人、服務和資訊，並已從聊天應用發展成為娛樂、社交和日常活動的中心。

此 [!DNL Adobe Experience Platform] [目標](/help/destinations/home.md) 利用 [[!DNL LINE] 消息傳遞API](https://developers.line.biz/en/reference/messaging-api/)。 您可以在Experience Platform段中作為連接激活配置檔案 [!DNL LINE] 滿足您的業務需要。

[!DNL LINE] 使用承載令牌作為與 [!DNL LINE] 消息傳遞API。 驗證到您 [!DNL LINE] 下面是實例， [驗證到目標](#authenticate) 的子菜單。

## 使用案例 {#use-cases}

作為營銷人員，您可以將移動項目目標中的用戶作為目標，並內置段 [!DNL Adobe Experience Platform]。 此外，您可以根據客戶的屬性為他們提供個性化體驗 [!DNL Adobe Experience Platform] 配置檔案，一旦在中更新段和配置檔案 [!DNL Adobe Experience Platform]。

## 先決條件 {#prerequisites}

### [!DNL LINE] 先決條件 {#prerequisites-destination}

請注意以下先決條件 [!DNL LINE]，以便將資料從平台導出到 [!DNL LINE] 帳戶：

#### 你需要 [!DNL LINE] 帳戶 {#prerequisites-account}

您需要註冊並建立 [!DNL LINE] 帳戶，如果你還沒有。 要建立帳戶：

1. 導航到 [!DNL LINE] [帳戶登錄](https://account.line.biz/login?redirectUri=https%3A%2F%2Fmanager.line.biz%2F) 頁
2. 選擇 **[!UICONTROL 建立帳戶]**。

#### 收集 [!DNL LINE channel access token (long-lived)] 從 [!DNL LINE] 開發者控制台 {#gather-credentials}

允許平台訪問 [!DNL LINE] 資源，你需要 *[!DNL Channel access token (long-lived)]* 從所需 [!DNL LINE] *消息傳遞API* 頻道。

1. 使用 [!DNL LINE] 帳戶 [[!DNL LINE] 開發人員控制台](https://developers.line.biz/console)。
1. 接下來，訪問 *[!DNL Providers]* ，然後選擇 *[!DNL Provider]* 並最終選擇 *消息傳遞API* 訪問其設定的通道。 如果您首次訪問開發人員控制台，請遵循 [[!DNL LINE] 文檔](https://developers.line.biz/en/docs/messaging-api/getting-started/) 完成建立提供程式所需的步驟。
1. 最後，導航到 ***[!DNL Channel access token]*** 並複製 ***[!DNL Channel access token (long-lived)]*** 所需值 [驗證到目標](#authenticate) 的子菜單。

| 憑據 | 說明 | 範例 |
| --- | --- | --- |
| `[!DNL Channel access token (long-lived)]` | 您的 [!DNL LINE Channel access token (long-lived)]。 | `aaa2112XSMWqLXR7..........nyilFU=` |

請參閱 [[!DNL LINE] 文檔](https://developers.line.biz/en/docs/messaging-api/getting-started/) 有關建立渠道或將渠道添加到現有渠道的指導 [!DNL LINE] 帳戶 [!DNL LINE] 開發人員控制台。

## 支援的身份 {#supported-identities}

[!DNL LINE] 支援更新和導出下表中描述的身份。 瞭解有關 [身份](/help/identity-service/namespaces.md)。

| 目標標識 | 說明 |
|---|---|
| 廣告商ID | 當源標識為IFA時，為廣告商(IFA)目標標識選擇ID *(廣告商的AppleID)* 或GAID *(Google廣告ID)命名空間。 |
| 行用戶ID | 當源標識為LINE用戶ID時，選擇UserID目標標識。 |

## 導出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 導出類型 | **[!UICONTROL 基於配置檔案]** | 您正在導出段（受眾）的所有成員，其中使用的標識符（名稱、電話號碼或其他） [!DNL LINE] 目標。 |
| 導出頻率 | **[!UICONTROL 流]** | 流目標是基於API的「始終開啟」連接。 一旦基於段評估在Experience Platform中更新配置檔案，連接器就將更新下游發送到目標平台。 閱讀有關 [流目標](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## 連接到目標 {#connect}

>[!IMPORTANT]
>
>要連接到目標，您需要 **[!UICONTROL 管理目標]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

要連接到此目標，請按照 [目標配置教程](../../ui/connect-destination.md)。 在配置目標工作流中，填寫下面兩節中列出的欄位。

在 **[!UICONTROL 目標]** > **[!UICONTROL 目錄]** 搜索 [!DNL LINE]。 或者，可將其定位在 **[!UICONTROL 移動接洽]** 的子菜單。

### 驗證到目標 {#authenticate}

要驗證到目標，請選擇 **[!UICONTROL 連接到目標]**。
![平台UI螢幕快照，顯示如何進行身份驗證。](../../assets/catalog/mobile-engagement/line/authenticate-destination.png)

填寫下面的必填欄位。
* **[!UICONTROL 持有者令牌]**:您 [!DNL LINE Channel access token (long-lived)] 從 [!DNL LINE] 開發人員控制台。 請參閱 [收集憑據](#gather-credentials) 的子菜單。

如果提供的詳細資訊有效，UI將顯示 **[!UICONTROL 已連接]** 狀態為綠色複選標籤。 然後，可以繼續下一步。

### 填寫目標詳細資訊 {#destination-details}

要配置目標的詳細資訊，請填寫以下必需欄位和可選欄位。 UI中某個欄位旁邊的星號表示該欄位是必需的。
![顯示目標詳細資訊的平台UI螢幕快照。](../../assets/catalog/mobile-engagement/line/destination-details.png)

* **[!UICONTROL 名稱]**:您將來識別此目標的名稱。
* **[!UICONTROL 說明]**:將幫助您在將來確定此目標的說明。
* **[!UICONTROL 受眾類型]**:選擇 **[!UICONTROL 廣告商ID]** 如果您要導出的標識類型 *廣告商ID*。 選擇 **[!UICONTROL 行用戶ID]** 如果您要導出的標識類型 *行用戶ID*。 請參閱 [支援的身份](#supported-identities) 的子菜單。

### 啟用警報 {#enable-alerts}

您可以啟用警報來接收有關目標資料流狀態的通知。 從清單中選擇要訂閱的警報以接收有關資料流狀態的通知。 有關警報的詳細資訊，請參閱上的指南 [使用UI訂閱目標警報](../../ui/alerts.md)。

完成提供目標連接的詳細資訊後，選擇 **[!UICONTROL 下一個]**。

## 將段激活到此目標 {#activate}

>[!IMPORTANT]
>
>要激活資料，您需要 **[!UICONTROL 管理目標]**。 **[!UICONTROL 激活目標]**。 **[!UICONTROL 查看配置檔案]**, **[!UICONTROL 查看段]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

閱讀 [激活配置檔案和段以流式處理段導出目標](/help/destinations/ui/activate-segment-streaming-destinations.md) 有關激活此目標受眾段的說明。

### 映射屬性和標識 {#map}

正確將您的受眾資料從Adobe Experience Platform發送到 [!DNL LINE] 目標，您需要完成欄位映射步驟。 映射包括在您的平台帳戶中的「體驗資料模型」(XDM)架構欄位與目標目標中對應的欄位之間建立連結。 正確將XDM欄位映射到 [!DNL LINE] 目標欄位，請執行以下步驟：

根據源標識，必須映射以下目標標識命名空間： |目標標識 |源欄位 |目標欄位 | | - | - | - | |廣告商ID(IFA) | `IDFA` 或 `GAID` | `LineId` | |行用戶ID | `UserID` | `LineId` |

如果目標身份是 *行用戶ID* 您需要以下內容：
![平台UI螢幕快照示例，顯示在將LINE用戶ID用於目標標識時的目標映射。](../../assets/catalog/mobile-engagement/line/mappings-userid.png)

如果目標標識為 *廣告商ID* 您需要以下內容：
![平台UI螢幕快照示例，顯示在將廣告商ID(IFA)用於目標標識時目標映射。](../../assets/catalog/mobile-engagement/line/mappings-idfa.png)

## 驗證資料導出 {#exported-data}

成功導出Experience Platform後， [!DNL LINE] 目標在 [!DNL LINE] 使用選定段名。

要驗證您是否正確設定了目標，請執行以下步驟：

1. 在 [!DNL LINE]，登錄到 [Manager控制台](https://manager.line.biz/)。

1. 接下來，導航到 **[!UICONTROL 資料控制項]** > **[!UICONTROL 觀眾]** 並檢查與 **[!UICONTROL 受眾名稱]** 的雙曲餘切值。

1. 更新的卷將與段內的計數相匹配。

1. 的 *類型* 列將提及 **[!UICONTROL 用戶ID]** 如果導出的標識屬於 *用戶ID*。 同樣， *類型* 列將提及 **[!UICONTROL 移動廣告ID]** 如果導出的標識屬於 *IDFA*。

中的示例設定 [!DNL LINE] 如下所示：
![顯示觀眾卷的LINE UI螢幕截圖。](../../assets/catalog/mobile-engagement/line/audience-volume.png)

## 資料使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目標在處理資料時符合資料使用策略。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料治理，請參見 [資料治理概述](/help/data-governance/home.md)。
