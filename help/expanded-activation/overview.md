---
title: Audience Manager 擴充啟用
description: 瞭解如何透過Audience Manager展開啟用，將Audience Manager對象啟用至社交和廣告目的地。
exl-id: 1f209578-a688-40b8-8f13-dab0d4380b3b
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 2%

---

# Audience Manager 擴充啟用

Audience Manager Extended Activation以Adobe Experience Platform為基礎，可協助現有的 [Audience Manager](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/aam-home) 使用者啟動其對象至 [社交](../destinations/catalog/social/overview.md) 和 [廣告](../destinations/catalog/advertising/overview.md) Real-Time CDP的目的地平台，例如 [facebook](../destinations/catalog/social/facebook.md)， [Google Ads](../destinations/catalog/advertising/google-ads-destination.md)、等等。

>[!IMPORTANT]
>
>[!DNL Audience Manager Expanded Activation] 僅供現有 [!DNL Audience Manager] 使用者。

## 術語 {#terminology}

Audience Manager Expanded Activation使用Adobe Experience Platform的概念和元件。 若要更清楚瞭解展開式啟動工作流程以及您將使用的元件，請確定您對下列概念有基本的瞭解：

* [受眾](../segmentation/ui/overview.md)：受眾是共用相似行為和/或特徵的一組人。 此人員集合可由Adobe Experience Platform使用區段定義或對象構成（平台產生的對象）產生，或由外部來源（例如自訂上傳）（外部產生的對象）產生。 在Expanded Activation中，您的Audience Manager區段（對象）會匯入為 [自訂上傳](../segmentation/ui/audience-portal.md#import-audience).
* [Source聯結器](../sources/home.md)：Source聯結器（也稱為來源）可協助Experience Platform使用者輕鬆擷取來自多個來源的資料，允許使用Experience Platform服務來建構、標籤和增強資料。 資料可從多種來源擷取，例如雲端儲存空間、協力廠商軟體和CRM系統。
* [目的地聯結器](../destinations/home.md)：目的地會說明受眾已啟用及傳送所在的任何端點，例如Adobe應用程式、廣告平台、雲端儲存服務或行銷服務。 [!DNL Expanded Activation] 支援啟用對象，以 [廣告](../destinations/catalog/advertising/overview.md) 和 [社交](../destinations/catalog/social/overview.md) 目的地聯結器。

## 先決條件 {#prerequisites}

在您可以透過展開啟用啟用來啟用對象之前，請確定您符合底下所述的先決條件。

### 使用者和角色需求 {#permission-requirements}

開始使用 [!DNL Expanded Activation]，您必須從Admin Console建立使用者帳戶，並將其指派給 [!DNL Expanded Activation] 角色。 請參閱 [管理](administration.md) 頁面，以取得執行此動作的詳細指示。

### 對象需求 {#audience-requirements}

若要透過啟用對象 [!DNL Expanded Activation]，確定您的Audience Manager對象是根據 **雜湊電子郵件地址**. 根據您的Audience Manager使用情況，有兩種方式可確保這一點：

* 如果您使用 [Audience Manager以人物為基礎的目的地](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview) 功能，則表示您已擷取Audience Manager中的雜湊電子郵件地址。 在此情況下，您不需要執行其他步驟。 您可以跳至 [透過展開的啟用來啟用對象](activate-audiences.md).
* 如果您是 _非_ 使用 [Audience Manager以人物為基礎的目的地](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview) 功能，您必須在Audience Manager中建立新的資料來源，並使用它來儲存雜湊電子郵件地址。 請參閱以下檔案： [設定雜湊電子郵件工作流程的資料來源](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/data-sources/create-data-source-hashed-emails) 以瞭解如何執行此動作。 在Audience Manager資料來源中擷取雜湊電子郵件地址後，請閱讀以下檔案： [透過展開的啟用來啟用對象](activate-audiences.md).

## 後續步驟 {#next-steps}

現在您已更瞭解使用的使用案例和優點 [!DNL Expanded Activation]，開始 [設定您的帳戶](administration.md) 然後 [啟用您的對象](activate-audiences.md).
