---
keywords: 廣告；交易台；廣告交易台
title: 貿易台連接
description: 交易台是廣告購買者的自助平台，可跨顯示器、視訊和行動詳細目錄來源執行重新定位和對象鎖定的數位促銷活動。
exl-id: b8f638e8-dc45-4aeb-8b4b-b3fa2906816d
source-git-commit: 802b1844bec1e577e978da5d5a69de87278c04b9
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 2%

---

# [!DNL The Trade Desk] 連接

## 概覽 {#overview}

[!DNL The Trade Desk] 目的地可協助您將設定檔資料傳送至 [!DNL The Trade Desk]。

[!DNL The Trade Desk] 是自助服務平台，供廣告購買者在顯示器、視訊和行動詳細目錄來源間，執行重新定位和對象鎖定目標的數位促銷活動。

若要將設定檔資料傳送至[!DNL Trade Desk]，您必須先連線至目的地。

## 使用案例 {#use-cases}

身為行銷人員，我想要使用[!DNL Trade Desk IDs]或裝置ID所建立的區段，建立重新鎖定目標或對象鎖定目標的數位行銷活動。

## 支援的身分 {#supported-identities}

[!DNL The Trade Desk] 支援啟用下表所述的身分。深入了解[identities](/help/identity-service/namespaces.md)。

| Target身分 | 說明 |
|---|---|
| GAID | [!DNL Google Advertising ID] |
| IDFA | [!DNL Apple ID for Advertisers] |
| 交易台ID | 交易台平台中的廣告商ID |

## 匯出類型 {#export-type}

**[!DNL Segment export]**  — 您會將區段（對象）的所有成員匯出至目的地。

## 先決條件 {#prerequisites}

如果您想使用[!DNL The Trade Desk]建立第一個目的地，而過去(使用Adobe Audience Manager或其他應用程式)未在Experience CloudID服務中啟用[ID同步功能](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html)，請洽詢Adobe諮詢或客戶服務以啟用ID同步。 如果您先前已在Audience Manager中設定[!DNL The Trade Desk]整合，則您設定的ID同步會持續到Platform。

## 連接到目標 {#connect}

要連接到此目標，請按照[目標配置教程](../../ui/connect-destination.md)中所述的步驟操作。

### 連線參數 {#parameters}

在[設定](../../ui/connect-destination.md)此目標時，您必須提供下列資訊：

* **[!UICONTROL 名稱]**:日後您將透過此名稱識別此目的地。
* **[!UICONTROL 說明]**:未來可協助您識別此目的地的說明。
* **[!UICONTROL 帳戶ID]**:您的 [!DNL Trade Desk] [!UICONTROL 帳戶ID]。
* **[!UICONTROL 伺服器位置]**:詢問您 [!DNL Trade Desk] 的代表您應使用哪個地區伺服器。以下是可供您選擇的可用區域伺服器：
   * **[!UICONTROL 歐洲]**
   * **[!UICONTROL 新加坡]**
   * **[!UICONTROL 東京]**
   * **[!UICONTROL 北美洲東]**
   * **[!UICONTROL 北美洲西]**
   * **[!UICONTROL 拉丁美洲]**

## 啟用此目的地的區段 {#activate}

請參閱[將設定檔和區段啟用至目的地](../../ui/activate-destinations.md) ，以取得將對象區段啟用至目的地的指示。

在[區段排程](../../ui/activate-destinations.md#segment-schedule)步驟中，您必須手動將區段對應至目標平台中對應的ID或好記名稱。

對應區段時，建議您使用平台區段名稱或更短的名稱，以方便使用。 不過，您目的地的區段ID或名稱不需要符合Platform帳戶中的區段ID或名稱。 您在對應欄位中插入的任何值都會由目的地反映。

如果您使用多個裝置對應(Cookie ID、[!DNL IDFA]、[!DNL GAID])，請務必對所有三個對應使用相同的對應值。 [!DNL The Trade Desk] 會以裝置層級劃分，將所有區段匯總為單一區段。

![區段對應ID](../../assets/common/segment-mapping-id.png)

## 匯出的資料 {#exported-data}

要驗證資料是否已成功導出到[!DNL The Trade Desk]目標，請檢查[!DNL Trade Desk]帳戶。 如果啟動成功，則會在您的帳戶中填入對象。
