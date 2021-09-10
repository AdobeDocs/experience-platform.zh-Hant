---
title: Twitter自訂對象連線
description: 鎖定Twitter中現有的追隨者和客戶，並啟用Adobe Experience Platform中建置的對象，建立相關的再行銷活動
source-git-commit: 3ea3f9ed156ba3a1fbc790153a4b8fa193d5e2da
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 2%

---


# [!DNL Twitter Custom Audiences] 連接

## 概覽 {#overview}

鎖定Twitter中現有的追隨者和客戶，並啟用Adobe Experience Platform中建置的對象，以建立相關的再行銷活動。

## 先決條件 {#prerequisites}

設定[!DNL Twitter Custom Audiences]目的地前，請務必檢閱您需要符合的下列Twitter必要條件。

1. 您的[!DNL Twitter Ads]帳戶必須符合廣告資格。 新[!DNL Twitter Ads]帳戶在建立後的前2週內不符合廣告資格。
2. 您在[!DNL Twitter Audience Manager]中授權存取的Twitter使用者帳戶必須已啟用&#x200B;*[!DNL Partner Audience Manager]*&#x200B;權限。


## 支援的身分 {#supported-identities}

[!DNL Twitter Custom Audiences] 支援啟用下表所述的身分。深入了解[identities](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started)。

| Target身分 | 說明 | 考量事項 |
|---|---|---|
| device_id | IDFA/AdID/Android ID | Adobe Experience Platform支援Google廣告ID(GAID)和廣告商適用的Apple ID(IDFA)。 請在目標激活工作流的[映射步驟](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping)中相應地映射源架構中的這些命名空間和/或屬性。 |
| 電子郵件 | 使用者的電子郵件地址 | 請將純文字電子郵件地址和SHA256雜湊電子郵件地址映射到此欄位。 當源欄位包含未雜湊屬性時，請核取&#x200B;**[!UICONTROL Apply transformation]**&#x200B;選項，讓[!DNL Platform]在啟動時自動雜湊資料。 如果您在將客戶電子郵件地址上傳至Adobe Experience Platform之前先雜湊這些電子郵件地址，請注意，這些身分識別必須使用SHA256雜湊處理，不含鹽。 |

{style=&quot;table-layout:auto&quot;}

## 匯出類型 {#export-type}

**區段匯出**  — 您會使用Twitter自訂對象目的地中使用的識別碼，匯出區段（對象）的所有成員。

## 使用案例 {#use-cases}

為協助您更清楚了解您應如何及何時使用[!DNL Twitter Custom Audiences]目的地，以下是Adobe Experience Platform客戶可借由使用此目的地解決的範例使用案例。

### 使用案例#1

將Twitter中現有的追隨者和客戶鎖定為目標，並透過啟用Twitter中[!DNL List Custom Audiences]在Adobe Experience Platform中建置的對象，建立相關的再行銷活動。

## 連接到目標 {#connect}

要連接到此目標，請按照[目標配置教程](../../ui/connect-destination.md)中所述的步驟操作。

### 連線參數 {#parameters}

在[設定](../../ui/connect-destination.md)此目標時，您必須提供下列資訊：

* **[!UICONTROL 名稱]**:日後您將透過此名稱識別此目的地。
* **[!UICONTROL 說明]**:未來可協助您識別此目的地的說明。
* **[!UICONTROL 帳戶ID]**:您的 [!DNL Twitter Ads] 帳戶ID。您可在[!DNL Twitter Ads]設定中找到。

## 啟用此目的地的區段 {#activate}

請參閱[啟動設定檔和區段至串流區段匯出目的地](/help/destinations/ui/activate-segment-streaming-destinations.md) ，以取得啟動受眾區段至此目的地的指示。

## 資料使用與控管 {#data-usage-governance}

處理資料時，所有[!DNL Adobe Experience Platform]目標都符合資料使用策略。 有關[!DNL Adobe Experience Platform]如何實施資料控管的詳細資訊，請參閱[資料控管概述](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html)。

## 其他資源 {#additional-resources}

將受眾區段對應至Twitter時，請務必符合下列區段命名需求：

1. 提供人類看得懂的區段對應名稱。 建議您使用與用於Experience Platform區段相同的名稱。
2. 請勿使用特殊字元(+ &amp; 、 %):;@ / = ? $)。 如果您的Experience Platform區段名稱包含這些字元，請先移除這些字元，再將區段對應至Twitter目的地。

有關Twitter中[!DNL List Custom Audiences]的詳細資訊，請參閱[Twitter檔案](https://business.twitter.com/en/help/campaign-setup/campaign-targeting/custom-audiences/lists.html)。