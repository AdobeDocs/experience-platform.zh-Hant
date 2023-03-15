---
keywords: 廣告；交易台；廣告交易台
title: 貿易台連接
description: 交易台是廣告購買者的自助平台，可跨顯示器、視訊和行動詳細目錄來源執行重新定位和對象鎖定的數位促銷活動。
exl-id: b8f638e8-dc45-4aeb-8b4b-b3fa2906816d
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '670'
ht-degree: 2%

---

# [!DNL The Trade Desk] 連接

## 總覽 {#overview}

[!DNL The Trade Desk] 目的地可協助您將設定檔資料傳送至 [!DNL The Trade Desk].

[!DNL The Trade Desk] 是自助服務平台，供廣告購買者在顯示器、視訊和行動詳細目錄來源間，執行重新定位和對象鎖定目標的數位促銷活動。

若要將設定檔資料傳送至 [!DNL Trade Desk]，您必須先連線至目的地。

## 使用案例 {#use-cases}

身為行銷人員，我想要使用以 [!DNL Trade Desk IDs] 或裝置ID，以建立重新定位或對象鎖定的數位行銷活動。

## 支援的身分 {#supported-identities}

[!DNL The Trade Desk] 支援啟用下表所述的身分。 深入了解 [身分](/help/identity-service/namespaces.md).

| Target身分 | 說明 |
|---|---|
| GAID | [!DNL Google Advertising ID] |
| IDFA | [!DNL Apple ID for Advertisers] |
| 交易台ID | 交易台平台中的廣告商ID |

{style="table-layout:auto"}

## 匯出類型和頻率 {#export-type-frequency}

有關目標導出類型和頻率的資訊，請參閱下表。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 區段匯出]** | 您正在將區段（對象）的所有成員匯出至目的地。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」API型連線。 一旦根據區段評估在Experience Platform中更新設定檔，連接器就會將更新傳送至下游的目的地平台。 深入了解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 先決條件 {#prerequisites}

>[!IMPORTANT]
>
>如果您想要使用 [!DNL The Trade Desk] 並未啟用 [ID同步功能](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) 過去(使用Adobe Audience Manager或其他應用程式)的Experience CloudID服務，請聯絡Adobe諮詢或客戶服務以啟用ID同步。 如果您之前 [!DNL The Trade Desk] Audience Manager中的整合，即您設定並繼承至Platform的ID同步。

## 連接到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線至目的地，您需要 **[!UICONTROL 管理目的地]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

若要連線至此目的地，請依照 [目的地設定教學課程](../../ui/connect-destination.md).

### 連線參數 {#parameters}

同時 [設定](../../ui/connect-destination.md) 此目的地時，您必須提供下列資訊：

* **[!UICONTROL 名稱]**:日後您將透過此名稱識別此目的地。
* **[!UICONTROL 說明]**:未來可協助您識別此目的地的說明。
* **[!UICONTROL 帳戶ID]**:您的 [!DNL Trade Desk] [!UICONTROL 帳戶ID].
* **[!UICONTROL 伺服器位置]**:詢問 [!DNL Trade Desk] 代表您應使用的地區伺服器。 以下是可供您選擇的可用區域伺服器：
   * **[!UICONTROL 歐洲]**
   * **[!UICONTROL 新加坡]**
   * **[!UICONTROL 東京]**
   * **[!UICONTROL 北美洲東]**
   * **[!UICONTROL 北美洲西]**
   * **[!UICONTROL 拉丁美洲]**

### 啟用警報 {#enable-alerts}

您可以啟用警報，接收有關資料流到目標狀態的通知。 從清單中選擇要訂閱的警報，以接收有關資料流狀態的通知。 如需警報的詳細資訊，請參閱 [使用UI訂閱目的地警報](../../ui/alerts.md).

完成提供目標連接的詳細資訊後，請選擇 **[!UICONTROL 下一個]**.

## 啟用此目的地的區段 {#activate}

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**, **[!UICONTROL 啟動目的地]**, **[!UICONTROL 檢視設定檔]**，和 **[!UICONTROL 檢視區段]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

請參閱 [對串流區段匯出目的地啟用受眾資料](../../ui/activate-segment-streaming-destinations.md) 以取得啟用受眾區段至此目的地的指示。

在 [區段排程](../../ui/activate-segment-streaming-destinations.md#scheduling) 步驟中，您必須手動將區段對應至其目標平台中的對應ID或好記名稱。

對應區段時，建議您使用平台區段名稱或更短的名稱，以方便使用。 不過，您目的地的區段ID或名稱不需要符合Platform帳戶中的區段ID或名稱。 您在對應欄位中插入的任何值都會由目的地反映。

如果您使用多個裝置對應(Cookie ID), [!DNL IDFA], [!DNL GAID])，請務必對所有三個對應使用相同的對應值。 [!DNL The Trade Desk] 會以裝置層級劃分，將所有區段匯總為單一區段。

![區段對應ID](../../assets/common/segment-mapping-id.png)

## 匯出的資料 {#exported-data}

驗證資料是否已成功導出到 [!DNL The Trade Desk] 目的地，檢查 [!DNL Trade Desk] 帳戶。 如果啟動成功，則會在您的帳戶中填入對象。
