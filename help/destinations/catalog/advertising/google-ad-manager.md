---
keywords: google廣告管理員；google廣告；doubleclick;DoubleClick AdX;DoubleClick;Google廣告管理員；Google廣告管理員
title: Google廣告管理員連線
description: 'Google Ad Manager之前稱為DoubleClick for Publishers或DoubleClick AdX，是來自谷歌的廣告服務平台，可讓出版業者透過視訊和行動應用程式管理其網站上的廣告展示。  '
translation-type: tm+mt
source-git-commit: 24e0a274e61fcf6311c647067920686e4f25e840
workflow-type: tm+mt
source-wordcount: '738'
ht-degree: 0%

---


# [!DNL Google Ad Manager] 連接

## 概述 {#overview}

[!DNL Google Ad Manager](之前稱為「發 [!DNL DoubleClick] 布者」或 [!DNL DoubleClick AdX]「發佈者」)是廣告服務平台，可 [!DNL Google] 讓發佈者透過視訊和行動應用程式管理其網站上的廣告顯示。

## 目標詳細資訊{#specifics}

請注意以下特定於[!DNL Google Ad Manager]目標的詳細資訊：

* 在[!DNL Google]平台中以程式設計方式建立已啟動的觀眾。
* [!DNL Platform] 目前不包含用於驗證成功啟動的測量量度。請參閱Google中的觀眾計數，以驗證整合併瞭解觀眾鎖定規模。

## 支援的身份{#supported-identities}

[!DNL Google Ad Manager] 支援啟用下表所述的身分。

| 目標識別 | 說明 | 考量事項 |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | 當您的來源識別為GAID命名空間時，請選取此目標識別。 |
| IDFA | [!DNL Apple ID for Advertisers] | 當您的來源識別為IDFA命名空間時，請選取此目標識別。 |
| AAMUUID | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html)，也叫做 [!DNL Device ID]。38位數的數位裝置ID，可Audience Manager與其互動的每個裝置相關聯。 | Google使用[AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en)來定位加州的使用者，並針對所有其他使用者使用Google Cookie ID。 |
| [!DNL Google] Cookie ID | [!DNL Google] Cookie ID | [!DNL Google] 使用此ID來定位加州以外的使用者。 |
| 瑞達 | 廣告的Roku ID。 此ID可唯一識別Roku裝置。 |  |
| 女傭 | Microsoft廣告ID。 此ID可唯一識別執行Windows 10的裝置。 |  |
| Amazon消防電視ID | 此ID可唯一識別Amazon消防電視。 |  |

## 導出類型{#export-type}

**區段匯出** -您正將區段（對象）的所有成員匯出至Google目標。

## 先決條件

如果您想要使用[!DNL Google Ad Manager]建立您的第一個目標，而過去(使用Experience Cloud或其他應用程式)未啟用Audience ManagerID服務中的[ID同步功能](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html)，請聯絡Adobe諮詢或客戶服務以啟用ID同步。 如果您先前已在Audience Manager中設定[!DNL Google]整合，您設定的ID同步化會延續至平台。

## 允許清單

>[!NOTE]
>
>在「平台」中設定您的第一個[!DNL Google Ad Manager]目標之前，允許清單是必填的。 在建立目標之前，請確保[!DNL Google]已完成下面所述的允許清單進程。

在「平台」中建立[!DNL Google Ad Manager]目標之前，您必須聯繫[!DNL Google]以便將Adobe放在允許的資料提供器清單上，並將您的帳戶添加到允許清單中。 聯絡[!DNL Google]並提供下列資訊：

* **帳戶ID** :這是Adobe的帳戶ID  [!DNL Google]請聯絡Adobe客戶服務或您的Adobe代表以取得此ID。
* **客戶ID** :這是Adobe的客戶帳戶ID  [!DNL Google]請聯絡Adobe客戶服務或您的Adobe代表以取得此ID。
* **網路ID** :這是您的帳戶，  [!DNL Google Ad Manager]
* **對象連結ID** :這是您的帳戶，  [!DNL Google Ad Manager]
* 您的帳戶類型。 Google或AdX採購員提供的DFP。

## 配置目標

在&#x200B;**[!UICONTROL Connections]** > **[!UICONTROL Destinations]**&#x200B;中，選擇&#x200B;**[!DNL Google Ad Manager]** ，然後選擇&#x200B;**[!UICONTROL Configure]**。

![Connect Google Ad Manager目標](../../assets/catalog/advertising/google-ad-manager/catalog.png)

>[!NOTE]
>
>如果已存在與此目標的連接，則可以在目標卡上看到&#x200B;**[!UICONTROL Activate]**&#x200B;按鈕。 有關&#x200B;**[!UICONTROL Activate]**&#x200B;和&#x200B;**[!UICONTROL Configure]**&#x200B;之間差異的詳細資訊，請參閱目標工作區文檔的[目錄](../../ui/destinations-workspace.md#catalog)部分。

在建立目標工作流的&#x200B;**設定**&#x200B;步驟中，為目標填寫[!UICONTROL Basic Information]。

![基本資訊Google廣告管理員](../../assets/catalog/advertising/google-ad-manager/setup.png)

* **[!UICONTROL Name]**:填寫此目標的首選名稱。
* **[!UICONTROL Description]**: 選用. 例如，您可以提及您使用此目的地的促銷活動。
* **[!UICONTROL Account Type]**:根據您使用Google的帳戶，選取一個選項：
   * 使用`DFP by Google`表示[!DNL DoubleClick]表示發佈者
   * 使用`AdX buyer`作為[!DNL Google AdX]
* **[!UICONTROL Account ID]**:在您的帳戶ID中填入 [!DNL Google]。這可以是您的網路ID或對象連結ID。 通常，這是8位數的ID。
* **[!UICONTROL Marketing action]**:行銷動作會指出將資料匯出至目的地的方式。您可以從Adobe定義的行銷動作中選擇，也可以建立自己的行銷動作。 如需行銷動作的詳細資訊，請參閱[資料使用政策概述](../../../data-governance/policies/overview.md)。

>[!NOTE]
>
>設定[!DNL Google Ad Manager]目標時，請與您的[!DNL Google Account Manager]或Adobe代表合作，以瞭解您擁有的帳戶類型。

## 啟用區段至[!DNL Google Ad Manager]

如需如何啟用區段至[!DNL Google Ad Manager]的指示，請參閱[啟用資料至目標](../../ui/activate-destinations.md)。

## 匯出的資料

要驗證資料是否已成功導出到[!DNL Google Ad Manager]目標，請檢查[!DNL Google Ad Manager]帳戶。 如果啟動成功，您的帳戶會填入觀眾。