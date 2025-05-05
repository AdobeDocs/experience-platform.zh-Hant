---
title: Adobe Amazon Conversions API擴充功能
description: 此Adobe Experience Platform網頁事件API可讓您直接與Amazon共用網站互動。
last-substantial-update: 2025-04-17T00:00:00Z
source-git-commit: 65a3eb20dc3de62319f73be49197dacb8fc1778b
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 1%

---

# [!DNL Amazon]網站事件API擴充功能總覽

[!DNL Amazon] Conversions API擴充功能會在來自廣告商伺服器的行銷資料與[!DNL Amazon]之間建立直接連線。 如此一來，廣告商就能評估促銷活動的成效，而無論轉換地點為何，並據此將促銷活動最佳化。 此擴充功能提供更完整的歸因、改善的資料可靠性，以及更理想的傳送方式。

## [!DNL Amazon]必要條件 {#prerequisites}

在安裝及設定[!DNL Amazon] Conversions API擴充功能之前，您必須完成數個先決條件步驟，以確保正確驗證及資料存取。

### 建立機密和資料元素 {#secret}

使用[!DNL Amazon]進行驗證需要安全權杖，必須正確儲存並參照：

1. 以唯一名稱建立新的[!DNL Amazon]事件轉寄密碼以進行驗證。
2. 使用包含&#x200B;**機密**&#x200B;資料元素型別的&#x200B;**核心**&#x200B;延伸來建立資料元素，以參考您的[!DNL Amazon]機密。

此程式可確保您的驗證憑證安全無虞，同時仍可於需要時供擴充功能存取。

## 安裝並設定[!DNL Amazon]擴充功能

安裝擴充功能需要存取Experience Platform中的事件轉送屬性：

- 建立或編輯事件轉送屬性。
- 在左側導覽中選取&#x200B;**擴充功能**，然後在[目錄]索引標籤中選取[!DNL Amazon]擴充功能。
- 選取&#x200B;**安裝**。

在擴充功能目錄中選取![[!DNL Amazon]擴充功能以及安裝按鈕。](../../../images/extensions/server/amazon/amazon-extension.png)

- 設定方式：

- **存取Token**：包含OAuth 2 Token的資料元素密碼

![要輸入資料元素密碼的個別設定會反白顯示。](../../../images/extensions/server/amazon/2.png)

- **實體ID**：您的實體ID （可在Campaign Manager入口網站URL中找到，首碼為&quot;entity&quot;）

![左側導覽中的行銷活動管理員入口網站。](../../../images/extensions/server/amazon/3.png)

- 選取「**儲存**」。

這些設定值會建立Platform與您的[!DNL Amazon]帳戶之間的連線。

### [!DNL Amazon] OAuth 2 {#oauth}

若要建立[!DNL Amazon] OAuth 2密碼：

- 從&#x200B;**型別**&#x200B;下拉式清單中選取[!DNL Amazon] OAuth 2，然後選取&#x200B;**建立密碼**。

在下拉式功能表中![Amazon OAuth 2。](../../../images/extensions/server/amazon/Oauth.png)

- 在彈出視窗上選取「**使用Amazon建立並授權密碼**」，以手動授權密碼並繼續。

![選取Amazon以建立並授權密碼。](../../../images/extensions/server/amazon/Oauth.1.png)

- 在出現的對話方塊中輸入您的[!DNL Amazon]認證。 依照提示操作，授予資料的事件轉送存取權。

完成後，您將在&#x200B;**密碼**&#x200B;索引標籤中看到密碼及其狀態和到期日期。

![在[密碼]索引標籤中建立的密碼。](../../../images/extensions/server/amazon/Oauth.2.png)

## 設定事件轉送規則 {#config-rule}

設定好所有資料元素後，您就可以建立事件轉送規則，以判斷將事件傳送至Amazon的時間和方式。

- 導覽至&#x200B;**規則**&#x200B;並建立新的事件轉送規則。
- 在&#x200B;**動作**&#x200B;底下，選取&#x200B;**Amazon Conversions API Extension**。
- 將&#x200B;**動作型別**&#x200B;設定為&#x200B;**匯入轉換事件**。

![反白的動作設定選項。](../../../images/extensions/server/amazon/4.png)

- 設定事件屬性，如下所示：

| 輸入 | 說明 |
| --- | --- |
| **事件名稱** | 轉換事件的名稱。 |
| **事件類型** | 定義追蹤的事件型別（例如，購買、購物車新增）。 |
| **時間戳記** | ISO格式的事件時間。 |
| **使用者端重複資料刪除識別碼** | 重複資料刪除的唯一ID。 |
| **比對索引鍵** | 歸因的使用者和裝置識別碼。 |
| **值** | 事件的貨幣值。 |
| **貨幣代碼** | ISO-4217格式的貨幣。 |
| **已售出件數** | 購買的專案數量。 |
| **國家/地區代碼** | 事件發生的國家/地區。 |
| **資料處理選項** | 標幟有限的資料使用。 |
| **同意** | 表示廣告資料使用的使用者同意。 |

- 選取&#x200B;**保留變更**&#x200B;以儲存規則。

![動作組態中的事件引數與[保留變更]按鈕一起反白顯示。](../../../images/extensions/server/amazon/5.png)

![動作設定中的其他事件引數會與保留變更按鈕一起反白顯示。](../../../images/extensions/server/amazon/6.png)

## 事件重複資料刪除 {#deduplication}

如果您針對相同事件同時使用[!DNL Amazon] Advertising Tag (AAT)和[!DNL Amazon] Conversions API擴充功能，則需要重複資料刪除設定。 在每個共用事件中包含`clientDedupeId`，以確保正確重複資料刪除。
如果使用者端和伺服器事件不重疊，則不需要重複資料刪除。

適當的重複資料刪除可避免轉換計數膨脹，並確保最佳化資料保持準確。

如需詳細資訊，請參閱[Amazon事件重複資料刪除指南](https://advertising.amazon.com/)。

## 後續步驟

本指南說明如何使用[!DNL Amazon] Conversions API擴充功能來設定轉換事件並傳送給[!DNL Amazon]。 如需[!DNL Adobe Experience Platform]中事件轉送功能的詳細資訊，請參閱[事件轉送概觀](../../../ui/event-forwarding/overview.md)

如需使用Experience Platform Debugger和「事件轉送監視」工具對實作除錯的詳細資訊，請閱讀[Adobe Experience Platform Debugger概觀](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/debugger/home)和[事件轉送中的監視活動](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/tags/event-forwarding/monitoring)。