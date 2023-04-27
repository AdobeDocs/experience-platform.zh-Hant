---
keywords: DoubleClick競標管理器；DoubleClick競標管理器；DoubleClick；顯示與影片360；顯示360；影片360；影片360；顯示360；顯示與影片
title: Google Display & Video 360連線
description: Display & Video 360（先前稱為DoubleClick競標管理器）是一種工具，用於在顯示、視訊和行動詳細目錄來源間執行重新定位和對象鎖定目標的數位促銷活動。
exl-id: bdd3b3fd-891f-44ec-bd47-daf7f3289f92
source-git-commit: 326127996a27df41383ef67da765f7b0818f17f2
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 2%

---

# [!DNL Google Display & Video 360] 連接

## 總覽 {#overview}

[!DNL Display & Video 360]，先前稱為 [!DNL DoubleClick Bid Manager]，是在顯示、視訊和行動詳細目錄來源上，執行重新鎖定目標和對象鎖定目標數位促銷活動的工具。

## 目的地細節 {#specifics}

請注意下列 [!DNL Google Display & Video 360] 目的地：

* 在Google平台中以程式設計方式建立已啟用的對象。
* 啟用對象回填至 [!DNL Google Display & Video 360] 目的地排程在區段首次對應至目的地連線後24到48小時內執行。 此更新是針對Google的政策，即等候24小時，直到擷取資料，而且旨在改善即時CDP與 [!DNL Google Display & Video 360]. 請注意，這是僅適用於此目的地的後端設定，且與UI中任何客戶可設定的排程選項無關。

>[!IMPORTANT]
>
>如果您想要使用Google Display &amp; Video 360建立第一個目的地，但尚未啟用 [ID同步功能](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) 過去(使用Adobe Audience Manager或其他應用程式)的Experience CloudID服務，請聯絡Adobe諮詢或客戶服務以啟用ID同步。 如果您先前已在Audience Manager中設定Google整合，則您設定的ID同步會持續到Platform。

## 支援的身分 {#supported-identities}

[!DNL Google Display & Video 360] 支援啟用下表所述的身分。

| Target身分 | 說明 | 考量事項 |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | 當源標識為GAID命名空間時，選擇此目標標識。 |
| IDFA | [!DNL Apple ID for Advertisers] | 當您的來源識別為IDFA命名空間時，請選取此目標識別。 |
| AAM UUID | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html)，又稱為 [!DNL Device ID]. 38位數的裝置ID,Audience Manager會與其互動的每個裝置建立關聯。 | Google使用 [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=zh-Hant) 來鎖定加州的使用者，以及所有其他使用者的Google Cookie ID。 |
| [!DNL Google] cookie ID | [!DNL Google] cookie ID | [!DNL Google] 使用此ID來鎖定加州以外的使用者。 |
| RIDA | 廣告專用的Roku ID。 此ID可唯一識別Roku裝置。 |  |
| 女傭 | Microsoft Advertising ID。 此ID可唯一識別執行Windows 10的裝置。 |  |
| Amazon Fire TV ID | 此ID可唯一識別Amazon Fire TV。 |  |

## 匯出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 區段匯出]** | 您正在將區段（對象）的所有成員匯出至Google目的地。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」API型連線。 一旦根據區段評估在Experience Platform中更新設定檔，連接器就會將更新傳送至下游的目的地平台。 深入了解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

## 先決條件 {#prerequisites}

### 允許清單 {#allow-listing}

>[!NOTE]
>
>在設定第一個 [!DNL Google Display & Video 360] 目標。 請確保以下所述的允許清單過程已由 [!DNL Google] 建立目的地之前。
>此規則的例外為 [Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/aam-home.html) 客戶。 如果您已Audience Manager建立連線至此Google目的地，則不需要再次執行允許清單程式，您可以繼續執行後續步驟。

建立之前 [!DNL Google Display & Video 360] 目的地，您必須連絡Google，要求將Adobe加入允許的資料提供者清單中，並將您的帳戶新增至允許清單。 請聯絡Google並提供下列資訊：

* **帳戶ID**:Adobe的帳戶ID與Google。 帳戶ID:87933855。
* **客戶ID**:Adobe的客戶帳戶ID與Google。 客戶ID:89690775。
* **您的帳戶類型**:use **[!DNL Invite advertiser]** 允許對象僅共用至您的Display &amp; Video 360帳戶中的特定品牌，或使用 **[!DNL Invite partner]** 允許將受眾共用至您的顯示與影片360帳戶中的所有品牌。

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線至目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

若要連線至此目的地，請依照 [目的地設定教學課程](../../ui/connect-destination.md).

### 連線參數 {#parameters}

同時 [設定](../../ui/connect-destination.md) 此目的地時，您必須提供下列資訊：

* **[!UICONTROL 名稱]**:填寫此目的地的首選名稱。
* **[!UICONTROL 說明]**:選填。 例如，您可以提及您使用此目的地的促銷活動。
* **[!UICONTROL 帳戶類型]**:根據您使用Google的帳戶選取選項：
   * 使用 `Invite Advertiser` 允許只將受眾共用至顯示與影片360帳戶中的特定品牌。
   * 使用 `Invite Partner` 允許將受眾共用至您的顯示與影片360帳戶中的所有品牌。
* **[!UICONTROL 帳戶ID]**:填入 **[!DNL Invite partner]** 或 **[!DNL Invite advertiser]** 帳戶ID與Google。 通常是6或7位數的ID。

>[!NOTE]
>
>設定 [!DNL Google Display & Video 360] 目的地，請與您的 [!DNL Google Account Manager] 或Adobe代表，了解您擁有的帳戶類型。

### 啟用警報 {#enable-alerts}

您可以啟用警報，接收有關資料流到目標狀態的通知。 從清單中選擇要訂閱的警報，以接收有關資料流狀態的通知。 如需警報的詳細資訊，請參閱 [使用UI訂閱目的地警報](../../ui/alerts.md).

完成提供目標連接的詳細資訊後，請選擇 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**, **[!UICONTROL 啟動目的地]**, **[!UICONTROL 檢視設定檔]**，和 **[!UICONTROL 檢視區段]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

請參閱 [對串流區段匯出目的地啟用受眾資料](../../ui/activate-segment-streaming-destinations.md) 以取得啟用受眾區段至此目的地的指示。

## 匯出的資料

驗證資料是否已成功導出到 [!DNL Google Display & Video 360] 目的地，檢查 [!DNL Google Display & Video 360] 帳戶。 如果啟動成功，則會在您的帳戶中填入對象。

## 疑難排解 {#troubleshooting}

### 400錯誤請求錯誤消息 {#bad-request}

設定此目的地時，您可能會收到下列錯誤：

`{"message":"Google Error: AuthorizationError.USER_PERMISSION_DENIED","code":"400 BAD_REQUEST"}`

當客戶帳戶不符合 [必要條件](#prerequisites). 若要修正此問題，請連絡Google，並確認您的帳戶已列入允許清單。