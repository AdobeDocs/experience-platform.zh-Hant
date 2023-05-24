---
keywords: 事件轉發擴展；twitter;twitter事件轉發擴展
title: Twitter事件轉發擴展
description: 此Adobe Experience Platform事件轉發擴展允許您根據業務需要將事件接收到Twitter。
last-substantial-update: 2023-05-24T00:00:00Z
source-git-commit: c5cc36d9530ff6fbb52a1995844f495b38e938b3
workflow-type: tm+mt
source-wordcount: '1140'
ht-degree: 3%

---

# [!DNL Twitter] 事件轉發擴展

[[!DNL Twitter]](https://www.twitter.com) 是一種線上社交媒體和社交網路服務，用戶在該服務上發佈和互動長達280個字元的消息，稱為tweet。 用戶可以使用瀏覽器、移動前端軟體或通過其寫程式方式與Twitter進行交互 [API](https://developer.twitter.com/en/docs/twitter-api)

的 [!DNL Twitter] Web轉換API [事件轉發](../../../ui/event-forwarding/overview.md) 擴展允許您利用在Adobe Experience Platform邊緣網路中捕獲的資料並將其發送到 [!DNL Twitter]。 本文檔介紹擴展的使用案例、如何安裝擴展，以及如何將其功能整合到事件轉發中 [規則](../../../ui/managing-resources/rules.md)。

[!DNL Twitter] 要求 [OAuth 1.0](https://developer.twitter.com/en/docs/authentication/oauth-1-0a) 用於與 [!DNL Twitter] [!DNL Web Conversions] API。

## 使用案例

如果要使用中的邊緣網路中的資料，應使用此擴展 [!DNL Twitter] 利用其客戶分析和目標能力。

例如，考慮組織中的市場營銷團隊。 該團隊從其網站捕獲用戶交互事件資料作為來自其網站的事件資料，並將其載入到 [!DNL Twitter] 使用此事件轉發擴展。

然後，營銷和分析團隊可以利用 [!DNL Twitter's] 執行其他分析並瞄準這些用戶進行目標廣告活動的功能。

有關特定於 [!DNL Twitter]，請參閱 [[!DNL Twitter] 使用案例](https://developer.twitter.com/en/use-cases/build-for-businesses) 文檔。

## [!DNL Twitter] 先決條件和護欄 {#prerequisites}

您必須具有 [!DNL Twitter] 帳戶以使用此分機。 轉到 [[!DNL Twitter] 註冊頁](https://help.twitter.com/en/using-twitter/create-twitter-account) 註冊並建立帳戶。

必須將帳戶設定為 [!DNL Twitter] 開發者帳戶。 要瞭解如何註冊為開發人員，請參閱 [[!DNL Twitter] 開發者帳戶](https://developer.twitter.com/en/support/twitter-api/developer-account)。

### API護欄 {#guardrails}

的 [!DNL Twitter] Web轉換API的速率限制為每15分鐘間隔60,000個請求，其中每個請求允許500個事件。

### 收集所需的配置詳細資訊 {#configuration-details}

為了將Experience Platform連接到 [!DNL Twitter]，需要輸入以下資料：

| 鍵類型 | 說明 |
| --- | --- |
| 使用者密鑰 | 用&#x200B;於訪問的應用的API密鑰 [!DNL Twitter] API。 請參閱 [!DNL Twitter] 文檔 [api鍵和密鑰](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/api-key-and-secret) 的上界。 |  |
| 消費者秘密 | API Secret允許你的應用訪問 [!DNL Twitter] API。 請參閱 [!DNL Twitter] 文檔 [api鍵和密鑰](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/api-key-and-secret) 的上界。 |
| 令牌密鑰 | 應用的非過期令牌密鑰，用於向 [!DNL Twitter] 通過OAuth的API。 請參閱 [!DNL Twitter] 文檔 [獲取使用訪問令牌](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens) 的上界。 |
| 訪問令牌 | 應用的非過期訪問令牌，用於向 [!DNL Twitter] 通過OAuth的API。 請參閱 [!DNL Twitter] 文檔 [獲取使用訪問令牌](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens) 的上界。 |
| 像素ID | 的 [!DNL Twitter] Pixel是網站標籤，在您的網站上實現，用於跟蹤網站操作或轉換。 請參閱 [!DNL Twitter] 文檔 [網站的轉換跟蹤](https://business.twitter.com/en/help/campaign-measurement-and-analytics/conversion-tracking-for-websites.html) 的上界。 |

## 安裝和配置 [!DNL Twitter] 擴展 {#install}

要安裝擴展， [建立事件轉發屬性](../../../ui/event-forwarding/overview.md#properties) 或選擇要編輯的現有屬性。

選擇 **[!UICONTROL 擴展]** 的子菜單。 在 **[!UICONTROL 目錄]** 頁籤 **[!UICONTROL 安裝]** 卡上 [!DNL Twitter] 擴展。

![顯示 [!DNL Twitter] 分機突出顯示安裝。](../../../images/extensions/server/twitter/install.png)

>[!IMPORTANT]
>
>根據您的實施需要，在配置擴展之前，可能需要建立架構、資料元素和資料集。 請在開始之前查看所有配置步驟，以確定您需要為使用案例設定哪些實體。

在下一個螢幕上，輸入以下 [配置值](#configuration-details) 你之前從 [!DNL Twitter]:

* **[!UICONTROL 像素ID]**
* **[!UICONTROL 使用者密鑰]**
* **[!UICONTROL 消費者秘密]**
* **[!UICONTROL 令牌]**
* **[!UICONTROL 令牌密鑰]**

完成後，選擇 **[!UICONTROL 保存]**。

![[!DNL Twitter] 配置螢幕 [!DNL Twitter] 擴展。](../../../images/extensions/server/twitter/configure.png)

## 配置事件轉發規則 {#config-rule}

設定所有資料元素後，您就可以開始建立事件轉發規則，這些規則將確定事件何時以及如何發送到 [!DNL Twitter]。

新建 [規則](../../../ui/managing-resources/rules.md) 在事件轉發屬性中。 下 **[!UICONTROL 操作]**，添加新操作並將擴展設定為 **[!UICONTROL Twitter]**。 將Adobe Experience Edge Network事件發送到 [!DNL Twitter]的子菜單。 **[!UICONTROL 操作類型]** 至 **[!UICONTROL 發送Web轉換]。**

選擇後，將顯示其他控制項以進一步配置事件。 你需要把 [!DNL Twitter] 事件屬性到先前建立的資料元素。 有關詳細資訊，請參閱 [[!DNL Twitter] Web轉換API](https://developer.twitter.com/en/docs/twitter-ads-api/measurement/api-reference/conversions)。

![的 [!DNL Twitter] 建立轉換事件規則。](../../../images/extensions/server/twitter/action-configuration.png)

**[!UICONTROL 用戶標識]**

| 欄位名稱 | 說明 | 範例 | 必填 |
| --- | --- | --- | --- |
| [!UICONTROL [!DNL Twitter] 按一下ID] | [!DNL Twitter] 按一下從點擊URL解析的ID。 | 26l6412g5p4iyj65a2oic2ayg2 | 如果未添加其他標識符，則為必需欄位。 |
| [!UICONTROL 電子郵件] | SHA256的電子郵件地址已散列。 文本必須為小寫，並且在散列前必須刪除任何尾隨空格或前導空格。 | eventforwarding@example.com | 如果未添加其他標識符，則為必需欄位。 |
| [!UICONTROL 電話] | 電話用作標識符以匹配轉換事件。 電話號碼必須採用E164格式[+][國家/地區代碼][區域代碼][local phone number] 之後再散列。 | +911234567875 | 如果未添加其他標識符，則為必需欄位。 |

**[!UICONTROL 轉換資料]**

| 欄位名稱 | 說明 | 範例 | 必填 |
| --- | --- | --- | --- |
| [!UICONTROL 轉換時間] | ISO 8601或yyyy-MM-dd&#39;T&#39;HH中的字串日期 — 時間:mm:ss:SSSZ格式。 | 2022-02-18T01:14:00.603Z | 是 |
| [!UICONTROL 事件ID] | 特定事件的基36 ID。 此ID應與包含在您 [!DNL Twitter] 廣告帳戶。 這稱為事件管理器中相應事件的ID。 | o87ne或tw-o8z6j-o87ne(tw-pixel_id-event-id) | 是 |
| [!UICONTROL 項目數] | 在事件中購買的物料數。 這必須是大於0的正數。 | 4 | 無 |
| [!UICONTROL 貨幣] | 在事件中購買的物料的幣種。 這在ISO-4217中表示，如果未提供，則預設值為USD。 | USD | 無 |
| [!UICONTROL 值] | 在事件中購買的物料的價格值。 | 100.00 | 無 |
| [!UICONTROL 轉換ID] | 轉換事件的標識符，可用於在同一事件標籤中的Web像素和轉換API轉換之間的重複資料消除。 | 23294827 | 無 |
| [!UICONTROL 說明] | 包含有關轉換的任何附加資訊的說明。 | Test轉換 | 無 |

## 驗證資料 [!DNL Twitter]

建立並執行事件轉發規則後，驗證是否將發送到 [!DNL Twitter] API按預期顯示在 [!DNL Twitter] UI。

如果事件集合和 [!DNL Experience Platform] 整合成功，您將看到 [!DNL Twitter] [!UICONTROL 事件管理器]。

![的 [!DNL Twitter] 事件管理器](../../../images/extensions/server/twitter/event-manager.png)

## 後續步驟

本指南介紹如何將轉換事件發送到 [!DNL Twitter] 使用事件轉發。 有關這些基礎技術的詳細資訊，請參閱正式文檔：

* [[!DNL Twitter] API](https://developer.twitter.com/en/docs/twitter-api)
* [[!DNL Twitter] Web轉換API](https://developer.twitter.com/en/docs/twitter-ads-api/measurement/api-reference/conversions)
* [[!DNL Twitter] 用戶訪問令牌](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens)
* [像素ID和轉換跟蹤](https://business.twitter.com/en/help/campaign-measurement-and-analytics/conversion-tracking-for-websites.html)
