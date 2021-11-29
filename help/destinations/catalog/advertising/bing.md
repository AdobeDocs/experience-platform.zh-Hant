---
keywords: '廣告；bing; '
title: Microsoft Bing連線
description: 使用Microsoft Bing連線目的地，您可以在Microsoft Display Advertising中執行重新鎖定目標和對象鎖定目標的數位促銷活動。
exl-id: e1c0273b-7e3c-4d77-ae14-d1e528ca0294
source-git-commit: 169a7ad1adfa3282bd0503ce277373b654ec57cd
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 1%

---

# [!DNL Microsoft Bing] 連接 {#bing-destination}

## 總覽 {#overview}

此 [!DNL Microsoft Bing] 目的地可協助您將設定檔資料傳送至 [!DNL Microsoft Display Advertising].

若要將設定檔資料傳送至 [!DNL Microsoft Bing]，您必須先連線至目的地。

## 使用案例 {#use-cases}

身為行銷人員，我想要使用以 [!DNL Microsoft Advertising IDs] 透過 [!DNL Microsoft Advertising] 管道。

## 支援的身分 {#supported-identities}

[!DNL Microsoft Bing] 支援啟用下表所述的身分。 深入了解 [身分](/help/identity-service/namespaces.md).

| Target身分 | 說明 |
|---|---|
| 女傭 | Microsoft Advertising ID |

## 匯出類型 {#export-type}

**[!DNL Segment Export]**  — 將區段（對象）的所有成員匯出至 [!DNL Microsoft Bing] 目的地。

## 先決條件 {#prerequisites}

>[!IMPORTANT]
>
>如果您想要使用 [!DNL Microsoft Bing] 並未啟用 [ID同步功能](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) 過去(使用Adobe Audience Manager或其他應用程式)的Experience CloudID服務，請聯絡Adobe諮詢或客戶服務以啟用ID同步。 如果您之前 [!DNL Microsoft Bing] Audience Manager中的整合，即您設定並繼承至Platform的ID同步。

設定目的地時，您必須提供下列資訊：

* [!UICONTROL 帳戶ID]:這是你的 [!DNL Bing Ads CID]，格式為整數。

## 連接到目標 {#connect}

若要連線至此目的地，請依照 [目的地設定教學課程](../../ui/connect-destination.md).

### 連線參數 {#parameters}

同時 [設定](../../ui/connect-destination.md) 此目的地時，您必須提供下列資訊：

* **[!UICONTROL 名稱]**:日後您將透過此名稱識別此目的地。
* **[!UICONTROL 說明]**:未來可協助您識別此目的地的說明。
* **[!UICONTROL 帳戶ID]**:您的 [!DNL Bing Ads CID].

## 啟用此目的地的區段 {#activate}

請參閱 [對串流區段匯出目的地啟用受眾資料](../../ui/activate-segment-streaming-destinations.md) 以取得啟用受眾區段至此目的地的指示。

在 [區段排程](../../ui/activate-segment-streaming-destinations.md#scheduling) 步驟中，您必須手動將區段對應至目的地中對應的ID或好記名稱。

對應區段時，建議您使用 [!DNL Platform] 區段名稱或較短的形式，以方便使用。 不過，目的地的區段ID或名稱不需要符合 [!DNL Platform] 帳戶。 您在對應欄位中插入的任何值都會由目的地反映。

## 匯出的資料 {#exported-data}

驗證資料是否已成功導出到 [!DNL Microsoft Bing] 目的地，檢查 [!DNL Microsoft Bing Ads] 帳戶。 如果啟動成功，則會在您的帳戶中填入對象。
