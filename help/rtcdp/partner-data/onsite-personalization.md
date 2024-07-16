---
title: 使用合作夥伴協助的訪客辨識功能，為未知訪客提供個人化的現場體驗
description: 了解如何使用合作夥伴輔助的訪客識別為訪客提供個人化的現場體驗。
feature: Use Cases, Personalization, Customer Acquisition
exl-id: 99677988-1df8-47b1-96b1-0ef6db818a1d
source-git-commit: 5b37b51308dc2097c05b0e763293467eb12a2f21
workflow-type: tm+mt
source-wordcount: '2673'
ht-degree: 90%

---

# 使用合作夥伴協助的訪客辨識功能，為未知訪客提供個人化的現場體驗

>[!AVAILABILITY]
>
>已授權Real-Time CDP （應用程式服務）、Adobe Experience Platform Activation、Real-Time CDP、Real-Time CDP Prime、Real-Time CDP Ultimate的客戶可使用此功能。 如需詳細資訊，請閱讀[產品說明](https://helpx.adobe.com/legal/product-descriptions.html)中有關這些套件的詳細資料，並和您的 Adob&#x200B;&#x200B;e 代表聯絡。

了解如何使用合作夥伴輔助的訪客識別為您的 Web 屬性訪客提供個人化的現場體驗。使用本教學課程了解 Experience Platform 和其他 Experience Cloud 解決方案中各種元素的實施順序，以便向經過身分驗證和未經身分驗證的訪客顯示個人化體驗。

![資訊圖：說明如何使用合作夥伴提供的屬性為訪客供個人化體驗。](/help/rtcdp/assets/partner-data/onsite-personalization/onsite-personalization-overview.png)

## 為何考慮此使用案例 {#why-this-use-case}

消費者以各種方式與品牌互動時，數位體驗呈現片段化是很真實的，而且越來越難以解決。 針對凝聚式體驗、鎖定目標的建議和量身打造的互動的最佳客戶參與策略，全都受到使用者認知度的限制。

這是合作夥伴協助的即時辨識可帶來有意義的差異之處。 Adobe可讓身分識別合作夥伴瞭解我們複雜的使用者端資料收集和領先市場的體驗最佳化產品，有效提升體驗傳送的標準（從第一次造訪開始），無需先前的記錄或驗證。

這對於驗證率低的垂直市場尤其有用，例如消費性包裝商品、線上零售等。

## 行業範例 {#industry-example}

舉個例子，考慮一個認證率較低的家居修繕品牌。該品牌希望為首次訪客提供個人化體驗，無需以前的歷史記錄或事先身分驗證，也不會逐漸依賴協力廠商 cookie。

該品牌選擇運用合作夥伴識別技術，以概率方式來識別訪客並提供更加個人化的體驗。當訪客順著行銷漏斗向下移動時，這有助於提高考慮度。例如，該品牌可能會使用合作夥伴提供的人口統計訊號來製作吸引最近搬家者的現場內容，並針對受歡迎 DIY 產品提供折扣優惠。

## 必要條件和規劃 {#prerequisites-and-planning}

當計劃使用合作夥伴提供的屬性向經過身分驗證和未經身分驗證的訪客提供個人化體驗時，請在規劃過程中考慮以下先決條件：

* 您合作夥伴的識別技術需要輸入哪些資料，以便他們能夠疊加其他屬性？
* 根據機率衍生的資料集和決定確認的屬性，您在多大程度上可以輕鬆地在不同頻道中並針對不同使用案例提供個人化？
* 預先經過身分驗證但已經過識別的訪客在進行身分驗證時，他們的體驗應該如何改變？

### 您將使用的 UI 功能、平台元件和 Experience Cloud 產品 {#ui-functionality-and-elements}

若要成功實施此使用案例，您必須使用多個區域的 Real-Time Customer Data Platform 和其他 Experience Cloud 解決方案。確保您擁有所有這些區域所需的[屬性型存取控制權限](/help/access-control/abac/overview.md)，或要求系統管理員授予您必要的權限。

* 資料收集
   * [Adobe Experience Platform Web SDK](/help/web-sdk/home.md)
   * [標記](/help/tags/home.md)
   * [資料流](/help/datastreams/overview.md)
* Real-Time CDP 中的資料管理
   * [身分](/help/identity-service/features/namespaces.md)
   * [結構描述](/help/xdm/home.md)
   * [資料使用情況標籤](/help/data-governance/labels/overview.md)
   * [資料集](/help/catalog/datasets/overview.md)
*  Web 屬性個人化
   * [邊緣分段](/help/segmentation/ui/edge-segmentation.md)
   * [邊緣個人化目的地](/help/destinations/destination-types.md#edge-personalization-destinations)
   * [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) (或您選擇的個人化平台。本使用案例教學課程旨在重點介紹以 Adobe Target 作為個人化引擎)

## 影片逐步解說 {#video-walkthrough}

觀看下方的影片教學課程，逐步瞭解如何為未知訪客個人化網站上的體驗：

>[!VIDEO](https://video.tv.adobe.com/v/3423076/?learn=on)

## 如何實現使用案例：高層級概觀 {#achieve-the-use-case-high-level}

![資訊圖：說明如何使用合作夥伴提供的屬性為訪客供個人化體驗。](/help/rtcdp/assets/partner-data/onsite-personalization/onsite-personalization-steps.png)

1. 作為&#x200B;**客戶**，您可授權&#x200B;**資料合作夥伴**&#x200B;有能力即時擷取對其他匿名網站訪客的分析。
2. 作為&#x200B;**訪客**，您可在自己的屬性上部署用戶端資料庫，以呼叫&#x200B;**合作夥伴** API，且您可設定 Web SDK 或行動 SDK 並將合作夥伴提供的訊號發送到 Real-Time CDP。
3. 瀏覽您的網站或應用程式時，**訪客**&#x200B;是由&#x200B;**合作夥伴**&#x200B;進行概率識別；合作夥伴會傳回屬性和 ID。
4. Real-Time CDP 會執行邊緣分段來評估導入事件點擊，並持續從 [ECID 識別碼](https://experienceleague.adobe.com/docs/id-service/using/home.html)得到結果。
5. Adobe Target 使用邊緣分段輸出將體驗回供給&#x200B;**訪客**，讓他們的工作階段得到個人化體驗。
6. 該事件將完整地保留下來，進行如分析和重新鎖定的下游工作流程。

## 如何實現使用案例：逐步說明 {#step-by-step-instructions}

詳閱以下章節，其中包含指向更多文件的連結，以完成上述高層級概觀中的每個步驟。

### 資料管理 - 建立身分識別命名空間、結構描述和資料集，以便管理資料屬性 {#data-management}

在準備為實現使用案例以便為未經身分驗證訪客的體驗進行個人化時，您必須首先在 Real-Time CDP 中設定資料管理結構，以接收傳入的即時事件和對象資格資料。

#### 建立合作夥伴 ID 身分識別命名空間

首先，您需要建立一個合作夥伴 ID 的身分識別命名空間。導覽至左側欄內的&#x200B;**[!UICONTROL 客戶]**>**[!UICONTROL 身分識別]**，然後在螢幕右上方選取「**[!UICONTROL 建立身分識別命名空間]**」。

![「建立身分識別命名空間」對話框及合作夥伴 ID 是以醒目顯示。](/help/rtcdp/assets/partner-data/onsite-personalization/create-identity-namespace.png)

閱讀更多關於如何[建立合作夥伴 ID 的身分識別命名空間](/help/rtcdp/partner-data/prospecting.md#create-partner-id-namespace)。

#### 建立結構描述

接下來，建立一個[!UICONTROL 體驗事件]結構描述，用來保存您稍後將從 Web 屬性收集的時間序列資料，並確保使用 [!UICONTROL XDM ExperienceEvent] 作為結構描述的基礎類別。閱讀有關如何[使用 Experience Platform UI 建立結構描述](/help/xdm/ui/resources/schemas.md#create)。

![具備「建立」結構描述的結構描述工作區，且 XDM Experience 事件以醒目顯示。](/help/rtcdp/assets/partner-data/onsite-personalization/create-experience-event-schema.png)

當您建立結構描述並[將欄位新增至您的結構描述](/help/xdm/ui/resources/schemas.md#add-field-groups)，考慮新增「[造訪 Web 頁面](/help/xdm/field-groups/event/web-details.md)」和「[身分識別地圖](/help/xdm/field-groups/profile/identitymap.md)」欄位群組。這是適用於您數位資產和資料收集方法的其他新增欄位群組。

此外，您可以建立或重複使用現有欄位群組並將其新增至您的結構描述，以擷取作夥伴提供關於訪客的見解。閱讀如何[建立欄位群組](/help/xdm/ui/resources/field-groups.md)以及如何[新增欄位](/help/xdm/ui/resources/field-groups.md)至欄位群組。例如，如果您希望針對合作夥伴所提供的分析 (例如年齡範圍、就業狀況、每月消費能力或購買行為) 進行個人化，請將您的欄位群組加入有關的欄位。

假設資料合作夥伴為訪客提供了穩定的識別碼，並且您希望將其引入 Real-Time CDP，請務必在自訂欄位群組中為識別碼提供適當命名的欄位。您應該還要在之前建立的身分識別命名空間中將該欄位標示為身分識別。記得還要[讓結構描述包含在設定檔中](/help/xdm/ui/resources/schemas.md#profile)。

#### 建立資料集

接下來，您必須建立一個資料集來保存您從 Web 屬性訪客收集的時間序列資料，以及保存您將用於現場個人化的時間序列資料。

閱讀有關[如何建立資料集](/help/catalog/datasets/user-guide.md#create)的教學課程，並記得要選取從結構描述建立資料集的選項。根據您在上一步建立的結構描述來建立資料集。

與建立結構描述的步驟類似，您需要讓資料集包含在[!UICONTROL 即時客戶設定檔]中。如需進一步了解關於啟用資料集以用於[!UICONTROL 即時客戶設定檔]，請閱讀[建立結構描述教學課程](/help/xdm/tutorials/create-schema-ui.md#profile)。

### 在您的 Web 屬性上實施事件資料收集 {#implement-data-collection}

進行您的資料管理配定後，您現在需要在您的 Web 屬性上實施即時事件的[資料收集](/help/collection/home.md)。您需要使用 Adobe 資籵收集庫來檢測您的屬性 -[!UICONTROL Web SDK] - 收集即時事件呼叫並將其發送回 Real-Time CDP。該項目由跨多個資料收集元件的數項個別任務組成。

>[!IMPORTANT]
>
>若要擷取合作夥伴提供的屬性，您還必須&#x200B;*將您的 Web 屬性與合作夥伴 API 或其他方法整合，以即時方式呼叫和擷取資料合作夥伴的屬性*。請與您選擇的合作夥伴討論這個方面，因為這不是本教學課程的主題。

首先，使用螢幕右上角的應用程式切換器導覽至&#x200B;**[!UICONTROL 資料收集]**&#x200B;部分。

>[!TIP]
>
>如果您在應用程式切換器中看不到[!UICONTROL 資料收集]，請聯絡您的系統管理員並要求存取權。

![應用程式切換器可進入資料收集部分。](/help/rtcdp/assets/partner-data/onsite-personalization/app-switcher-data-collection.png)

UI 的&#x200B;**[!UICONTROL 資料收集]**&#x200B;部分看起來類似於下影像。

![Platform UI 的資料收集部分。](/help/rtcdp/assets/partner-data/onsite-personalization/data-collection-home.png)

#### 建立資料流

資料收集部分的第一步，[建立一個新的資料流](/help/datastreams/configure.md)。資料流是如何收集資料並將資料以正確路由發送到正確 Adobe 應用程式 (在本例中為 Experience Platform) 的基礎。

當您建立資料流時，在&#x200B;**[!UICONTROL 事件結構描述]**&#x200B;欄位中，選取您之前建立的結構描述。

![設定新資料流時醒目顯示的事件結構描述選擇器。](/help/rtcdp/assets/partner-data/onsite-personalization/event-schema-selector-datastream.png)

[選取事件資料集](/help/datastreams/configure.md#aep) (您之前從下拉式選單建立)，勾選&#x200B;**[!UICONTROL 邊緣分割]**&#x200B;和&#x200B;**[!UICONTROL 個人化目的地]**&#x200B;旁邊的方格，然後選取「**[!UICONTROL 儲存]**」。

請注意，在此場境中您不必選取設定檔資料集，因為您引入的是以事件為主的時間序列資料。

#### 建立標記屬性

將屬性視為是一個容器，當您將標記部署至網站時，在其中裝入擴充功能、規則、資料元素和程式庫。

導覽至&#x200B;**[!UICONTROL 標記]**&#x200B;並選取&#x200B;**[!UICONTROL 全新屬性]**。

![建立新的標記屬性。](/help/rtcdp/assets/partner-data/onsite-personalization/create-tag-property.png)

填寫必填欄位並選取「**[!UICONTROL 儲存]**」。

![為您的新屬性填寫必填欄位。](/help/rtcdp/assets/partner-data/onsite-personalization/tag-property-fields.png)

取得有關如何[建立標記屬性](https://experienceleague.adobe.com/docs/platform-learn/implement-in-websites/configure-tags/create-a-property.html)的完整資訊。

接下來，您必須在屬性內安裝各種擴充功能。選取您的標記屬性，並導覽至[!UICONTROL 擴充功能]部分。

![選取您的新標記屬性。](/help/rtcdp/assets/partner-data/onsite-personalization/select-tag-property.png)

請注意，[!UICONTROL 核心]擴充功能已安裝。您必須安裝另外兩個擴充功能 (依接下來部份的詳述)。

![檢視已安裝的擴充功能。](/help/rtcdp/assets/partner-data/onsite-personalization/view-existing-extensions.png)

#### 安裝 Web SDK 擴充功能

請注意，本教學課程旨在說明如何使用 Web SDK 檢測您的網站。您還可以在您的應用程式上使用[行動 SDK](https://developer.adobe.com/client-sdks/documentation/)，為您的應用程式訪客提供個人化體驗。

![檢視擴充功能目錄中的 Web SDK 擴充功能。](/help/rtcdp/assets/partner-data/onsite-personalization/web-sdk-extension.png)

在設定 Web SDK 螢幕中，向下導覽至&#x200B;**[!UICONTROL 資料流]**&#x200B;部分，並提供有關您正在使用的 Experience Platform 沙箱資訊。從下一個下拉式選單中，選取適當的沙箱以及在前面步驟中建立的資料流。您可以為所有其他環境選擇相同的沙箱和資料流數值。保持其他設定不變並選取「**[!UICONTROL 儲存]**」。

取得[如何安裝 Web SDK](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/tags-configuration/install-web-sdk.html)的完整資訊。

#### 安裝 ID 服務擴充功能

使用 [Experience Cloud ID 服務擴充功能](/help/tags/extensions/client/id-service/overview.md)，為所有 Experience Cloud 解決方案的訪客建立以裝置為主的獨特第一方身分識別。在擴充功能中搜尋&#x200B;**[!UICONTROL ID 服務]**&#x200B;並安裝。安裝擴充功能時保留所有預設設定。

![擴充功能目錄中的 ID 服務擴充功能視圖。](/help/rtcdp/assets/partner-data/onsite-personalization/id-service-extension.png)

#### 設定環境

接下來，從左側導覽前往&#x200B;**[!UICONTROL 環境]**&#x200B;部分在此步驟中，您必須將您的網站連接到 Adobe Edge Network，以便即時擷取並提供訪客資訊。

選擇右邊開發環境的方格圖示，然後複製模式視窗中顯示的 JavaScript 代碼片段標準版本。

![選取資料收集 UI 環境部分中醒目顯示的方格圖示。](/help/rtcdp/assets/partner-data/onsite-personalization/select-box-icon.png)

您必須將此代碼片段新增至網站最上方。因此，您的網站將呼叫 Adobe Edge Network，以擷取將在頁面載入和執行的 JavaScript 邏輯。這樣就可以實施訪客 ID 生成、資料收集和即時體驗個人化等功能。

#### 設定資料元素

資料元素是資料字典 (或資料地圖) 的建置組塊。單一資料元素是變數，其值可對應至查詢字串、URL、Cookie 值、JavaScript 變數等資料。閱讀更多關於[資料元素](/help/tags/ui/managing-resources/data-elements.md)。

為了這項使用案例的目的，您必須設定兩個資料元素。

首先，設定一個 `partnerData` 元素。導覽至&#x200B;**[!UICONTROL 資料元素]**&#x200B;部分，然後選取&#x200B;**[!UICONTROL 建立新資料元素]**。

![建立新資料元素。](/help/rtcdp/assets/partner-data/onsite-personalization/create-data-element.gif)

為資料元素命名`partnerData`，將[!UICONTROL 擴充功能]的值留為[!UICONTROL 核心]，並將&#x200B;**[!UICONTROL 資料元素類型]**&#x200B;設定為&#x200B;**[!UICONTROL JavaScript 變數]**。在標題為「**[!UICONTROL JavaScript 變數名稱]**」的欄位內輸入 `partnerData`，並選取「**[!UICONTROL 儲存]**」。

![醒目顯示正確設定 PartnerData 資料元素的選擇。](/help/rtcdp/assets/partner-data/onsite-personalization/create-partnerdata-data-element.png)

若要設定第二個資料元素，請為新變數 `pageVisit` 命名，設定&#x200B;**[!UICONTROL 擴充功能]**&#x200B;至 **[!UICONTROL Adobe Experience Platform]**，並選擇&#x200B;**[!UICONTROL XDM 物件]**&#x200B;作為資料類型。

![醒目顯示正確設定 pageVisit 資料元素的選擇。](/help/rtcdp/assets/partner-data/onsite-personalization/page-visit-data-element.png)

從結構描述中，依據您期望從資料合作夥伴獲得的值，選取與其相對應的協力廠商屬性。然後，選擇標題為「**[!UICONTROL 提供整個物件]**」的選項按鈕。選擇看起來像資料庫的圖示，然後選擇您之前建立的 `partnerData` 資料元素。

#### 設定規則

在&#x200B;**[!UICONTROL 規則]**&#x200B;部分內，您可以將您的網站設定為 Adobe 發送個人化請求，並將屬性載入您剛才建立的資料元素中。閱讀更多關於[建立規則](/help/tags/ui/managing-resources/rules.md)。

選取「**[!UICONTROL 建立新規則]**」。將該規則命名為「**[!UICONTROL 個人化]**」，然後選取&#x200B;**[!UICONTROL 事件]**&#x200B;旁邊的 + 號。選取「**[!UICONTROL 頁底]**」作為事件並儲存。

![規則事件類型部分的選擇。](/help/rtcdp/assets/partner-data/onsite-personalization/add-events-rule.png)

選擇「**[!UICONTROL 動作]**」旁邊的 + 號。將擴充功能更新至 **[!UICONTROL Adobe Experience Platform Web SDK]**，並設定&#x200B;**[!UICONTROL 動作類型]**&#x200B;為「**[!UICONTROL 發送事件]**」。

![規則動作類型部分的選擇。](/help/rtcdp/assets/partner-data/onsite-personalization/add-action-rule.png)

從右邊「**[!UICONTROL 類型]**」下拉式選單選擇器中，選取 `web.webpagedetails.pageViews` 作為事件類型。

![選取事件類型。](/help/rtcdp/assets/partner-data/onsite-personalization/add-pageview-type-rule.png)

選取 XDM 資料旁邊的資料庫圖示，然後選取 `pageVisit` 資料元素。

將動作設定清單向下捲動，且務必勾選標題為「**[!UICONTROL 呈現視覺個人化決定]**」。若要透過 Adobe Target 或其他類似產品傳遞在網頁上呈現視覺效果的體驗，這項設定非常重要。選取「**[!UICONTROL 保留變更]**」，然後「**[!UICONTROL 儲存]**」規則。

![選取「呈現視覺個人化決定」勾選方格。](/help/rtcdp/assets/partner-data/onsite-personalization/render-visual-personalization-toggle.png)

#### 設定發佈工作流程

若要將此設定部署到網頁，下一步是建立一個資料庫且含有您剛才建立的資源。閱讀更多關於[設定發佈流程](/help/tags/ui/publishing/publishing-flow.md)。

選取「**[!UICONTROL 發佈流程]**」，然後&#x200B;**[!UICONTROL 新增資料庫]**。

選取「**[!UICONTROL 新增所有變更的資源]**」，為資料庫命名，將環境設定為「**[!UICONTROL 開發]**」，並選取「**[!UICONTROL 儲存並建置至開發]**」。

![建立資料庫並部署到開發環境](/help/rtcdp/assets/partner-data/onsite-personalization/create-publishing-workflow.gif)

#### 測試您的網站

此時，您的網站應該已完全經過 Web SDK 的檢測。若要測試資料收集是否按預期進行，您可以導覽至您的網站並使用瀏覽器的開發人員工具來檢查網絡流量。

在搜尋方塊中輸入 `interact`、重新整理頁面，您應該會看到您網站呼叫網絡進行 Adobe Edge 網絡填入。

![開發人員工具中網絡事件填入的視圖。](/help/rtcdp/assets/partner-data/onsite-personalization/events-filtered.png)

### 個人化 {#personalization}

您現在已準備好建立並啟動對象進行個人化。

#### 建立對象並設定邊緣細分

在Platform UI中，導覽至&#x200B;**[!UICONTROL 客戶]** > **[!UICONTROL 對象]**，並建立對象以擷取您的網站訪客。

![如何導覽至對象的檢視。](/help/rtcdp/assets/partner-data/onsite-personalization/navigate-to-audiences.png)

您必須使用[邊緣細分](/help/segmentation/ui/edge-segmentation.md)設定您的對象，以便在訪客造訪您的Web屬性時，即時評估訪客的對象成員資格。

還要確保為邊緣對象設定一項「[有效邊緣合併原則](/help/destinations/ui/activate-edge-personalization-destinations.md#create-merge-policy)。

#### 與 Adobe Target 或其他自訂個人化目的地整合

您現在已準備就緒可與個人化引擎整合，並向您網站上或應用程式的訪客顯示個人化內容。Adobe 建議為此目的使用 [Adobe Target 目的地](/help/destinations/catalog/personalization/adobe-target-connection.md)。

>[!IMPORTANT]
>
>閱讀有關[對邊緣個人化目的地啟用對象](/help/destinations/ui/activate-edge-personalization-destinations.md)，了解啟用對象所需步驟的完整情況。

## 限制和疑難排解 {#limitations-and-troubleshooting}

當您探索本頁說明的使用案例時，請注意下列限制：

* 如果您使用合作夥伴 ID，請注意在建置您的[身分識別圖譜](/help/identity-service/features/identity-graph-viewer.md)時不要使用這些 ID。

## 其他透過合作夥伴資料支援封存的使用案例 {#other-use-cases}

探索透過 Real-Time CDP 中的合作夥伴資料支援啟用的更多使用案例：

* [使用受信任資料合作夥伴的屬性來補充第一方設定檔，以改善您的資料基礎並對客戶群取得新的分析，而且獲致更佳的對象最佳化。](/help/rtcdp/partner-data/supplement-first-party-profiles.md)
* 使用 Real-Time CDP 的協力廠商資料支援，透過資料合作夥伴的潛在客戶設定檔來[擴大您的設定檔庫，並與其互動以獲取或接觸新客戶。](/help/rtcdp/partner-data/prospecting.md)
* [擴大啟用潛在客戶個人資料和潛在客戶對象](/help/destinations/ui/activate-prospect-audiences.md)以選取目的地。
