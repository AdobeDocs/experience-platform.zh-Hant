---
keywords: google廣告管理員；google廣告；doubleclick;DoubleClick AdX;DoubleClick;Google廣告管理員；Google廣告管理員；DFP
title: Google Ad Manager連線
description: Google Ad Manager（舊稱DoubleClick for Publishers或DoubleClick AdX）是Google的廣告服務平台，可讓發佈商透過視訊和行動應用程式管理其網站上廣告的顯示。
exl-id: e93f1bd5-9d29-43a1-a9a6-8933f9d85150
source-git-commit: ea480854c6058d84615b66a7df2d7c8fbd619bab
workflow-type: tm+mt
source-wordcount: '911'
ht-degree: 2%

---

# [!DNL Google Ad Manager] 連接

## 總覽 {#overview}

[!DNL Google Ad Manager]，先前稱為 [!DNL DoubleClick for Publishers] (DFP)或 [!DNL DoubleClick AdX]，是來自的廣告服務平台 [!DNL Google] 這讓發佈商能夠通過視頻和移動應用管理其網站上的廣告顯示。

## 目的地細節 {#specifics}

請注意下列 [!DNL Google Ad Manager] 目的地：

* 以程式設計方式在 [!DNL Google] 平台。
* [!DNL Platform] 目前不包含驗證是否成功啟用的測量量度。 請參考Google中的對象計數，以驗證整合併了解對象鎖定目標大小。
* 將區段對應至 [!DNL Google Ad Manager] 目的地中，區段名稱會立即顯示在 [!DNL Google Ad Manager] 使用者介面。
* 區段母體需要24到48小時才會顯示於 [!DNL Google Ad Manager]. 此外，區段的對象大小必須至少為50個設定檔，才能顯示在 [!DNL Google Ad Manager]. 對象大小小於50個設定檔的區段不會填入 [!DNL Google Ad Manager].

## 支援的身分 {#supported-identities}

[!DNL Google Ad Manager] 支援啟用下表所述的身分。

| Target身分 | 說明 | 考量事項 |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | 當源標識為GAID命名空間時，選擇此目標標識。 |
| IDFA | [!DNL Apple ID for Advertisers] | 當您的來源識別為IDFA命名空間時，請選取此目標識別。 |
| AAM UUID | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html)，又稱為 [!DNL Device ID]. 38位數的裝置ID,Audience Manager會與其互動的每個裝置建立關聯。 | Google使用 [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=zh-Hant) 來鎖定加州的使用者，以及所有其他使用者的Google Cookie ID。 |
| [!DNL Google] cookie ID | [!DNL Google] cookie ID | [!DNL Google] 使用此ID來鎖定加州以外的使用者。 |
| RIDA | 廣告專用的Roku ID。 此ID可唯一識別Roku裝置。 |  |
| 女傭 | Microsoft Advertising ID。 此ID可唯一識別執行Windows 10的裝置。 |  |
| Amazon Fire TV ID | 此ID可唯一識別Amazon Fire TV。 |  |

{style="table-layout:auto"}

## 匯出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 區段匯出]** | 您正在將區段（對象）的所有成員匯出至Google目的地。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」API型連線。 一旦根據區段評估在Experience Platform中更新設定檔，連接器就會將更新傳送至下游的目的地平台。 深入了解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 先決條件 {#prerequisites}

如果您想要使用 [!DNL Google Ad Manager] 並未啟用 [ID同步功能](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) 過去的Experience CloudID服務(含Audience Manager或其他應用程式)，請聯絡Adobe諮詢或客戶服務以啟用ID同步。 如果您之前 [!DNL Google] Audience Manager中的整合，即您設定並繼承至Platform的ID同步。

### 允許清單 {#allow-listing}

在設定第一個 [!DNL Google Ad Manager] 目標。 建立目的地之前，請務必完成下述的允許清單程式。

1. 請依照 [Google Ad Manager檔案](https://support.google.com/admanager/answer/3289669?hl=en) 將Adobe新增為連結的資料管理平台(DMP)。
2. 在 [!DNL Google Ad Manager] 介面，轉到 **[!UICONTROL 管理]** > **[!UICONTROL 全域設定]** > **[!UICONTROL 網路設定]**，並啟用 **[!UICONTROL API存取]** 滑桿。

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線至目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

若要連線至此目的地，請依照 [目的地設定教學課程](../../ui/connect-destination.md).

### 連線參數 {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_gam_appendSegmentID"
>title="將區段ID附加至區段名稱"
>abstract="選取此選項，讓Google廣告管理員中的區段名稱包含來自Experience Platform的區段ID，如下所示： `Segment Name (Segment ID)`"

同時 [設定](../../ui/connect-destination.md) 此目的地時，您必須提供下列資訊：

* **[!UICONTROL 名稱]**:填寫此目的地的首選名稱。
* **[!UICONTROL 說明]**:選填。 例如，您可以提及您使用此目的地的促銷活動。
* **[!UICONTROL 帳戶ID]**:輸入 [!DNL Audience Link ID] 從 [!DNL Google] 帳戶。 這是與 [!DNL Google Ad Manager] 網路(不是 [!DNL Network code])。 您可以在 **[!UICONTROL 「管理員>全域設定」]** 在 [!DNL Google Ad Manager] 介面。
* **[!UICONTROL 帳戶類型]**:根據您使用Google的帳戶選取選項：
   * 使用 `DFP by Google` for [!DNL DoubleClick] 適用於發佈者
   * 使用 `AdX buyer` for [!DNL Google AdX]

<!--

*  **[!UICONTROL Append segment ID to segment name]**: Select this option to have the segment name in Google Ad Manager include the segment ID from Experience Platform, like this: `Segment Name (Segment ID)`

-->

>[!NOTE]
>
>設定 [!DNL Google Ad Manager] 目的地，請與您的 [!DNL Google Account Manager] 或Adobe代表，了解您擁有的帳戶類型。

### 啟用警報 {#enable-alerts}

您可以啟用警報，接收有關資料流到目標狀態的通知。 從清單中選擇要訂閱的警報，以接收有關資料流狀態的通知。 如需警報的詳細資訊，請參閱 [使用UI訂閱目的地警報](../../ui/alerts.md).

完成提供目標連接的詳細資訊後，請選擇 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**, **[!UICONTROL 啟動目的地]**, **[!UICONTROL 檢視設定檔]**，和 **[!UICONTROL 檢視區段]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

請參閱 [對串流區段匯出目的地啟用受眾資料](../../ui/activate-segment-streaming-destinations.md) 以取得啟用受眾區段至此目的地的指示。

## 匯出的資料 {#exported-data}

驗證資料是否已成功導出到 [!DNL Google Ad Manager] 目的地，檢查 [!DNL Google Ad Manager] 帳戶。 如果啟動成功，則會在您的帳戶中填入對象。

## 疑難排解 {#troubleshooting}

如果您在使用此目的地時遇到任何錯誤，且需要聯絡Adobe或Google，請保留下列ID。

這些是Adobe的Google帳戶ID:

* **[!UICONTROL 帳戶ID]**:87933855
* **[!UICONTROL 客戶ID]**:89690775