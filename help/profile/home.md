---
title: 即時客戶個人檔案概述
description: 即時客戶個人檔案會合併來自各種來源的資料，並以個別客戶個人檔案和相關時間序列事件的形式提供對該資料的存取權。 此功能可讓行銷人員跨多個管道，與其對象推動協調、一致且相關的體驗。
exl-id: c93d8d78-b215-4559-a806-f019c602c4d2
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '1821'
ht-degree: 1%

---

# [!DNL Real-Time Customer Profile] 概觀

Adobe Experience Platform 讓您能夠為客戶提供一致且相關的協調體驗，無論他們何時何地與您的品牌互動。替換為 [!DNL Real-Time Customer Profile]，您能透過合併來自多個管道（包括線上、離線、CRM和協力廠商）的資料，檢視每個個別客戶的整體檢視。 [!DNL Profile] 可讓您將客戶資料合併成統一的檢視畫面，針對每個客戶互動提供可採取行動且附有時間戳記的說明。 此總覽可協助您瞭解的角色和使用 [!DNL Real-Time Customer Profile] 在 [!DNL Experience Platform].

## [!DNL Profile] 在Experience Platform中

下圖會強調即時客戶設定檔與Experience Platform內其他服務之間的關係：

![即時客戶個人檔案與Adobe Experience Platform中其他服務之間的關係。 此圖表顯示設定檔是Adobe Experience Platform的核心元件之一。](images/profile-overview/profile-in-platform.png)

## 瞭解設定檔

[!DNL Real-Time Customer Profile] 合併來自各種企業系統的資料，然後以客戶個人檔案與相關時間序列事件的形式提供對該資料的存取權。 此功能可讓行銷人員跨多個管道，與其對象推動協調、一致且相關的體驗。 以下章節重點說明為了在Platform內有效建置和維護設定檔，您必須瞭解的一些核心概念。

### 設定檔實體組合

即時客戶個人檔案是由一個名為的主要實體所組成， **主要實體**&#x200B;和各種支援實體。 在Experience Platform的情境下，主要實體通常是 **設定檔實體**，由個人特徵、行為和對象會籍組成。 其他實體可讓細分引擎使用設定檔主要實體以外的資料，並包括下列專案：

- **維度實體**：用來簡化跨事件或設定檔記錄共用資訊的資料模型化程式的實體。 這也稱為查詢實體或分類實體。
- **B2B實體**：說明設定檔與企業對企業帳戶和商機關係的實體。

![說明設定檔實體組成的圖表。](./images/profile-overview/profile-entity-composition.png)

>[!IMPORTANT]
>
>由於維度和B2B實體僅存在於主要實體之外，因此它們僅用於批次分段。

維度和B2B實體透過連結至主要實體 **綱要關係**. 如需詳細資訊，請參閱下列檔案：

- [為查閱實體建立一對一的結構描述關係](../xdm/tutorials/relationship-ui.md)
- [為B2B實體建立多對一結構描述關係](../xdm/tutorials/relationship-b2b.md)

### 設定檔資料存放區

雖然 [!DNL Real-Time Customer Profile] 處理所擷取的資料並使用Adobe Experience Platform [!DNL Identity Service] 若要透過身分對應來合併相關資料，它會將自己的資料維護在 [!DNL Profile] 資料存放區。 此 [!DNL Profile] 存放區與資料湖中的目錄資料分開，且 [!DNL Identity Service] 身分圖表中的資料。

設定檔存放區使用Microsoft Azure Cosmos DB基礎結構，而平台資料湖使用Microsoft Azure資料湖儲存空間。

### 輪廓護欄

Experience Platform提供一系列護欄，協助您避免建立 [體驗資料模型(XDM)結構描述](../xdm/home.md) 哪些即時客戶設定檔不支援。 這包括會導致效能降低的軟性限制，以及會導致錯誤和系統中斷的硬性限制。 如需詳細資訊，包括指引清單和使用案例範例，請參閱 [輪廓護欄](guardrails.md) 檔案。

### 設定檔儀表板 {#profile-dashboard}

Experience PlatformUI提供了一個儀表板，您可以在其中檢視有關即時客戶設定檔資料的重要資訊，如每日快照期間所擷取。 若要瞭解如何存取和使用 [!DNL Profile] UI中的儀表板，以及有關儀表板中所顯示量度的詳細資訊，請參閱 [設定檔控制面板UI指南](ui/profile-dashboard.md).

