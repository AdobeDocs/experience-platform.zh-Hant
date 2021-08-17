---
keywords: google廣告管理員；google廣告；doubleclick;DoubleClick AdX;DoubleClick;Google廣告管理員；Google廣告管理員；DFP
title: Google Ad Manager連線
description: Google Ad Manager（原稱為DoubleClick for Publishers或DoubleClick AdX）是谷歌的一個廣告服務平台，它讓出版商能夠通過視頻和移動應用管理其網站上的廣告顯示。
exl-id: e93f1bd5-9d29-43a1-a9a6-8933f9d85150
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 2%

---

# [!DNL Google Ad Manager] 連接

## 概覽 {#overview}

[!DNL Google Ad Manager](先前稱為( [!DNL DoubleClick for Publishers] DFP)或 [!DNL DoubleClick AdX])是的廣告服務平台，可讓 [!DNL Google] 發佈商管理其網站、透過視訊和行動應用程式中的廣告顯示。

## 目的地細節 {#specifics}

請注意下列特定於[!DNL Google Ad Manager]目的地的詳細資訊：

* 在[!DNL Google]平台中以程式設計方式建立已啟用的對象。
* [!DNL Platform] 目前不包含驗證是否成功啟用的測量量度。請參考Google中的對象計數，以驗證整合併了解對象鎖定目標大小。

## 支援的身分 {#supported-identities}

[!DNL Google Ad Manager] 支援啟用下表所述的身分。

| Target身分 | 說明 | 考量事項 |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | 當源標識為GAID命名空間時，選擇此目標標識。 |
| IDFA | [!DNL Apple ID for Advertisers] | 當您的來源識別為IDFA命名空間時，請選取此目標識別。 |
| AAM UUID | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html)，也稱為 [!DNL Device ID]。38位數的裝置ID,Audience Manager會與其互動的每個裝置建立關聯。 | Google使用[AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en)來鎖定加州的使用者，並將Google Cookie ID設為所有其他使用者。 |
| [!DNL Google] cookie ID | [!DNL Google] cookie ID | [!DNL Google] 使用此ID來鎖定加州以外的使用者。 |
| RIDA | 廣告專用的Roku ID。 此ID可唯一識別Roku裝置。 |  |
| 女傭 | Microsoft Advertising ID。 此ID可唯一識別執行Windows 10的裝置。 |  |
| Amazon Fire TV ID | 此ID可唯一識別Amazon Fire TV。 |  |

## 匯出類型 {#export-type}

**區段匯出**  — 您正在將區段（對象）的所有成員匯出至Google目的地。

## 先決條件

如果您想使用[!DNL Google Ad Manager]建立第一個目的地，而過去(透過Audience Manager或其他應用程式)未在Experience CloudID服務中啟用[ID同步功能](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html)，請洽詢Adobe諮詢或客戶服務以啟用ID同步。 如果您先前已在Audience Manager中設定[!DNL Google]整合，則您設定的ID同步會持續到Platform。

## 允許清單

>[!NOTE]
>
>在Platform中設定您的第一個[!DNL Google Ad Manager]目的地前，允許清單是必填的。 建立目標之前，請確保[!DNL Google]已完成下面所述的允許清單進程。

在Platform中建立[!DNL Google Ad Manager]目的地之前，您必須聯絡[!DNL Google]，才能將Adobe加入允許的資料提供者清單中，並將您的帳戶新增至允許清單中。 聯繫[!DNL Google]並提供以下資訊：

* **帳戶ID**:Adobe的帳戶ID與Google。帳戶ID:87933855。
* **客戶ID**:Adobe的客戶帳戶ID與Google。客戶ID:89690775。
* **網路ID** :這是你的帳戶  [!DNL Google Ad Manager]
* **對象連結ID** :這是你的帳戶  [!DNL Google Ad Manager]
* 您的帳戶類型。 Google或AdX購買者提供的DFP。

## 連接到目標 {#connect}

要連接到此目標，請按照[目標配置教程](../../ui/connect-destination.md)中所述的步驟操作。

### 連線參數 {#parameters}

在[設定](../../ui/connect-destination.md)此目標時，您必須提供下列資訊：

* **[!UICONTROL 名稱]**:填寫此目的地的首選名稱。
* **[!UICONTROL 說明]**:選填。例如，您可以提及您使用此目的地的促銷活動。
* **[!UICONTROL 帳戶類型]**:根據您使用Google的帳戶，選取選項：
   * 對於[!DNL DoubleClick]，請使用`DFP by Google`對於發佈者
   * 對[!DNL Google AdX]使用`AdX buyer`
* **[!UICONTROL 帳戶ID]**:用填入您的帳戶ID  [!DNL Google]。這可以是您的網路ID或對象連結ID。 通常為8位數的ID。

>[!NOTE]
>
>設定[!DNL Google Ad Manager]目的地時，請與您的[!DNL Google Account Manager]或Adobe代表合作，了解您擁有的帳戶類型。

## 啟用此目的地的區段 {#activate}

請參閱[對串流區段匯出目的地啟用受眾資料](../../ui/activate-segment-streaming-destinations.md) ，以取得對此目的地啟用受眾區段的指示。

## 匯出的資料

要驗證資料是否已成功導出到[!DNL Google Ad Manager]目標，請檢查[!DNL Google Ad Manager]帳戶。 如果啟動成功，則會在您的帳戶中填入對象。
