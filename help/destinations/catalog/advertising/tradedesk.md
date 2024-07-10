---
keywords: 廣告；營業部；廣告營業部
title: 交易台連線
description: Trade Desk是廣告買方適用的自助式平台，可在各種顯示、影片和行動詳細目錄來源中執行重新定位以及以對象為目標的數位行銷活動。
exl-id: b8f638e8-dc45-4aeb-8b4b-b3fa2906816d
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 3%

---

# [!DNL The Trade Desk] 連線

## 概觀 {#overview}

[!DNL The Trade Desk] 目的地可幫助您傳送設定檔資料至 [!DNL The Trade Desk].

[!DNL The Trade Desk] 是一個自助式平台，可供廣告購買者跨顯示器、影片和行動詳細目錄來源執行重新定位以及以對象為目標的數位行銷活動。

若要傳送設定檔資料至 [!DNL Trade Desk]，您必須先連線至目的地。

## 使用案例 {#use-cases}

身為行銷人員，我想要能夠使用由下列專案建立的對象： [!DNL Trade Desk IDs] 或裝置ID來建立重新定位或以對象為目標的數位行銷活動。

## 支援的身分 {#supported-identities}

[!DNL The Trade Desk] 支援根據下表所示的身分來啟用對象。 進一步瞭解 [身分](/help/identity-service/features/namespaces.md).

| 身分 | 說明 |
|---|---|
| GAID | [!DNL Google Advertising ID] |
| IDFA | [!DNL Apple ID for Advertisers] |
| 交易台ID | Trade Desk平台中的廣告商ID |

{style="table-layout:auto"}

## 支援的對象 {#supported-audiences}

本節說明您可以將哪些型別的對象匯出至此目的地。

| 對象來源 | 支援 | 說明 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ (A) | 透過Experience Platform產生的對象 [分段服務](../../../segmentation/home.md). |
| 自訂上傳 | ✓ (A) | 受眾 [已匯入](../../../segmentation/ui/audience-portal.md#import-audience) 從CSV檔案Experience Platform為。 |

{style="table-layout:auto"}

## 匯出型別和頻率 {#export-type-frequency}

請參閱下表以取得目的地匯出型別和頻率的資訊。

| 項目 | 類型 | 附註 |
---------|----------|---------|
| 匯出類型 | **[!UICONTROL 對象匯出]** | 您正在將對象的所有成員匯出至目的地。 |
| 匯出頻率 | **[!UICONTROL 串流]** | 串流目的地是「一律開啟」的API型連線。 一旦根據對象評估在Experience Platform中更新了設定檔，聯結器就會將更新傳送至下游的目的地平台。 深入瞭解 [串流目的地](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 先決條件 {#prerequisites}

>[!IMPORTANT]
>
>如果您打算使用建立您的第一個目的地 [!DNL The Trade Desk] 且尚未啟用 [ID同步功能](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) 若是過去的Experience CloudID服務(使用Adobe Audience Manager或其他應用程式)，請聯絡Adobe Consulting或客戶服務以啟用ID同步。 如果您先前已設定 [!DNL The Trade Desk] Audience Manager中的整合，也就是您設定的ID同步會移轉到Platform。

## 連線到目標 {#connect}

>[!IMPORTANT]
> 
>若要連線到目的地，您需要 **[!UICONTROL 檢視目的地]** 和 **[!UICONTROL 管理目的地]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

若要連線至此目的地，請遵循以下說明的步驟： [目的地設定教學課程](../../ui/connect-destination.md).

### 連線參數 {#parameters}

當 [設定](../../ui/connect-destination.md) 您必須提供下列資訊給此目的地：

* **[!UICONTROL 名稱]**：您日後可辨識此目的地的名稱。
* **[!UICONTROL 說明]**：可協助您日後識別此目的地的說明。
* **[!UICONTROL 帳戶ID]**：您的 [!DNL Trade Desk] [!UICONTROL 帳戶ID].
* **[!UICONTROL 伺服器位置]**：詢問您的 [!DNL Trade Desk] 代表您應使用的地區伺服器。 您可選擇的區域伺服器包括：
   * **[!UICONTROL 歐洲]**
   * **[!UICONTROL 新加坡]**
   * **[!UICONTROL 東京]**
   * **[!UICONTROL 北美洲東部]**
   * **[!UICONTROL 北美西部]**
   * **[!UICONTROL 拉丁美洲]**

### 啟用警示 {#enable-alerts}

您可以啟用警報以接收有關傳送到您目的地的資料流狀態的通知。 從清單中選取警報以訂閱接收有關資料流狀態的通知。 如需警示的詳細資訊，請參閱以下指南： [使用UI訂閱目的地警報](../../ui/alerts.md).

當您完成提供目的地連線的詳細資訊時，請選取「 」 **[!UICONTROL 下一個]**.

## 啟動此目標的對象 {#activate}

>[!IMPORTANT]
> 
>* 若要啟用資料，您需要 **[!UICONTROL 檢視目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。
>* 要匯出 *身分*，您需要 **[!UICONTROL 檢視身分圖表]** [存取控制許可權](/help/access-control/home.md#permissions). <br> ![選取工作流程中反白顯示的身分名稱空間，以將對象啟用至目的地。](/help/destinations/assets/overview/export-identities-to-destination.png "選取工作流程中反白顯示的身分名稱空間，以將對象啟用至目的地。"){width="100" zoomable="yes"}

另請參閱 [啟用受眾資料至串流受眾匯出目的地](../../ui/activate-segment-streaming-destinations.md) 以取得啟用此目的地對象的指示。

在 [對象排程](../../ui/activate-segment-streaming-destinations.md#scheduling) 步驟，您必須手動將對象對應至其在目的地平台中的對應ID或好記名稱。

對應區段時，建議您使用Platform對象名稱或較短的形式，以方便使用。 不過，您目的地中的對象ID或名稱不需要符合您Platform帳戶中的對象ID。 您在對應欄位中插入的任何值都會反映在目的地中。

如果您使用多個裝置對應(Cookie ID、 [!DNL IDFA]， [!DNL GAID])，請確定所有這三個對應都使用相同的對應值。 [!DNL The Trade Desk] 會將其彙總成單一區段，並具備裝置層級的劃分。

![區段對應ID](../../assets/common/segment-mapping-id.png)

## 匯出的資料 {#exported-data}

驗證資料是否已成功匯出到 [!DNL The Trade Desk] 目的地，請檢視您的 [!DNL Trade Desk] 帳戶。 如果成功啟用，系統會將對象填入您的帳戶。
