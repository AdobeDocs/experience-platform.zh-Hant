---
title: 建立和設定資料串流
description: 了解如何將您的用戶端 Web SDK 整合和其他 Adobe 產品及協力廠商目的地連線。
exl-id: 4924cd0f-5ec6-49ab-9b00-ec7c592397c8
source-git-commit: d7a0299c5fe3729620e74602ac99459093cc2e28
workflow-type: tm+mt
source-wordcount: '2779'
ht-degree: 75%

---


# 建立和設定資料串流

本文件會介紹在 UI 中設定[資料流](./overview.md)的步驟。

## 存取[!UICONTROL 資料流]工作區

在左側導覽中選取&#x200B;**[!UICONTROL 資料流]**，即可建立並管理資料收集 UI 或 Experience Platform UI 中的資料流。

![資料收集 UI 中的資料流索引標籤](assets/configure/datastreams-tab.png)

**[!UICONTROL 資料流]**&#x200B;索引標籤會顯示現有資料流的清單，包括其易記名稱、ID 和上次修改日期。選取資料流的名稱以[檢視其詳細資料並設定服務](#view-details)。

選取特定資料流的「更多」圖示 (**...**)，即可顯示更多選項。選取&#x200B;**[!UICONTROL 編輯]**，可更新資料流的[基本設定](#configure)，或選取&#x200B;**[!UICONTROL 刪除]**，即可移除資料流。

![編輯或刪除現有資料流的選項](assets/configure/edit-datastream.png)

## 新建資料流 {#create}

若要建立資料流，首先請選取&#x200B;**[!UICONTROL 新資料流]**。

![選取新資料流](assets/configure/new-datastream-button.png)。

資料流建立工作流程隨即顯示，首先是設定步驟。在這裡，您必須提供資料流的名稱和說明 (選用)。

如果您要設定此資料流以用於 Experience Platform 並會使用 Platform Web SDK，則還必須選取[事件型體驗資料模型 (XDM) 綱要](../xdm/classes/experienceevent.md)，以代表您計劃擷取的資料。

![資料流的基本設定](assets/configure/configure.png)

### 設定地理位置與網路查閱 {#geolocation-network-lookup}

地理位置和網路查詢設定可協助您定義要收集的地理和網路層級資料的詳細程度。

展開 **[!UICONTROL 地理位置與網路查詢]** 區段來設定底下所述的設定。

![Platform UI熒幕擷取畫面會顯示資料流設定畫面，且地理位置和網路查詢設定會反白顯示。](assets/configure/geolookup.png)

| 設定 | 說明 |
| --- | --- |
| [!UICONTROL 地理查詢] | 根據訪客的IP位址啟用所選選項的地理位置查閱。 可用的選項包括： <ul><li>**國家**：填入 `xdm.placeContext.geo.countryCode`</li><li>**郵遞區號**：填入 `xdm.placeContext.geo.postalCode`</li><li>**州/省**：填入 `xdm.placeContext.geo.stateProvince`</li><li>**DMA**：填入 `xdm.placeContext.geo.dmaID`</li><li>**城市**：填入 `xdm.placeContext.geo.city`</li><li>**緯度**：填入 `xdm.placeContext.geo._schema.latitude`</li><li>**經度**：填入 `xdm.placeContext.geo._schema.longitude`</li></ul>無論選取其他什麼選項，選取&#x200B;**[!UICONTROL 城市]**、**[!UICONTROL 緯度]**&#x200B;或&#x200B;**[!UICONTROL 經度]**&#x200B;都會提供最多兩個小數點的座標。這被認為是城市級精細度。<br> <br>未選取任何選項會停用地理位置查詢。 地理位置發生在之前 [!UICONTROL IP模糊化]，表示它不受此程式庫的 [!UICONTROL IP模糊化] 設定。 |
| [!UICONTROL 網路查詢] | 根據訪客的IP位址啟用所選選項的網路查閱。 可用的選項包括： <ul><li>**電信業者**：填入 `xdm.environment.carrier`</li><li>**網域**：填入 `xdm.environment.domain`</li><li>**ISP**：填入 `xdm.environment.ISP`</li></ul> |

