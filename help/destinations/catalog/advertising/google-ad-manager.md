---
keywords: google廣告管理器；google廣告；按兩下廣告；按兩下廣告；Google廣告管理器；Google廣告管理器；DFP
title: Google廣告經理連接
description: Google廣告管理器以前叫DoubleClick for Publishers或DoubleClick AdX，是Google的一個廣告服務平台，它使出版商能夠通過視頻和移動應用管理其網站上廣告的顯示。
exl-id: e93f1bd5-9d29-43a1-a9a6-8933f9d85150
source-git-commit: f163b1e3c60953192b2ddf543eb4f3e8df88799b
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 3%

---

# [!DNL Google Ad Manager] 連接

## 總覽 {#overview}

[!DNL Google Ad Manager]，以前稱為 [!DNL DoubleClick for Publishers] (DFP)或 [!DNL DoubleClick AdX]，是來自 [!DNL Google] 這讓出版商能夠通過視頻和移動應用管理其網站上的廣告顯示。

## 目標說明 {#specifics}

請注意以下特定於 [!DNL Google Ad Manager] 目標：

* 在中以寫程式方式建立激活的受眾 [!DNL Google] 平台。
* [!DNL Platform] 當前不包括用於驗證成功激活的度量度量。 請參考Google的受眾數量，以驗證整合併瞭解受眾的目標規模。

## 支援的身份 {#supported-identities}

[!DNL Google Ad Manager] 支援激活下表中描述的身份。

| 目標標識 | 說明 | 考量事項 |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | 當源標識為GAID命名空間時，選擇此目標標識。 |
| IDFA | [!DNL Apple ID for Advertisers] | 當源標識為IDFA命名空間時，選擇此目標標識。 |
| UUIDAAM | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html)，也稱為 [!DNL Device ID]。 一個38位的數字設備ID,Audience Manager將其與其交互的每個設備相關聯。 | Google用途 [UUIDAAM](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en) 目標加州用戶和所有其他用戶的GoogleCookie ID。 |
| [!DNL Google] Cookie ID | [!DNL Google] Cookie ID | [!DNL Google] 使用此ID將目標用戶鎖定在加利福尼亞以外的地區。 |
| 里達 | 廣告的Roku ID。 此ID唯一標識Roku設備。 |  |
| 女僕 | Microsoft廣告ID。 此ID唯一標識運行Windows 10的設備。 |  |
| Amazon消防電視ID | 此ID唯一標識Amazon消防電視。 |  |

{style=&quot;table-layout:auto&quot;}

## 導出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 導出類型 | **[!UICONTROL 區段匯出]** | 您正在將段（受眾）的所有成員導出到Google目標。 |
| 導出頻率 | **[!UICONTROL 流]** | 流目標是基於API的「始終開啟」連接。 一旦基於段評估在Experience Platform中更新配置檔案，連接器就將更新下游發送到目標平台。 閱讀有關 [流目標](/help/destinations/destination-types.md#streaming-destinations)。 |

{style=&quot;table-layout:auto&quot;&quot;

## 先決條件 {#prerequisites}

如果您希望建立第一個目標 [!DNL Google Ad Manager] 還沒啟用 [ID同步功能](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) 在過去的Experience CloudID服務(包括Audience Manager或其他應用程式)中，請聯繫Adobe咨詢或客戶服務以啟用ID同步。 如果你之前 [!DNL Google] Audience Manager中的整合，您設定的ID同步將傳遞到平台。

### 允許清單 {#allow-listing}

>[!NOTE]
>
>在設定第一個允許清單之前，該允許清單是必需的 [!DNL Google Ad Manager] 目標。 請確保以下描述的允許清單過程已由 [!DNL Google] 建立目標之前。

在建立 [!DNL Google Ad Manager] 目標在平台中，您必須聯繫 [!DNL Google] 用於將Adobe置於允許的資料提供程式清單中，以及將帳戶添加到允許清單中。 聯繫人 [!DNL Google] 並提供以下資訊：

* **帳戶ID**:Adobe的Google賬戶ID。 帳戶ID:87933855。
* **客戶ID**:Adobe的客戶帳戶ID與Google。 客戶ID:89690775。
* **網路代碼**:這是你的 [!DNL Google Ad Manager] 網路標識符，在 **[!UICONTROL 「管理」>「全局設定」]** 的子菜單。
* **受眾連結ID**:這是與您的 [!DNL Google Ad Manager] 網路 [!DNL Network code]) **[!UICONTROL 「管理」>「全局設定」]** 在Google介面。
* 您的帳戶類型。 由Google或AdX買家提供的DFP。

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>要連接到目標，您需要 **[!UICONTROL 管理目標]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

要連接到此目標，請按照 [目標配置教程](../../ui/connect-destination.md)。

### 連接參數 {#parameters}

同時 [設定](../../ui/connect-destination.md) 此目標，必須提供以下資訊：

* **[!UICONTROL 名稱]**:填寫此目標的首選名稱。
* **[!UICONTROL 說明]**:可選。 例如，您可以提及您為此目標使用的市場活動。
* **[!UICONTROL 帳戶類型]**:根據您與Google的帳戶選擇選項：
   * 使用 `DFP by Google` 為 [!DNL DoubleClick] 對於發佈者
   * 使用 `AdX buyer` 為 [!DNL Google AdX]
* **[!UICONTROL 帳戶ID]**:使用 [!DNL Google]。

>[!NOTE]
>
>設定 [!DNL Google Ad Manager] 目標，請與 [!DNL Google Account Manager] 或Adobe代表，瞭解您的帳戶類型。

### 啟用警報 {#enable-alerts}

您可以啟用警報來接收有關目標資料流狀態的通知。 從清單中選擇要訂閱的警報以接收有關資料流狀態的通知。 有關警報的詳細資訊，請參閱上的指南 [使用UI訂閱目標警報](../../ui/alerts.md)。

完成提供目標連接的詳細資訊後，選擇 **[!UICONTROL 下一個]**。

## 將段激活到此目標 {#activate}

>[!IMPORTANT]
> 
>要激活資料，您需要 **[!UICONTROL 管理目標]**。 **[!UICONTROL 激活目標]**。 **[!UICONTROL 查看配置檔案]**, **[!UICONTROL 查看段]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

請參閱 [將受眾資料激活到流段導出目標](../../ui/activate-segment-streaming-destinations.md) 有關激活此目標受眾段的說明。

## 導出的資料 {#exported-data}

驗證資料是否已成功導出到 [!DNL Google Ad Manager] 目標，檢查 [!DNL Google Ad Manager] 帳戶。 如果激活成功，則會在您的帳戶中填充受眾。
