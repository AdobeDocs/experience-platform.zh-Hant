---
keywords: 事件轉送擴充功能；pinterest;pinterest事件轉送擴充功能
title: Pinterest事件轉送擴充功能
description: 此Adobe Experience Platform事件轉送擴充功能可讓您根據業務需求將事件內嵌至Pinterest。
last-substantial-update: 2023-04-27T00:00:00Z
source-git-commit: 87c76ef4b95bc05a64d9d124d69c2a51b7b77c08
workflow-type: tm+mt
source-wordcount: '1550'
ht-degree: 4%

---

# [!DNL Pinterest] 事件轉送擴充功能

[!DNL Pinterest] 是視覺探索引擎，可尋找食譜、家居裝飾、風格靈感等概念。 上面有數十億個針 [!DNL Pinterest]，也可在 [!DNL Pinterest]. 您可以整理使用者互動事件並運用 [!DNL Pinterest Analytics] 了解使用者行為並執行目標廣告。

此 [[!DNL Pinterest] 轉換](https://developers.pinterest.com/docs/conversions/conversion-management/) API [事件轉送](../../../ui/event-forwarding/overview.md) 擴充功能可讓您運用Adobe Experience Platform邊緣網路中擷取的資料，並將其傳送至 [!DNL Pinterest]. 本檔案說明擴充功能的使用案例、如何安裝，以及如何將其功能整合至事件轉送 [規則](../../../ui/managing-resources/rules.md).

轉換存取權杖是使用的驗證方法 [!DNL Pinterest] 與 [!DNL Pinterest] API。

## 使用案例

如果您想要使用來自邊緣網路的資料，應使用此擴充功能。 [!DNL Pinterest] 以善用其客戶分析功能。

例如，假設組織中有行銷團隊。 團隊會從其網站擷取使用者互動事件資料，並將其載入 [!DNL Pinterest] 使用此事件轉送擴充功能。

行銷和分析團隊便可運用 [!DNL Pinterest] Analytics功能，可了解關鍵使用者互動和行為，讓您更清楚了解使用者，並針對目標廣告促銷活動鎖定他們。

如需特定使用案例的詳細資訊，請參閱 [!DNL Pinterest]，請參閱 [[!DNL Pinterest] 使用案例](https://business.pinterest.com/en/success-stories) 檔案。

## [!DNL Pinterest] 必要條件 {#prerequisites}

您必須具備有效 [!DNL Pinterest] [業務帳戶](https://help.pinterest.com/en/business/article/get-a-business-account) 才能使用此擴充功能。 前往 [[!DNL Pinterest] 註冊頁面](https://www.pinterest.com/business/create/) 註冊並建立帳戶（如果尚未註冊）。

您還需要 [!DNL Pinterest] 開發人員帳戶，此帳戶需要與 [!DNL Pinterest] 商業帳戶。 若要將您的開發人員帳戶與您的商業帳戶建立關聯，請參閱 [[!DNL Pinterest ] 開發人員帳戶](https://developers.pinterest.com/account-setup/).

### 收集所需配置詳細資訊 {#configuration-details}

將Experience Platform連結至 [!DNL Pinterest]，需要下列輸入：

| 憑據 | 說明 | 範例 |
| --- | --- | --- |
| Ads帳戶Id | 您的 [!DNL Pinterest] 廣告帳戶Id。 請參閱 [[!DNL Pinterest] 檔案](https://help.pinterest.com/en/business/article/find-ids-in-ads-manager) 以取得指引。 | 123456789012 |
| 轉換存取權杖 | 您的 [!DNL Pinterest] 轉換存取權杖。 請參閱 [[!DNL Pinterest] 轉換API](https://developers.pinterest.com/docs/conversions/conversions/#Get%20the%20conversion%20token) 指導檔案。 <br> **由於此代號不會過期，您只需執行一次。** | {YOUR_PINTEREST_BEARER_TOKEN} |

## 安裝並設定 [!DNL Pinterest] 擴充功能 {#install}

若要安裝擴充功能， [建立事件轉送屬性](../../../ui/event-forwarding/overview.md#properties) 或選擇要編輯的現有屬性。

在左側導覽中，選取 **[!UICONTROL 擴充功能]**. 選擇 **[!UICONTROL 安裝]** 在 [!DNL Pinterest] 擴充功能 **[!UICONTROL 目錄]** 標籤。

![顯示 [!DNL Pinterest] 擴充功能 [!UICONTROL 安裝] 突出顯示。](../../../images/extensions/server/pinterest/install.png)

### 設定 [!DNL Pinterest] 擴充功能

>[!IMPORTANT]
>
>視您的實作需求而定，在設定擴充功能之前，您可能需要先建立結構、資料元素和資料集。 開始之前，請先檢閱所有設定步驟，以判斷您需要針對使用案例設定哪些實體。

在左側導覽中，選取 **[!UICONTROL 擴充功能]**. 選擇 **[!UICONTROL 設定]** 在 [!DNL Pinterest] 擴充功能 [!UICONTROL 已安裝]**標籤。

![[!DNL Pinterest] 擴充功能中顯示 [!UICONTROL 安裝] 標籤 [!UICONTROL 設定] 突出顯示。](../../../images/extensions/server/pinterest/configure.png)

在下一個畫面中，輸入 [!UICONTROL Ads帳戶Id] 和 [!UICONTROL 轉換存取權杖] 之前收集於 [設定詳細資訊](#configuration-details) 區段。 完成後，請選擇 **[!UICONTROL 儲存]**.

![此 [!DNL Pinterest] [!UICONTROL 設定] 螢幕突出顯示 [!UICONTROL Ads帳戶Id] 和 [!UICONTROL 轉換存取權杖] 輸入欄位。](../../../images/extensions/server/pinterest/input.png)

## 設定事件轉送規則 {#config-rule}

設定好所有資料元素後，您就可以開始建立事件轉送規則，以決定事件的傳送時間和方式 [!DNL Pinterest].

建立新 [規則](../../../ui/managing-resources/rules.md) 在事件轉送屬性中。 在 **[!UICONTROL 動作]**，新增動作並將擴充功能設為 **[!UICONTROL Pinterest]**. 若要將Adobe Experience Edge Network事件傳送至 [!DNL Pinterest]，請設定 **[!UICONTROL 動作類型]** to **[!UICONTROL 傳送事件].**

![此 [!DNL Pinterest] [!UICONTROL 傳送事件] 規則建立。](../../../images/extensions/server/pinterest/rule.png)

選取後，會出現其他控制項以進一步設定事件。 您需要對應 [!DNL Pinterest] 事件屬性至您先前建立的資料元素。

### [!UICONTROL 事件資料]

建立新規則需要下列事件資料：

| 欄位名稱 | 說明 | 範例 |
| --- | --- | --- | 
| [!UICONTROL 活動名稱] | 使用者事件的類型。 不過，這可以是任何事件類型，以利用 [!DNL Pinterest Analytics] 建議使用 [[!DNL Pinterest] 事件代碼](https://help.pinterest.com/en/business/article/add-event-codes) | *結帳 <br> * add_to_cart <br> * page_visit <br> *註冊 <br> * [使用者定義的事件] |
| [!UICONTROL 動作來源] | 指出轉換事件發生位置的來源。 | * app_android <br> * app_ios <br> * web <br> *離線 |
| [!UICONTROL 事件時間] | 這是指事件時間。 使用的預設時間格式為UNIX，格式為 `<seconds>.<miliseconds>` 取決於您的當地時區。 如需詳細資訊，請參閱 [[!DNL Pinterest] API](https://developers.pinterest.com/docs/api/v5/#operation/events/create). | 1433188255.500表示Epoch之後的1433188255秒和500毫秒，或2015年6月1日星期一，為7:50:55 PM GMT。 |
| [!UICONTROL 事件ID] | 識別此事件的唯一ID字串，可用於透過轉換API和Pinterest追蹤擷取的事件之間的去重複化。 若未這麼做，事件的資料可能會重複計算，並回報量度膨脹。 | ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad |
| [!UICONTROL 事件屬性] | 包含事件自訂屬性的JSON物件。 從提供原始JSON或使用簡化的鍵值輸入集進行選取。 | { &quot;event_source_url&quot;:&quot;http://site.com&quot; } |

![此 [!DNL Pinterest] [!UICONTROL 事件資料] 在規則動作中強調顯示。](../../../images/extensions/server/pinterest/event-data.png)

可以配置以下事件屬性：

| 欄位名稱 | 說明 |
| --- | --- |
| 事件來源URL | Web轉換事件的URL。 |
| 應用程式儲存ID | 應用程式商店應用程式ID。 |
| 應用程式名稱 | 應用程式的名稱。 |
| Application Version | 應用程式的版本。 |
| 裝置品牌 | 使用者使用的裝置品牌。 |
| 裝置載體 | 使用者裝置的行動電信業者。 |
| 裝置型號 | 使用者裝置的型號。 |
| 裝置類型 | 使用者使用的裝置類型。 |
| OS版本 | 裝置的作業系統版本。 |
| 使用者語言 | 表示用戶語言的雙字元ISO-639-1語言代碼。 |

### [!UICONTROL 使用者資料]

可以輸入以下非必填欄位的使用者資料：

| 欄位名稱 | 說明 | 範例 |
| --- | --- | --- | 
| [!UICONTROL 電子郵件] | 使用者電子郵件地址或使用者地址電子郵件的SHA256雜湊。 | ebd543592...f2b7e1 |
| [!UICONTROL 行動廣告ID] | 使用者的「Google Advertising ID」(GAID)或「Apple Indifiers for Advertisers」(IDFA)的Sha256雜湊 | ebd543592...f2b7e1 |
| [!UICONTROL 客戶端IP地址] | 用戶的IP地址，可以是IPv4或IPv6格式。 用於比對。 | 192.168.0.1 |
| [!UICONTROL 用戶端使用者代理] | 使用者網頁瀏覽器的使用者代理字串。 | Mozilla/5.0(平台；rv:geckoversion)Gecko/geckotrail Firefox/firefoxversion |
| [!UICONTROL 客戶資訊資料] | 包含其他客戶資訊的JSON物件。 從提供原始JSON或使用簡化的鍵值輸入集進行選取。 | { &quot;ph&quot;:&quot;122333445&quot; } |

![此 [!DNL Pinterest] [!UICONTROL 使用者資料] 在規則動作中強調顯示。](../../../images/extensions/server/pinterest/user-data.png)

可設定的客戶資訊屬性包括：

| 欄位名稱 | 說明 |
| --- | --- |
| 電話 | 用戶聯繫電話。 僅接受數字，應使用國家/地區代碼、區號和數字輸入。 |
| 性別 | 性別可以輸入為「f」（女性）、「m」（男性）或「n」（非二進位）。 |
| 出生日期 | 出生日期，以年、月和日輸入。 |
| 「姓氏」 | 用戶的姓氏。 |
| 「名字」 | 使用者的名字。 |
| 城市 | 用戶居住城。 這主要用於帳單用途。 |
| 狀態 | 使用者的狀態，以小寫的雙字母代碼提供。 |
| 郵遞區號 | 使用者的zipcode，主要用於計費用途。 |
| 國家/地區 | 兩個字元的ISO-3166國家/地區代碼，用於表示使用者的國家/地區。 |
| 外部ID | 來自廣告商的唯一ID，可在其空間中識別使用者。 例如，使用者ID、忠誠度ID等。 |
| 按一下ID | 儲存在網域的_epik Cookie中或URL中的&amp;epik=查詢參數中的唯一識別碼。 |

>[!IMPORTANT]
>
>將資料傳送至 [!DNL Pinterest] API端點，擴充功能會雜湊並標準化下列欄位的值：電子郵件、電話號碼、名字、姓氏、性別、出生日期、城市、州、郵遞區號、國家/地區和外部ID。 如果已存在SHA256字串，擴充功能不會雜湊這些欄位的值。

### [!UICONTROL 自訂資料]

可為規則輸入下列自訂資料：

| 欄位名稱 | 說明 |
| --- | --- |
| 貨幣 | ISO-4217貨幣代碼。 若未提供， [!DNL Pinterest] 將預設為在帳戶建立期間設定的廣告商貨幣。 |
| 值 | 事件的總值。 在要求中接受為字串。 這會剖析為兩位數。 |
| 搜尋字串 | 與使用者轉換事件相關的搜尋字串。 |
| 訂購 ID | 訂單ID。 傳送 `order_id` 將提供幫助 [!DNL Pinterest] 視需要刪除重複事件。 |
| 產品數量 | 事件的產品總數。 例如，在結帳事件中購買的項目總數。 |
| 內容ID | 產品ID的清單（陣列）。 |
| 內容 | 包含產品相關資訊（如價格和數量）的對象清單（陣列）。 |

![此 [!DNL Pinterest] [!UICONTROL 自訂資料] 在規則動作中強調顯示。](../../../images/extensions/server/pinterest/custom-data.png)

## 在內驗證資料 [!DNL Pinterest]

建立並執行事件轉送規則後，驗證是否已將事件傳送至 [!DNL Pinterest] API會如預期顯示在 [!DNL Pinterest] UI。

如果事件集合和 [!DNL Experience Platform] 整合成功，您會在中看到事件 [!DNL Pinterest] UI。

![此 [!DNL Pinterest] 事件管理員](../../../images/extensions/server/pinterest/event-history.png)

您可以進一步穿透鑽取並查看 [!DNL Pinterest] 事件資料分送。

![此 [!DNL Pinterest] 資料分佈](../../../images/extensions/server/pinterest/event-history-distribution.png)

## 後續步驟

本指南說明如何安裝和設定 [!DNL Pinterest] 事件轉送UI中的擴充功能。 如需詳細資訊，請參閱官方檔案：

* [[!DNL Pinterest] API](https://developers.pinterest.com/docs/api/v5/)
* [[!DNL Pinterest] 轉換API概觀](https://help.pinterest.com/en/business/article/the-pinterest-api-for-conversions)