如果您為資料收集啟用上述任何欄位，請確定您已正確設定 [`context`](../edge/data-collection/automatic-information.md) 陣列屬性，當 [設定Web SDK](../edge/fundamentals/configuring-the-sdk.md).

地理位置查詢欄位使用 `context` 陣列字串 `"placeContext"`，而網路查詢欄位則使用 `context` 陣列字串 `"environment"`.

此外，請確定您的結構描述中存在每個所需的XDM欄位。 如果不適用，您可以新增Adobe提供的專案 `Environment Details` 欄位群組至您的結構描述。

### 設定裝置查詢 {#geolocation-device-lookup}

此 **[!UICONTROL 裝置查詢]** 設定可讓您選取要收集的裝置特定資訊。

展開 **[!UICONTROL 裝置查詢]** 區段來設定底下所述的設定。

![Platform UI熒幕擷取畫面會顯示醒目提示裝置查詢設定的資料流設定畫面。](assets/configure/device-lookup.png)

>[!IMPORTANT]
>
>下表所述的設定是互斥的。 您無法同時選取使用者代理程式資訊和裝置查詢資料。

| 設定 | 說明 |
| --- | --- |
| **[!UICONTROL 保留使用者代理和使用者端提示標題]** | 選取此選項可僅收集儲存在使用者代理字串中的資訊。 此設定預設為選取。 填入 `xdm.environment.browserDetails.userAgent` |
| **[!UICONTROL 使用裝置查詢功能來收集下列資訊]** | 如果要收集下列一或多個裝置特定資訊，請選取此選項： <ul><li>**[!UICONTROL 裝置]** 資訊：<ul><li>**裝置製造商**：填入 `xdm.device.manufacturer`</li><li>**裝置型號**：填入 `xdm.device.modelNumber`</li><li>**行銷名稱**：填入 `xdm.device.model`</li></ul></li><li>**[!UICONTROL 硬體]** 資訊： <ul><li>**硬體型別**：填入 `xdm.device.type`</li><li>**顯示高度**：填入 `xdm.device.screenHeight`</li><li>**顯示寬度**：填入 `xdm.device.screenWidth`</li><li>**顯示色彩深度**：填入 `xdm.device.colorDepth`</li></ul></li><li>**[!UICONTROL 瀏覽器]** 資訊： <ul><li>**瀏覽器供應商**：填入 `xdm.environment.browserDetails.vendor`</li><li>**瀏覽器名稱**：填入 `xdm.environment.browserDetails.name`</li><li>**瀏覽器版本**：填入 `xdm.environment.browserDetails.version`</li></ul></li><li>**[!UICONTROL 作業系統]** 資訊： <ul><li>**作業系統供應商**：填入 `xdm.environment.operatingSystemVendor`</li><li>**作業系統名稱**：填入 `xdm.environment.operatingSystem`</li><li>**作業系統版本**：填入 `xdm.environment.operatingSystemVersion`</li></ul></li></ul>裝置查詢資訊無法與使用者代理程式和使用者端提示一起收集。 選擇收集裝置資訊會停用收集使用者代理程式和使用者端提示，反之亦然。 |
| **[!UICONTROL 不要收集任何裝置資訊]** | 如果您不想收集任何裝置查詢資訊，請選取此選項。 未收集任何裝置、硬體、瀏覽器、作業系統、使用者代理程式或使用者端提示資料。 |

如果您為資料收集啟用上述任何欄位，請確定您已正確設定 [`context`](../edge/data-collection/automatic-information.md) 陣列屬性，當 [設定Web SDK](../edge/fundamentals/configuring-the-sdk.md).

裝置和硬體資訊使用 `context` 陣列字串 `"device"`，而瀏覽器和作業系統資訊會使用 `context` 陣列字串 `"environment"`.

此外，請確定您的結構描述中存在每個所需的XDM欄位。 如果不適用，您可以新增Adobe提供的專案 `Environment Details` 欄位群組至您的結構描述。

### 設定進階選項 {#@advanced-options}

選取 **[!UICONTROL 進階選項]** 以顯示其他控制項來設定資料串流，例如IP模糊化、第一方ID Cookie等。

![進階設定選項](assets/configure/advanced-settings.png)

