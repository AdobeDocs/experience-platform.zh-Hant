---
keywords: 事件轉發擴展；pinterest;pinterest事件轉發擴展
title: Pinterest事件轉發擴展
description: 此Adobe Experience Platform事件轉發擴展允許您根據業務需要將事件接收到Pinterest。
last-substantial-update: 2023-04-27T00:00:00Z
source-git-commit: 87c76ef4b95bc05a64d9d124d69c2a51b7b77c08
workflow-type: tm+mt
source-wordcount: '1550'
ht-degree: 4%

---

# [!DNL Pinterest] 事件轉發擴展

[!DNL Pinterest] 是一個視覺發現引擎，用於發現食譜、家居裝飾、風格靈感等等。 上面有幾十億個針 [!DNL Pinterest]，也可以與其他人共用 [!DNL Pinterest]。 您可以整理用戶交互事件並利用 [!DNL Pinterest Analytics] 瞭解用戶行為並運行目標播發。

的 [[!DNL Pinterest] 轉換](https://developers.pinterest.com/docs/conversions/conversion-management/) API [事件轉發](../../../ui/event-forwarding/overview.md) 擴展允許您利用在Adobe Experience Platform邊緣網路中捕獲的資料並將其發送到 [!DNL Pinterest]。 本文檔介紹擴展的使用案例、如何安裝擴展，以及如何將其功能整合到事件轉發中 [規則](../../../ui/managing-resources/rules.md)。

轉換訪問令牌是使用的驗證方法 [!DNL Pinterest] 與 [!DNL Pinterest] API。

## 使用案例

如果要使用中的邊緣網路中的資料，應使用此擴展 [!DNL Pinterest] 利用其客戶分析功能。

例如，考慮組織中的市場營銷團隊。 團隊從其網站捕獲用戶交互事件資料並將其載入到 [!DNL Pinterest] 使用此事件轉發擴展。

然後，營銷和分析團隊可以利用 [!DNL Pinterest] 分析功能可以瞭解關鍵用戶交互和行為，使您能夠更好地瞭解用戶並將其定向用於目標廣告活動。

有關特定於 [!DNL Pinterest]，請參閱 [[!DNL Pinterest] 使用案例](https://business.pinterest.com/en/success-stories) 文檔。

## [!DNL Pinterest] 先決條件 {#prerequisites}

您必須具有 [!DNL Pinterest] [業務帳戶](https://help.pinterest.com/en/business/article/get-a-business-account) 以便使用此擴展。 轉到 [[!DNL Pinterest] 註冊頁](https://www.pinterest.com/business/create/) 註冊並建立帳戶。

您還需要 [!DNL Pinterest] 開發人員帳戶，需要與您的 [!DNL Pinterest] 業務帳戶。 要將開發人員帳戶與業務帳戶關聯，請參閱 [[!DNL Pinterest ] 開發者帳戶](https://developers.pinterest.com/account-setup/)。

### 收集所需的配置詳細資訊 {#configuration-details}

為了將Experience Platform連接到 [!DNL Pinterest]，需要輸入以下資料：

| 憑據 | 說明 | 範例 |
| --- | --- | --- |
| 廣告帳戶ID | 您 [!DNL Pinterest] 廣告帳戶ID。 請參閱 [[!DNL Pinterest] 文檔](https://help.pinterest.com/en/business/article/find-ids-in-ads-manager) 的上界。 | 123456789012 |
| 轉換訪問令牌 | 您 [!DNL Pinterest] 轉換訪問令牌。 請參閱 [[!DNL Pinterest] 轉換API](https://developers.pinterest.com/docs/conversions/conversions/#Get%20the%20conversion%20token) 文檔。 <br> **由於此令牌未過期，您將只需要執行一次此操作。** | {YOUR_GENARE_TOKEN} |

## 安裝和配置 [!DNL Pinterest] 擴展 {#install}

要安裝擴展， [建立事件轉發屬性](../../../ui/event-forwarding/overview.md#properties) 或選擇要編輯的現有屬性。

在左側導航中，選擇 **[!UICONTROL 擴展]**。 選擇 **[!UICONTROL 安裝]** 卡上 [!DNL Pinterest] 的 **[!UICONTROL 目錄]** 頁籤。

![顯示目錄 [!DNL Pinterest] 擴展 [!UICONTROL 安裝] 。](../../../images/extensions/server/pinterest/install.png)

### 設定 [!DNL Pinterest] 擴充功能

>[!IMPORTANT]
>
>根據您的實施需要，在配置擴展之前，可能需要建立架構、資料元素和資料集。 請在開始之前查看所有配置步驟，以確定您需要為使用案例設定哪些實體。

在左側導航中，選擇 **[!UICONTROL 擴展]**。 選擇 **[!UICONTROL 配置]** 卡上 [!DNL Pinterest] 的 [!UICONTROL 已安裝]**頁籤。

![[!DNL Pinterest] 擴展 [!UICONTROL 安裝] 頁籤 [!UICONTROL 配置] 。](../../../images/extensions/server/pinterest/configure.png)

在下一個螢幕上，輸入 [!UICONTROL 廣告帳戶ID] 和 [!UICONTROL 轉換訪問令牌] 你之前收集的 [配置詳細資訊](#configuration-details) 的子菜單。 完成後，選擇 **[!UICONTROL 保存]**。

![的 [!DNL Pinterest] [!UICONTROL 配置] 螢幕突出顯示 [!UICONTROL 廣告帳戶ID] 和 [!UICONTROL 轉換訪問令牌] 輸入欄位。](../../../images/extensions/server/pinterest/input.png)

## 配置事件轉發規則 {#config-rule}

設定所有資料元素後，您就可以開始建立事件轉發規則，這些規則將確定事件何時以及如何發送到 [!DNL Pinterest]。

新建 [規則](../../../ui/managing-resources/rules.md) 在事件轉發屬性中。 下 **[!UICONTROL 操作]**，添加新操作並將擴展設定為 **[!UICONTROL Pinterest]**。 將Adobe Experience Edge Network事件發送到 [!DNL Pinterest]的子菜單。 **[!UICONTROL 操作類型]** 至 **[!UICONTROL 發送事件]。**

![的 [!DNL Pinterest] [!UICONTROL 發送事件] 規則建立。](../../../images/extensions/server/pinterest/rule.png)

選擇後，將顯示其他控制項以進一步配置事件。 你需要把 [!DNL Pinterest] 事件屬性到先前建立的資料元素。

### [!UICONTROL 事件資料]

建立新規則需要以下事件資料：

| 欄位名稱 | 說明 | 範例 |
| --- | --- | --- | 
| [!UICONTROL 活動名稱] | 用戶事件的類型。 但是，這可以是任何事件類型，以利用 [!DNL Pinterest Analytics] 建議使用 [[!DNL Pinterest] 事件代碼](https://help.pinterest.com/en/business/article/add-event-codes) | *結帳 <br> *添加到購物車 <br> *頁面訪問 <br> *註冊 <br> * [用戶定義的事件] |
| [!UICONTROL 操作源] | 指示轉換事件發生位置的源。 | *應用程式安卓系統 <br> *應用程式_ios <br> * Web <br> *離線 |
| [!UICONTROL 事件時間] | 這指事件時間。 使用的預設時間格式為UNIX，格式為 `<seconds>.<miliseconds>` 取決於您的本地時區。 有關詳細資訊，請參閱 [[!DNL Pinterest] API](https://developers.pinterest.com/docs/api/v5/#operation/events/create)。 | 1433188255.500表示1433188255秒和500毫秒（或2015年6月1日星期一，7）:50:格林尼治時間下午5點 |
| [!UICONTROL 事件ID] | 標識此事件的唯一ID字串，可用於在通過轉換API和Pinterest跟蹤所接收的事件之間執行重複資料消除。 如果沒有這一點，該事件的資料可能會重複計算，並報告衡量通脹的指標。 | ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad |
| [!UICONTROL 事件屬性] | 包含事件的自定義屬性的JSON對象。 從提供原始JSON或使用一組簡化的鍵值輸入中進行選擇。 | { &quot;event_source_url&quot;:&quot;http://site.com&quot; } |

![的 [!DNL Pinterest] [!UICONTROL 事件資料] 在規則操作中突出顯示。](../../../images/extensions/server/pinterest/event-data.png)

可以配置以下事件屬性：

| 欄位名稱 | 說明 |
| --- | --- |
| 事件源URL | Web轉換事件的URL。 |
| 應用程式儲存ID | 應用商店應用ID。 |
| 應用程式名稱 | 應用程式的名稱。 |
| Application Version | 應用程式的版本。 |
| 設備品牌 | 用戶使用的設備的品牌。 |
| 設備載體 | 用於其設備的用戶移動載體。 |
| 設備型號 | 用戶設備的型號。 |
| 裝置類型 | 用戶使用的設備類型。 |
| 作業系統版本 | 設備作業系統的版本。 |
| 用戶語言 | 表示用戶語言的兩字元ISO-639-1語言代碼。 |

### [!UICONTROL 用戶資料]

以下用戶資料可以由非必填欄位輸入：

| 欄位名稱 | 說明 | 範例 |
| --- | --- | --- | 
| [!UICONTROL 電子郵件] | 用戶電子郵件地址或用戶地址電子郵件的SHA256哈希。 | ebd543592...f2b7e1 |
| [!UICONTROL 移動廣告ID] | Sha256散列用戶的「Google廣告ID」(GAID)或「Apple廣告商標識」(IDFA) | ebd543592...f2b7e1 |
| [!UICONTROL 客戶端IP地址] | 用戶的IP地址，可以是IPv4或IPv6格式。 用於匹配。 | 192.168.0.1 |
| [!UICONTROL 客戶端用戶代理] | 用戶Web瀏覽器的用戶代理字串。 | Mozilla/5.0(平台；rv:geckoversion)Gecko/geckotrail Firefox/firefoxversion |
| [!UICONTROL 客戶資訊資料] | 包含其他客戶資訊的JSON對象。 從提供原始JSON或使用一組簡化的鍵值輸入中進行選擇。 | { &quot;ph&quot;:&quot;122333445&quot; } |

![的 [!DNL Pinterest] [!UICONTROL 用戶資料] 在規則操作中突出顯示。](../../../images/extensions/server/pinterest/user-data.png)

可配置的客戶資訊屬性包括：

| 欄位名稱 | 說明 |
| --- | --- |
| 電話 | 用戶聯繫人號碼。 只接受數字，並且應輸入國家代碼、區號和數字。 |
| 性別 | 性別可以輸入為&quot;f&quot;（女性）、&quot;m&quot;（男性）或&quot;n&quot;（非二進位）。 |
| 出生日期 | 按年、月和日輸入的出生日期。 |
| 「姓氏」 | 用戶的姓。 |
| 「名字」 | 用戶的名。 |
| 城市 | 用戶的居住城市。 這主要用於計費目的。 |
| 狀態 | 用戶狀態，它以小寫形式提供為兩個字母的代碼。 |
| 郵遞區號 | 用戶的壓縮碼，主要用於計費目的。 |
| 國家/地區 | 表示用戶國家/地區的兩字元ISO-3166國家/地區代碼。 |
| 外部ID | 來自廣告商的唯一ID，用於標識其空間中的用戶。 例如，用戶ID、會員ID等。 |
| 按一下ID | 儲存在域_epik cookie中或URL中的&amp;epik=查詢參數中的唯一標識符。 |

>[!IMPORTANT]
>
>在將資料發送到 [!DNL Pinterest] API端點，擴展將散列並規範下列欄位的值：電子郵件、電話號碼、名字、姓氏、性別、出生日期、城市、州、郵遞區號、國家/地區和外部ID。 如果SHA256字串已存在，擴展將不會散列這些欄位的值。

### [!UICONTROL 自定義資料]

可以為規則輸入以下自定義資料：

| 欄位名稱 | 說明 |
| --- | --- |
| 貨幣 | ISO-4217貨幣代碼。 如果沒有提供， [!DNL Pinterest] 將預設為在建立帳戶期間設定的廣告商幣種。 |
| 值 | 事件的總值。 已接受為請求中的字串。 這將被分析為兩位數。 |
| 搜索字串 | 與用戶轉換事件相關的搜索字串。 |
| 訂購 ID | 訂單ID。 發送 `order_id` 會幫助 [!DNL Pinterest] 在必要時刪除重複事件。 |
| 產品數 | 事件的產品總數。 例如，在簽出事件中購買的物料總數。 |
| 內容ID | 產品ID的清單（陣列） |
| 內容 | 包含產品資訊（如價格和數量）的對象清單（陣列）。 |

![的 [!DNL Pinterest] [!UICONTROL 自定義資料] 在規則操作中突出顯示。](../../../images/extensions/server/pinterest/custom-data.png)

## 驗證資料 [!DNL Pinterest]

建立並執行事件轉發規則後，驗證是否將發送到 [!DNL Pinterest] API按預期顯示在 [!DNL Pinterest] UI。

如果事件集合和 [!DNL Experience Platform] 整合成功，您將看到 [!DNL Pinterest] UI。

![的 [!DNL Pinterest] 事件管理器](../../../images/extensions/server/pinterest/event-history.png)

您可以進一步穿透鑽取並查看 [!DNL Pinterest] 事件資料分發。

![的 [!DNL Pinterest] 資料分佈](../../../images/extensions/server/pinterest/event-history-distribution.png)

## 後續步驟

本指南介紹如何安裝和配置 [!DNL Pinterest] 事件轉發UI中的擴展。 有關詳細資訊，請參閱正式文檔：

* [[!DNL Pinterest] API](https://developers.pinterest.com/docs/api/v5/)
* [[!DNL Pinterest] 轉換API概述](https://help.pinterest.com/en/business/article/the-pinterest-api-for-conversions)
