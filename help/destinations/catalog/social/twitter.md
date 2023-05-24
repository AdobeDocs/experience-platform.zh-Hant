---
title: Twitter自定義觀眾連接
description: 瞄準您在Twitter的現有追隨者和客戶，並通過激活您在Adobe Experience Platform內構建的受眾來建立相關的再營銷活動
exl-id: fd244e58-cd94-4de7-81e4-c321eb673b65
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '806'
ht-degree: 4%

---

# [!DNL Twitter Custom Audiences] 連接

## 總覽 {#overview}

瞄準您在Twitter的現有追隨者和客戶，並通過激活您在Adobe Experience Platform內構建的受眾來建立相關的再營銷活動。

## 先決條件 {#prerequisites}

在配置之前 [!DNL Twitter Custom Audiences] 目標，確保查看您需要滿足的以下Twitter先決條件。

1. 您 [!DNL Twitter Ads] 帳戶必須符合廣告資格。 新建 [!DNL Twitter Ads] 帳戶在建立後的頭2週內無資格進行廣告。
2. 您授權訪問的Twitter用戶帳戶 [!DNL Twitter Audience Manager] 必須 *[!DNL Partner Audience Manager]* 權限已啟用。

## 支援的身份 {#supported-identities}

[!DNL Twitter Custom Audiences] 支援激活下表中描述的身份。 瞭解有關 [身份](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started)。

| 目標標識 | 說明 | 考量事項 |
|---|---|---|
| 設備id | IDFA/AdID/Android ID | Google廣告ID(GAID)和Apple廣告商IDFA(IDFA)在Adobe Experience Platform得到支援。 請相應地在中從源架構映射這些命名空間和/或屬性 [映射步驟](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) 目標激活工作流。 |
| 電子郵件 | 用戶的電子郵件地址 | 請將純文字檔案電子郵件地址和SHA256散列的電子郵件地址映射到此欄位。 如果源欄位包含未散列的屬性，請檢查 **[!UICONTROL 應用轉換]** 選項 [!DNL Platform] 激活時自動對資料進行散列。 如果您在將客戶電子郵件地址上傳到Adobe Experience Platform之前先對它們進行散列，請注意，這些標識必須使用SHA256進行散列，而不需要鹽。 |

{style="table-layout:auto"}

## 導出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 導出類型 | **[!UICONTROL 區段匯出]** | 您正在導出段（受眾）的所有成員，其標識符在Twitter自定義受眾目標中使用。 |
| 導出頻率 | **[!UICONTROL 流]** | 流目標是基於API的「始終開啟」連接。 一旦基於段評估在Experience Platform中更新配置檔案，連接器就將更新下游發送到目標平台。 閱讀有關 [流目標](/help/destinations/destination-types.md#streaming-destinations)。 |

{style="table-layout:auto"}

## 使用案例 {#use-cases}

幫助您更好地瞭解您應如何以及何時使用 [!DNL Twitter Custom Audiences] 目的地，以下是Adobe Experience Platform客戶可通過使用此目的地解決的示例使用案例。

### 用例#1

瞄準您在Twitter的現有追隨者和客戶，並通過激活您在Adobe Experience Platform內構建的受眾，建立相關的再營銷活動 [!DNL List Custom Audiences] 在Twitter。

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>要連接到目標，您需要 **[!UICONTROL 管理目標]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

要連接到此目標，請按照 [目標配置教程](../../ui/connect-destination.md)。 在配置目標工作流中，填寫下面兩節中列出的欄位。

### 驗證到目標 {#authenticate}

1. 查找 [!DNL Twitter Custom Audiences] 目標目錄中的目標，然後選擇 **[!UICONTROL 設定]**。
2. 選擇 **[!UICONTROL 連接到目標]**。
   ![驗證到LinkedIn](/help/destinations/assets/catalog/social/twitter/authenticate-twitter-destination.png)
3. 輸入您的Twitter憑據並選擇 **登錄**。

### 填寫目標詳細資訊 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_twitter_accountid"
>title="帳戶 ID"
>abstract="您的 Twitter 廣告帳戶 ID。這可以在您的 Twitter 廣告設定中找到。"

要配置目標的詳細資訊，請填寫以下必需欄位和可選欄位。 UI中某個欄位旁邊的星號表示該欄位是必需的。

* **[!UICONTROL 名稱]**:您將來識別此目標的名稱。
* **[!UICONTROL 說明]**:將幫助您在將來確定此目標的說明。
* **[!UICONTROL 帳戶ID]**:您 [!DNL Twitter Ads] 帳戶ID。 可以在 [!DNL Twitter Ads] 的子菜單。

### 啟用警報 {#enable-alerts}

您可以啟用警報來接收有關目標資料流狀態的通知。 從清單中選擇要訂閱的警報以接收有關資料流狀態的通知。 有關警報的詳細資訊，請參閱上的指南 [使用UI訂閱目標警報](../../ui/alerts.md)。

完成提供目標連接的詳細資訊後，選擇 **[!UICONTROL 下一個]**。

## 將段激活到此目標 {#activate}

>[!IMPORTANT]
> 
>要激活資料，您需要 **[!UICONTROL 管理目標]**。 **[!UICONTROL 激活目標]**。 **[!UICONTROL 查看配置檔案]**, **[!UICONTROL 查看段]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

閱讀 [激活配置檔案和段以流式處理段導出目標](/help/destinations/ui/activate-segment-streaming-destinations.md) 有關激活此目標受眾段的說明。

## 資料使用和治理 {#data-usage-governance}

全部 [!DNL Adobe Experience Platform] 目標在處理資料時符合資料使用策略。 有關如何 [!DNL Adobe Experience Platform] 強制實施資料治理，請參見 [資料治理概述](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=zh-Hant)。

## 其他資源 {#additional-resources}

將受眾段映射到Twitter時，請確保滿足以下段命名要求：

1. 提供人可讀段映射名稱。 我們建議使用您用於Experience Platform段的相同名稱。
2. 不要使用特殊字元(+ &amp;, % :;@ / = $)。 如果您的Experience Platform段名稱包含這些字元，請在將段映射到Twitter目標之前將其刪除。

有關 [!DNL List Custom Audiences] 在Twitter [Twitter文檔](https://business.twitter.com/en/help/campaign-setup/campaign-targeting/custom-audiences/lists.html)。
