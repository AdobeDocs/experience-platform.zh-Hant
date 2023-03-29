---
title: 中繼轉換API擴充功能概觀
description: 了解Adobe Experience Platform中用於事件轉送的中繼轉換API擴充功能。
exl-id: 6b5836d6-6674-4978-9165-0adc1d7087b7
source-git-commit: ec1e2b792ff827fd791576d904858ef9abb98947
workflow-type: tm+mt
source-wordcount: '2261'
ht-degree: 0%

---

# [!DNL Meta Conversions API] 擴充功能概觀

此 [[!DNL Meta Conversions API]](https://developers.facebook.com/docs/marketing-api/conversions-api/) 可讓您將伺服器端行銷資料連結至 [!DNL Meta] 技術，以最佳化您的廣告鎖定目標、降低每個動作的成本並衡量結果。 事件會連結至 [[!DNL Meta Pixel]](https://developers.facebook.com/docs/meta-pixel/) ID和的處理方式與用戶端事件類似。

使用 [!DNL Meta Conversions API] 擴充功能，您可以在 [事件轉送](../../../ui/event-forwarding/overview.md) 將資料傳送至的規則 [!DNL Meta] 來自Adobe Experience Platform Edge Network。 本檔案說明如何安裝擴充功能，以及在事件轉送中使用其功能 [規則](../../../ui/managing-resources/rules.md).

## 先決條件

強烈建議使用 [!DNL Meta Pixel] 和 [!DNL Conversions API] 分別從用戶端和伺服器端共用和傳送相同事件，因為這可能有助於復原未擷取的事件 [!DNL Meta Pixel]. 安裝之前 [!DNL Conversions API] 擴充功能，請參閱 [[!DNL Meta Pixel] 擴充功能](../../client/meta/overview.md) 以了解如何將其整合至用戶端標籤實施的步驟。

>[!NOTE]
>
>的 [事件去重複化](#deduplication) 本檔案稍後將說明確保不會使用相同事件兩次的步驟，因為同一事件可能會從瀏覽器和伺服器接收。

若要使用 [!DNL Conversions API] 擴充功能，您必須擁有事件轉送的存取權，且具備有效 [!DNL Meta] 有權存取的帳戶 [!DNL Ad Manager] 和 [!DNL Event Manager]. 具體來說，您必須複製現有 [[!DNL Meta Pixel]](https://www.facebook.com/business/help/952192354843755?id=1205376682832142) (或 [建立新 [!DNL Pixel]](https://www.facebook.com/business/help/952192354843755) )，以便將擴充功能設定至您的帳戶。

## 安裝擴充功能

若要安裝 [!DNL Meta Conversions API] 擴充功能，請導覽至資料收集UI或Experience PlatformUI，然後選取 **[!UICONTROL 事件轉送]** 從左側導覽。 從此處，選取要新增擴充功能的屬性，或改為建立新屬性。

選取或建立所需屬性後，請選取 **[!UICONTROL 擴充功能]** 在左側導覽器中，選取 **[!UICONTROL 目錄]** 標籤。 搜尋 [!UICONTROL 中繼轉換API] 卡片，然後選取 **[!UICONTROL 安裝]**.

![此 [!UICONTROL 安裝] 按鈕 [!UICONTROL 中繼轉換API] 擴充功能。](../../../images/extensions/server/meta/install.png)

在顯示的設定檢視中，您必須提供 [!DNL Pixel] 您先前複製的ID，將擴充功能連結至您的帳戶。 您可以直接將ID貼入輸入，或改用資料元素。

您也需要提供存取權杖，才能使用 [!DNL Conversions API] 具體來說。 請參閱 [!DNL Conversions API] 檔案 [產生存取權杖](https://developers.facebook.com/docs/marketing-api/conversions-api/get-started#access-token) 以取得此值的步驟。

完成後，請選取 **[!UICONTROL 儲存]**

![此 [!DNL Pixel] 在擴充功能組態檢視中以資料元素形式提供的ID。](../../../images/extensions/server/meta/configure.png)

擴充功能已安裝，您現在可以在事件轉送規則中運用其功能。

## 設定事件轉送規則 {#rule}

本節說明如何使用 [!DNL Conversions API] 一般事件轉送規則中的擴充功能。 實際上，您應設定數個規則，以傳送所有已接受的 [標準事件](https://developers.facebook.com/docs/meta-pixel/reference) via [!DNL Meta Pixel] 和 [!DNL Conversions API].

>[!NOTE]
>
>事件應為 [即時傳送](https://www.facebook.com/business/help/379226453470947?id=818859032317965) 或盡可能接近即時，以更佳的廣告促銷活動最佳化。

開始建立新的事件轉送規則，並視需要設定其條件。 選取規則的動作時，請選取 **[!UICONTROL 中繼轉換API擴充功能]** 對於擴充功能，請選取 **[!UICONTROL 傳送轉換API事件]** （針對動作類型）。

![此 [!UICONTROL 傳送頁面檢視] 在資料收集UI中為規則選取的動作類型。](../../../images/extensions/server/meta/select-action.png)

控制項可讓您設定要傳送至的事件資料 [!DNL Meta] 透過 [!DNL Conversions API]. 這些選項可直接輸入到提供的輸入中，或者您可以選取現有資料元素來代表值。 設定選項分為四個主要部分，如下所述。

| 設定區段 | 說明 |
| --- | --- |
| [!UICONTROL 伺服器事件參數] | 事件的一般資訊，包括發生時間和觸發事件的來源動作。 請參閱 [!DNL Meta] 開發人員檔案，以取得 [標準事件參數](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/server-event) 接受 [!DNL Conversions API].<br><br>如果您同時使用 [!DNL Meta Pixel] 和 [!DNL Conversions API] 若要傳送事件，請務必同時包含 **[!UICONTROL 事件名稱]** (`event_name`)和 **[!UICONTROL 事件ID]** (`event_id`)，因為這些值會用於 [事件去重複化](#deduplication).<br><br>您也可以選擇 **[!UICONTROL 啟用有限的資料使用]** 以協助遵守客戶選擇退出。 請參閱 [!DNL Conversions API] 檔案 [資料處理選項](https://developers.facebook.com/docs/marketing-apis/data-processing-options/) 以取得此功能的詳細資訊。 |
| [!UICONTROL 客戶資訊參數] | 用於將事件歸因給客戶的使用者身分資料。 其中有些值必須先經過雜湊處理，才能傳送至API。<br><br>為確保良好的通用API連線和高事件符合品質(EMQ)，建議您全部傳送 [接受的客戶資訊參數](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/customer-information-parameters) 與伺服器事件一起使用。 這些參數也應為 [根據其重要性和對EMQ的影響來排定優先順序](https://www.facebook.com/business/help/765081237991954?id=818859032317965). |
| [!UICONTROL 自訂資料] | 要用於廣告傳送最佳化的其他資料，以JSON物件的形式提供。 請參閱 [[!DNL Conversions API] 檔案](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/custom-data) ，以了解此對象的接受屬性。<br><br>如果您要傳送購買事件，必須使用此區段來提供必要的屬性 `currency` 和 `value`. |
| [!UICONTROL 測試事件] | 此選項用於驗證您的配置是否導致接收伺服器事件 [!DNL Meta] 如預期。 若要使用此功能，請選取 **[!UICONTROL 以測試事件的形式傳送]** 核取方塊，然後在下方輸入中提供您所選取的測試事件程式碼。 部署事件轉送規則後，如果您正確設定擴充功能和動作，應該會看到活動出現在 **[!DNL Test Events]** 檢視 [!DNL Meta Events Manager]. |

{style="table-layout:auto"}

完成後，請選取 **[!UICONTROL 保留變更]** 將動作新增至規則設定。

![[!UICONTROL 保留變更] 正在為操作配置選擇。](../../../images/extensions/server/meta/keep-changes.png)

對規則感到滿意時，請選取 **[!UICONTROL 儲存至程式庫]**. 最後，發佈新的事件轉送 [建置](../../../ui/publishing/builds.md) 啟用對程式庫所做的變更。

## 事件重複資料刪除 {#deduplication}

如 [必要條件一節](#prerequisites)，建議您同時使用 [!DNL Meta Pixel] 標籤擴充功能和 [!DNL Conversions API] 事件轉送擴充功能，在備援設定中從用戶端和伺服器傳送相同事件。 這有助於復原某個擴充功能或其他擴充功能未擷取的事件。

如果您從客戶端和伺服器發送不同的事件類型，且兩者之間沒有重疊，則不需要重複資料刪除。 不過，如果兩者共用任何單一事件 [!DNL Meta Pixel] 和 [!DNL Conversions API]，您必須確保這些重複事件已去除重複資料，以免對您的報表造成不利影響。

傳送共用事件時，請務必在您從用戶端和伺服器傳送的每個事件中加入事件ID和名稱。 收到多個ID和名稱相同的事件時， [!DNL Meta] 會自動採用數種策略來去除重複項目，並保留最相關的資料。 請參閱 [!DNL Meta] 檔案 [重複資料消除 [!DNL Meta Pixel] 和 [!DNL Conversions API] 事件](https://www.facebook.com/business/help/823677331451951?id=1205376682832142) 以取得此程式的詳細資訊。

## 快速入門工作流程：中繼轉換API擴充功能（測試版） {#quick-start}

>[!IMPORTANT]
>
>* 已購買Real-Time CDP Prime和Ultimate套件的客戶可使用快速入門功能。 如需詳細資訊，請連絡您的Adobe代表。
>* 此功能適用於新的淨實作，目前不支援在現有標籤和事件轉送屬性上自動安裝擴充功能和設定。


快速入門功能可協助您透過中繼轉換API和中繼像素擴充功能，輕鬆且有效率地完成設定。 此工具會自動執行Adobe標籤和事件轉送中的多個步驟，大幅縮短設定時間。

此功能會自動在新自動產生的標籤和事件轉送屬性上，使用必要的規則和資料元素，安裝並設定中繼轉換API和中繼像素擴充功能。 此外，它也會自動安裝及設定Experience PlatformWeb SDK和資料流。 最後，快速入門功能會在開發環境中自動將程式庫發佈至指定的URL，透過事件轉送和Experience Edge即時執行用戶端資料收集和伺服器端事件轉送。

以下影片介紹快速入門功能。

>[!VIDEO](https://publish.tv.adobe.com/bucket/1/category/5138/video/3416939/)

### 安裝快速入門功能

>[!NOTE]
>
>此功能旨在協助您開始實施事件轉送。 它不會提供端對端、功能完整的實作，以配合所有使用案例。

此設定會自動安裝中繼轉換API和中繼像素擴充功能。 Meta建議此混合式實作，以收集和轉送事件轉換伺服器端。
快速設定功能旨在協助客戶開始實施事件轉送實施，不是要提供端對端、功能完整的實施，以因應所有使用案例。

要安裝該功能，請選擇 **[!UICONTROL 開始使用]** for **[!DNL Send Conversions Data to Meta]** 在Adobe Experience Platform資料收集上 **[!UICONTROL 首頁]** 頁面。

![資料收集首頁，顯示轉換資料至中繼](../../../images/extensions/server/meta/conversion-data-to-meta.png)

輸入 **[!UICONTROL 網域]**，然後選取 **[!UICONTROL 下一個]**. 此網域將用作自動產生的標籤和事件轉送屬性、規則、資料元素、資料流等的命名慣例。

![請求域名的歡迎螢幕](../../../images/extensions/server/meta/welcome.png)

在 **[!UICONTROL 初始設定]** 對話框輸入 **[!UICONTROL 元像素ID]**, **[!UICONTROL 中繼轉換API存取權杖]**，和 **[!UICONTROL 資料層路徑]**，然後選取 **[!UICONTROL 下一個]**.

![初始設定對話框](../../../images/extensions/server/meta/initial-setup.png)

完成初始設定程式需要幾分鐘，然後選取 **[!UICONTROL 下一個]**.

![初始設定完成確認螢幕](../../../images/extensions/server/meta/setup-complete.png)

從 **[!UICONTROL 在您的網站上新增程式碼]** 對話方塊會複製使用復本提供的程式碼 ![複製](../../../images/extensions/server/meta/copy-icon.png) 函式，並將其貼入 `<head>` 來源網站。 實作後，選取 **[!UICONTROL 開始驗證]**

![在您的網站對話方塊上新增程式碼](../../../images/extensions/server/meta/add-code-on-your-site.png)

此 [!UICONTROL 驗證結果] 對話框顯示元擴展實施結果。 選取&#x200B;**[!UICONTROL 「下一步」]**。您也可以選取 **[!UICONTROL 保證]** 連結。

![測試結果對話方塊顯示實作結果](../../../images/extensions/server/meta/test-results.png)

此 **[!UICONTROL 後續步驟]** 螢幕顯示可確認設定完成。 從這裡，您可以選擇透過新增事件來最佳化實作，新事件會顯示在下一節。

如果您不想新增其他事件，請選取 **[!UICONTROL 關閉]**.

![「下一步」對話框](../../../images/extensions/server/meta/next-steps.png)

#### 新增其他事件

若要新增事件，請選取 **[!UICONTROL 編輯標籤Web屬性]**.

![顯示編輯標籤Web屬性的「下一步」對話框](../../../images/extensions/server/meta/edit-your-tags-web-property.png)

選取與您要編輯之中繼事件相對應的規則。 例如， **MetaConversion_AddToCart**.

>[!NOTE]
>
>如果沒有事件，則此規則不會執行。 所有規則皆適用，且 **MetaConversion_PageView** 規則為例外。

若要新增事件，請選取 **[!UICONTROL 新增]** 在 [!UICONTROL 事件] 標題。

![標籤屬性頁面沒有顯示事件](../../../images/extensions/server/meta/edit-rule.png)

選取 [!UICONTROL 事件類型]. 在此範例中，我們已選取 [!UICONTROL 按一下] 事件，並將其設定為在 **.add-to-cart-button** 中所有規則的URL。 選取&#x200B;**[!UICONTROL 「保留變更」]**。

![顯示點按事件的事件設定畫面](../../../images/extensions/server/meta/event-configuration.png)

已儲存新事件。 選擇 **[!UICONTROL 選取工作程式庫]** 並選取您要建置的程式庫。

![選取工作程式庫下拉式清單](../../../images/extensions/server/meta/working-library.png)

下一步，選取旁邊的下拉式清單 **[!UICONTROL 儲存至程式庫]** 選取 **[!UICONTROL 儲存至程式庫並建置]**. 這會在程式庫中發佈變更。

![選取儲存至程式庫並建置](../../../images/extensions/server/meta/save-and-build.png)

對您要設定的任何其他中繼轉換事件重複這些步驟。

#### 資料層組態

>[!IMPORTANT]
>
>更新此全域資料層的方式取決於您的網站架構。 單頁應用程式與伺服器端轉譯應用程式不同。 您也可能全權負責在標籤產品中建立和更新此資料。 在所有情況下，每次執行 `MetaConversion_* rules`. 如果您未更新規則之間的資料，可能也會遇到您從上次傳送過時資料的情況 `MetaConversion_* rule` 在當前 `MetaConversion_* rule`.

在設定期間，系統會詢問您的資料層位置。 依預設，這會是 `window.dataLayer.meta`，和內部 `meta` 物件，您的資料將會如下所示。

![資料層元資訊](../../../images/extensions/server/meta/data-layer-meta.png)

這一點很重要 `MetaConversion_*` 規則會使用此資料結構，將相關資料片段傳遞至 [!DNL Meta Pixel] 擴充功能和 [!DNL Meta Conversions API]. 請參閱 [標準事件](https://developers.facebook.com/docs/meta-pixel/reference#standard-events) 以取得不同中繼事件所需資料的詳細資訊。

例如，如果您想使用 `MetaConversion_Subscribe` 規則，您需要更新 `window.dataLayer.meta.currency`, `window.dataLayer.meta.predicted_ltv`，和 `window.dataLayer.meta.value` 如 [標準事件](https://developers.facebook.com/docs/meta-pixel/reference#standard-events).

以下是在執行規則之前，需要在網站上執行以更新資料層的範例。

![更新資料層元資訊](../../../images/extensions/server/meta/update-data-layer-meta.png)

依預設， `<datalayerpath>.conversionData.eventId` 會由任何 `MetaConversion_* rules`.

若要取得資料層外觀的本機參考，您可以在 `MetaConversion_DataLayer` 屬性上的資料元素。

## 後續步驟

本指南說明如何將伺服器端事件資料傳送至 [!DNL Meta] 使用 [!DNL Meta Conversions API] 擴充功能。 在此處，建議您透過連接更多 [!DNL Pixels] 和共用更多事件（若適用）。 執行下列任一操作有助於進一步提高廣告效能：

* 連接任何其他 [!DNL Pixels] 尚未連線至 [!DNL Conversions API] 整合。
* 如果您只是透過 [!DNL Meta Pixel] 在用戶端上，將這些相同的事件傳送至 [!DNL Conversions API] 從伺服器端。

請參閱 [!DNL Meta] 檔案 [最佳實務 [!DNL Conversions API]](https://www.facebook.com/business/help/308855623839366?id=818859032317965) 以取得如何有效實作整合的詳細指引。 如需Adobe Experience Cloud中標籤和事件轉送的更一般資訊，請參閱 [標籤概述](../../../home.md).
