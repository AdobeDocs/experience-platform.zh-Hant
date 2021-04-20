---
keywords: Experience Platform；配置檔案；即時客戶配置檔案；疑難排解；API；統一配置檔案；統一配置檔案；配置檔案；rtcp;XDM圖
title: 即時客戶個人檔案概觀
topic: guide
description: 即時客戶描述檔是一般查閱實體儲存，可合併來自各種企業資料資產的資料，然後以個別客戶描述檔和相關時間系列事件的形式提供對該資料的存取。 此功能可讓行銷人員跨多個通道，推動與受眾的協調、一致且相關的體驗。
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '1827'
ht-degree: 0%

---


# [!DNL Real-time Customer Profile]概述

Adobe Experience Platform可讓您為客戶推動協調、一致且相關的體驗，不論客戶在何處或何時與您的品牌互動。 透過[!DNL Real-time Customer Profile]，您可以結合來自多個通道（包括線上、離線、CRM和協力廠商）的資料，全面瞭解每個客戶。 [!DNL Profile] 可讓您將客戶資料整合到統一的檢視中，提供每個客戶互動的可操作、時間戳記帳戶。本概述將幫助您瞭解[!DNL Experience Platform]中[!DNL Real-time Customer Profile]的角色和使用。

## [!DNL Profile] Experience Platform

「即時客戶基本資料」與Experience Platform內其他服務之間的關係在下圖中突出顯示：

![](images/profile-overview/profile-in-platform.png)

## 瞭解個人檔案

[!DNL Real-time Customer Profile] 合併來自各種企業系統的資料，然後以客戶個人檔案的形式與相關的時間序列事件來存取該資料。此功能可讓行銷人員跨多個通道，推動與受眾之間協調、一致且相關的體驗。 以下幾節重點說明您必須瞭解的一些核心概念，以便在Platform中有效建立和維護個人檔案。

### 描述檔資料儲存

雖然[!DNL Real-time Customer Profile]會處理收錄的資料，並使用Adobe Experience Platform[!DNL Identity Service]透過身分對應來合併相關資料，但它會在[!DNL Profile]資料儲存區中維護其自己的資料。 [!DNL Profile]儲存區與資料湖中的目錄資料及識別圖中的[!DNL Identity Service]資料分開。

Profile Store使用Microsoft Azure Cosmos DB基礎架構，Platform Data Lake使用Microsoft Azure Data Lake儲存。

### 輪廓護欄

Experience Platform提供一系列保護欄，可協助您避免建立「即時客戶個人檔案」無法支援的[體驗資料模型(XDM)結構。 ](../xdm/home.md)這包括會導致效能降低的軟限制，以及導致錯誤和系統中斷的硬限制。 如需詳細資訊，包括准則清單和範例使用案例，請閱讀[描述檔護欄](guardrails.md)檔案。

### （測試版）設定檔控制面板{#profile-dashboard}

>[!IMPORTANT]
>
>控制面板功能目前處於測試階段，並非所有使用者都能使用。 文件和功能可能會有所變更。

Experience PlatformUI提供儀表板，您可通過該儀表板查看有關即時客戶概要檔案資料的重要資訊（在每日快照中捕獲）。 若要瞭解如何存取和使用UI中的[!DNL Profile]控制面板，以及控制面板中顯示的度量的詳細資訊，請參閱[描述檔控制面板UI指南](ui/profile-dashboard.md)。

### 描述檔片段與合併的描述檔{#profile-fragments-vs-merged-profiles}

每個客戶個人檔案都由多個已合併的個人檔案片段組成，以形成該客戶的單一檢視。 例如，如果客戶透過多個通道與您的品牌互動，您的組織將會在多個資料集中顯示與該單一客戶相關的多個描述檔片段。 當這些片段被收錄到Platform中時，會將它們合併在一起，以便為該客戶建立單一個人檔案。

