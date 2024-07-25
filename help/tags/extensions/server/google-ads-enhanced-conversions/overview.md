---
title: Google Ads增強型轉換延伸功能
description: 瞭解Adobe Experience Platform中用於事件轉送的Google Ads Enhanced Conversion擴充功能。
exl-id: 65cdff40-276f-4481-9621-6c6861dbd412
last-substantial-update: 2022-11-23T00:00:00Z
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '1296'
ht-degree: 1%

---

# [!DNL Google Ads]增強型轉換延伸

使用[!DNL Google Ads] API，您可以透過以轉換調整的形式傳送第一方客戶資料，以運用[增強型轉換](https://support.google.com/google-ads/answer/9888656)。 Google會使用這項額外資料，改善由廣告互動驅動的線上轉換報表。

[[!DNL Google Ads] Enhanced Conversions事件轉送擴充功能](https://exchange.adobe.com/apps/ec/108630/google-ads-enhanced-conversions) （先前稱為[!DNL Enhanced Conversions]擴充功能）提供使用者易記的範本，可輕鬆實作[!DNL Google Ads] API的增強型轉換。

>[!IMPORTANT]
>
>增強型轉換僅適用於存在客戶資料的轉換型別，例如訂閱、註冊和購買。 下列一或多個客戶資料片段必須可供使用，因為當[為事件轉送規則設定轉換動作](#conversion-action-event-forwarding)時，這些片段是必要的：
>
>* 電子郵件地址（偏好設定）
>* 名稱和住家地址（街道地址、城市、州/地區和郵遞區號）
>* 電話號碼（必須在上述其他兩個資訊之一之外提供）

## 實施概述

增強型轉換可運用[!DNL Google Ads] API將第一方資料新增至使用者端裝置（通常是網站）上發生的轉換。 也就是說，實作增強型轉換有兩個步驟：

1. 從使用者端傳送轉換。
1. 使用事件轉送來傳送其他第一方資料，以增強從使用者端傳送的轉換資料。

>[!TIP]
>
>若要將使用者端轉換事件與從事件轉送傳送的第一方資料建立關聯，兩個呼叫中的`transaction_ID`必須相同。 如需每個服務必須提供此值的位置詳細資訊，請參閱分別為[標籤](#conversion-action-tags)和[事件轉送](#conversion-action-event-forwarding)設定轉換動作的章節。

由於傳送轉換事件涉及使用者端和伺服器端實作，因此除了事件轉送的[!DNL Enhanced Conversions]擴充功能之外，本檔案還涵蓋設定使用者端[[!DNL Google Global Site Tag] (gtag)擴充功能](https://exchange.adobe.com/apps/ec/101437/google-global-site-tag-gtag)的先決條件步驟。

下列影片介紹[!DNL Enhanced Conversions]擴充功能，並逐步說明高階實作步驟：

>[!VIDEO](https://video.tv.adobe.com/v/3411365?quality=12&learn=on)

## 使用標籤傳送轉換

若要從網站上傳送轉換事件，必須部署[!DNL Google Global Site Tag] (gtag)。 您可以設定並安裝[!DNL Google Global Site Tag] (gtag)擴充功能，以使用標籤達成此目的。

### 設定並安裝[!DNL Google Global Site Tag]擴充功能

導覽至[!UICONTROL 資料彙集] UI或Experience Platform UI，然後在左側導覽中選取&#x200B;**[!UICONTROL 標籤]**。 選取您要安裝擴充功能的標籤屬性，然後在左側導覽中選取&#x200B;**[!UICONTROL 擴充功能]**。 在&#x200B;**[!UICONTROL 目錄]**&#x200B;標籤下，找到[!UICONTROL Google全域網站標籤(gtag)]擴充功能，然後選取&#x200B;**[!UICONTROL 安裝]**。

![在[!UICONTROL 資料彙集] UI中的[!UICONTROL 擴充功能]檢視下選取[!UICONTROL Google全域網站標籤(gtag)]擴充功能。](../../../images/extensions/server/google-ads-enhanced-conversions/install-gtag-extension.png)

安裝對話方塊隨即顯示。 從這裡，選取&#x200B;**[!UICONTROL 新增帳戶]**，並在出現提示時提供下列值：

| 帳戶屬性 | 說明 |
| --- | --- |
| 帳戶名稱 | 帳戶的唯一名稱。 此名稱僅用於標籤UI。 |
| 帳戶 ID | 您的[!DNL Google Ads]帳戶識別碼。 若要尋找此值，請登入[!DNL Google Ads]並導覽至： **[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Install the Tag yourself]**。 您可以在以`AW-`或`d`開頭的程式碼片段視窗中找到帳戶ID字串。 |
| 產品 | 選取&#x200B;**[!UICONTROL Google Ads (AdWords)]**。 |

{style="table-layout:auto"}

完成時，請選取&#x200B;**[!UICONTROL 新增帳戶]**，然後選取&#x200B;**[!UICONTROL 儲存]**。

### 新增傳送轉換動作 {#conversion-action-tags}

安裝擴充功能後，您就可以開始將轉換動作納入標籤規則。 建立或編輯監聽要增強之轉換的規則時，請在[!UICONTROL 動作]下選取&#x200B;**[!UICONTROL 新增]**。 在下一個對話方塊中，從[!UICONTROL 擴充功能]下拉式清單中選取&#x200B;**[!UICONTROL Google全域網站標籤(gtag)]**，然後在[!UICONTROL 動作型別]下選取&#x200B;**[!UICONTROL 傳送事件]**。

![在規則編輯工作流程的動作組態檢視中選取的[!UICONTROL 傳送事件]動作型別。](../../../images/extensions/server/google-ads-enhanced-conversions/select-client-action.png)

會出現其他控制項，可讓您設定[!DNL gtag]事件。 至少必須填寫下列欄位：

1. **[!UICONTROL 事件名稱（動作）]**：輸入`conversion`作為值。
1. 新增索引鍵為`transaction_id`且值為包含[交易ID](https://support.google.com/google-ads/answer/6386790)值的[資料元素](../../../ui/managing-resources/data-elements.md)的欄位。
1. **[!UICONTROL 轉換標籤]**：從您的[!DNL Google Ads]帳戶輸入適當的轉換標籤。 若要尋找此值，請登入Google Ads並導覽至&#x200B;**[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Use Google Tag Manager]**。 您可以在[!DNL Instructions]下找到轉換標籤。
   >[!IMPORTANT]
   >
   >當您在[!DNL Google Ads]帳戶的標籤設定區域中時，請確定已啟用增強型轉換。 若要這麼做，請檢閱並接受服務條款，然後選取&#x200B;**[!DNL Turn on enhanced conversions]**&#x200B;與&#x200B;**[!DNL API]**&#x200B;作為實作方法。

設定動作後，選取&#x200B;**[!UICONTROL 保留變更]**&#x200B;以將動作新增至規則設定。 如果您對規則感到滿意，請選取&#x200B;**[!UICONTROL 儲存至程式庫]**。

最後，發佈新的[組建](../../../ui/publishing/builds.md)以啟用程式庫的變更。

## 使用事件轉送來傳送第一方資料

一旦您可以從使用者端傳送轉換事件，您就可以使用[!DNL Enhanced Conversions]事件轉送擴充功能來增強這些轉換。

### 建立Google OAuth 2密碼和資料元素 {#create-secret-data-element}

在設定擴充功能之前，您必須在事件轉送中建立存取Token，以驗證[!DNL Google Ads] API。

如需詳細步驟，請參閱[建立事件轉送密碼](../../../ui/event-forwarding/secrets.md)的指南。 請確定您選取&#x200B;**[!UICONTROL Google OAuth 2]**&#x200B;作為機密型別。 繼續依照提示進行，並在系統要求您選取Google帳戶設定檔時，請選取可存取正在設定之轉換動作的帳戶。

建立密碼之後，[建立新的資料元素](../../../ui/managing-resources/data-elements.md#create-a-data-element)，並為資料元素型別選取&#x200B;**[!UICONTROL 密碼]**。 為每個環境選取適當的Google OAuth 2密碼，然後選取&#x200B;**[!UICONTROL 儲存至資料庫]**。

### 設定並安裝[!DNL Enhanced Conversions]擴充功能 {#install-enhanced-conversions}

在事件轉寄目錄中尋找[!UICONTROL Google Ads增強型轉換]擴充功能，並選取&#x200B;**[!UICONTROL 安裝]**。

![在[!UICONTROL 資料彙集] UI中的[!UICONTROL 延伸模組]檢視下選取[!UICONTROL Google Ads增強型轉換]延伸模組。](../../../images/extensions/server/google-ads-enhanced-conversions/install-enhanced-conversions.png)

若要設定擴充功能，您必須填入兩個必填欄位：

1. **[!UICONTROL 客戶識別碼]**：可唯一識別您[!DNL Google Ads]帳戶的識別碼。 若要尋找此值，請登入[!DNL Google Ads]並導覽至&#x200B;**[!DNL Help]** > **[!DNL Customer ID]**。
2. **[!UICONTROL 存取Token資料元素]**：選取資料元素圖示（![資料元素圖示](/help/images/icons/database.png)），然後從功能表中選擇您在上一個步驟](#create-secret-data-element)中[設定的Google OAuth 2機密資料元素。

完成時，選取&#x200B;**[!UICONTROL 儲存]**&#x200B;以安裝擴充功能。

### 將[!UICONTROL 傳送轉換]動作新增至規則 {#conversion-action-event-forwarding}

安裝擴充功能後，您就可以開始將[!UICONTROL 傳送轉換]動作納入事件轉送規則。 建立或編輯監聽您要增強之轉換的規則時，請在[!UICONTROL 動作]下選取&#x200B;**[!UICONTROL 新增]**。 在下一個對話方塊中，從[!UICONTROL 擴充功能]下拉式清單中選取&#x200B;**[!UICONTROL Google Ads增強型轉換]**，然後在[!UICONTROL 動作型別]下選取&#x200B;**[!UICONTROL 傳送轉換]**。

![正在規則編輯工作流程的動作組態檢視中選取的[!UICONTROL 傳送轉換]動作型別。](../../../images/extensions/server/google-ads-enhanced-conversions/select-server-action.png)

新的控制項會顯示在右側面板中，供您設定轉換。 至少必須完成下列欄位：

**轉換資訊**

| 輸入 | 說明 |
| --- | --- |
| 客戶ID | 您的[!DNL Google Ads]客戶識別碼。 預設為您在[安裝擴充功能](#install-enhanced-conversions)時輸入的客戶ID。 |
| 轉換ID或轉換標籤 | 設定轉換追蹤時從[!DNL Google Ads]取得的追蹤值。 值以`AW-`開頭。<br><br>如需如何尋找這些值的詳細資訊，請參閱[[!DNL Google Ads] 檔案](https://support.google.com/tagmanager/answer/6105160?hl=en)。 |
| 交易 ID | 選取一個資料元素，該資料元素具有使用[!DNL Google Global Site Tag]延伸從使用者端](#conversion-action-tags)傳送的相同交易ID值[。 |

**使用者識別**

* 至少必須包含下列三個使用者識別碼之一：
   * 電子郵件
   * 電話號碼
   * 完整地址

>[!TIP]
>
>必須先雜湊使用者識別資料，才能將其傳送至Google。 如果事件轉送收到資料時未進行雜湊處理，請選取指定欄位上的&#x200B;**[!UICONTROL 標準化與雜湊]**&#x200B;切換按鈕，指示擴充功能將值雜湊。
>
>![已在[!UICONTROL 傳送轉換]動作設定表單中，為[!UICONTROL 電子郵件]輸入啟用[!UICONTROL 標準化與雜湊]切換。](../../../images/extensions/server/google-ads-enhanced-conversions/hash-user-id-values.png)

完成後，選取&#x200B;**[!UICONTROL 保留變更]**&#x200B;以將動作新增至規則設定。 如果您對規則感到滿意，請選取&#x200B;**[!UICONTROL 儲存至程式庫]**。

最後，發佈新的事件轉送[組建](../../../ui/publishing/builds.md)，以啟用程式庫的變更。

## 後續步驟

本指南說明如何使用[!DNL Enhanced Conversions]事件轉送擴充功能，將轉換事件傳送至[!DNL Google Ads]。 如需Experience Platform中事件轉送功能的詳細資訊，請參閱[事件轉送概觀](../../../ui/event-forwarding/overview.md)。
