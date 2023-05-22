---
title: 元轉換API擴展概述
description: 瞭解在Adobe Experience Platform用於事件轉發的Meta Conversions API擴展。
exl-id: 6b5836d6-6674-4978-9165-0adc1d7087b7
source-git-commit: f5a9e8cb5cdbff485bc7d50e9567b0236ae5872e
workflow-type: tm+mt
source-wordcount: '2368'
ht-degree: 0%

---

# [!DNL Meta Conversions API] 擴展概述

的 [[!DNL Meta Conversions API]](https://developers.facebook.com/docs/marketing-api/conversions-api/) 允許您將伺服器端營銷資料連接到 [!DNL Meta] 以優化您的廣告目標、降低每項操作的成本並衡量結果。 事件連結到 [[!DNL Meta Pixel]](https://developers.facebook.com/docs/meta-pixel/) ID，並以與客戶端事件類似的方式進行處理。

使用 [!DNL Meta Conversions API] 擴展，您可以在 [事件轉發](../../../ui/event-forwarding/overview.md) 將資料發送到的規則 [!DNL Meta] 從Adobe Experience Platform邊緣網。 本文檔介紹如何安裝擴展並在事件轉發時使用其功能 [規則](../../../ui/managing-resources/rules.md)。

## 先決條件

強烈建議使用 [!DNL Meta Pixel] 和 [!DNL Conversions API] 從客戶端和伺服器端分別共用和發送相同事件，因為這可能有助於恢復未由 [!DNL Meta Pixel]。 安裝前 [!DNL Conversions API] 擴展，請參閱 [[!DNL Meta Pixel] 擴展](../../client/meta/overview.md) 有關如何將其整合到客戶端標籤實施中的步驟。

>[!NOTE]
>
>關於 [事件重複消除](#deduplication) 本文檔稍後介紹的步驟可確保不兩次使用同一事件，因為可能同時從瀏覽器和伺服器接收該事件。

為了使用 [!DNL Conversions API] 擴展，您必須有權訪問事件轉發，並且 [!DNL Meta] 有權訪問的帳戶 [!DNL Ad Manager] 和 [!DNL Event Manager]。 具體來說，必須複製現有 [[!DNL Meta Pixel]](https://www.facebook.com/business/help/952192354843755?id=1205376682832142) 或 [新建 [!DNL Pixel]](https://www.facebook.com/business/help/952192354843755) 而是)，以便可以將擴展配置到您的帳戶。

>[!INFO]
>
>如果您計畫將此擴展用於移動應用資料，或者您還在處理離線事件資料 [!DNL Meta] 市場活動，您需要通過現有應用建立您的資料集並選擇 **從像素ID建立** 提示。 請參閱文章 [確定哪個資料集建立選項適合您的業務](https://www.facebook.com/business/help/5270377362999582?id=490360542427371) 的雙曲餘切值。 請參閱 [轉換應用程式事件的API](https://developers.facebook.com/docs/marketing-api/conversions-api/app-events) 文檔，以獲取所有必需和可選的應用程式跟蹤參數。

## 安裝擴展

安裝 [!DNL Meta Conversions API] 擴展，導航到資料收集UI或Experience PlatformUI並選擇 **[!UICONTROL 事件轉發]** 的上界。 在此處，選擇要向其添加副檔名的屬性，或改為建立新屬性。

選擇或建立所需屬性後，選擇 **[!UICONTROL 擴展]** 在左側導航中，選擇 **[!UICONTROL 目錄]** 頁籤。 搜索 [!UICONTROL 元轉換API] 卡，然後選擇 **[!UICONTROL 安裝]**。

![的 [!UICONTROL 安裝] 按鈕 [!UICONTROL 元轉換API] 資料收集UI中的擴展。](../../../images/extensions/server/meta/install.png)

在顯示的配置視圖中，必須提供 [!DNL Pixel] 您以前複製的ID，用於將分機連結到您的帳戶。 您可以直接將ID貼上到輸入中，也可以改用資料元素。

您還需要提供訪問令牌以使用 [!DNL Conversions API] 特別是。 請參閱 [!DNL Conversions API] 文檔 [生成訪問令牌](https://developers.facebook.com/docs/marketing-api/conversions-api/get-started#access-token) 獲取此值的步驟。

完成後，選擇 **[!UICONTROL 保存]**

![的 [!DNL Pixel] 作為擴展配置視圖中的資料元素提供的ID。](../../../images/extensions/server/meta/configure.png)

擴展已安裝，您現在可以將其功能用於事件轉發規則。

## 配置事件轉發規則 {#rule}

本節介紹如何使用 [!DNL Conversions API] 泛型事件轉發規則中的擴展。 在實踐中，您應配置多個規則以發送所有接受的規則 [標準事件](https://developers.facebook.com/docs/meta-pixel/reference) 通過 [!DNL Meta Pixel] 和 [!DNL Conversions API]。 有關移動應用資料，請參閱必填欄位、應用資料欄位、客戶資訊參數和自定義資料詳細資訊 [這裡](https://developers.facebook.com/docs/marketing-api/conversions-api/app-events)。

>[!NOTE]
>
>事件應為 [即時發送](https://www.facebook.com/business/help/379226453470947?id=818859032317965) 或盡可能接近即時地優化廣告活動。

開始建立新事件轉發規則並根據需要配置其條件。 為規則選擇操作時，選擇 **[!UICONTROL 元轉換API擴展]** ，然後選擇 **[!UICONTROL 發送轉換API事件]** 按鈕。

![的 [!UICONTROL 發送頁面視圖] 正在為資料收集UI中的規則選擇操作類型。](../../../images/extensions/server/meta/select-action.png)

顯示允許您配置將發送到的事件資料的控制項 [!DNL Meta] 通過 [!DNL Conversions API]。 這些選項可直接輸入到提供的輸入中，或者可以選擇現有資料元素來代表值。 配置選項分為以下四個主要部分。

| 「配置」部分 | 說明 |
| --- | --- |
| [!UICONTROL 伺服器事件參數] | 有關事件的一般資訊，包括事件發生的時間和觸發事件的源操作。 請參閱 [!DNL Meta] 開發人員文檔，瞭解有關 [標準事件參數](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/server-event) 被接受 [!DNL Conversions API]。<br><br>如果同時使用 [!DNL Meta Pixel] 和 [!DNL Conversions API] 要發送事件，請確保同時包含 **[!UICONTROL 事件名稱]** (`event_name`) **[!UICONTROL 事件ID]** (`event_id`)，因為這些值用於 [事件重複消除](#deduplication)。<br><br>您還可以選擇 **[!UICONTROL 啟用有限資料使用]** 幫助客戶選擇退出。 查看 [!DNL Conversions API] 文檔 [資料處理選項](https://developers.facebook.com/docs/marketing-apis/data-processing-options/) 的子菜單。 |
| [!UICONTROL 客戶資訊參數] | 用於將事件屬性化給客戶的用戶標識資料。 其中一些值必須經過散列後才能發送到API。<br><br>為確保良好的公共API連接和高事件匹配質量(EMQ)，建議您發送所有 [接受的客戶資訊參數](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/customer-information-parameters) 與伺服器事件並列。 這些參數也應 [根據其重要性和對EMQ的影響](https://www.facebook.com/business/help/765081237991954?id=818859032317965)。 |
| [!UICONTROL 自定義資料] | 用於廣告傳遞優化的附加資料，以JSON對象的形式提供。 請參閱 [[!DNL Conversions API] 文檔](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/custom-data) 的子菜單。<br><br>如果要發送採購事件，則必須使用此部分提供所需的屬性 `currency` 和 `value`。 |
| [!UICONTROL Test事件] | 此選項用於驗證配置是否導致伺服器事件被 [!DNL Meta] 如預期。 要使用此功能，請選擇 **[!UICONTROL 作為Test事件發送]** 複選框，然後在下面的輸入中提供您選擇的test事件代碼。 部署事件轉發規則後，如果正確配置了擴展和操作，則應看到在 **[!DNL Test Events]** 查看 [!DNL Meta Events Manager]。 |

{style="table-layout:auto"}

完成後，選擇 **[!UICONTROL 保留更改]** 將操作添加到規則配置。

![[!UICONTROL 保留更改] 正在為操作配置選擇。](../../../images/extensions/server/meta/keep-changes.png)

對規則滿意後，選擇 **[!UICONTROL 保存到庫]**。 最後，發佈新事件轉發 [構建](../../../ui/publishing/builds.md) 以啟用對庫所做的更改。

## 事件重複資料刪除 {#deduplication}

如 [先決條件部分](#prerequisites)，建議您同時使用 [!DNL Meta Pixel] 標籤擴展和 [!DNL Conversions API] 事件轉發擴展，在冗餘設定中從客戶端和伺服器發送相同的事件。 這有助於恢復未被一個擴展或另一個擴展拾取的事件。

如果從客戶端和伺服器發送不同的事件類型，但兩者之間沒有重疊，則無需進行重複資料消除。 但是，如果任何單個事件由兩者共用 [!DNL Meta Pixel] 和 [!DNL Conversions API]，您必須確保對這些冗餘事件進行重複資料消除，以便不會對報告造成負面影響。

在發送共用事件時，請確保包含從客戶端和伺服器發送的每個事件的事件ID和名稱。 當收到多個ID和名稱相同的事件時， [!DNL Meta] 自動採用多種策略來消除重複並保留最相關的資料。 查看 [!DNL Meta] 文檔 [重複資料消除 [!DNL Meta Pixel] 和 [!DNL Conversions API] 事件](https://www.facebook.com/business/help/823677331451951?id=1205376682832142) 的子菜單。

## 快速啟動工作流：元轉換API擴展(Beta) {#quick-start}

>[!IMPORTANT]
>
>* 快速入門功能適用於購買了Real-Time CDPPrime和Ultimate包的客戶。 請聯繫您的Adobe代表以瞭解更多資訊。
>* 此功能適用於新的網路實現，目前不支援在現有標籤和事件轉發屬性上自動安裝擴展和配置。


快速啟動功能可幫助您輕鬆、高效地設定元轉換API和元像素擴展。 此工具自動執行在Adobe標籤和事件轉發中執行的多個步驟，從而顯著縮短了設定時間。

此功能會自動在新自動生成的標籤和事件轉發屬性上安裝和配置元轉換API和元像素擴展，並使用必要的規則和資料元素。 此外，它還自動安裝和配置Experience PlatformWeb SDK和Datastream。 最後，快速啟動功能自動將庫發佈到開發環境中的指定URL，從而通過事件轉發和體驗邊緣即時收集客戶端資料和伺服器端事件轉發。

以下視頻介紹了快速啟動功能。

>[!VIDEO](https://video.tv.adobe.com/v/3416939?quality=12&learn=on)

### 安裝快速啟動功能

>[!NOTE]
>
>此功能旨在幫助您開始執行事件轉發實現。 它不會提供端對端、功能齊全的適用所有使用情形的實施。

此設定自動安裝元轉換API和元像素擴展。 此混合實現由Meta推薦，用於收集和轉發事件轉換伺服器端。
快速設定功能旨在幫助客戶開始執行事件轉發實施，而不是旨在提供端對端、功能齊全的實施，以適應所有使用情形。

要安裝該功能，請選擇 **[!UICONTROL 開始]** 為 **[!DNL Send Conversions Data to Meta]** Adobe Experience Platform資料收集 **[!UICONTROL 首頁]** 的子菜單。

![資料收集首頁，顯示將資料轉換為元](../../../images/extensions/server/meta/conversion-data-to-meta.png)

輸入 **[!UICONTROL 域]**，然後選擇 **[!UICONTROL 下一個]**。 此域將用作自動生成的標籤和事件轉發屬性、規則、資料元素、資料流等的命名約定。

![請求域名的歡迎螢幕](../../../images/extensions/server/meta/welcome.png)

在 **[!UICONTROL 初始設定]** 對話框 **[!UICONTROL 元像素ID]**。 **[!UICONTROL 元轉換API訪問令牌]**, **[!UICONTROL 資料層路徑]**，然後選擇 **[!UICONTROL 下一個]**。

![初始設定對話框](../../../images/extensions/server/meta/initial-setup.png)

允許完成初始安裝過程幾分鐘，然後選擇 **[!UICONTROL 下一個]**。

![初始設定完成確認螢幕](../../../images/extensions/server/meta/setup-complete.png)

從 **[!UICONTROL 在您的站點上添加代碼]** 對話框複製使用副本提供的代碼 ![複製](../../../images/extensions/server/meta/copy-icon.png) 函式並貼上到 `<head>` 源網站。 實施後，選擇 **[!UICONTROL 開始驗證]**

![在站點對話框中添加代碼](../../../images/extensions/server/meta/add-code-on-your-site.png)

的 [!UICONTROL 驗證結果] 對話框顯示元擴展實現結果。 選取&#x200B;**[!UICONTROL 「下一步」]**。通過選擇 **[!UICONTROL 保證]** 的子菜單。

![Test結果對話框顯示實現結果](../../../images/extensions/server/meta/test-results.png)

的 **[!UICONTROL 後續步驟]** 螢幕顯示確認安裝完成。 在此處，您可以選擇通過添加新事件來優化實施，這些事件將在下一節中顯示。

如果不想添加其他事件，請選擇 **[!UICONTROL 關閉]**。

![「下一步」對話框](../../../images/extensions/server/meta/next-steps.png)

#### 添加其他事件

要添加新事件，請選擇 **[!UICONTROL 編輯標籤Web屬性]**。

![顯示編輯標籤Web屬性的後續步驟對話框](../../../images/extensions/server/meta/edit-your-tags-web-property.png)

選擇與要編輯的元事件對應的規則。 比如說， **元轉換_添加到購物車**。

>[!NOTE]
>
>如果沒有事件，則此規則將不運行。 對於所有規則，這是正確的 **元轉換_頁視圖** 規則是例外。

添加事件選擇 **[!UICONTROL 添加]** 下 [!UICONTROL 事件] 的子菜單。

![「標籤屬性」頁，不顯示任何事件](../../../images/extensions/server/meta/edit-rule.png)

選擇 [!UICONTROL 事件類型]。 在此示例中，我們選擇了 [!UICONTROL 按一下] 事件，並將其配置為在 **.Add-to-cart按鈕** 的子菜單。 選取&#x200B;**[!UICONTROL 「保留變更」]**。

![顯示按一下事件的事件配置螢幕](../../../images/extensions/server/meta/event-configuration.png)

新事件已保存。 選擇 **[!UICONTROL 選擇工作庫]** 並選擇要構建到的庫。

![選擇工作庫下拉清單](../../../images/extensions/server/meta/working-library.png)

下一步選擇旁邊的下拉清單 **[!UICONTROL 保存到庫]** 選擇 **[!UICONTROL 保存到庫並生成]**。 這將在庫中發佈更改。

![選擇保存到庫並生成](../../../images/extensions/server/meta/save-and-build.png)

對要配置的任何其他元轉換事件重複這些步驟。

#### 資料層配置 {#configuration}

>[!IMPORTANT]
>
>更新此全局資料層的方式取決於您的網站體系結構。 單頁應用程式與伺服器端呈現應用程式不同。 另外，您還可能完全負責在標籤產品內建立和更新此資料。 在所有情況下，資料層都需要在運行 `MetaConversion_* rules`。 如果您不在規則之間更新資料，則可能還會遇到從上一個規則發送過時資料的情況 `MetaConversion_* rule` 的 `MetaConversion_* rule`。

在配置過程中，系統會詢問您的資料層位於何處。 預設情況下， `window.dataLayer.meta`，內部 `meta` 對象，您的資料應如下所示。

![資料層元資訊](../../../images/extensions/server/meta/data-layer-meta.png)

這很重要，因為 `MetaConversion_*` 規則使用此資料結構將相關資料段傳遞給 [!DNL Meta Pixel] 和 [!DNL Meta Conversions API]。 請參閱上 [標準事件](https://developers.facebook.com/docs/meta-pixel/reference#standard-events) 的子菜單。

例如，如果您想使用 `MetaConversion_Subscribe` 規則，你需要 `window.dataLayer.meta.currency`。 `window.dataLayer.meta.predicted_ltv`, `window.dataLayer.meta.value` 按照上文檔中描述的對象屬性 [標準事件](https://developers.facebook.com/docs/meta-pixel/reference#standard-events)。

下面是一個示例，說明在執行規則之前需要在網站上運行什麼才能更新資料層。

![更新資料層元資訊](../../../images/extensions/server/meta/update-data-layer-meta.png)

預設情況下， `<datalayerpath>.conversionData.eventId` 將通過「生成新事件ID」操作隨機生成 `MetaConversion_* rules`。

有關資料層應該如何顯示的本地參考，可在 `MetaConversion_DataLayer` 屬性上的資料元素。

## 後續步驟

本指南介紹如何將伺服器端事件資料發送到 [!DNL Meta] 使用 [!DNL Meta Conversions API] 擴展。 在此處，建議通過連接更多內容來擴展整合 [!DNL Pixels] 並在適用時共用更多事件。 執行以下任一操作都有助於進一步提高廣告效能：

* 連接任何其他 [!DNL Pixels] 尚未連接到 [!DNL Conversions API] 整合。
* 如果您僅通過 [!DNL Meta Pixel] 在客戶端，將這些相同的事件發送到 [!DNL Conversions API] 從伺服器端。

查看 [!DNL Meta] 文檔 [最佳實踐 [!DNL Conversions API]](https://www.facebook.com/business/help/308855623839366?id=818859032317965) 有關如何有效實施整合的更多指導。 有關Adobe Experience Cloud標籤和事件轉發的更一般資訊，請參閱 [標籤概述](../../../home.md)。
