---
title: 使用合作夥伴協助的訪客辨識，提供個人化的站上體驗
description: 瞭解如何使用合作夥伴協助的訪客辨識，為訪客提供個人化的現場體驗。
hide: true
hidefromtoc: true
source-git-commit: f63cddc1158e739ce26e0ce1d3d54b491bd80c06
workflow-type: tm+mt
source-wordcount: '2493'
ht-degree: 7%

---

# 使用合作夥伴協助的訪客辨識，提供個人化的站上體驗

瞭解如何使用合作夥伴協助的辨識，為您的Web屬性訪客提供個人化體驗。 使用本教學課程瞭解Experience Platform和其他Experience Cloud解決方案中各種元素的實作順序，向已驗證和未驗證的訪客顯示個人化體驗。

![此資訊圖表說明如何使用合作夥伴提供的屬性，為訪客提供個人化體驗。](/help/rtcdp/assets/partner-data/onsite-personalization/onsite-personalization-steps.png)

## 產業範例 {#industry-example}

例如，考慮低驗證率的家用改善品牌。 此品牌想要為首次造訪的訪客提供個人化體驗，而無先前的記錄或驗證，且對第三方Cookie的依賴程度不會下降。

此品牌選擇運用合作夥伴辨識技術，儘可能辨識訪客，並提供更個人化的體驗。 當訪客在行銷漏斗中向下移動時，這有助於提高考量。 例如，該品牌可能會針對網站上的內容使用合作夥伴提供的人口統計訊號，以吸引最近搬家的人，並提供熱門DIY產品的折扣。

## 必要條件和規劃 {#prerequisites-and-planning}

規劃使用合作夥伴提供的屬性，將個人化體驗提供給已驗證和未驗證的訪客時，請在規劃程式中考慮下列必要條件：

* 您合作夥伴的辨識技術需要哪些輸入，才能將其置於其他屬性上？
* 根據可能衍生的屬性與確定性確認的屬性相比，您在多大程度上願意在不同管道以及不同使用案例中提供個人化？
* 已預先驗證但已識別的訪客在驗證時，其體驗應該如何變更？

### 您將使用的UI功能、平台元件和Experience Cloud產品 {#ui-functionality-and-elements}

若要成功實作此使用案例，您必須使用Real-time Customer Data Platform和其他Experience Cloud解決方案的多個區域。 確定您具備必要的 [以屬性為基礎的存取控制許可權](/help/access-control/abac/overview.md) 或要求系統管理員授與您必要的許可權。

* 資料集合
   * [Adobe Experience Platform Web SDK](/help/edge/home.md)
   * [標記](/help/tags/home.md)
   * [資料流](/help/datastreams/overview.md)
* Real-Time CDP的資料管理
   * [身分](/help/identity-service/namespaces.md)
   * [結構描述](/help/xdm/home.md)
   * [資料使用情況標籤](/help/data-governance/labels/overview.md)
   * [資料集](/help/catalog/datasets/overview.md)
* Web屬性個人化
   * [邊緣細分](/help/segmentation/ui/edge-segmentation.md)
   * [Edge Personalization目的地](/help/destinations/destination-types.md#edge-personalization-destinations)
   * [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) （或您選擇的個人化平台）。 此使用案例教學課程強調Adobe Target作為個人化引擎)

## 如何實現使用案例：高層級概觀 {#achieve-the-use-case-high-level}

![此資訊圖表說明如何使用合作夥伴提供的屬性，為訪客提供個人化體驗。](/help/rtcdp/assets/partner-data/onsite-personalization/onsite-personalization-steps.png)

