---
keywords: '廣告；bing; '
title: Microsoft Bing連接
description: 使用Microsoft Bing連線目的地，您可以在Microsoft Display Advertising中執行重新定位和對象鎖定的數位促銷活動。
exl-id: e1c0273b-7e3c-4d77-ae14-d1e528ca0294
source-git-commit: 15ea3ab9370541c35b874414a8753e8812eea9c6
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 1%

---

# [!DNL Microsoft Bing] 連接 {#bing-destination}

## 概覽 {#overview}

[!DNL Microsoft Bing]目的地可協助您將設定檔資料傳送至[!DNL Microsoft Display Advertising]。

若要將設定檔資料傳送至[!DNL Microsoft Bing]，您必須先連線至目的地。

## 使用案例 {#use-cases}

身為行銷人員，我想要使用[!DNL Microsoft Advertising IDs]建置的區段，透過[!DNL Microsoft Advertising]管道的顯示廣告來鎖定使用者。

## 支援的身分 {#supported-identities}

[!DNL Microsoft Bing] 支援啟用下表所述的身分。深入了解[identities](/help/identity-service/namespaces.md)。

| Target身分 | 說明 |
|---|---|
| 女傭 | Microsoft Advertising ID |

## 匯出類型 {#export-type}

**[!DNL Segment Export]**  — 您會將區段（對象）的所有成員匯出至目 [!DNL Microsoft Bing] 的地。

## 先決條件 {#prerequisites}

如果您想使用[!DNL Microsoft Bing]建立第一個目的地，而過去(使用Adobe Audience Manager或其他應用程式)未在Experience CloudID服務中啟用[ID同步功能](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html)，請洽詢Adobe諮詢或客戶服務以啟用ID同步。 如果您先前已在Audience Manager中設定[!DNL Microsoft Bing]整合，則您設定的ID同步會持續到Platform。

設定目的地時，您必須提供下列資訊：

* [!UICONTROL 帳戶ID]:這是整 [!DNL Bing Ads CID]數格式的。

## 連接到目標 {#connect}

要連接到此目標，請按照[目標配置教程](../../ui/connect-destination.md)中所述的步驟操作。

### 連線參數 {#parameters}

在[設定](../../ui/connect-destination.md)此目標時，您必須提供下列資訊：

* **[!UICONTROL 名稱]**:日後您將透過此名稱識別此目的地。
* **[!UICONTROL 說明]**:未來可協助您識別此目的地的說明。
* **[!UICONTROL 帳戶ID]**:您的 [!DNL Bing Ads CID]。

## 啟用此目的地的區段 {#activate}

請參閱[將設定檔和區段啟用至目的地](../../ui/activate-destinations.md) ，以取得將對象區段啟用至目的地的指示。

在[區段排程](../../ui/activate-destinations.md#segment-schedule)步驟中，您必須手動將區段對應至目的地中的對應ID或好記名稱。

對應區段時，建議您使用[!DNL Platform]區段名稱或更短的名稱，以方便使用。 不過，您目的地的區段ID或名稱不需要與[!DNL Platform]帳戶中的ID或名稱相符。 您在對應欄位中插入的任何值都會由目的地反映。

## 匯出的資料 {#exported-data}

要驗證資料是否已成功導出到[!DNL Microsoft Bing]目標，請檢查[!DNL Microsoft Bing Ads]帳戶。 如果啟動成功，則會在您的帳戶中填入對象。
