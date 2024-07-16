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

Audience Manager Expanded Activation是以Adobe Experience Platform為基礎，可協助現有[Audience Manager](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/aam-home)使用者從Real-Time CDP啟用其對象至[社交](../destinations/catalog/social/overview.md)和[廣告](../destinations/catalog/advertising/overview.md)目的地平台，例如[Facebook](../destinations/catalog/social/facebook.md)、[Google Ads](../destinations/catalog/advertising/google-ads-destination.md)等。

>[!IMPORTANT]
>
>[!DNL Audience Manager Expanded Activation]僅供現有[!DNL Audience Manager]使用者使用。

## 術語 {#terminology}

Audience Manager Expanded Activation使用Adobe Experience Platform的概念和元件。 若要更清楚瞭解展開式啟動工作流程以及您將使用的元件，請確定您對下列概念有基本的瞭解：

* [對象](../segmentation/ui/overview.md)：對象是共用類似行為和/或特徵的一組人員。 此人員集合可由Adobe Experience Platform使用區段定義或對象構成（平台產生的對象）產生，或由外部來源（例如自訂上傳）（外部產生的對象）產生。 在展開的啟用中，您的Audience Manager區段（對象）會匯入為[自訂上傳](../segmentation/ui/audience-portal.md#import-audience)。
* [Source聯結器](../sources/home.md)： Source聯結器（也稱為來源）可協助Experience Platform使用者輕鬆地從多個來源擷取資料，允許使用Experience Platform服務來建構、標示和增強資料。 資料可從多種來源擷取，例如雲端儲存空間、協力廠商軟體和CRM系統。
* [目的地聯結器](../destinations/home.md)：目的地會說明任何端點，例如Adobe應用程式、廣告平台、雲端儲存服務或行銷服務，其中會啟動並傳送對象。 [!DNL Expanded Activation]支援啟用受眾至[advertising](../destinations/catalog/advertising/overview.md)和[social](../destinations/catalog/social/overview.md)目的地聯結器。

## 先決條件 {#prerequisites}

在您可以透過展開啟用啟用來啟用對象之前，請確定您符合底下所述的先決條件。

### 使用者和角色需求 {#permission-requirements}

您必須先從Admin Console建立使用者帳戶，並將其指派給[!DNL Expanded Activation]角色，才能使用[!DNL Expanded Activation]。 請參閱[管理](administration.md)頁面，以取得執行此動作的詳細指示。

### 對象需求 {#audience-requirements}

若要透過[!DNL Expanded Activation]啟用對象，請確定您的Audience Manager對象是以&#x200B;**雜湊電子郵件地址**&#x200B;為基礎。 根據您的Audience Manager使用情況，有兩種方式可確保這一點：

* 如果您使用[Audience Manager以人物為基礎的目的地](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview)功能，表示您已擷取雜湊電子郵件地址的Audience Manager。 在此情況下，您不需要執行其他步驟。 您可以跳到[透過[展開啟用]啟用對象](activate-audiences.md)。
* 如果您&#x200B;_不是_&#x200B;使用[Audience Manager以人物為基礎的目的地](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview)功能，您必須在Audience Manager中建立新的資料來源，並使用它來儲存雜湊電子郵件地址。 如需瞭解如何設定雜湊電子郵件工作流程的資料來源[，請參閱相關檔案](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/data-sources/create-data-source-hashed-emails)。 在您的Audience Manager資料來源中擷取雜湊電子郵件地址後，請閱讀有關[透過展開啟用啟用對象](activate-audiences.md)的檔案。

## 後續步驟 {#next-steps}

現在您已更瞭解使用[!DNL Expanded Activation]的使用案例和優點，請開始[設定您的帳戶](administration.md)，然後[啟用您的對象](activate-audiences.md)。
