---
title: 中繼轉換API擴充功能概觀
description: 瞭解Adobe Experience Platform中用於事件轉送的Meta Conversions API擴充功能。
exl-id: 6b5836d6-6674-4978-9165-0adc1d7087b7
source-git-commit: 3cd937f49f27006e3cab60df1692d33138944ce2
workflow-type: tm+mt
source-wordcount: '2583'
ht-degree: 0%

---

# [!DNL Meta Conversions API]擴充功能概觀

[[!DNL Meta Conversions API]](https://developers.facebook.com/docs/marketing-api/conversions-api/)可讓您將伺服器端行銷資料連線到[!DNL Meta]技術，以最佳化您的廣告目標定位、降低每個動作的成本並測量結果。 事件連結至[[!DNL Meta Pixel]](https://developers.facebook.com/docs/meta-pixel/) ID，並以類似使用者端事件的方式處理。

使用[!DNL Meta Conversions API]擴充功能時，您可以在[事件轉送](../../../ui/event-forwarding/overview.md)規則中運用API的功能，從Adobe Experience PlatformEdge Network傳送資料給[!DNL Meta]。 本文介紹如何安裝擴充功能，以及如何在事件轉送[規則](../../../ui/managing-resources/rules.md)中使用其功能。

## 示範

以下影片旨在協助您瞭解[!DNL Meta Conversions API]。

>[!VIDEO](https://unlockmarketingdata.com/video-meta-conversions-api)

## 先決條件

強烈建議分別使用[!DNL Meta Pixel]和[!DNL Conversions API]來共用和傳送使用者端和伺服器端的相同事件，因為這樣可能有助於復原[!DNL Meta Pixel]未擷取的事件。 在安裝[!DNL Conversions API]擴充功能之前，請參閱[[!DNL Meta Pixel] 擴充功能](../../client/meta/overview.md)的指南，以瞭解如何在使用者端標籤實作中整合擴充功能的步驟。

>[!NOTE]
>
>本檔案稍後關於[事件重複資料刪除](#deduplication)的章節涵蓋確保同一個事件不會使用兩次的步驟，因為從瀏覽器和伺服器都可能會收到該事件。

若要使用[!DNL Conversions API]擴充功能，您必須擁有事件轉送的存取權，並擁有可存取[!DNL Ad Manager]和[!DNL Event Manager]的有效[!DNL Meta]帳戶。 具體來說，您必須複製現有[[!DNL Meta Pixel]](https://www.facebook.com/business/help/952192354843755?id=1205376682832142)的識別碼（或是[改為建立新的 [!DNL Pixel]](https://www.facebook.com/business/help/952192354843755)），才能將擴充功能設定到您的帳戶。

>[!INFO]
>
>如果您打算將此擴充功能與行動應用程式資料搭配使用，或同時處理[!DNL Meta]行銷活動中的離線事件資料，則需透過現有應用程式建立資料集，並在系統提示時選取「**從畫素ID建立**」。 請參閱文章[決定適合您企業的資料集建立選項](https://www.facebook.com/business/help/5270377362999582?id=490360542427371)以取得詳細資料。 如需所有必要和選用應用程式追蹤引數，請參閱[應用程式事件轉換API](https://developers.facebook.com/docs/marketing-api/conversions-api/app-events)檔案。

## 安裝擴充功能

若要安裝[!DNL Meta Conversions API]擴充功能，請導覽至資料收集UI或Experience PlatformUI，然後從左側導覽中選取&#x200B;**[!UICONTROL 事件轉送]**。 從這裡，選取要新增擴充功能的屬性，或改為建立新屬性。

選取或建立所需的屬性後，在左側導覽中選取&#x200B;**[!UICONTROL 擴充功能]**，然後選取&#x200B;**[!UICONTROL 目錄]**&#x200B;索引標籤。 搜尋[!UICONTROL Meta Conversions API]卡片，然後選取&#x200B;**[!UICONTROL 安裝]**。

![正在資料收集UI中為[!UICONTROL Meta Conversions API]擴充功能選取[!UICONTROL 安裝]選項。](../../../images/extensions/server/meta/install.png)

在出現的設定檢視中，您必須提供您先前複製的[!DNL Pixel] ID，以將擴充功能連結至您的帳戶。 您可以直接將ID貼入輸入中，也可以改用資料元素。

您也需要提供存取權杖以專門使用[!DNL Conversions API]。 如需如何取得此值的步驟，請參閱有關[產生存取權杖](https://developers.facebook.com/docs/marketing-api/conversions-api/get-started#access-token)的[!DNL Conversions API]檔案。

完成後，選取&#x200B;**[!UICONTROL 儲存]**

![擴充功能組態檢視中作為資料元素提供的[!DNL Pixel] ID。](../../../images/extensions/server/meta/configure.png)

擴充功能已安裝，您現在可以在事件轉送規則中運用其功能。

## 與Facebook和Instagram擴充功能整合 {#facebook}

使用Facebook和Instagram擴充功能的整合可讓您快速驗證您的中繼企業帳戶。 然後這會自動填入您的[!UICONTROL 畫素ID]和中繼轉換API [!UICONTROL 存取權杖]，讓您更容易安裝和設定中繼轉換API。

安裝[!UICONTROL Meta Conversions API]擴充功能時，會出現在Facebook和Instagram中進行驗證的對話方塊提示。

![ [!UICONTROL Meta Conversions API擴充功能]安裝頁面醒目提示[!UICONTROL 連線至Meta]。](../../../images/extensions/server/meta/mbe-extension-install.png)

在Facebook和Instagram中驗證的對話方塊提示也會顯示在事件轉送的快速啟動工作流程UI中。

![快速入門工作流程UI醒目提示[!UICONTROL 連線至中繼資料]。](../../../images/extensions/server/meta/mbe-extension-quick-start.png)

## 與事件品質比對分數(EMQ)整合 {#emq}

與事件品質比對分數(EMQ)的整合可讓您藉由顯示EMQ分數，輕鬆檢視實作的成效。 此整合可儘量減少上下文切換，並幫助您提高中繼轉換API實施的成功率。 這些事件分數會顯示在[!UICONTROL Meta Conversions API擴充功能]設定畫面中。

![ [!UICONTROL Meta Conversions API擴充功能]設定頁面醒目提示[!UICONTROL 檢視EMQ分數]。](../../../images/extensions/server/meta/emq-score.png)

## 與LiveRamp (Alpha)整合 {#alpha}

[!DNL LiveRamp]個在其網站上部署了[!DNL LiveRamp]的已驗證流量解決方案(ATS)的客戶可選擇共用RampIDs作為客戶資訊引數。 請與您的[!DNL Meta]帳戶團隊合作，以加入此功能的Alpha計畫。

![中繼事件轉送[!UICONTROL 規則]設定頁面醒目提示[!UICONTROL 合作夥伴名稱(alpha)]和[!UICONTROL 合作夥伴ID (alpha)]。](../../../images/extensions/server/meta/live-ramp.png)

## 設定事件轉送規則 {#rule}

本節說明如何在一般事件轉送規則中使用[!DNL Conversions API]擴充功能。 實際上，您應該設定數個規則，以便透過[!DNL Meta Pixel]和[!DNL Conversions API]傳送所有已接受的[標準事件](https://developers.facebook.com/docs/meta-pixel/reference)。 如需行動應用程式資料，請在[這裡](https://developers.facebook.com/docs/marketing-api/conversions-api/app-events)參閱必要欄位、應用程式資料欄位、客戶資訊引數以及自訂資料詳細資訊。

>[!NOTE]
>
>事件應為[即時傳送](https://www.facebook.com/business/help/379226453470947?id=818859032317965)或儘可能接近即時傳送，以便更佳地最佳化廣告行銷活動。

開始建立新的事件轉送規則，並視需要設定其條件。 為規則選取動作時，請為擴充功能選取&#x200B;**[!UICONTROL Meta Conversions API Extension]**，然後為動作型別選取&#x200B;**[!UICONTROL Send Conversions API Event]**。

![正在為資料收集UI中的規則選取[!UICONTROL 傳送頁面檢視]動作型別。](../../../images/extensions/server/meta/select-action.png)

顯示的控制項可讓您設定將透過[!DNL Conversions API]傳送至[!DNL Meta]的事件資料。 這些選項可以直接輸入到提供的輸入中，或者您可以選取現有的資料元素來代表值。 設定選項分為四個主要區段，如下所述。

| 設定區段 | 說明 |
| --- | --- |
| [!UICONTROL 伺服器事件引數] | 有關事件的一般資訊，包括發生時間和觸發事件的來源動作。 請參閱[!DNL Meta]開發人員檔案，以取得有關[!DNL Conversions API]所接受的[標準事件引數](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/server-event)的詳細資訊。<br><br>如果您同時使用[!DNL Meta Pixel]和[!DNL Conversions API]來傳送事件，請確定每個事件都包含&#x200B;**[!UICONTROL 事件名稱]** (`event_name`)和&#x200B;**[!UICONTROL 事件識別碼]** (`event_id`)，因為這些值用於[事件重複資料刪除](#deduplication)。<br><br>您也可選擇&#x200B;**[!UICONTROL 啟用有限資料使用]**，協助遵守客戶選擇退出的規定。 如需此功能的詳細資訊，請參閱有關[資料處理選項](https://developers.facebook.com/docs/marketing-apis/data-processing-options/)的[!DNL Conversions API]檔案。 |
| [!UICONTROL 客戶資訊引數] | 用於將事件歸因於客戶的使用者身分資料。 在將其中某些值傳送至API之前，必須先進行雜湊處理。<br><br>為確保良好的通用API連線及高事件比對品質(EMQ)，建議您連同伺服器事件一起傳送所有[接受的客戶資訊引數](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/customer-information-parameters)。 這些引數也應根據它們對EMQ](https://www.facebook.com/business/help/765081237991954?id=818859032317965)的重要性和影響來排定[優先順序。 |
| [!UICONTROL 自訂資料] | 用於廣告傳送最佳化的其他資料，以JSON物件的形式提供。 請參閱[[!DNL Conversions API] 檔案](https://developers.facebook.com/docs/marketing-api/conversions-api/parameters/custom-data)，以取得此物件所接受屬性的詳細資訊。<br><br>如果您要傳送購買事件，則必須使用此區段來提供必要的屬性`currency`和`value`。 |
| [!UICONTROL 測試事件] | 此選項用於驗證您的組態是否造成[!DNL Meta]如預期般接收伺服器事件。 若要使用此功能，請選取&#x200B;**[!UICONTROL 以測試事件傳送]**&#x200B;核取方塊，然後在下列輸入中提供您選擇的測試事件程式碼。 在部署事件轉送規則後，如果您已正確設定擴充功能和動作，您應該會在[!DNL Meta Events Manager]的&#x200B;**[!DNL Test Events]**&#x200B;檢視中看到活動。 |

{style="table-layout:auto"}

完成後，選取&#x200B;**[!UICONTROL 保留變更]**&#x200B;以將動作新增至規則設定。

![[!UICONTROL 保留變更]為動作設定選取。](../../../images/extensions/server/meta/keep-changes.png)

如果您對規則感到滿意，請選取&#x200B;**[!UICONTROL 儲存至程式庫]**。 最後，發佈新的事件轉送[組建](../../../ui/publishing/builds.md)，以啟用對程式庫所做的變更。

## 事件重複資料刪除 {#deduplication}

如[必要條件區段](#prerequisites)中所述，建議您同時使用[!DNL Meta Pixel]標籤延伸與[!DNL Conversions API]事件轉送延伸來以備援設定從使用者端與伺服器傳送相同的事件。 這有助於復原其中一個擴充功能未擷取的事件。

如果您從使用者端和伺服器傳送不同的事件型別，且兩者之間沒有重疊，則不需要重複資料刪除。 但是，如果任何單一事件由[!DNL Meta Pixel]和[!DNL Conversions API]共用，您必須確保這些多餘事件會刪除重複專案，以免您的報告受到負面影響。

傳送共用事件時，請務必加入事件ID和名稱，以及您從使用者端和伺服器傳送的每個事件。 收到多個具有相同ID和名稱的事件時，[!DNL Meta]會自動使用數個策略來重複刪除這些事件，並保留最相關的資料。 如需此程式的詳細資訊，請參閱有關 [!DNL Meta Pixel] 和 [!DNL Conversions API] 事件](https://www.facebook.com/business/help/823677331451951?id=1205376682832142)的[重複資料刪除的[!DNL Meta]檔案。

## 快速入門工作流程：中繼轉換API擴充功能(Beta) {#quick-start}

>[!IMPORTANT]
>
>* 已購買Real-Time CDP Prime和Ultimate套件的客戶可以使用快速入門功能。 如需詳細資訊，請聯絡您的Adobe代表。
>* 此功能適用於全新實作，目前不支援在現有標籤和事件轉送屬性上自動安裝擴充功能和設定。

>[!NOTE]
>
>任何現有使用者端都可使用快速入門工作流程建立可供下列專案使用的參考實作：
>* 作為全新實作的開始。
>* 將其當作參考實作，您可以檢查以瞭解其設定方式，然後在目前的生產實作中複製。

快速入門功能可協助您使用中繼轉換API和中繼畫素擴充功能輕鬆而高效地完成設定。 此工具會自動執行在Adobe標籤和事件轉送中執行的多個步驟，大幅縮短設定時間。

此功能會在新自動產生的標籤上自動安裝及設定中繼轉換API和中繼畫素擴充功能，並使用必要的規則和資料元素來設定事件轉送屬性。 此外，也會自動安裝及設定Experience Platform Web SDK和資料流。 最後，快速入門功能會自動將程式庫發佈到開發環境中的指定URL，如此即可透過事件轉送和Experience PlatformEdge Network即時啟用使用者端資料收集和伺服器端事件轉送。

以下影片介紹快速入門功能。

>[!VIDEO](https://video.tv.adobe.com/v/3416939?quality=12&learn=on)

### 安裝快速入門功能

>[!NOTE]
>
>此功能旨在協助您開始實施事件轉送。 它不會提供端對端、功能齊全的實施，以配合所有使用案例。

此設定會自動安裝中繼轉換API和中繼畫素擴充功能。 Meta建議使用此混合式實作，以收集並轉寄事件轉換伺服器端。
快速設定功能旨在協助客戶開始事件轉送實作，而非旨在提供因應所有使用案例的端對端完整功能實作。

若要安裝此功能，請在Adobe Experience Platform資料彙集&#x200B;**[!UICONTROL 首頁]**&#x200B;頁面上選取&#x200B;**[!DNL Send Conversions Data to Meta]**&#x200B;的&#x200B;**[!UICONTROL 開始使用]**。

![資料彙集首頁顯示中繼資料的轉換](../../../images/extensions/server/meta/conversion-data-to-meta.png)

輸入您的&#x200B;**[!UICONTROL 網域]**，然後選取&#x200B;**[!UICONTROL 下一步]**。 此網域將用作您自動產生的標籤和事件轉送屬性、規則、資料元素、資料串流等的命名慣例。

![要求網域名稱的歡迎畫面](../../../images/extensions/server/meta/welcome.png)

在&#x200B;**[!UICONTROL 初始設定]**&#x200B;對話方塊中，輸入您的&#x200B;**[!UICONTROL 中繼畫素ID]**、**[!UICONTROL 中繼轉換API存取權杖]**&#x200B;和&#x200B;**[!UICONTROL 資料層路徑]**，然後選取&#x200B;**[!UICONTROL 下一步]**。

![初始設定對話方塊](../../../images/extensions/server/meta/initial-setup.png)

請等候幾分鐘讓初始設定程式完成，然後選取&#x200B;**[!UICONTROL 下一步]**。

![初始設定完成確認畫面](../../../images/extensions/server/meta/setup-complete.png)

從&#x200B;**[!UICONTROL 在您的網站上新增程式碼]**&#x200B;對話方塊中，複製使用複製![複製](../../../images/extensions/server/meta/copy-icon.png)函式提供的程式碼，並將其貼到來源網站的`<head>`中。 實作之後，請選取&#x200B;**[!UICONTROL 開始驗證]**

![在您的網站對話方塊上新增程式碼](../../../images/extensions/server/meta/add-code-on-your-site.png)

[!UICONTROL 驗證結果]對話方塊會顯示中繼延伸實作結果。 選取&#x200B;**[!UICONTROL 下一步]**。 您也可以選取&#x200B;**[!UICONTROL 保證]**&#x200B;連結，以檢視其他驗證結果。

![顯示實作結果的測試結果對話方塊](../../../images/extensions/server/meta/test-results.png)

**[!UICONTROL 後續步驟]**&#x200B;畫面顯示確認安裝完成。 從這裡，您可以選擇新增事件以最佳化實施，如下節所示。

如果您不想新增其他事件，請選取&#x200B;**[!UICONTROL 關閉]**。

![後續步驟對話方塊](../../../images/extensions/server/meta/next-steps.png)

#### 新增其他事件

若要新增事件，請選取&#x200B;**[!UICONTROL 編輯您的標籤網頁屬性]**。

![顯示編輯標籤網頁屬性的後續步驟對話方塊](../../../images/extensions/server/meta/edit-your-tags-web-property.png)

選取與您要編輯之中繼事件對應的規則。 例如，**MetaConversion_AddToCart**。

>[!NOTE]
>
>如果沒有事件，此規則將不會執行。 所有規則都是如此，**MetaConversion_PageView**&#x200B;規則為例外。

若要新增事件，請選取[!UICONTROL 事件]標題下的&#x200B;**[!UICONTROL 新增]**。

![標籤屬性頁面未顯示任何事件](../../../images/extensions/server/meta/edit-rule.png)

選取[!UICONTROL 事件型別]。 在此範例中，我們已選取[!UICONTROL Click]事件，並將其設定為選取&#x200B;**.add-to-cart-button**&#x200B;時觸發。 選取&#x200B;**[!UICONTROL 保留變更]**。

![顯示點選事件的事件設定畫面](../../../images/extensions/server/meta/event-configuration.png)

已儲存新事件。 選取&#x200B;**[!UICONTROL 選取工作程式庫]**&#x200B;並選取您要建置的程式庫。

![選取工作程式庫下拉式清單](../../../images/extensions/server/meta/working-library.png)

接著，選取&#x200B;**[!UICONTROL 儲存至程式庫]**&#x200B;旁的下拉式清單，並選取&#x200B;**[!UICONTROL 儲存至程式庫並建置]**。 這會在程式庫中發佈變更。

![選取儲存至程式庫並建置](../../../images/extensions/server/meta/save-and-build.png)

對您要設定的任何其他中繼轉換事件重複這些步驟。

#### 資料層設定 {#configuration}

>[!IMPORTANT]
>
>您更新此全域資料層的方式取決於您的網站架構。 單一頁面應用程式將與伺服器端轉譯應用程式不同。 此外，您可能將完全負責在Tags產品內建立和更新此資料。 在所有執行個體中，在執行每個`MetaConversion_* rules`之間，都需要更新資料層。 如果您沒有在規則之間更新資料，您也可能遇到傳送來自目前`MetaConversion_* rule`中最後`MetaConversion_* rule`個過時資料的情況。

在設定期間，系統會詢問您資料層的所在位置。 預設為`window.dataLayer.meta`，在`meta`物件內，您的資料應如下所示。

![資料層中繼資訊](../../../images/extensions/server/meta/data-layer-meta.png)

這是很重要的一點，因為每個`MetaConversion_*`規則都使用此資料結構來傳遞相關資料片段至[!DNL Meta Pixel]擴充功能和[!DNL Meta Conversions API]。 請參閱[標準事件](https://developers.facebook.com/docs/meta-pixel/reference#standard-events)的相關檔案，以取得不同中繼事件需要哪些資料的詳細資訊。

例如，如果您想要使用`MetaConversion_Subscribe`規則，則需要根據[標準事件](https://developers.facebook.com/docs/meta-pixel/reference#standard-events)的檔案中所述的物件屬性來更新`window.dataLayer.meta.currency`、`window.dataLayer.meta.predicted_ltv`和`window.dataLayer.meta.value`。

以下範例說明執行規則前，需要在網站上執行哪些動作以更新資料層。

![更新資料層中繼資訊](../../../images/extensions/server/meta/update-data-layer-meta.png)

根據預設，`<datalayerpath>.conversionData.eventId`將會由任何`MetaConversion_* rules`上的「產生新事件ID」動作隨機產生。

如需資料層外觀的本機參考，您可以在屬性上的`MetaConversion_DataLayer`資料元素上開啟自訂程式碼編輯器。

## 後續步驟

本指南說明如何使用[!DNL Meta Conversions API]擴充功能將伺服器端事件資料傳送至[!DNL Meta]。 從此處，建議您連線更多[!DNL Pixels]並共用更多事件（如適用）以擴大整合。 執行下列任一項作業有助於進一步改善廣告效能：

* 連線尚未連線到[!DNL Conversions API]整合的任何其他[!DNL Pixels]。
* 如果您只透過使用者端的[!DNL Meta Pixel]傳送某些事件，請一併從伺服器端傳送這些相同事件至[!DNL Conversions API]。

如需有關如何有效實作整合的更多指引，請參閱 [!DNL Conversions API]](https://www.facebook.com/business/help/308855623839366?id=818859032317965)之[最佳實務的[!DNL Meta]檔案。 如需Adobe Experience Cloud中標籤與事件轉送的一般詳細資訊，請參閱[標籤總覽](../../../home.md)。