當來自多個來源的資料發生衝突（例如，一個片段將客戶列為「單一」，而另一個片段將客戶列為「已婚」）時，[合併原則](#merge-policies)會決定要排定優先順序並納入個人設定檔的資訊。 因此，平台內的描述檔片段總數可能永遠高於合併描述檔的總數，因為每個描述檔都包含多個片段。

### 記錄資料

描述檔是由許多屬性（也稱為記錄資料）組成的主體、組織或個人的表示。 例如，產品的描述檔可能包含SKU和說明，而人員的描述檔則包含名字、姓氏和電子郵件地址等資訊。 使用[!DNL Experience Platform]，您可以自訂個人檔案，以使用與您的業務相關的特定資料。 標準[!DNL Experience Data Model](XDM)類[!DNL XDM Individual Profile]是在描述客戶記錄資料時用來構建模式的首選類，並為平台服務之間的許多交互提供資料。 有關在[!DNL Experience Platform]中使用方案的詳細資訊，請從閱讀[ XDM系統概述](../xdm/home.md)開始。

### 時間系列事件

時間序列資料提供了對象直接或間接採取操作時系統的快照，以及詳細描述事件本身的資料。 由標準架構類別XDM ExperienceEvent表示，時間系列資料可說明事件，例如新增至購物車的項目、被點按的連結和檢視的視訊。 時間系列資料可用來建立區段規則，而事件則可在描述檔的內容中個別存取。

### 身份

每家企業都想以個人化的方式與客戶溝通。 不過，為客戶提供相關數位體驗的其中一項挑戰，是瞭解如何將互不相連的資料連結在一起，這通常會跨不同的數位通道（例如平板電腦、行動電話和筆記型電腦）傳播。 [!DNL Identity Service] 可讓您從多個通道連結身分，並為每個客戶建立身份圖表，將客戶的完整形象拼湊在一起。如需詳細資訊，請造訪[身分服務概觀](../identity-service/home.md)。

### 合併原則

當從多個來源將資料片段匯整並合併，以便瞭解每個客戶的完整檢視時，合併原則是[!DNL Platform]用來決定資料的優先順序以及將哪些資料用於建立客戶個人檔案的規則。 當來自多個資料集的資料有衝突時，合併原則將決定該資料的處理方式以及應使用的值。 使用REST風格的API或用戶介面，您可以建立新的合併策略、管理現有策略，並為組織設定預設的合併策略。

有關使用[!DNL Real-time Customer Profile] API使用合併策略的詳細資訊，請參閱[合併策略端點指南](api/merge-policies.md)。 要使用[!DNL Experience Platform] UI使用合併策略，請參閱[合併策略UI指南](ui/merge-policies.md)。

### 聯合結構{#profile-fragments-and-union-schemas}

[!DNL Real-time Customer Profile]的主要功能之一是統一多頻道資料。 當[!DNL Real-time Customer Profile]用於訪問實體時，它可以為您提供該實體跨資料集的所有配置檔案片段的合併視圖（稱為「聯合視圖」），並通過稱為聯合模式實現。

若要進一步瞭解聯合架構，包括如何在UI中存取聯合架構，請造訪[聯合架構UI指南](ui/union-schema.md)。

### (Alpha)計算屬性

>[!IMPORTANT]
>
>計算的屬性功能為alpha。 說明檔案和功能可能會有所變更。

計算屬性是用於將事件級別資料聚合到配置檔案級別屬性的函式。 這些函式會自動計算，以便跨區段、啟動和個人化使用。 這些計算可協助您輕鬆回答與期限購買值、購買間隔時間或應用程式開啟次數等相關的問題，而不需在每次需要資訊時手動執行複雜的計算。 有關計算屬性的詳細資訊(包括瞭解Adobe Experience Platform內的角色計算屬性)，請首先閱讀[計算屬性概述](computed-attributes/overview.md)。

## 描述檔和區段

Adobe Experience Platform[!DNL Segmentation Service]為個別客戶提供體驗所需的受眾。 建立觀眾區段時，該區段的ID會新增至所有符合資格的設定檔的區段成員資格清單。 區段規則是使用REST風格的API和「區段產生器」使用者介面建立並套用至[!DNL Real-time Customer Profile]資料。 若要進一步瞭解分段，請先閱讀[分段服務概觀](../segmentation/home.md)。

### 串流擷取與串流分段

透過稱為串流擷取的程式，即可進行即時輸入。 當收錄描述檔和時間系列資料時，[!DNL Real-time Customer Profile]會自動決定透過稱為串流分段的持續程式，將該資料加入或排除區段，然後將其與現有資料合併並更新聯合檢視。 因此，您可以即時執行計算並做出決策，以便客戶在與品牌互動時提供增強的個人化體驗。 在攝取資料時，也經過驗證，以確保正確攝取資料，並符合資料集所依據的架構。 有關擷取期間執行哪些驗證的詳細資訊，請先閱讀[資料擷取品質概觀](../ingestion/quality/overview.md)開始。

## 邊緣投影

為即時跨多個通道為客戶提供協調、一致且個人化的體驗，需要隨時提供適當的資料，並在變更時持續更新。 Adobe Experience Platform使用戶能夠通過使用所謂的邊來即時訪問資料。 邊緣是地理位置優越的伺服器，可儲存資料，讓應用程式可輕鬆存取。 例如，Adobe應用程式(例如Adobe Target和Adobe Campaign)使用邊緣，以便即時提供個人化的客戶體驗。 資料通過投影被路由到邊，投影目的地定義資料要發送到的邊，投影配置定義將在邊上提供的特定資訊。 若要進一步瞭解並開始使用[!DNL Real-time Customer Profile] API處理投影，請參閱[邊緣投影端點指南](api/edge-projections.md)。

## 將資料收錄到[!DNL Profile]

[!DNL Platform] 可設定為傳送記錄和時間系列資料至 [!DNL Profile]，支援即時串流擷取和批次擷取。如需詳細資訊，請參閱教學課程，其中說明如何將資料新增至即時客戶個人檔案](tutorials/add-profile-data.md)。[

>[!NOTE]
>
>通過Adobe解決方案（包括[!DNL Analytics Cloud]、[!DNL Marketing Cloud]和[!DNL Advertising Cloud]）收集的資料流入[!DNL Experience Platform]並被吸收到[!DNL Profile]。

### 描述檔擷取量度

可觀性洞察可讓您公開Adobe Experience Platform的關鍵量度。 除了[!DNL Experience Platform]各種[!DNL Platform]功能的使用統計資料和效能指標外，還有特定的描述檔相關度量，可讓您深入瞭解傳入的請求率、成功的擷取率、收錄的記錄大小等。 若要進一步瞭解，請先閱讀[可觀察性洞察API概觀](../observability/api/overview.md)，如需即時客戶個人資料量度的完整清單，請參閱[可用量度](../observability/api/metrics.md#available-metrics)的檔案。

## [!DNL Data governance] 和 [!DNL Privacy]

[!DNL Data governance] 是用於管理客戶資料並確保遵守適用於資料使用的法規、限制和政策的一系列策略和技術。

由於與訪問資料有關，資料治理在[!DNL Experience Platform]的不同級別發揮了關鍵作用：
* 資料使用標籤
* 資料存取策略
* 對行銷動作資料的存取控制

[!DNL Data governance] 在幾個點進行管理。這包括決定哪些資料已收錄至[!DNL Platform]，以及擷取特定行銷動作後可存取哪些資料。 如需詳細資訊，請先閱讀[資料控管概述](../data-governance/home.md)。

### 處理退出和資料隱私權要求

[!DNL Experience Platform] 可讓客戶傳送與其資料使用和儲存相關的退出要求 [!DNL Real-time Customer Profile]。如需如何處理退出要求的詳細資訊，請參閱[上的檔案，以符合退出要求](../segmentation/honoring-opt-outs.md)。

## 後續步驟和其他資源

若要進一步瞭解如何使用Experience PlatformUI或描述檔API來處理[!DNL Real-time Customer Profile]資料，請先分別閱讀[描述檔UI指南](ui/user-guide.md)或[API開發人員指南](api/overview.md)。