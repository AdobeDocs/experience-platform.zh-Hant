---
keywords: Google ads;google ads;google adwords;Google AdWords;Google Adwords
title: Google Ads連線
description: Google Ads（先前稱為Google AdWords）是線上廣告服務，可讓企業透過文字搜尋、圖形顯示、YouTube視訊和應用程式內行動顯示，按點擊付費廣告。
translation-type: tm+mt
source-git-commit: 0759919dc458798ca4bc5f233a9cb319194ea534
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 0%

---


# [!DNL Google Ads] 連接

[!DNL Google Ads]線上廣告服 [!DNL Google AdWords]務，可讓企業透過文字搜尋、圖形顯示、視訊和應用程式內行動顯示，以每次點按付費 [!DNL YouTube] 方式進行廣告。

## 目標規格

請注意以下特定於[!DNL Google Ads]目標的詳細資訊：

* 在[!DNL Google]平台中以程式設計方式建立已啟動的觀眾。
* 平台目前不包含用於驗證成功啟動的測量量度。 請參閱Google中的觀眾計數，以驗證整合併瞭解觀眾鎖定規模。

>[!IMPORTANT]
>
>如果您想要使用[!DNL Google Ads]建立您的第一個目標，而過去(使用Experience Cloud或其他應用程式)未啟用Audience ManagerID服務中的[ID同步功能](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html)，請聯絡Adobe諮詢或客戶服務以啟用ID同步。 如果您先前在Audience Manager中設定Google整合，您設定的ID會同步至平台。

### 支援的身份{#supported-identities}

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

### 導出類型{#export-type}

**區段匯出** -您正將區段（對象）的所有成員匯出至Google目標。

## 先決條件

### 現有[!DNL Google Ads]帳戶

>[!IMPORTANT]
>
> [!DNL Google] 已過時與 [!DNL Google Ads] 協力廠商整合的新Cookie。要執行下一節中的允許清單步驟，您必須與[!DNL Google Ads]現有整合。 因此，使用[!DNL Google Ads]的建議方法是設定[!DNL Google Customer Match]整合。 有關建立[!DNL Google Customer Match]整合的詳細資訊，請閱讀有關建立[[!DNL Google Customer Match]](./google-customer-match.md)連接的教程。

### 允許清單

>[!NOTE]
>
>在「平台」中設定您的第一個[!DNL Google Ads]目標之前，允許清單是必填的。 在建立目標之前，請確保[!DNL Google]已完成下面所述的允許清單進程。

在「平台」中建立[!DNL Google Ads]目標之前，您必須聯繫[!DNL Google]以便將Adobe放在允許的資料提供器清單上，並將您的帳戶添加到允許清單中。 聯絡[!DNL Google]並提供下列資訊：

* **帳戶ID** :這是Adobe的帳戶ID  [!DNL Google]請聯絡Adobe客戶服務或您的Adobe代表以取得此ID。
* **客戶ID** :這是Adobe的客戶帳戶ID  [!DNL Google]請聯絡Adobe客戶服務或您的Adobe代表以取得此ID。
* 您的帳戶類型：**AdWords**
* **Google AdWords ID** :這是您的ID [!DNL Google]。ID格式通常為123-456-7890。

## 配置目標

在&#x200B;**[!UICONTROL Connections]** > **[!UICONTROL Destinations]**&#x200B;中，選擇[!DNL Google Ads] ，然後選擇&#x200B;**[!UICONTROL Configure]**。

![Connect Google Ads目的地](../../assets/catalog/advertising/google-ads-destination/catalog.png)

>[!NOTE]
>
>如果已存在與此目標的連接，則可以在目標卡上看到&#x200B;**[!UICONTROL Activate]**&#x200B;按鈕。 有關&#x200B;**[!UICONTROL Activate]**&#x200B;和&#x200B;**[!UICONTROL Configure]**&#x200B;之間差異的詳細資訊，請參閱目標工作區文檔的[目錄](../../ui/destinations-workspace.md#catalog)部分。

在建立目標工作流的&#x200B;**設定**&#x200B;步驟中，為目標填寫[!UICONTROL Basic Information]。

![基本資訊Google廣告](../../assets/catalog/advertising/google-ads-destination/setup.png)

* **[!UICONTROL Name]**:填寫此目標的首選名稱。
* **[!UICONTROL Description]**: 選用. 例如，您可以提及您使用此目的地的促銷活動。
* **[!UICONTROL Account Type]**:AdWords是唯一可用的選項。
* **[!UICONTROL Account ID]**:在您的帳戶ID中填入 [!DNL Google Ads]。ID格式通常為123-456-7890。
* **[!UICONTROL Marketing action]**:行銷動作會指出將資料匯出至目的地的方式。您可以從Adobe定義的行銷動作中選擇，也可以建立自己的行銷動作。 如需行銷動作的詳細資訊，請參閱[資料使用政策概述](../../../data-governance/policies/overview.md)。

## 啟用區段至[!DNL Google Ads]

如需如何啟用區段至[!DNL Google Ads]的指示，請參閱[啟用資料至目標](../../ui/activate-destinations.md)。

## 匯出的資料

要驗證資料是否已成功導出到[!DNL Google Ads]目標，請檢查[!DNL Google Ads]帳戶。 如果啟動成功，您的帳戶會填入觀眾。