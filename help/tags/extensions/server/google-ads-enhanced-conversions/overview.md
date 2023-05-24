---
title: Google廣告增強轉換擴展
description: 瞭解Google廣告增強轉換擴展，以在Adobe Experience Platform進行事件轉發。
exl-id: 65cdff40-276f-4481-9621-6c6861dbd412
last-substantial-update: 2022-11-23T00:00:00Z
source-git-commit: 1c417744518a7ac7cfb9c65d6af8219dcbc70d46
workflow-type: tm+mt
source-wordcount: '1311'
ht-degree: 1%

---

# [!DNL Google Ads] 增強的轉換擴展

使用 [!DNL Google Ads] API，您可以 [增強轉換](https://support.google.com/google-ads/answer/9888656) 以轉換調整的形式發送第一方客戶資料。 Google使用此附加資料來改進由廣告交互驅動的線上轉換的報告。

的 [[!DNL Google Ads] 增強的轉換事件轉發擴展](https://exchange.adobe.com/apps/ec/108630/google-ads-enhanced-conversions) (前稱 [!DNL Enhanced Conversions] 擴展)提供了用戶友好的模板，可輕鬆實現增強的轉換 [!DNL Google Ads] API。

>[!IMPORTANT]
>
>增強的轉換只適用於存在客戶資料的轉換類型，如訂閱、註冊和購買。 以下一個或多個客戶資料必須可用，因為在 [配置轉換操作](#conversion-action-event-forwarding) 對於事件轉發規則：
>
>* 電子郵件地址（首選）
>* 名稱和住址（街道地址、城市、州/地區和郵遞區號）
>* 電話號碼（除上述另外兩條資訊之一外，還必須提供）


## 實施概述

增強的轉換利用 [!DNL Google Ads] 將第一方資料添加到客戶端設備（通常是網站）上發生的轉換的API。 這意味著要實施增強的轉換有兩個步驟：

1. 從客戶端發送轉換。
1. 使用事件轉發來發送附加的第一方資料，以增強從客戶端發送的轉換資料。

>[!TIP]
>
>要將客戶端轉換事件與從事件轉發發送的第一方資料關聯， `transaction_ID` 在兩個呼叫中必須相同。 有關必須為每個服務提供此值的位置的詳細資訊，請參閱有關為 [標籤](#conversion-action-tags) 和 [事件轉發](#conversion-action-event-forwarding)的下界。

由於發送轉換事件涉及客戶端和伺服器端實現，因此本文檔介紹了設定客戶端的先決條件步驟 [[!DNL Google Global Site Tag] (gtag)擴展](https://exchange.adobe.com/apps/ec/101437/google-global-site-tag-gtag) 除了 [!DNL Enhanced Conversions] 事件轉發的擴展。

以下視頻介紹 [!DNL Enhanced Conversions] 在高級別上逐步推廣和逐步實施：

>[!VIDEO](https://video.tv.adobe.com/v/3411365?quality=12&learn=on)

## 使用標籤發送轉換

要從網站發送轉換事件， [!DNL Google Global Site Tag] 必須部署(gtag)。 通過配置和安裝 [!DNL Google Global Site Tag] (gtag)擴展。

### 配置和安裝 [!DNL Google Global Site Tag] 擴展

導航到 [!UICONTROL 資料收集] UI或Experience PlatformUI並選擇 **[!UICONTROL 標籤]** 的子菜單。 選擇要安裝擴展的標籤屬性，然後選擇 **[!UICONTROL 擴展]** 的子菜單。 在 **[!UICONTROL 目錄]** 頁籤 [!UICONTROL Google全球站點標籤(gtag)] 擴展和選擇 **[!UICONTROL 安裝]**。

![的 [!UICONTROL Google全球站點標籤(gtag)] 正在選擇擴展 [!UICONTROL 擴展] 的 [!UICONTROL 資料收集] UI。](../../../images/extensions/server/google-ads-enhanced-conversions/install-gtag-extension.png)

出現安裝對話框。 從此處，選擇 **[!UICONTROL 添加帳戶]** 並在出現提示時提供以下值：

| 帳戶屬性 | 說明 |
| --- | --- |
| 帳戶名 | 帳戶的唯一名稱。 此名稱僅在標籤UI中使用。 |
| 帳戶 ID | 您 [!DNL Google Ads] 帳戶ID。 要查找此值，請登錄 [!DNL Google Ads] 並導航至： **[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Install the Tag yourself]**。 帳戶ID字串可在以開始的代碼段窗口中找到 `AW-` 或 `d`。 |
| 產品 | 選擇 **[!UICONTROL Google廣告（廣告詞）]**。 |

{style="table-layout:auto"}

完成後，選擇 **[!UICONTROL 添加帳戶]**，然後選擇 **[!UICONTROL 保存]**。

### 添加發送轉換操作 {#conversion-action-tags}

安裝擴展後，可以開始在標籤規則中包括轉換操作。 建立或編輯偵聽要增強的轉換的規則時，選擇 **[!UICONTROL 添加]** 在 [!UICONTROL 操作]。 在下一個對話框中，選擇 **[!UICONTROL Google全球站點標籤(gtag)]** 從 [!UICONTROL 擴展] 下拉清單，然後選擇 **[!UICONTROL 發送事件]** 在 [!UICONTROL 操作類型]。

![的 [!UICONTROL 發送事件] 在規則編輯工作流的操作配置視圖中選擇的操作類型。](../../../images/extensions/server/google-ads-enhanced-conversions/select-client-action.png)

將顯示允許您配置 [!DNL gtag] 的子菜單。 至少必須填寫以下欄位：

1. **[!UICONTROL 事件名稱（操作）]**:輸入 `conversion` 值。
1. 添加鍵所在的新欄位 `transaction_id` 值是 [資料元](../../../ui/managing-resources/data-elements.md) 包含 [事務ID](https://support.google.com/google-ads/answer/6386790) 值。
1. **[!UICONTROL 轉換標籤]**:從您的 [!DNL Google Ads] 帳戶。 要查找此值，請登錄Google廣告並導航至 **[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Use Google Tag Manager]**。 轉換標籤可在 [!DNL Instructions]。
   >[!IMPORTANT]
   >
   >當您處於您的標籤設定區域時 [!DNL Google Ads] 帳戶，確保已啟用增強的轉換。 要執行此操作，請查看並接受服務條款，然後選擇 **[!DNL Turn on enhanced conversions]** 和 **[!DNL API]** 作為實現方法。

配置操作後，選擇 **[!UICONTROL 保留更改]** 將操作添加到規則配置。 對規則滿意後，選擇 **[!UICONTROL 保存到庫]**。

最後，發佈新 [構建](../../../ui/publishing/builds.md) 以啟用對庫的更改。

## 使用事件轉發發送第一方資料

一旦您能夠從客戶端發送轉換事件，則可以使用 [!DNL Enhanced Conversions] 事件轉發擴展。

### 建立GoogleOAuth 2機密和資料元素 {#create-secret-data-element}

在配置擴展之前，必須建立訪問令牌，以便將身份驗證轉發到 [!DNL Google Ads] API。

請參閱上的指南 [建立事件轉發機密](../../../ui/event-forwarding/secrets.md) 的子菜單。 確保您選擇 **[!UICONTROL GoogleOAuth 2]** 作為機密類型。 繼續按照提示操作，當要求選擇Google帳戶配置檔案時，選擇有權訪問您正在配置的轉換操作的帳戶。

一旦秘密被製造， [建立新資料元素](../../../ui/managing-resources/data-elements.md#create-a-data-element) 選擇 **[!UICONTROL 秘密]** 的子菜單。 為每個環境選擇相應的GoogleOAuth 2機密，然後選擇 **[!UICONTROL 保存到庫]**。

### 配置和安裝 [!DNL Enhanced Conversions] 擴展 {#install-enhanced-conversions}

查找 [!UICONTROL Google廣告增強轉換] 在事件轉發目錄中擴展並選擇 **[!UICONTROL 安裝]**。

![的 [!UICONTROL Google廣告增強轉換] 正在選擇擴展 [!UICONTROL 擴展] 的 [!UICONTROL 資料收集] UI。](../../../images/extensions/server/google-ads-enhanced-conversions/install-enhanced-conversions.png)

要配置擴展，必須填寫以下兩個必填欄位：

1. **[!UICONTROL 客戶ID]**:唯一標識您的ID [!DNL Google Ads] 帳戶。 要查找此值，請登錄 [!DNL Google Ads] 導航 **[!DNL Help]** > **[!DNL Customer ID]**。
1. **[!UICONTROL 訪問令牌資料元素]**:選擇資料元素表徵圖(![資料元素表徵圖](../../../images/extensions/server/google-ads-enhanced-conversions/data-element-icon.png))並選擇您的GoogleOAuth 2機密資料元素 [在上一步中配置](#create-secret-data-element) 的子菜單。

完成後，選擇 **[!UICONTROL 保存]** 安裝擴展。

### 添加 [!UICONTROL 發送轉換] 對規則的操作 {#conversion-action-event-forwarding}

安裝擴展後，您可以開始包括 [!UICONTROL 發送轉換] 事件轉發規則中的操作。 建立或編輯偵聽要增強的轉換的規則時，選擇 **[!UICONTROL 添加]** 在 [!UICONTROL 操作]。 在下一個對話框中，選擇 **[!UICONTROL Google廣告增強轉換]** 從 [!UICONTROL 擴展] 下拉清單，然後選擇 **[!UICONTROL 發送轉換]** 在 [!UICONTROL 操作類型]。

![的 [!UICONTROL 發送轉換] 在規則編輯工作流的操作配置視圖中選擇的操作類型。](../../../images/extensions/server/google-ads-enhanced-conversions/select-server-action.png)

右面板中會出現新控制項，允許您配置轉換。 至少必須完成以下欄位：

**轉換資訊**

| 輸入 | 說明 |
| --- | --- |
| Customer ID | 您 [!DNL Google Ads] 客戶ID。 預設為您輸入的客戶ID [安裝擴展](#install-enhanced-conversions)。 |
| 轉換ID或轉換標籤 | 從中獲取的跟蹤值 [!DNL Google Ads] 設定轉換跟蹤時。 值以開頭 `AW-`。<br><br>有關如何查找這些值的詳細資訊，請參閱 [[!DNL Google Ads] 文檔](https://support.google.com/tagmanager/answer/6105160?hl=en)。 |
| 交易 ID | 選擇具有與 [從客戶端發送](#conversion-action-tags) 使用 [!DNL Google Global Site Tag] 擴展。 |

**用戶標識**

* 必須至少包括三個用戶標識符之一：
   * 電子郵件
   * 電話號碼
   * 完整地址

>[!TIP]
>
>用戶標識資料在發送到Google之前必須進行散列處理。 如果事件轉發收到資料時資料沒有散列，請選擇 **[!UICONTROL 規範化和散列]** 在給定欄位上切換，以指示擴展對值進行散列。
>
>![的 [!UICONTROL 規範化和散列] 啟用切換 [!UICONTROL 電子郵件] 輸入 [!UICONTROL 發送轉換] 操作配置窗體。](../../../images/extensions/server/google-ads-enhanced-conversions/hash-user-id-values.png)

完成後，選擇 **[!UICONTROL 保留更改]** 將操作添加到規則配置。 對規則滿意後，選擇 **[!UICONTROL 保存到庫]**。

最後，發佈新事件轉發 [構建](../../../ui/publishing/builds.md) 以啟用對庫的更改。

## 後續步驟

本指南介紹如何將轉換事件發送到 [!DNL Google Ads] 使用 [!DNL Enhanced Conversions] 事件轉發擴展。 有關Experience Platform中事件轉發功能的詳細資訊，請參閱 [事件轉發概述](../../../ui/event-forwarding/overview.md)。
