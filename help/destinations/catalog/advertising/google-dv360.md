---
keywords: DoubleClick競標管理器；DoubleClick競標管理器；DoubleClick；顯示與影片360；顯示360；影片360；影片360；顯示360；顯示與影片
title: Google Display & Video 360連線
description: Display & Video 360（先前稱為DoubleClick競標管理器）是一種工具，用於在顯示、視訊和行動詳細目錄來源間執行重新定位和對象鎖定目標的數位促銷活動。
exl-id: bdd3b3fd-891f-44ec-bd47-daf7f3289f92
source-git-commit: 7e2f6f54e754c52c8de7f98372d041b2a6520d46
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 1%

---

# [!DNL Google Display & Video 360] 連接

## 概覽 {#overview}

[!DNL Display & Video 360]，舊稱為，是 [!DNL DoubleClick Bid Manager]用來在顯示、視訊和行動詳細目錄來源執行重新鎖定目標和對象鎖定的數位促銷活動的工具。

## 目的地細節 {#specifics}

請注意下列特定於[!DNL Google Display & Video 360]目的地的詳細資訊：

* 已啟用的對象是以程式設計方式在Google平台中建立。
* [!DNL Platform] 目前不包含驗證是否成功啟用的測量量度。請參考Google中的對象計數，以驗證整合併了解對象鎖定目標大小。

>[!IMPORTANT]
>
>如果您想使用Google Display &amp; Video 360建立第一個目的地，而過去(使用Adobe Audience Manager或其他應用程式)未在Experience CloudID服務中啟用[ID同步功能](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html)，請連絡Adobe諮詢或客戶服務以啟用ID同步。 如果您先前已在Audience Manager中設定Google整合，則您設定的ID同步會持續到Platform。

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

### 允許清單

>[!NOTE]
>
>在Platform中設定您的第一個[!DNL Google Display & Video 360]目的地前，允許清單是必填的。 建立目的地之前，請確定Google已完成下述的允許清單程式。

在Platform中建立[!DNL Google Display & Video 360]目的地之前，您必須聯絡Google，要求將Adobe加入允許的資料提供者清單中，並將您的帳戶新增至允許清單中。 請連絡Google並提供下列資訊：

* **帳戶ID**:Adobe的帳戶ID與Google。帳戶ID:87933855。
* **客戶ID**:Adobe的客戶帳戶ID與Google。客戶ID:89690775。
* **您的帳戶類型**:使 **[!DNL Invite advertiser]** 用僅可讓受眾共用至您的Display &amp; Video 360帳戶中的特定品牌，或使用 **[!DNL Invite partner]** 讓受眾共用至您的Display &amp; Video 360帳戶中的所有品牌。

## 設定目的地

在&#x200B;**[!UICONTROL 連接]** > **[!UICONTROL 目標]**&#x200B;中，選擇[!DNL Google Display & Video 360]，然後選擇&#x200B;**[!UICONTROL 配置]**。

![連接Google Display &amp; Video 360目的地](../../assets/catalog/advertising/google-dv360/catalog.png)

>[!NOTE]
>
>如果與此目的地的連線已存在，您可以在目標卡上看到&#x200B;**[!UICONTROL 啟動]**&#x200B;按鈕。 有關[!UICONTROL Activate]和[!UICONTROL Configure]之間差異的詳細資訊，請參閱目標工作區檔案的[Catalog](../../ui/destinations-workspace.md#catalog)區段。

在建立目標工作流的&#x200B;**設定**&#x200B;步驟中，填入目標的[!UICONTROL 基本資訊]以及應套用至此目標的行銷動作。

![基本資訊Google Display &amp; Video 360](../../assets/catalog/advertising/google-dv360/setup.png)

* **[!UICONTROL 名稱]**:填寫此目的地的首選名稱。
* **[!UICONTROL 說明]**:選填。例如，您可以提及您使用此目的地的促銷活動。
* **[!UICONTROL 帳戶類型]**:根據您使用Google的帳戶，選取選項：
   * 使用`Invite Advertiser`只允許將對象共用至您的Display &amp; Video 360帳戶中的特定品牌。
   * 使用`Invite Partner`允許將受眾共用至您的Display &amp; Video 360帳戶中的所有品牌。
* **[!UICONTROL 帳戶ID]**:使用Google填 **[!DNL Invite partner]** 入 **[!DNL Invite advertiser]** 或帳戶ID。通常是6或7位數的ID。
* **[!UICONTROL 行銷動作]**:行銷動作會指出要將資料匯出至目的地的目的。您可以從Adobe定義的行銷動作中選取，或者您可以建立自己的行銷動作。 如需行銷動作的詳細資訊，請參閱[資料使用原則概述](../../../data-governance/policies/overview.md)。

>[!NOTE]
>
>設定[!DNL Google Display & Video 360]目標時，請與[!DNL Google Account Manager]或Adobe代表合作，了解您擁有的帳戶類型。

## 將區段啟用至[!DNL Google Display & Video 360]

如需如何將區段啟用至[!DNL Google Display & Video 360]的指示，請參閱[將資料啟用至目的地](../../ui/activate-destinations.md)。

## 匯出的資料

要驗證資料是否已成功導出到[!DNL Google Display & Video 360]目標，請檢查[!DNL Google Display & Video 360]帳戶。 如果啟動成功，則會在您的帳戶中填入對象。