### 設定檔片段與合併的設定檔 {#profile-fragments-vs-merged-profiles}

每個個別客戶設定檔都由多個設定檔片段組成，這些片段已合併以構成該客戶的單一檢視。 例如，如果客戶跨多個管道與您的品牌互動，則您的組織將會有多個與該單一客戶相關的設定檔片段出現在多個資料集中。 這些片段在擷取至Platform時，會合併在一起，以便為該客戶建立單一設定檔。

換言之，設定檔片段代表唯一的主要身分以及對應的 [記錄](#record-data) 或 [事件](#time-series-events) 指定資料集中該ID的資料。

當來自多個資料集的資料衝突時（例如，一個片段將客戶列為「單身」，而另一個片段將客戶列為「已婚」）， [合併原則](#merge-policies) 決定哪些資訊要優先處理，並包含在個人設定檔中。 因此，Platform內的設定檔片段總數可能一律高於合併的設定檔總數，因為每個設定檔通常是由多個資料集中的多個片段組成。

### 記錄資料 {#record-data}

設定檔是由許多屬性（也稱為記錄資料）組成的主體、組織或個人的表示法。 例如，產品的設定檔可能包含SKU和說明，而人員的設定檔包含名字、姓氏和電子郵件地址等資訊。 使用 [!DNL Experience Platform]，您可以自訂設定檔，以使用與業務相關的特定資料。 標準 [!DNL Experience Data Model] (XDM)類別， [!DNL XDM Individual Profile]是描述客戶記錄資料時用來建置結構的偏好類別，並提供平台服務之間許多互動不可或缺的資料。 如需在中使用綱要的詳細資訊 [!DNL Experience Platform]，請先閱讀 [XDM系統概覽](../xdm/home.md).

### 時間序列事件 {#time-series-events}

時間序列資料提供主體直接或間接執行動作時的系統快照，以及詳細說明事件本身的資料。 以標準結構描述類別XDM ExperienceEvent表示，時間序列資料可說明新增至購物車的專案、點按連結及檢視影片等事件。 時間序列資料可用於建立分段規則的基礎，而事件可在設定檔的情境中個別存取。

### 身分

每個企業都想要以個人化的方式與客戶溝通。 然而，為客戶提供相關數位體驗的挑戰之一，就是瞭解如何將中斷連線的資料繫結在一起，這通常會分散在平板電腦、行動電話和筆記型電腦等不同數位頻道中。 [!DNL Identity Service] 可讓您連結來自多個頻道的身分，並為每個客戶建立身分圖表，藉此拼接客戶的完整面貌。 造訪 [Identity Service總覽](../identity-service/home.md) 以取得詳細資訊。

### 合併原則

將來自多個來源的資料片段彙整在一起並加以合併，以便檢視每個個別客戶的完整檢視時，合併原則是指 [!DNL Platform] 會使用來決定資料的優先順序，以及會使用哪些資料來建立客戶設定檔。

當多個資料集中的資料發生衝突時，合併原則會決定該資料應該如何處理，以及應該使用哪個值。 透過RESTful API或使用者介面，您可以建立新的合併原則、管理現有原則，並為您的組織設定預設合併原則。

若要進一步瞭解合併原則及其在Experience Platform中的角色，請先閱讀 [合併原則概觀](merge-policies/overview.md).

### 聯合結構描述 {#profile-fragments-and-union-schemas}

的主要功能之一 [!DNL Real-Time Customer Profile] 是統一多管道資料的能力。 時間 [!DNL Real-Time Customer Profile] 用於存取實體，可為您提供該實體跨資料集的所有設定檔片段的合併檢視，稱為「聯合檢視」，並可透過稱為聯合結構描述的方式使用。

若要進一步瞭解聯合結構，包括如何在UI中存取聯合結構，請造訪 [聯合結構描述UI指南](ui/union-schema.md).

<!-- ### (Alpha) Computed attributes

>[!IMPORTANT]
>
>Computed attribute functionality is in alpha. The documentation and functionality are subject to change.

Computed attributes are functions used to aggregate event-level data into profile-level attributes. These functions are automatically computed so that they can be used across segmentation, activation, and personalization. These computations help you to easily answer questions related to things like lifetime purchase value, time between purchases, or number of application opens, without requiring you to manually perform complex calculations each time the information is needed. For more information on computed attributes, including understanding the role computed attributes play within Adobe Experience Platform, please begin by reading the [computed attributes overview](computed-attributes/overview.md). -->

## 設定檔與對象

Adobe Experience Platform [!DNL Segmentation Service] 會產生為個別客戶提供體驗所需支援的受眾。 建立受眾時，該受眾的ID會新增至所有合格設定檔的受眾成員資格清單中。 區段規則建立並套用至 [!DNL Real-Time Customer Profile] 使用RESTful API和區段產生器使用者介面的資料。 若要深入瞭解細分，請先閱讀 [Segmentation Service概述](../segmentation/home.md).

### 串流擷取和串流細分

即時輸入可透過稱為串流擷取的流程進行。 當個人資料和時間序列資料被擷取時， [!DNL Real-Time Customer Profile] 在將資料與現有資料合併並更新聯合檢視之前，會透過進行中的串流細分程式，自動決定從對象中包含或排除該資料。 因此，您可以即時執行計算並作出決定，在客戶與您的品牌互動時，向客戶傳遞強化的個人化體驗。 在內嵌資料時，資料也會經過驗證，以確保資料可正確內嵌，並符合資料集所依據的結構描述。 如需有關內嵌期間所完成驗證的詳細資訊，請從閱讀 [資料擷取品質概觀](../ingestion/quality/overview.md).

## 將資料擷取至 [!DNL Profile]

[!DNL Platform] 可將記錄和時間序列資料傳送至 [!DNL Profile]，支援即時串流擷取和批次擷取。 如需詳細資訊，請參閱教學課程，概述如何 [新增資料至即時客戶個人檔案](tutorials/add-profile-data.md).

>[!NOTE]
>
>透過Adobe解決方案收集的資料，包括 [!DNL Analytics Cloud]， [!DNL Marketing Cloud]、和 [!DNL Advertising Cloud]，流入 [!DNL Experience Platform] 並內嵌至 [!DNL Profile].

### 設定檔擷取量度

可觀察性深入分析可讓您在Adobe Experience Platform中公開關鍵量度。 除了 [!DNL Experience Platform] 各種使用情況統計資料和績效指標 [!DNL Platform] 透過這些功能，您可以檢視特定的設定檔相關量度，深入瞭解傳入請求率、成功擷取率、擷取記錄大小等。 若要進一步瞭解，請先閱讀 [可觀察性深入分析API概觀](../observability/api/overview.md)和如需即時客戶個人檔案量度的完整清單，請參閱以下檔案： [可用量度](../observability/api/metrics.md#available-metrics).

## 更新設定檔存放區資料

有時候，您可能需要更新組織設定檔存放區中的資料。 例如，您可能需要更正記錄或變更屬性值。 這可以透過批次擷取完成，並需要設定檔啟用的資料集設定為upsert標籤。 如需如何設定屬性更新資料集的詳細資訊，請參閱的教學課程 [為設定檔和更新插入啟用資料集](../catalog/datasets/enable-upsert.md).

## 資料控管和 [!DNL Privacy]

資料控管是用於管理客戶資料並確保遵守適用於資料使用的法規、限制和政策的一系列策略和技術。

在存取資料方面，資料控管扮演關鍵角色 [!DNL Experience Platform] 在不同層級：

- 資料使用標籤
- 資料存取原則
- 行銷動作資料的存取控制

資料控管可在數個時間點進行管理。 這包括決定要擷取哪些資料 [!DNL Platform] 以及擷取後指定的行銷動作可存取哪些資料。 如需詳細資訊，請先閱讀 [資料治理總覽](../data-governance/home.md).

### 處理選擇退出和資料隱私權請求

[!DNL Experience Platform] 可讓您的客戶傳送與其資料在中的使用及儲存相關的選擇退出請求 [!DNL Real-Time Customer Profile]. 如需如何處理選擇退出請求的詳細資訊，請參閱以下檔案： [接受選擇退出請求](../segmentation/consents.md).

## 後續步驟和其他資源

若要進一步瞭解如何使用Experience PlatformUI或設定檔API處理即時客戶設定檔資料，請從閱讀 [設定檔UI指南](ui/user-guide.md) 或 [API開發人員指南](api/overview.md)，依序輸入。
