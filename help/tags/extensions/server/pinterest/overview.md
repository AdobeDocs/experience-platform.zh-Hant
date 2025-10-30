---
keywords: 事件轉送擴充功能；pinterest；pinterest事件轉送擴充功能
title: Pinterest事件轉送擴充功能
description: 此Adobe Experience Platform事件轉送擴充功能可讓您將事件擷取至Pinterest，以滿足您的業務需求。
last-substantial-update: 2023-04-27T00:00:00Z
exl-id: 44f38a9b-0a28-4b51-bead-ee460eb8405e
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '1427'
ht-degree: 3%

---

# [!DNL Pinterest] 事件轉送擴充功能

[!DNL Pinterest]是視覺探索引擎，可尋找配方、家庭裝飾、風格靈感等概念。 [!DNL Pinterest]上有數十億個釘選，也可與[!DNL Pinterest]上的其他人共用。 您可以整理使用者互動事件並運用[!DNL Pinterest Analytics]來瞭解使用者行為並執行目標式廣告。

[[!DNL Pinterest] 轉換](https://developers.pinterest.com/docs/conversions/conversion-management/) API [事件轉送](../../../ui/event-forwarding/overview.md)擴充功能可讓您運用Adobe Experience Platform Edge Network中擷取的資料，並將其傳送給[!DNL Pinterest]。 本檔案說明擴充功能的使用案例、安裝方式，以及如何將其功能整合至您的事件轉送[規則](../../../ui/managing-resources/rules.md)。

轉換存取權杖是[!DNL Pinterest]與[!DNL Pinterest] API互動時使用的驗證方法。

## 使用案例

如果您想要在[!DNL Pinterest]中使用Edge Network的資料，以善用其客戶分析功能，應使用此擴充功能。

例如，以組織中的行銷團隊為例。 團隊從他們的網站擷取使用者互動事件資料，並使用這個事件轉送擴充功能將其載入到[!DNL Pinterest]中。

行銷與分析團隊可以善用[!DNL Pinterest] Analytics功能來瞭解重要的使用者互動與行為，讓您更瞭解使用者，並針對目標廣告促銷活動鎖定使用者。

如需[!DNL Pinterest]特定使用案例的詳細資訊，請參閱[[!DNL Pinterest] 使用案例](https://business.pinterest.com/en/success-stories)檔案。

## [!DNL Pinterest]必要條件 {#prerequisites}

您必須擁有有效的[!DNL Pinterest] [商業帳戶](https://help.pinterest.com/en/business/article/get-a-business-account)才能使用此延伸模組。 移至[[!DNL Pinterest] 註冊頁面](https://www.pinterest.com/business/create/)進行註冊並建立帳戶（如果尚未建立帳戶）。

您也需要[!DNL Pinterest]開發人員帳戶，該帳戶需要與您的[!DNL Pinterest]企業帳戶相關聯。 若要將您的開發人員帳戶與您的企業帳戶建立關聯，請參閱[[!DNL Pinterest ] 開發人員帳戶](https://developers.pinterest.com/account-setup/)。

### 收集必要的設定詳細資料 {#configuration-details}

若要將Experience Platform連線至[!DNL Pinterest]，需要下列輸入：

| 認證 | 說明 | 範例 |
| --- | --- | --- |
| 廣告帳戶ID | 您的[!DNL Pinterest] Ads帳戶Id。 請參閱[[!DNL Pinterest] 檔案](https://help.pinterest.com/en/business/article/find-ids-in-ads-manager)以取得指引。 | 123456789012 |
| 轉換存取權杖 | 您的[!DNL Pinterest]轉換存取權杖。 請參閱[[!DNL Pinterest] 轉換API](https://developers.pinterest.com/docs/conversions/conversions/#Get%20the%20conversion%20token)檔案以取得指引。<br> **您只需要執行此動作一次，因為此Token並未過期。** | {YOUR_PINTEREST_BEARER_TOKEN} |

## 安裝並設定[!DNL Pinterest]擴充功能 {#install}

若要安裝擴充功能，[請建立事件轉送屬性](../../../ui/event-forwarding/overview.md#properties)，或選擇現有的屬性來編輯。

在左側導覽中，選取&#x200B;**[!UICONTROL Extensions]**。 在&#x200B;**[!UICONTROL Install]**&#x200B;索引標籤中，選取[!DNL Pinterest]擴充功能的卡片上的&#x200B;**[!UICONTROL Catalog]**。

![目錄顯示[!DNL Pinterest]延伸並反白顯示[!UICONTROL Install]。](../../../images/extensions/server/pinterest/install.png)

### 設定 [!DNL Pinterest] 擴充功能

>[!IMPORTANT]
>
>根據您的實作需求，您可能需要先建立結構、資料元素和資料集，才能設定擴充功能。 開始之前，請先檢閱所有設定步驟，以決定您需要為使用案例設定的實體。

在左側導覽中，選取&#x200B;**[!UICONTROL Extensions]**。 在&#x200B;**[!UICONTROL Configure]**&#x200B;索引標籤中，選取[!DNL Pinterest]擴充功能的卡片**[!UICONTROL Installed]。

在![[!DNL Pinterest]標籤中顯示的[!UICONTROL Install]延伸模組已反白顯示[!UICONTROL Configure]。](../../../images/extensions/server/pinterest/configure.png)

在下一個畫面中，輸入您先前在[!UICONTROL Ads Account Id]組態詳細資料[!UICONTROL Conversion Access Token]區段中收集的[和](#configuration-details)。 完成後，選取「**[!UICONTROL Save]**」。

![ [!DNL Pinterest] [!UICONTROL Configure]畫面醒目提示[!UICONTROL Ads Account Id]和[!UICONTROL Conversion Access Token]輸入欄位。](../../../images/extensions/server/pinterest/input.png)

## 設定事件轉送規則 {#config-rule}

設定好所有資料元素後，您就可以開始建立事件轉送規則，以判斷將事件傳送至[!DNL Pinterest]的時間和方式。

在您的事件轉送屬性中建立新的[規則](../../../ui/managing-resources/rules.md)。 在&#x200B;**[!UICONTROL Actions]**&#x200B;底下，新增動作並將擴充功能設為&#x200B;**[!UICONTROL Pinterest]**。 若要將Edge Network事件傳送至[!DNL Pinterest]，請將&#x200B;**[!UICONTROL Action Type]**&#x200B;設為&#x200B;**[!UICONTROL Send Event]。**

![建立[!DNL Pinterest] [!UICONTROL Send Event]規則。](../../../images/extensions/server/pinterest/rule.png)

選取後，會出現其他控制項以進一步設定事件。 您必須將[!DNL Pinterest]事件屬性對應至您先前建立的資料元素。

### [!UICONTROL Event Data]

建立新規則需要下列事件資料：

| 欄位名稱 | 說明 | 範例 |
| --- | --- | --- | 
| [!UICONTROL Event Name] | 使用者事件的型別。 這可以是任何事件型別，但若要利用[!DNL Pinterest Analytics]，建議使用[[!DNL Pinterest] 事件代碼](https://help.pinterest.com/en/business/article/add-event-codes) | &amp;amp；ast；簽出<br> &amp;amp；ast； add_to_cart <br> &amp;amp；ast； page_visit <br> &amp;amp；ast；註冊<br> &amp;amp；ast； [使用者定義的事件] |
| [!UICONTROL Action Source] | 表示轉換事件發生位置的來源。 | &amp;amp；ast； app_android <br> &amp;amp；ast； app_ios <br> &amp;amp；ast；網頁<br> &amp;amp；ast；離線 |
| [!UICONTROL Event Time] | 這是指事件時間。 使用的預設時間格式為UNIX，格式為`<seconds>.<miliseconds>`，視您的當地時區而定。 如需詳細資訊，請參閱[[!DNL Pinterest] API](https://developers.pinterest.com/docs/api/v5/#operation/events/create)。 | 1433188255.500表示2015年6月1日星期一晚上7:50:55 GMT時新紀元後的1433188255秒和500毫秒。 |
| [!UICONTROL Event ID] | 此唯一ID字串可識別此事件，並可用於透過轉換API和Pinterest追蹤所擷取事件之間的重複資料刪除。 若沒有此專案，事件的資料可能會重複計算，並回報量度膨脹。 | ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad |
| [!UICONTROL Event Properties] | 包含事件自訂屬性的JSON物件。 從提供原始JSON或使用簡化的鍵值輸入集進行選取。 | { &quot;event_source_url&quot;： &quot;http://site.com&quot; } |

![規則動作中反白顯示的[!DNL Pinterest] [!UICONTROL Event Data]。](../../../images/extensions/server/pinterest/event-data.png)

可以設定下列事件屬性：

| 欄位名稱 | 說明 |
| --- | --- |
| 事件Source URL | 網頁轉換事件的URL。 |
| 應用程式商店ID | 應用程式商店應用程式ID。 |
| 應用程式名稱 | 應用程式的名稱。 |
| Application Version | 應用程式的版本。 |
| 裝置品牌 | 使用者正在使用的裝置品牌。 |
| 裝置載體 | 使用者裝置的行動電信業者。 |
| 裝置型號 | 使用者裝置的型號。 |
| 裝置類型 | 使用者使用的裝置型別。 |
| 作業系統版本 | 裝置的作業系統版本。 |
| 使用者語言 | 表示使用者語言的雙字元ISO-639-1語言代碼。 |

### [!UICONTROL User Data]

下列使用者資料可由輸入，並非必填欄位：

| 欄位名稱 | 說明 | 範例 |
| --- | --- | --- | 
| [!UICONTROL Email] | 使用者電子郵件地址或使用者地址電子郵件的SHA256雜湊。 | ebd543592...f2b7e1 |
| [!UICONTROL Mobile Adverstising IDs] | 使用者的「Google Advertising ID」(GAID)或「Apple的廣告商識別碼」(IDFA)的Sha256雜湊 | ebd543592...f2b7e1 |
| [!UICONTROL Client IP Address] | 使用者的IP位址，可以是IPv4或IPv6格式。 用於比對。 | 192.168.0.1 |
| [!UICONTROL Client User Agent] | 使用者網頁瀏覽器的使用者代理字串。 | Mozilla/5.0 （平台；rv:geckoversion） Gecko/geckotrail Firefox/firefoxversion |
| [!UICONTROL Customer information data] | 包含其他客戶資訊的JSON物件。 從提供原始JSON或使用簡化的鍵值輸入集進行選取。 | { &quot;ph&quot;： &quot;122333445&quot; } |

![規則動作中反白顯示的[!DNL Pinterest] [!UICONTROL User Data]。](../../../images/extensions/server/pinterest/user-data.png)

可設定的客戶資訊屬性包括：

| 欄位名稱 | 說明 |
| --- | --- |
| 電話 | 使用者聯絡電話。 只接受數字，並且應輸入國碼、區碼和數字。 |
| 性別 | 性別可以輸入為「f」代表女性、「m」代表男性，或「n」代表非二進位。 |
| 出生日期 | 以年、月、日形式輸入的出生日期。 |
| 姓氏 | 使用者的姓氏。 |
| 名字 | 使用者的名字。 |
| 城市 | 使用者的居住城市。 這主要用於計費目的。 |
| 狀態 | 使用者的狀態，以小寫形式的雙字母程式碼提供。 |
| 郵遞區號 | 使用者的拉鍊碼，主要用於計費用途。 |
| 國家/地區 | 表示使用者國家/地區的雙字元ISO-3166國家/地區代碼。 |
| 外部 ID | 來自廣告商的唯一ID，可識別其空間中的使用者。 例如，使用者ID、忠誠度ID等。 |
| 點按ID | 儲存在網域上_epik Cookie或URL中&amp;epik=查詢引數中的唯一識別碼。 |

>[!IMPORTANT]
>
>在傳送資料至[!DNL Pinterest] API端點之前，擴充功能會雜湊並標準化下列欄位的值：電子郵件、電話號碼、名字、姓氏、性別、出生日期、城市、州、郵遞區號、國家/地區及外部ID。 如果SHA256字串已存在，擴充功能就不會雜湊這些欄位的值。

### [!UICONTROL Custom Data]

您可以為規則輸入下列自訂資料：

| 欄位名稱 | 說明 |
| --- | --- |
| 貨幣 | ISO-4217貨幣代碼。 如果未提供，[!DNL Pinterest]將預設為廣告商在建立帳戶期間所設定的貨幣。 |
| 價值 | 事件的總值。 已接受為請求中的字串。 這將會剖析為兩位數。 |
| 搜尋字串 | 與使用者轉換事件相關的搜尋字串。 |
| 訂單ID | 訂單ID。 傳送`order_id`可協助[!DNL Pinterest]在必要時刪除重複事件。 |
| 產品數量 | 事件的產品總數。 例如，結帳事件中購買的專案總數。 |
| 內容ID | 產品ID清單（陣列）。 |
| 內容 | 包含產品相關資訊（例如價格和數量）的物件清單（陣列）。 |

![規則動作中反白顯示的[!DNL Pinterest] [!UICONTROL Custom Data]。](../../../images/extensions/server/pinterest/custom-data.png)

## 驗證[!DNL Pinterest]中的資料

建立並執行事件轉送規則後，請驗證傳送至[!DNL Pinterest] API的事件是否如預期般顯示在[!DNL Pinterest] UI中。

如果事件集合和[!DNL Experience Platform]整合成功，您將會在[!DNL Pinterest] UI中看到事件。

![ [!DNL Pinterest]事件管理員](../../../images/extensions/server/pinterest/event-history.png)

您可以進一步鑽研並檢視[!DNL Pinterest]事件資料分佈。

![ [!DNL Pinterest]資料分佈](../../../images/extensions/server/pinterest/event-history-distribution.png)

## 後續步驟

本指南說明如何在UI中安裝和設定[!DNL Pinterest]事件轉送擴充功能。 如需詳細資訊，請參閱正式檔案：

* [[!DNL Pinterest] API](https://developers.pinterest.com/docs/api/v5/)
* [[!DNL Pinterest] 轉換API總覽](https://help.pinterest.com/en/business/article/the-pinterest-api-for-conversions)