1. 作為 **客戶**，您從中取得授權 **資料合作夥伴** 能夠即時擷取對其他匿名網站訪客的深入分析。
2. 作為 **客戶**，您可在您的屬性上部署使用者端程式庫來呼叫 **合作夥伴** API和您設定Web SDK或Mobile SDK，將合作夥伴提供的訊號傳送至Real-Time CDP。
3. 瀏覽您的網站或應用程式時， **訪客** 可能會被 **合作夥伴**，會連同ID一起傳回屬性。
4. Real-Time CDP會執行邊緣分段，以評估傳入的事件點選，並將結果儲存在 [ECID識別碼](https://experienceleague.adobe.com/docs/id-service/using/home.html).
5. Adobe Target使用邊緣分段輸出，將體驗呈現回 **訪客** 用於工作階段內個人化。
6. 分析和重新目標定位等下游工作流程會完整保留此事件。

## 如何實現使用案例：逐步說明 {#step-by-step-instructions}

詳閱以下章節，其中包含指向更多文件的連結，以完成上述高層級概觀中的每個步驟。

### 資料管理 — 建立身分名稱空間、結構和資料集以管理資料屬性 {#data-management}

為了達成使用案例來個人化未經驗證訪客的體驗，您必須先在Real-Time CDP中設定資料管理結構，以接收傳入的即時事件和對象資格資料。

#### 建立合作夥伴ID身分名稱空間

首先，您需要建立合作夥伴ID身分名稱空間。 瀏覽至 **[!UICONTROL 客戶]** > **[!UICONTROL 身分]** 在左側邊欄中，然後選取 **[!UICONTROL 建立身分名稱空間]** 在畫面的右上角。

![會醒目顯示合作夥伴ID的「建立身分名稱空間」對話方塊。](/help/rtcdp/assets/partner-data/onsite-personalization/create-identity-namespace.png)

深入瞭解如何 [建立合作夥伴ID身分名稱空間](/help/rtcdp/partner-data/prospecting.md#create-partner-id-namespace).

#### 建立方案

接下來，建立 [!UICONTROL 體驗事件] 結構描述，用來儲存您稍後將從Web屬性收集的時間序列資料，並確定使用 [!UICONTROL XDM ExperienceEvent] 做為結構描述的基底類別。 閱讀如何 [使用Experience Platform UI建立結構描述](/help/xdm/ui/resources/schemas.md#create).

![包含建立結構描述和XDM體驗事件的結構描述工作區會反白顯示。](/help/rtcdp/assets/partner-data/onsite-personalization/create-experience-event-schema.png)

當您建立結構描述和 [將欄位群組新增到您的結構描述](/help/xdm/ui/resources/schemas.md#add-field-groups)，考慮新增 [造訪網頁](/help/xdm/field-groups/event/web-details.md) 和 [身分對應](/help/xdm/field-groups/profile/identitymap.md) 欄位群組。 這是除了適用於您數位屬性和資料收集實務的其他欄位群組之外。

此外，您可以建立或重複使用現有欄位群組，並將其新增至您的結構描述，以擷取合作夥伴提供的訪客相關深入分析。 閱讀如何 [建立欄位群組](/help/xdm/ui/resources/field-groups.md) 以及如何 [新增欄位](/help/xdm/ui/resources/field-groups.md) 至欄位群組。 例如，如果您希望根據合作夥伴提供的見解（如年齡範圍、就業狀態、每月消費能力或購買行為）進行個人化，請讓您的欄位群組包含適當的欄位。

假設資料合作夥伴為訪客提供穩定的識別碼，而您想要將這個識別碼帶入Real-Time CDP，請確定您的自訂欄位群組中的識別碼有正確命名的欄位。 您也應在先前建立的身分名稱空間中將欄位標示為身分。 也請記住 [啟用要包含在設定檔中的結構描述](/help/xdm/ui/resources/schemas.md#profile).

#### 建立資料集

接下來，您必須建立資料集，用以儲存您從Web屬性訪客收集且將用於站上個人化的時間序列資料。

閱讀有關教學課程 [如何建立資料集](/help/catalog/datasets/user-guide.md#create) 別忘了選取從結構描述建立資料集的選項。 根據您在上一步中建立的結構描述建立資料集。

與建立結構時的步驟類似，您需要啟用要包含在中的資料集 [!UICONTROL 即時客戶個人檔案]. 如需啟用資料集以用於中的詳細資訊 [!UICONTROL 即時客戶個人檔案]，閱讀 [建立結構描述教學課程。](/help/xdm/tutorials/create-schema-ui.md#profile)

### 在您的Web屬性上實作事件資料收集 {#implement-data-collection}

設定資料管理設定後，您現在需要實作即時事件 [資料彙集](/help/collection/home.md) 在您的Web屬性上。 您需要使用Adobe資料收集程式庫檢測您的屬性 —  [!UICONTROL Web SDK]  — 收集即時事件呼叫，並將其傳回Real-Time CDP。 此專案由幾個資料收集元件中的幾個個別工作組成。

>[!IMPORTANT]
>
>若要擷取合作夥伴提供的屬性，您還必須 *將您的Web屬性與合作夥伴API或其他方法整合，以便即時呼叫資料合作夥伴並擷取其屬性*. 請與您選擇的合作夥伴討論此方面，因為這不是本教學課程的主題。

首先，使用畫面右上角的應用程式切換器，導覽至 **[!UICONTROL 資料彙集]** 區段。

>[!TIP]
>
>如果您無法檢視，請聯絡系統管理員以要求存取權 [!UICONTROL 資料彙集] 應用程式切換器中的。

![應用程式切換器，前往「資料收集」區段。](/help/rtcdp/assets/partner-data/onsite-personalization/app-switcher-data-collection.png)

此 **[!UICONTROL 資料彙集]** UI的區段看起來類似於下圖。

![Platform UI的資料收集區段。](/help/rtcdp/assets/partner-data/onsite-personalization/data-collection-home.png)

#### 建立資料串流

作為資料收集區段的第一步， [建立新的資料流](/help/datastreams/configure.md). 資料串流是收集資料並正確路由至正確Adobe應用程式(在此例中為Experience Platform)的基礎。

當您建立資料流時，請在 **[!UICONTROL 事件結構描述]** 欄位中，選取您先前建立的綱要。

![設定新資料流時，事件結構選擇器會醒目提示。](/help/rtcdp/assets/partner-data/onsite-personalization/event-schema-selector-datastream.png)

[選取事件資料集](/help/datastreams/configure.md#aep) 之前從下拉式清單建立的下拉式功能表，勾選旁邊的方塊 **[!UICONTROL 邊緣細分]** 和 **[!UICONTROL 個人化目的地]**，並選取 **[!UICONTROL 儲存]**.

請注意，由於您引進了事件型時間序列資料，因此不必在此案例中選取設定檔資料集。

#### 建立標籤屬性

將屬性視為容器，當您將標籤部署至網站時，在其中裝入擴充功能、規則、資料元素和程式庫。

瀏覽至 **[!UICONTROL 標籤]** 並選取 **[!UICONTROL 新增屬性]**.

![建立新的標籤屬性。](/help/rtcdp/assets/partner-data/onsite-personalization/create-tag-property.png)

填寫必填欄位並選取 **[!UICONTROL 儲存]**.

![填寫新屬性的必填欄位。](/help/rtcdp/assets/partner-data/onsite-personalization/tag-property-fields.png)

取得關於如何 [建立標籤屬性](https://experienceleague.adobe.com/docs/platform-learn/implement-in-websites/configure-tags/create-a-property.html).

接下來，您必須在屬性內安裝各種擴充功能。 選取您的標籤屬性並導覽至 [!UICONTROL 擴充功能] 區段。

![選取您的新標籤屬性。](/help/rtcdp/assets/partner-data/onsite-personalization/select-tag-property.png)

請注意 [!UICONTROL 核心] 已安裝擴充功能。 您必須再安裝兩個擴充功能，如下節所述。

![檢視已安裝的擴充功能。](/help/rtcdp/assets/partner-data/onsite-personalization/view-existing-extensions.png)

#### 安裝Web SDK擴充功能

請注意，本教學課程說明如何使用Web SDK檢測您的網站。 您也可以使用 [行動SDK](https://developer.adobe.com/client-sdks/documentation/) 將體驗個人化給應用程式訪客。

![擴充功能目錄中的Web SDK擴充功能檢視。](/help/rtcdp/assets/partner-data/onsite-personalization/web-sdk-extension.png)

在設定Web SDK的畫面中，向下導覽至 **[!UICONTROL 資料串流]** 區段，並提供您正在使用的Experience Platform沙箱相關資訊。 從下一個下拉式清單中選取適當的沙箱以及在先前步驟中建立的資料流。 您可以為所有其他環境選擇相同的沙箱和資料流值。 保留其他設定不變，並選取 **[!UICONTROL 儲存]**.

取得完整的資訊 [如何安裝Web SDK](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/tags-configuration/install-web-sdk.html).

#### 安裝ID服務擴充功能

使用 [Experience CloudID服務擴充功能](/help/tags/extensions/client/id-service/overview.md) 為所有Experience Cloud解決方案的訪客建立以裝置為基礎的唯一第一方身分識別。 搜尋 **[!UICONTROL ID服務]** 並將它安裝在擴充功能目錄中。 安裝擴充功能時，請保留所有預設設定。

![擴充功能目錄中的ID服務擴充功能檢視。](/help/rtcdp/assets/partner-data/onsite-personalization/id-service-extension.png)

#### 設定環境

接下來，繼續前往 **[!UICONTROL 環境]** 左側導覽的區段。 在此步驟中，您必須將網站連線至Adobe Edge網路，以即時擷取及傳遞訪客資訊。

選取開發環境右側的方塊圖示，並複製出現在強制回應視窗中的JavaScript程式碼片段的標準版本。

![在資料收集UI的「環境」區段中選取醒目提示的方塊圖示。](/help/rtcdp/assets/partner-data/onsite-personalization/select-box-icon.png)

您必須將此程式碼片段新增至網站的最上方。 因此，您的網站會呼叫Adobe Edge Network以擷取將在頁面上載入及執行的JavaScript邏輯。 這可讓訪客ID產生、資料收集和即時體驗個人化等功能，順利運作。

#### 設定資料元素

資料元素是資料字典 (或資料地圖) 的建置組塊。單一資料元素是變數，其值可對應至查詢字串、URL、Cookie 值、JavaScript 變數等資料。深入瞭解 [資料元素](/help/tags/ui/managing-resources/data-elements.md).

出於此使用案例的目的，您必須設定兩個資料元素。

首先，設定 `partnerData` 元素。 導覽至 **[!UICONTROL 資料元素]** 區段並選取 **[!UICONTROL 建立新資料元素]**.

![建立新的資料元素。](/help/rtcdp/assets/partner-data/onsite-personalization/create-data-element.gif)

為資料元素命名 `partnerData`，保留 [!UICONTROL 副檔名] 值為 [!UICONTROL 核心]，並設定 **[!UICONTROL 資料元素型別]** 作為 **[!UICONTROL javascript變數]**. 輸入 `partnerData` 在標題為的欄位中 **[!UICONTROL javascript變數名稱]** 並選取 **[!UICONTROL 儲存]**.

![醒目提示要正確設定partnerData資料元素的選取專案。](/help/rtcdp/assets/partner-data/onsite-personalization/create-partnerdata-data-element.png)

若要設定第二個資料元素，請命名新變數 `pageVisit`，設定 **[!UICONTROL 副檔名]** 至 **[!UICONTROL Adobe Experience Platform]** 並選擇 **[!UICONTROL xdm物件]** 作為資料型別。

![反白顯示選取專案，以正確設定pageVisit資料元素。](/help/rtcdp/assets/partner-data/onsite-personalization/page-visit-data-element.png)

從結構描述中，選取與您預期來自資料合作夥伴的值對應的第三方屬性。 然後，選取標題為的選項按鈕 **[!UICONTROL 提供整個物件]**. 選取看起來像資料庫的圖示，然後選擇 `partnerData` 您先前建立的資料元素。

#### 設定規則

在 **[!UICONTROL 規則]** 區段，您可以設定網站以傳送個人化請求給Adobe，並將屬性載入您剛建立的資料元素中。 深入瞭解 [建立規則](/help/tags/ui/managing-resources/rules.md).

選取 **[!UICONTROL 建立新規則]**. 命名此規則 **[!UICONTROL 個人化]** 並選取旁邊的+符號 **[!UICONTROL 活動]**. 選取 **[!UICONTROL 頁面底部]** 做為事件並儲存。

![規則之事件型別部分的選取專案。](/help/rtcdp/assets/partner-data/onsite-personalization/add-events-rule.png)

選取旁邊的+符號 **[!UICONTROL 動作]**. 將擴充功能更新至 **[!UICONTROL Adobe Experience Platform Web SDK]** 並設定 **[!UICONTROL 動作型別]** 至 **[!UICONTROL 傳送事件]**.

![規則之動作型別部分的選取專案。](/help/rtcdp/assets/partner-data/onsite-personalization/add-action-rule.png)

從 **[!UICONTROL 型別]** 在右側的下拉式選取器中，選取 `web.webpagedetails.pageViews` 做為事件型別。

![選取事件型別。](/help/rtcdp/assets/partner-data/onsite-personalization/add-pageview-type-rule.png)

選取XDM資料旁的資料庫圖示，然後選取 `pageVisit` 資料元素。

向下捲動動作設定清單，並確實勾選標題為的方塊 **[!UICONTROL 呈現視覺個人化決定]**. 這對於允許在網頁上以視覺化方式呈現透過Adobe Target或其他類似產品提供的體驗很重要。 選取 **[!UICONTROL 保留變更]**，然後 **[!UICONTROL 儲存]** 規則。

![選取「呈現視覺個人化決策」核取方塊。](/help/rtcdp/assets/partner-data/onsite-personalization/render-visual-personalization-toggle.png)

#### 設定發佈工作流程

若要將此設定部署到網頁，下一步是建置包含您剛才建立之資源的程式庫。 深入瞭解 [設定發佈流程](/help/tags/ui/publishing/publishing-flow.md).

選取 **[!UICONTROL 發佈流程]** 然後 **[!UICONTROL 新增程式庫]**.

選取 **[!UICONTROL 新增所有變更的資源]**，為程式庫命名，將環境設為 **[!UICONTROL 開發]** 並選取 **[!UICONTROL 儲存並建置到開發環境]**.

![建立程式庫並部署至開發環境](/help/rtcdp/assets/partner-data/onsite-personalization/create-publishing-workflow.gif)

#### 測試您的網站

此時，您的網站應該已透過Web SDK完成檢測。 若要測試資料收集是否如預期運作，您可以導覽至您的網站，並使用瀏覽器的開發人員工具來檢查網路流量。

輸入 `interact` 在搜尋方塊中，重新整理頁面，您應該會看到從網站到Adobe Edge網路的網路呼叫正在填入。

![檢視填入開發人員工具中的網路事件。](/help/rtcdp/assets/partner-data/onsite-personalization/events-filtered.png)

### 個人化 {#personalization}

您現在已準備好建立並啟用個人化對象。

#### 設定邊緣細分

設定 [邊緣細分](/help/segmentation/ui/edge-segmentation.md) 因此，當訪客造訪您的Web屬性時，會即時評估訪客的對象成員資格。

也請務必設定 [主動邊緣合併原則](/help/destinations/ui/activate-edge-personalization-destinations.md#create-merge-policy) 適用於edge對象。

#### 與Adobe Target或其他自訂個人化目的地整合

您現在已準備好與個人化引擎整合，以便向您的網站或應用程式訪客顯示個人化內容。 Adobe建議使用 [Adobe Target目的地](/help/destinations/catalog/personalization/adobe-target-connection.md) 以達成此目的。

>[!IMPORTANT]
>
>閱讀有關教學課程 [啟用對象以邊緣個人化目的地](/help/destinations/ui/activate-edge-personalization-destinations.md) 以取得啟用對象所需步驟的完整檢視。

## 限制和疑難排解 {#limitations-and-troubleshooting}

當您探索本頁說明的使用案例時，請注意下列限制：

* 如果您使用合作夥伴ID，請注意，建置您的合作夥伴ID時不會使用這些ID [身分圖表](/help/identity-service/ui/identity-graph-viewer.md).

## 其他透過合作夥伴資料支援封存的使用案例 {#other-use-cases}

探索透過 Real-Time CDP 中的合作夥伴資料支援啟用的更多使用案例：

* [使用受信任資料合作夥伴的屬性來補充第一方設定檔，以改善您的資料基礎並對客戶群取得新的分析，而且獲致更佳的對象最佳化。](/help/rtcdp/partner-data/supplement-first-party-profiles.md)
* 使用Real-Time CDP中的協力廠商資料支援，以 [透過資料合作夥伴的潛在客戶設定檔來擴大您的設定檔基礎，並與他們互動以贏取或接觸新客戶](/help/rtcdp/partner-data/prospecting.md).
* (**即將推出**) [!BADGE Beta]{type=Informative}**擴大的啟動範圍**&#x200B;使用合作夥伴 ID 發佈不接受 PII 或雜湊 PII 的生態系統。