>[!IMPORTANT]
>
> 若要收集、處理和傳輸包括地理位置資訊在內的個人資料，您有責任確保已取得適用法律和法規要求的所有必要權限、同意、許可和授權。
> 
> 您的 IP 位址模糊化選擇並不會影響衍生自 IP 位址並發送到您設定的 Adobe 解決方案的地理位置資訊的層級。地理位址查詢必須單獨限制或停用。

| 設定 | 說明 |
| --- | --- |
| [!UICONTROL IP 模糊化] | 說明要套用於資料流的 IP 模糊化的類型。任何根據客戶 IP 進行的處理都會受到 IP 模糊化設定的影響。這包括從資料流接收資料的所有 Experience Cloud 服務。 <p>可使用的選項：</p> <ul><li>**[!UICONTROL 無]**：停用 IP 模糊化。完整的使用者 IP 位址會透過資料流傳送。</li><li>**[!UICONTROL 部分]**：若為 IPv4 位址，模糊化使用者 IP 位址的最後八位元。若為 IPv6 位址，模糊化位址的最後 80 個位元。 <p>範例：</p> <ul><li>IPv4：`1.2.3.4` -> `1.2.3.0`</li><li>IPv6：`2001:0db8:1345:fd27:0000:ff00:0042:8329` -> `2001:0db8:1345:0000:0000:0000:0000:0000`</li></ul></li><li>**[!UICONTROL 全部]**：模糊化整個 IP 位址。 <p>範例：</p> <ul><li>IPv4：`1.2.3.4` -> `0.0.0.0`</li><li>IPv6：`2001:0db8:1345:fd27:0000:ff00:0042:8329` -> `0:0:0:0:0:0:0:0`</li></ul></li></ul> IP 模糊化會對其他 Adobe 產品造成影響： <ul><li>**Adobe Target**：資料流層級 [!UICONTROL IP模糊化] 之前套用 [!UICONTROL IP模糊化] 在Adobe Target中執行，針對要求中存在的所有IP位址。 例如，如果資料流層級 [!UICONTROL IP模糊化] 選項已設為 **[!UICONTROL 完整]** 且Adobe Target IP模糊化選項設為 **[!UICONTROL 最後一個八位元模糊化]**，Adobe Target會收到完全模糊化的IP。 如果資料流層級 [!UICONTROL IP模糊化] 選項已設為 **[!UICONTROL 部分]** 且Adobe Target IP模糊化選項設為 **[!UICONTROL 完整]**，Adobe Target會收到部分模糊化的IP，然後套用完整模糊化功能。 Adobe Target IP模糊化是獨立於資料流管理。 如需更多詳細資料，請至 [IP 模糊化](https://developer.adobe.com/target/before-implement/privacy/privacy/)和[地理位置](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html?lang=zh-Hant)，參閱 Adobe Target 文件。</li><li>**Audience Manager**：資料流層級 [!UICONTROL IP模糊化] 設定會套用在 [!UICONTROL IP模糊化] 在Audience Manager中執行，針對要求中存在的所有IP位址。 Audience Manager 完成的任何地理位置查詢都會受到資料流層級 [!UICONTROL IP 模糊化]選項的影響。Audience Manager 中根據完全模糊化 IP 進行的地理位置查詢會導致未知區域，而根據所產生的地理位置資料無法實現任何區段。如需更多詳細資料，請至 [IP 模糊化](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/administration/ip-obfuscation.html?lang=zh-Hant)，參閱 Audience Manager 文件。</li><li>**Adobe Analytics**：如果選取任何 IP 模糊化選項而非選取「無」，Adobe Analytics 目前會接收到部分模糊化的 IP 位址。若要讓 Analytics 接收完全模糊化的 IP 位址，您必須在 Adobe Analytics 中單獨設定 IP 模糊化。此行為會在未來版本中更新。如需有關如何在 Analytics 中啟用 IP 模糊化的詳細資料，請參閱 Adobe Analytics [文件](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/general-acct-settings-admin.html)。</li></ul> |
| [!UICONTROL 第一方 ID Cookie] | 啟用後，在查詢[第一方裝置 ID](../edge/identity/first-party-device-ids.md) 時，此設定會告知 Edge Network 參照指定的 cookie，而不是在身分對應中查詢這個值。<br><br>啟用此設定時，您必須提供預期會儲存 ID 的 cookie 的名稱。 |
| [!UICONTROL 協力廠商 ID 同步] | 將 ID 同步分組至不同的容器中，即可讓不同的 ID 同步在不同時間執行。啟用後，此設定會讓您指定為此資料流執行哪個 ID 同步的容器。 |
| [!UICONTROL 協力廠商 ID 同步容器 ID] | 用於協力廠商 ID 同步之容器的數值 ID。 |
| [!UICONTROL 容器 ID 覆寫] | 在本區段中，您可以定義其他協力廠商 ID 同步容器 ID，以用於覆寫預設的 ID。 |
| [!UICONTROL 存取類型] | 定義 Edge Network 接受資料流的驗證類型。 <ul><li>**[!UICONTROL 混合驗證]**：選取此選項時，Edge Network 會同時接受已驗證和未驗證的要求。當您計劃使用 Web SDK 或 [Mobile SDK](https://developer.adobe.com/client-sdks/documentation/) 以及[伺服器 API](../server-api/overview.md) 時，請選取此選項。 </li><li>**[!UICONTROL 僅限已驗證]**：選取此選項時，Edge Network 只接受已驗證的要求。當您計劃只使用伺服器 API 並希望防止 Edge Network 處理任何未驗證的要求時，請選取此選項。</li></ul> |
| [!UICONTROL Media Analytics] | 選取此選項即可啟用透過Experience Platform SDK或Media Edge API處理Edge Network整合的串流追蹤資料。 若要瞭解Media Analytics，請參閱 [檔案](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html?lang=zh-Hant). |

在這裡，如果您要設定 Experience Platform 的資料流，請依照[資料收集的資料準備](./data-prep.md)教學課程的說明，將資料對應至 Platform 事件綱要，然後才返回本指南。否則，請選取「**[!UICONTROL 儲存]**」，並繼續進行下一區段。

## 檢視資料流詳細資料 {#view-details}

設定新資料流或選取要檢視的現有資料流後，該資料流的詳細資料頁面會隨即顯示。您可以在此處找到有關資料流的進一步資訊，包括其 ID。

![已建立的資料流的詳細資料頁面](assets/configure/view-details.png)

在資料流詳細資料畫面中，您可以[新增服務](#add-services)，以啟用您有權存取的 Adobe Experience Cloud 產品的功能。您還可以編輯資料流的[基本設定](#create)、更新其[對應規則](./data-prep.md)、[複製資料流](#copy)，或將其完全刪除。

## 將服務新增至資料流 {#add-services}

在資料流的詳細資料頁面上，選取&#x200B;**[!UICONTROL 新增服務]**，即可開始為該資料流新增可用的服務。

![選取「新增服務」以繼續](assets/configure/add-service.png)

在下一個畫面上，使用下拉選單選取要為此資料流設定的服務。只有您有權存取的服務才會顯示在此清單中。

![從清單中選取服務](assets/configure/service-selection.png)

選取所需的服務，填寫顯示的設定選項，然後選取「**[!UICONTROL 儲存]**」，即可將服務新增至資料流。所有已新增的服務都會顯示在資料流的詳細資料檢視中。

![已新增至資料流的服務](assets/configure/services-added.png)

以下子區段會說明每項服務的設定選項。

>[!NOTE]
>
>每個服務設定都包含「**[!UICONTROL 已啟用]**」開關，選取服務時會自動啟動。若要停用為此資料流選取的服務，請再次選取「**[!UICONTROL 已啟用]**」開關。

### Adobe Analytics 設定 {#analytics}

此服務會控制是否將資料傳送到 Adobe Analytics 以及傳送方式。如需其他詳細資料，可前往[將資料傳送到 Analytics](../edge/data-collection/adobe-analytics/analytics-overview.md)，查看指南。

![Adobe Analytics 設定區塊](assets/configure/analytics-config.png)

| 設定 | 說明 |
| --- | --- |
| [!UICONTROL 報告套裝 ID] | **(必要)** 您要將資料傳送到的 Analytics 報告套裝的 ID。此 ID 可以在「[!UICONTROL 管理員] > [!UICONTROL 報告套裝]」下的 Adobe Analytics UI 中找到。如果指定多個報告套裝，則資料會複製到每個報告套裝。 |
| [!UICONTROL 報告套裝覆寫] | 在本區段中，您可以新增其他報告套裝 ID，以用於覆寫預設的報告套裝 ID。 |

### Adobe Audience Manager 設定 {#audience-manager}

此服務會控制是否將資料傳送到 Adobe Audience Manager 以及傳送方式。若要將資料傳送到 Audience Manager，需要做的就是啟用本區段。其他設定為選用，但建議使用。

![Adobe Audience Manager 設定區塊](assets/configure/audience-manager-config.png)

| 設定 | 說明 |
| --- | --- |
| [!UICONTROL 已啟用 Cookie 目的地] | 允許 SDK 透過 [cookie 目的地](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-cookie-destination.html)從 [!DNL Audience Manager] 共用區段資訊。 |
| [!UICONTROL 已啟用 URL 目的地] | 允許 SDK 透過 [URL 目的地](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/custom-destinations/create-url-destination.html)從 [!DNL Audience Manager] 共用區段資訊。 |

### Adobe Experience Platform 設定 {#aep}

>[!IMPORTANT]
>
>啟用 Platform 的資料流時，請記下目前使用的 Platform 沙箱 (顯示在 UI 的頂端功能區中)。
>
>![選取的沙箱](assets/configure/platform-sandbox.png)
>
>沙箱是 Adobe Experience Platform 中的虛擬分區，可讓您將資料和實作與貴組織中的其他項目隔離。資料流建立後，其沙箱即無法變更。如需在 Experience Platform 中的沙箱角色的更多詳細資料，請參閱[沙箱文件](../sandboxes/home.md)。

此服務會控制是否將資料傳送到 Adobe Experience Platform 以及傳送方式。

![Adobe Experience Platform 設定區塊](assets/configure/platform-config.png)

| 設定 | 說明 |
|---| --- |
| [!UICONTROL 事件資料集] | **(必要)** 選取要將客戶事件資料串流到的 Platform 資料集。此綱要必須使用 [XDM 體驗事件類別](../xdm/classes/experienceevent.md)。若要新增其他資料集，請選取&#x200B;**[!UICONTROL 新增事件資料集]**。 |
| [!UICONTROL 設定檔資料集] | 選取要將客戶屬性資料傳送到的 Platform 資料集。此綱要必須使用 [XDM 個人設定檔類別](../xdm/classes/individual-profile.md)。 |
| [!UICONTROL Offer Decisioning] | 選取此核取方塊即可啟用 Platform Web SDK 實作的 Offer Decisioning。如需更多實作的詳細資料，請至[透過 Platform Web SDK 使用 Offer Decisioning](../edge/personalization/offer-decisioning/offer-decisioning-overview.md)，詳閱指南。<br><br>如需有關 Offer Decisioning 功能的詳細資訊，請參閱 [Adobe Journey Optimizer 文件](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started/starting-offer-decisioning.html?lang=zh-Hant)。 |
| [!UICONTROL 邊緣分段] | 選取此核取方塊，即可啟用此資料流的[邊緣分段](../segmentation/ui/edge-segmentation.md)。當 SDK 透過支援邊緣分段的資料流傳送資料時，相關設定檔的任何更新的區段會籍都會在回應中傳回。<br><br>此選項可以和[!UICONTROL 個人化目的地] (用於[下一頁個人化使用案例)](../destinations/ui/activate-edge-personalization-destinations.md) 結合在一起使用。 |
| [!UICONTROL 個人化目的地] | 啟用[!UICONTROL 邊緣分段]核取方塊後再啟用此功能時，此選項可讓資料流連線至個人化目的地，例如[自訂個人化](../destinations/catalog/personalization/custom-personalization.md)。<br><br>如需有關[設定個人化目的地](../destinations/ui/activate-edge-personalization-destinations.md)的具體步驟，請參閱目的地文件。 |
| [!UICONTROL Adobe Journey Optimizer] | 選取此核取方塊即可為此資料流啟用 [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html)。<br><br>啟用此選項可讓資料流從 [!DNL Adobe Journey Optimizer] 中以 Web 和應用程式為主的傳入行銷活動傳回個人化內容。此選項需要[!UICONTROL 邊緣分段]才能啟用。如果未勾選[!UICONTROL 邊緣分段]，此選項會顯示為灰色。 |

### Adobe Target 設定 {#target}

此服務會控制是否將資料傳送到 Adobe Target 以及傳送方式。

![Adobe Target 設定區塊](assets/configure/target-config.png)

| 設定 | 說明 |
| --- | --- |
| [!UICONTROL 屬性語彙基元] | [!DNL Target] 可讓客戶透過使用屬性控制權限。如需有關屬性的詳細資訊，請至[設定企業權限](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html) (在 [!DNL Target] 文件中)，詳閱指南。<br><br>如需屬性語彙基元，可以在「[!UICONTROL 設定] > [!UICONTROL 屬性]」下的 Adobe Target UI 中找到。 |
| [!UICONTROL 目標環境 ID] | [Adobe Target 中的環境](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html)可協助您管理全部開發階段的實作。此設定會指定您將使用此資料流的環境。<br><br>最佳做法是針對您的每個 `dev`、`stage` 和 `prod` 資料流環境對此做不同的設定，以保持事情簡單。但是，如果您已經定義了 Adobe Target 環境，則可以使用已定義的環境。 |
| [!UICONTROL Target 協力廠商 ID 命名空間] | 您要用於此資料流之 `mbox3rdPartyId` 的身分識別命名空間。如需詳細資訊，請至[實作 `mbox3rdPartyId` 和 Web SDK](../edge/personalization/adobe-target/using-mbox-3rdpartyid.md)，詳閱指南。 |
| [!UICONTROL 屬性語彙基元覆寫] | 在本區段中，您可以定義其他屬性語彙基元，以用於覆寫預設的語彙基元。 |

### [!UICONTROL 事件轉送]設定

此服務會控制是否將資料傳送到[事件轉送](../tags/ui/event-forwarding/overview.md)以及傳送方式。

![設定 UI 的事件轉送區段](assets/configure/event-forwarding-config.png)

| 設定 | 說明 |
| --- | --- |
| [!UICONTROL 啟動屬性] | **(必要)** 您要將資料傳送到的事件轉送屬性。 |
| [!UICONTROL 啟動環境] | **(必要)** 您要將資料傳送到的選取屬性內的環境。 |

>[!NOTE]
>
>選取&#x200B;**[!UICONTROL 手動輸入 ID]**，即可鍵入屬性和環境名稱，而不用使用下拉選單。

## 複製資料流 {#copy}

您可以建立現有資料流的副本並根據需要變更其詳細資料。

>[!NOTE]
>
>資料流只能在相同的[沙箱](../sandboxes/home.md)內複製。換句話說，您無法將資料流從一個沙箱複製到另一個沙箱。

在[!UICONTROL 資料流]工作區中的主要頁面，選取要複製之資料流的省略符號 (**....**)，然後選取「**[!UICONTROL 複製]**」。

![影像顯示[!UICONTROL 複製]選項已在資料流清單檢視中選取](assets/configure/copy-datastream-list.png)

或者，您可以從特定資料流的詳細資料檢視中選取&#x200B;**[!UICONTROL 複製資料流]**。

![影像顯示[!UICONTROL 複製]選項已在資料流詳細資料檢視中選取](assets/configure/copy-datastream-details.png)

確認對話框隨即顯示，提示您為要將建立的新資料流提供唯一名稱，以及有關將複製的設定選項的詳細資料。就緒後，請選取&#x200B;**[!UICONTROL 複製]**。

![複製資料流的確認對話框的圖示](assets/configure/copy-datastream-confirm.png)

[!UICONTROL 資料流]工作區的主要頁面會隨即重新顯示，並列出新的資料流。

## 後續步驟

本指南會介紹如何在資料收集 UI 中管理資料流。如需有關如何在設定資料流後安裝並設定 Web SDK 的詳細資訊，請參閱[資料收集 E2E 指南](../collection/e2e.md#install)。
