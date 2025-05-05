---
keywords: 事件轉送擴充功能；twitter；twitter事件轉送擴充功能
title: twitter事件轉送擴充功能
description: 此Adobe Experience Platform事件轉送擴充功能可讓您將事件擷取至Twitter中，以滿足您的業務需求。
last-substantial-update: 2023-05-24T00:00:00Z
exl-id: 54c240e5-6160-4654-ac5b-6afa8d99a765
source-git-commit: 4ee895cb8371646fd2013e2a8f65c2ffdae95850
workflow-type: tm+mt
source-wordcount: '1048'
ht-degree: 3%

---

# [!DNL Twitter] 事件轉送擴充功能

[[!DNL Twitter]](https://twitter.com/i/flow/login)是線上社群媒體和社交網路服務，使用者可在該服務上張貼及互動280個字元的訊息（稱為推文）。 使用者可以使用瀏覽器、行動前端軟體，或透過其[API](https://developer.twitter.com/en/docs/twitter-api)以程式設計方式與Twitter互動

[!DNL Twitter] Web Conversions API [事件轉送](../../../ui/event-forwarding/overview.md)擴充功能可讓您運用Adobe Experience PlatformEdge Network中擷取的資料，並將其傳送給[!DNL Twitter]。 本檔案說明擴充功能的使用案例、安裝方式，以及如何將其功能整合至您的事件轉送[規則](../../../ui/managing-resources/rules.md)。

[!DNL Twitter]需要[OAuth 1.0](https://developer.twitter.com/en/docs/authentication/oauth-1-0a)才能使用[!DNL Twitter] [!DNL Web Conversions] API進行驗證。

## 使用案例

如果您想要使用[!DNL Twitter]中Edge Network的資料，以利用其客戶分析和目標定位功能，應使用此擴充功能。

例如，以組織中的行銷團隊為例。 團隊從他們的網站擷取使用者互動事件資料，做為他們網站的事件資料，並使用這個事件轉送擴充功能將其載入到[!DNL Twitter]中。

行銷與分析團隊接著可運用[!DNL Twitter's]功能執行其他分析，並將目標鎖定於這些使用者，以進行目標定位的廣告行銷活動。

如需[!DNL Twitter]特定使用案例的詳細資訊，請參閱[[!DNL Twitter] 使用案例](https://developer.twitter.com/en/use-cases/build-for-businesses)檔案。

## [!DNL Twitter]先決條件和護欄 {#prerequisites}

您必須擁有有效的[!DNL Twitter]帳戶才能使用此擴充功能。 移至[[!DNL Twitter] 註冊頁面](https://help.twitter.com/en/using-twitter/create-twitter-account)進行註冊並建立帳戶（如果尚未建立帳戶）。

您必須將您的帳戶設定為[!DNL Twitter]開發人員帳戶。 若要瞭解如何註冊為開發人員，請參閱[[!DNL Twitter] 開發人員帳戶](https://developer.twitter.com/en/support/twitter-api/developer-account1)。

### API護欄 {#guardrails}

[!DNL Twitter] Web Conversions API具有每15分鐘間隔60,000個要求的速率限制，其中每個要求允許500個事件。

### 收集必要的設定詳細資料 {#configuration-details}

若要將Experience Platform連線到[!DNL Twitter]，需要下列輸入：

| 金鑰型別 | 說明 |
| --- | --- |
| 使用者金鑰 | 用&#x200B;於存取[!DNL Twitter] API的應用程式API金鑰。 如需指引，請參閱[API金鑰和秘密](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/api-key-and-secret)上的[!DNL Twitter]檔案。 | |
| 使用者密碼 | API密碼可讓您的應用程式存取[!DNL Twitter] API。 如需指引，請參閱[API金鑰和秘密](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/api-key-and-secret)上的[!DNL Twitter]檔案。 |
| 權杖密碼 | 您應用程式的不到期權杖密碼，用於透過OAuth驗證[!DNL Twitter] API。 如需指引，請參閱有關[取得使用存取權杖](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens)的[!DNL Twitter]檔案。 |
| 存取權杖 | 您應用程式不會到期的存取權杖，用於透過OAuth驗證[!DNL Twitter] API。 如需指引，請參閱有關[取得使用存取權杖](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens)的[!DNL Twitter]檔案。 |
| 畫素ID | [!DNL Twitter] Pixel是在您的網站上實作的網站標籤，用來追蹤網站動作或轉換。 如需指引，請參閱有關網站[&#128279;](https://business.twitter.com/en/help/campaign-measurement-and-analytics/conversion-tracking-for-websites.html)的轉換追蹤的[!DNL Twitter]檔案。 |

## 安裝並設定[!DNL Twitter]擴充功能 {#install}

若要安裝擴充功能，[請建立事件轉送屬性](../../../ui/event-forwarding/overview.md#properties)，或選擇現有的屬性來編輯。

在左側導覽中選取&#x200B;**[!UICONTROL 擴充功能]**。 在&#x200B;**[!UICONTROL 目錄]**&#x200B;標籤中，選取[!DNL Twitter]擴充功能的卡片上的&#x200B;**[!UICONTROL 安裝]**。

![目錄顯示[!DNL Twitter]擴充功能醒目提示安裝。](../../../images/extensions/server/twitter/install.png)

>[!IMPORTANT]
>
>根據您的實作需求，您可能需要先建立結構、資料元素和資料集，才能設定擴充功能。 開始之前，請先檢閱所有設定步驟，以決定您需要為使用案例設定的實體。

在下一個畫面中，輸入您先前從[!DNL Twitter]收集的下列[組態值](#configuration-details)：

* **[!UICONTROL 畫素識別碼]**
* **[!UICONTROL 消費者金鑰]**
* **[!UICONTROL 使用者密碼]**
* **[!UICONTROL Token]**
* **[!UICONTROL 權杖密碼]**

完成後，選取&#x200B;**[!UICONTROL 儲存]**。

[!DNL Twitter]擴充功能的![[!DNL Twitter]設定畫面。](../../../images/extensions/server/twitter/configure.png)

## 設定事件轉送規則 {#config-rule}

設定好所有資料元素後，您就可以開始建立事件轉送規則，以判斷將事件傳送至[!DNL Twitter]的時間和方式。

在您的事件轉送屬性中建立新的[規則](../../../ui/managing-resources/rules.md)。 在&#x200B;**[!UICONTROL 動作]**&#x200B;底下，新增動作並將擴充功能設為&#x200B;**[!UICONTROL Twitter]**。 若要將Edge Network事件傳送至[!DNL Twitter]，請將&#x200B;**[!UICONTROL 動作型別]**&#x200B;設定為&#x200B;**[!UICONTROL 傳送Web轉換]。**

選取後，會出現其他控制項以進一步設定事件。 您必須將[!DNL Twitter]事件屬性對應至您先前建立的資料元素。 如需詳細資訊，請參閱[[!DNL Twitter] 網頁轉換API](https://developer.twitter.com/en/docs/twitter-ads-api/measurement/api-reference/conversions)。

![建立轉換事件規則的[!DNL Twitter]。](../../../images/extensions/server/twitter/action-configuration.png)

**[!UICONTROL 使用者識別]**

| 欄位名稱 | 說明 | 範例 | 必要 |
| --- | --- | --- | --- |
| [!UICONTROL [!DNL Twitter]點按識別碼] | [!DNL Twitter]從點進URL剖析的點選ID。 | 26l6412g5p4iyj65a2oic2ayg2 | 如果未新增其他識別碼，則為必要。 |
| [!UICONTROL 電子郵件] | 使用SHA256雜湊的電子郵件地址。 文字必須為小寫，且必須在雜湊前移除任何結尾或前導空格。 | eventforwarding@example.com | 如果未新增其他識別碼，則為必要。 |
| [!UICONTROL 電話] | 電話會作為識別碼使用，以符合轉換事件。 在雜湊之前，電話號碼必須是E164格式[+][國家代碼][區號][local phone number]。 | +911234567875 | 如果未新增其他識別碼，則為必要。 |

**[!UICONTROL 轉換資料]**

| 欄位名稱 | 說明 | 範例 | 必要 |
| --- | --- | --- | --- |
| [!UICONTROL 轉換時間] | 以ISO 8601或`yyyy-MM-dd'T'HH:mm:ss:SSSZ`格式作為字串的日期時間。 | 2022-02-18T01:14:00.603Z | 是 |
| [!UICONTROL 事件識別碼] | 特定事件的基底36 ID。 此ID應符合您[!DNL Twitter]廣告帳戶中包含的預先設定事件。 這稱為「事件管理員」中對應事件的ID。 | o87ne或tw-o8z6j-o87ne (tw-pixel_id-event-id) | 是 |
| [!UICONTROL 專案數] | 在事件中購買的專案數。 這必須是大於0的正數。 | 4 | 無 |
| [!UICONTROL 貨幣] | 事件中購買專案的貨幣。 這以ISO-4217表示，若未提供，預設為USD。 | 美元 | 無 |
| [!UICONTROL 值] | 在事件中購買之專案的價格值。 | 100.00 | 無 |
| [!UICONTROL 轉換ID] | 轉換事件的識別碼，可用於相同事件標籤中，Web畫素和轉換API轉換之間的重複資料刪除。 | 23294827 | 無 |
| [!UICONTROL 說明] | 轉換的說明及任何其他資訊。 | 測試轉換 | 無 |

## 驗證[!DNL Twitter]中的資料

建立並執行事件轉送規則後，請驗證傳送至[!DNL Twitter] API的事件是否如預期般顯示在[!DNL Twitter] UI中。

如果事件集合與[!DNL Experience Platform]整合成功，您將會在[!DNL Twitter] [!UICONTROL 事件管理員]中看到事件。

![ [!DNL Twitter]事件管理員](../../../images/extensions/server/twitter/event-manager.png)

## 後續步驟

本指南說明如何使用事件轉送將轉換事件傳送至[!DNL Twitter]。 如需這些基礎技術的詳細資訊，請參閱正式檔案：

* [[!DNL Twitter] API](https://developer.twitter.com/en/docs/twitter-api)
* [[!DNL Twitter] 網頁轉換API](https://developer.twitter.com/en/docs/twitter-ads-api/measurement/api-reference/conversions)
* [[!DNL Twitter] 使用者存取權杖](https://developer.twitter.com/en/docs/authentication/oauth-1-0a/obtaining-user-access-tokens)
* [畫素ID和轉換追蹤](https://business.twitter.com/en/help/campaign-measurement-and-analytics/conversion-tracking-for-websites.html)
