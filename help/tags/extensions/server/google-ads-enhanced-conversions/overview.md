---
title: Google Ads Enhanced Conversions擴充功能
description: 了解Adobe Experience Platform中用於事件轉送的Google Ads Enhanced Conversions擴充功能。
exl-id: 65cdff40-276f-4481-9621-6c6861dbd412
source-git-commit: bfbad3c11df64526627e4ce2d766b527df678bca
workflow-type: tm+mt
source-wordcount: '1311'
ht-degree: 1%

---

# [!DNL Google Ads] 增強轉換擴充功能

使用 [!DNL Google Ads] API，您可以運用 [增強轉換](https://support.google.com/google-ads/answer/9888656) 以轉換調整的形式傳送第一方客戶資料。 Google會使用此額外資料來改善廣告互動所驅動的線上轉換報告。

此 [[!DNL Google Ads] 增強轉換事件轉送擴充功能](https://exchange.adobe.com/apps/ec/108630/google-ads-enhanced-conversions) (前稱為 [!DNL Enhanced Conversions] 擴充功能)提供方便使用的範本，可輕鬆實作增強的轉換 [!DNL Google Ads] API。

>[!IMPORTANT]
>
>增強的轉換僅適用於有客戶資料的轉換類型，例如訂閱、註冊和購買。 下列一或多個客戶資料必須可供使用，如 [設定轉換動作](#conversion-action-event-forwarding) 對於事件轉發規則：
>
>* 電子郵件地址（首選）
>* 姓名和住址（街道地址、城市、州/地區和郵遞區號）
>* 電話號碼（除了上面另外兩條資訊之一外，還必須提供）


## 實施概述

增強的轉換會利用 [!DNL Google Ads] 將第一方資料新增至用戶端裝置（通常是網站）上發生的轉換。 這表示實作增強轉換有兩個步驟：

1. 從用戶端傳送轉換。
1. 使用事件轉送來傳送其他第一方資料，以增強從用戶端傳送的轉換資料。

>[!TIP]
>
>若要將用戶端轉換事件與從事件轉送傳送的第一方資料建立關聯，請 `transaction_ID` 在兩個呼叫中必須相同。 如需每個服務必須提供此值的詳細資訊，請參閱 [標籤](#conversion-action-tags) 和 [事件轉送](#conversion-action-event-forwarding)，分別為。

由於傳送轉換事件同時涉及用戶端和伺服器端實作，本檔案涵蓋設定用戶端的先決條件步驟 [[!DNL Google Global Site Tag] (gtag)擴充功能](https://exchange.adobe.com/apps/ec/101437/google-global-site-tag-gtag) 除了 [!DNL Enhanced Conversions] 事件轉送的擴充功能。

以下影片介紹 [!DNL Enhanced Conversions] 擴充功能並逐步說明高階的實作步驟：

>[!VIDEO](https://video.tv.adobe.com/v/3411365?quality=12&learn=on)

## 使用標籤傳送轉換

若要從網站上傳送轉換事件， [!DNL Google Global Site Tag] (gtag)必須部署。 您可以透過設定和安裝 [!DNL Google Global Site Tag] (gtag)擴充功能。

### 配置和安裝 [!DNL Google Global Site Tag] 擴充功能

導覽至 [!UICONTROL 資料收集] UI或Experience PlatformUI，並選取 **[!UICONTROL 標籤]** 的下一頁。 選取您要安裝擴充功能的標籤屬性，然後選取 **[!UICONTROL 擴充功能]** 的下一頁。 在 **[!UICONTROL 目錄]** 頁簽，找到 [!UICONTROL Google全域網站標籤(gtag)] 擴充功能和選取 **[!UICONTROL 安裝]**.

![此 [!UICONTROL Google全域網站標籤(gtag)] 正在下選取擴充功能 [!UICONTROL 擴充功能] 檢視 [!UICONTROL 資料收集] UI。](../../../images/extensions/server/google-ads-enhanced-conversions/install-gtag-extension.png)

安裝對話框隨即顯示。 從此處，選擇 **[!UICONTROL 新增帳戶]** 並在出現提示時提供下列值：

| 帳戶屬性 | 說明 |
| --- | --- |
| 帳戶名稱 | 帳戶的唯一名稱。 此名稱僅用於標籤UI中。 |
| 帳戶 ID | 您的 [!DNL Google Ads] 帳戶ID。 若要尋找此值，請登入 [!DNL Google Ads] 並導覽至： **[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Install the Tag yourself]**. 帳戶ID字串可在程式碼片段視窗中找到，開頭為 `AW-` 或 `d`. |
| 產品 | 選擇 **[!UICONTROL Google廣告(AdWords)]**. |

{style="table-layout:auto"}

完成後，請選取 **[!UICONTROL 新增帳戶]**，然後選取 **[!UICONTROL 儲存]**.

### 新增傳送轉換動作 {#conversion-action-tags}

安裝擴充功能後，您可以開始在標籤規則中加入轉換動作。 建立或編輯監聽要增強的轉換的規則時，請選取 **[!UICONTROL 新增]** 在 [!UICONTROL 動作]. 在下一個對話方塊中，選取 **[!UICONTROL Google全域網站標籤(gtag)]** 從 [!UICONTROL 擴充功能] 下拉式清單，然後選取 **[!UICONTROL 傳送事件]** 在 [!UICONTROL 動作類型].

![此 [!UICONTROL 傳送事件] 在規則編輯工作流程的動作設定檢視中選取的動作類型。](../../../images/extensions/server/google-ads-enhanced-conversions/select-client-action.png)

其他控制項可讓您設定 [!DNL gtag] 事件。 至少必須填寫下列欄位：

1. **[!UICONTROL 事件名稱（動作）]**:輸入 `conversion` 作為值。
1. 新增鍵值為 `transaction_id` 而值是 [資料元素](../../../ui/managing-resources/data-elements.md) 包含 [交易ID](https://support.google.com/google-ads/answer/6386790) 值。
1. **[!UICONTROL 轉換標籤]**:從 [!DNL Google Ads] 帳戶。 若要尋找此值，請登入Google Ads並導覽至 **[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Use Google Tag Manager]**. 轉換標籤位於 [!DNL Instructions].
   >[!IMPORTANT]
   >
   >當您位於 [!DNL Google Ads] 帳戶，請確定已啟用增強的轉換。 要執行此操作，請查看並接受服務條款，然後選擇 **[!DNL Turn on enhanced conversions]** 和 **[!DNL API]** 作為實施方法。

設定動作後，請選取 **[!UICONTROL 保留變更]** 將動作新增至規則設定。 對規則感到滿意時，請選取 **[!UICONTROL 儲存至程式庫]**.

最後，發佈新 [建置](../../../ui/publishing/builds.md) 啟用程式庫的變更。

## 使用事件轉送傳送第一方資料

從用戶端傳送轉換事件後，您就可以使用 [!DNL Enhanced Conversions] 事件轉送擴充功能。

### 建立Google OAuth 2密碼和資料元素 {#create-secret-data-element}

設定擴充功能前，您必須在事件轉送中建立存取權杖，才能驗證 [!DNL Google Ads] API。

請參閱 [建立事件轉送機密](../../../ui/event-forwarding/secrets.md) 以取得詳細步驟。 確定您選取 **[!UICONTROL GoogleOAuth 2]** 作為機密類型。 繼續遵循提示操作，當系統要求您選取Google帳戶設定檔時，請選取可存取您所設定之轉換動作的帳戶。

一旦密碼被建立， [建立新資料元素](../../../ui/managing-resources/data-elements.md#create-a-data-element) 選取 **[!UICONTROL 機密]** （適用於資料元素類型）。 為每個環境選取適當的Google OAuth 2密碼，然後選取 **[!UICONTROL 儲存至程式庫]**.

### 配置和安裝 [!DNL Enhanced Conversions] 擴充功能 {#install-enhanced-conversions}

尋找 [!UICONTROL Google Ads增強轉換] 事件轉送目錄中的擴充功能，然後選取 **[!UICONTROL 安裝]**.

![此 [!UICONTROL Google Ads增強轉換] 正在下選取擴充功能 [!UICONTROL 擴充功能] 檢視 [!UICONTROL 資料收集] UI。](../../../images/extensions/server/google-ads-enhanced-conversions/install-enhanced-conversions.png)

若要設定擴充功能，您必須填入兩個必填欄位：

1. **[!UICONTROL 客戶ID]**:可唯一識別您 [!DNL Google Ads] 帳戶。 若要尋找此值，請登入 [!DNL Google Ads] 並導覽至 **[!DNL Help]** > **[!DNL Customer ID]**.
1. **[!UICONTROL 存取權杖資料元素]**:選取資料元素圖示(![資料元素圖示](../../../images/extensions/server/google-ads-enhanced-conversions/data-element-icon.png))，然後選取您的Google OAuth 2機密資料元素 [在上一步中設定](#create-secret-data-element) 的上界。

完成後，請選取 **[!UICONTROL 儲存]** 以安裝擴充功能。

### 新增 [!UICONTROL 傳送轉換] 動作至規則 {#conversion-action-event-forwarding}

安裝擴充功能後，您就可以開始包括 [!UICONTROL 傳送轉換] 動作。 建立或編輯監聽您要增強的轉換的規則時，請選取 **[!UICONTROL 新增]** 在 [!UICONTROL 動作]. 在下一個對話方塊中，選取 **[!UICONTROL Google Ads增強轉換]** 從 [!UICONTROL 擴充功能] 下拉式清單，然後選取 **[!UICONTROL 傳送轉換]** 在 [!UICONTROL 動作類型].

![此 [!UICONTROL 傳送轉換] 在規則編輯工作流程的動作設定檢視中選取的動作類型。](../../../images/extensions/server/google-ads-enhanced-conversions/select-server-action.png)

右側面板中會顯示新控制項，允許您設定轉換。 至少必須填入下列欄位：

**轉換資訊**

| 輸入 | 說明 |
| --- | --- |
| Customer ID | 您的 [!DNL Google Ads] 客戶ID。 預設為您在 [安裝擴充功能](#install-enhanced-conversions). |
| 轉換ID或轉換標籤 | 從 [!DNL Google Ads] 設定轉換追蹤時識別。 值開頭為 `AW-`.<br><br>如需如何尋找這些值的詳細資訊，請參閱 [[!DNL Google Ads] 檔案](https://support.google.com/tagmanager/answer/6105160?hl=en). |
| 交易 ID | 選取具有相同交易ID值(即 [從用戶端傳送](#conversion-action-tags) 使用 [!DNL Google Global Site Tag] 擴充功能。 |

**使用者識別**

* 必須包括三個用戶標識符中的至少一個：
   * 電子郵件
   * 電話號碼
   * 完整地址

>[!TIP]
>
>使用者識別資料必須先經過雜湊處理，才能傳送至Google。 如果資料在事件轉送收到時沒有雜湊，請選取 **[!UICONTROL 標準化與雜湊]** 開啟指定欄位，指示擴充功能雜湊值。
>
>![此 [!UICONTROL 標準化與雜湊] 切換為啟用 [!UICONTROL 電子郵件] 輸入 [!UICONTROL 傳送轉換] 動作設定表單。](../../../images/extensions/server/google-ads-enhanced-conversions/hash-user-id-values.png)

完成後，請選取 **[!UICONTROL 保留變更]** 將動作新增至規則設定。 對規則感到滿意時，請選取 **[!UICONTROL 儲存至程式庫]**.

最後，發佈新的事件轉送 [建置](../../../ui/publishing/builds.md) 啟用程式庫的變更。

## 後續步驟

本指南說明如何將轉換事件傳送至 [!DNL Google Ads] 使用 [!DNL Enhanced Conversions] 事件轉送擴充功能。 如需Experience Platform中事件轉送功能的詳細資訊，請參閱 [事件轉送概觀](../../../ui/event-forwarding/overview.md).
