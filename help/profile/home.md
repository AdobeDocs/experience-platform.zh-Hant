---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API；統一設定檔；統一設定檔；統一；設定檔；rtcp;XDM圖表
title: 即時客戶個人檔案概觀
topic-legacy: guide
description: 即時客戶設定檔可合併來自各種來源的資料，並以個別客戶設定檔和相關時間序列事件的形式提供對該資料的存取。 此功能可讓行銷人員跨多個管道，透過受眾推動協調、一致且相關的體驗。
exl-id: c93d8d78-b215-4559-a806-f019c602c4d2
source-git-commit: 7ebd84f31161b45c2904545a2310c8b1f7831593
workflow-type: tm+mt
source-wordcount: '1779'
ht-degree: 0%

---

# [!DNL Real-time Customer Profile] 概觀

Adobe Experience Platform可讓您為客戶提供協調、一致且相關的體驗，無論客戶在何處或何時與您的品牌互動。 透過[!DNL Real-time Customer Profile]，您可結合來自多個管道的資料，包括線上、離線、CRM和協力廠商，以全面了解每個客戶。 [!DNL Profile] 可讓您將客戶資料併入統一檢視中，提供每個客戶互動的可操作、時間戳記帳戶。此概述將幫助您了解[!DNL Experience Platform]中[!DNL Real-time Customer Profile]的角色和使用。

## [!DNL Profile] Experience Platform

下圖強調顯示「即時客戶個人檔案」與Experience Platform內其他服務之間的關係：

![](images/profile-overview/profile-in-platform.png)

## 了解設定檔

[!DNL Real-time Customer Profile] 合併來自各種企業系統的資料，然後以客戶配置檔案的形式提供對資料的訪問，並包含相關的時間序列事件。此功能可讓行銷人員跨多個管道，透過受眾推動協調、一致且相關的體驗。 以下小節著重說明您必須了解的一些核心概念，以便在Platform內有效建立和維護設定檔。

### 設定檔資料存放區

雖然[!DNL Real-time Customer Profile]會處理擷取的資料，並使用Adobe Experience Platform [!DNL Identity Service]透過身分對應來合併相關資料，但會在[!DNL Profile]資料存放區中維護自己的資料。 [!DNL Profile]儲存區與資料湖中的目錄資料和身分圖中的[!DNL Identity Service]資料分開。

配置檔案儲存使用Microsoft Azure Cosmos DB基礎架構，而Platform Data Lake使用Microsoft Azure Data Lake儲存。

### 設定檔護欄

Experience Platform提供一系列護欄，協助您避免建立「即時客戶設定檔」無法支援的[Experience Data Model(XDM)結構](../xdm/home.md)。 這包括會導致效能降低的軟限制，以及會導致錯誤和系統中斷的硬限制。 欲知更多資訊，包括指南清單和示例使用案例，請參閱[配置式護欄](guardrails.md)文檔。

### 設定檔控制面板 {#profile-dashboard}

Experience PlatformUI提供控制面板，您可透過控制面板檢視即時客戶個人檔案資料的重要資訊，如每日快照中所擷取。 若要了解如何存取和使用UI中的[!DNL Profile]控制面板，以及控制面板中顯示之量度的詳細資訊，請參閱[設定檔控制面板UI指南](ui/profile-dashboard.md)。

### 設定檔片段與合併的設定檔 {#profile-fragments-vs-merged-profiles}

每個個別客戶設定檔都由多個已合併的設定檔片段組成，以形成該客戶的單一檢視。 例如，如果客戶跨多個管道與您的品牌互動，您的組織會在多個資料集中顯示與該單一客戶相關的多個設定檔片段。 將這些片段擷取至Platform時，會合併在一起，以便為該客戶建立單一設定檔。

當來自多個來源的資料發生衝突時（例如，一個片段將客戶列為「單一」，而另一個片段將客戶列為「已婚」）,[合併策略](#merge-policies)會決定要優先排列哪些資訊，並將哪些資訊包含在個人的設定檔中。 因此，Platform內的設定檔片段總數可能一律高於已合併設定檔的總數，因為每個設定檔都由多個片段組成。

### 記錄資料

設定檔是由許多屬性（也稱為記錄資料）所組成的主體、組織或個人的表示。 例如，產品的設定檔可能包含SKU和說明，而人員的設定檔則包含名字、姓氏和電子郵件地址等資訊。 使用[!DNL Experience Platform]，您可以自訂設定檔，以使用與業務相關的特定資料。 標準[!DNL Experience Data Model](XDM)類[!DNL XDM Individual Profile]是在描述客戶記錄資料時建立架構的首選類，並為Platform服務之間的許多交互提供整合的資料。 有關使用[!DNL Experience Platform]中架構的詳細資訊，請從閱讀[XDM系統概述](../xdm/home.md)開始。

### 時間序列事件

時間序列資料提供了在主題直接或間接地採取某個動作時系統的快照，以及詳細說明事件本身的資料。 以標準結構類別XDM ExperienceEvent表示，時間系列資料可說明事件，例如新增至購物車的項目、點按的連結，以及檢視的視訊。 時間序列資料可用來建立區段規則的基礎，而事件則可在設定檔的內容中個別存取。

### 身分

每家企業都想以一種個人化的方式與客戶溝通。 不過，向客戶提供相關數位體驗的其中一項挑戰，是了解如何將其中斷連結的資料連結在一起，這通常會分散在不同的數位通道，例如平板電腦、行動電話和筆記型電腦。 [!DNL Identity Service] 可讓您從多個管道連結身分，並為每個客戶建立身分圖表，將客戶的完整圖片拼湊在一起。如需詳細資訊，請造訪[Identity服務概述](../identity-service/home.md)。

### 合併策略

將來自多個來源的資料片段匯整在一起並合併，以查看每個個別客戶的完整檢視時，合併原則是[!DNL Platform]用來判斷資料如何排定優先順序的規則，以及將使用哪些資料來建立客戶設定檔。

當多個資料集中有衝突資料時，合併策略將確定應如何處理該資料以及應使用哪個值。 通過RESTful API或用戶介面，您可以建立新的合併策略、管理現有策略，以及為組織設定預設的合併策略。

要了解有關合併策略及其在Experience Platform中的角色的詳細資訊，請從閱讀[合併策略概述](merge-policies/overview.md)開始。

### 聯合結構 {#profile-fragments-and-union-schemas}

[!DNL Real-time Customer Profile]的一個關鍵特徵是能夠統一多通道資料。 使用[!DNL Real-time Customer Profile]存取實體時，可提供該實體跨資料集之所有設定檔片段的合併檢視（稱為「聯合檢視」），並透過所謂的聯合架構實現。

若要進一步了解聯合結構，包括如何在UI中存取聯合結構，請參閱[聯合結構UI指南](ui/union-schema.md)。

### (Alpha)計算屬性

>[!IMPORTANT]
>
>計算屬性功能為Alpha。 檔案和功能可能會有所變更。

計算屬性是用於將事件層級資料匯總到設定檔層級屬性的函式。 系統會自動計算這些函式，以便用於不同區段、啟動和個人化。 這些計算有助於您輕鬆回答與期限購買值、購買間時間或應用程式開啟數量等相關的問題，而無需您每次需要資訊時都手動執行複雜的計算。 有關計算屬性的詳細資訊，包括了解Adobe Experience Platform中的計算屬性所發揮的作用，請從閱讀[計算屬性概述](computed-attributes/overview.md)開始。

## 設定檔和區段

Adobe Experience Platform [!DNL Segmentation Service]會產生支援個別客戶體驗所需的對象。 建立受眾區段時，該區段的ID會新增至所有合格設定檔的區段成員資格清單中。 區段規則是使用RESTful API和「區段產生器」使用者介面建立並套用至[!DNL Real-time Customer Profile]資料。 若要進一步了解分段，請先閱讀[分段服務概述](../segmentation/home.md)開始。

### 串流獲取和串流細分

即時輸入可通過稱為流獲取的過程實現。 當擷取設定檔和時間序列資料時，[!DNL Real-time Customer Profile]會自動決定先透過稱為串流分段的持續程式，將該資料納入或排除於區段之外，再與現有資料合併並更新聯合檢視。 因此，您可以即時執行計算，並做出決策，在客戶與您的品牌互動時，向客戶提供增強的個人化體驗。 擷取資料時，也會進行驗證，以確保正確擷取資料，並符合資料集所依據的結構。 如需擷取期間已執行哪些驗證的詳細資訊，請從閱讀[資料擷取品質概述](../ingestion/quality/overview.md)開始。

## 邊緣投影

為了即時為跨多個管道的客戶提供協調、一致且個人化的體驗，需要隨著變更隨時提供正確的資料並持續更新。 Adobe Experience Platform可透過使用所謂的Edge來即時存取資料。 邊緣是地理位置的伺服器，可儲存資料，讓應用程式可輕鬆存取。 例如，Adobe Target和Adobe Campaign等Adobe應用程式會使用Edge，以即時提供個人化的客戶體驗。 通過投影將資料路由到邊，投影目標定義要向其發送資料的邊，投影配置定義將在邊上提供的特定資訊。 若要深入了解並開始使用[!DNL Real-time Customer Profile] API的投影，請參閱[邊緣投影端點指南](api/edge-projections.md)。

## 將資料內嵌至[!DNL Profile]

[!DNL Platform] 可設定為將記錄和時間序列資料傳送至， [!DNL Profile]以支援即時串流內嵌和批次內嵌。如需詳細資訊，請參閱教學課程，其中說明如何[將資料新增至即時客戶設定檔](tutorials/add-profile-data.md)。

>[!NOTE]
>
>透過Adobe解決方案（包括[!DNL Analytics Cloud]、[!DNL Marketing Cloud]及[!DNL Advertising Cloud]）收集的資料會流入[!DNL Experience Platform]並匯入至[!DNL Profile]。

### 設定檔擷取量度

可觀察性前瞻分析可讓您公開Adobe Experience Platform中的關鍵量度。 除了各種[!DNL Platform]功能的[!DNL Experience Platform]使用統計資料和效能指標外，還有特定的設定檔相關量度，可讓您深入分析傳入的請求率、成功的擷取率、擷取的記錄大小等。 若要深入了解，請先閱讀[可觀察性前瞻分析API概述](../observability/api/overview.md)，並參閱[可用量度](../observability/api/metrics.md#available-metrics)的相關檔案，以取得即時客戶設定檔量度的完整清單。

## [!DNL Data governance] 和 [!DNL Privacy]

[!DNL Data governance] 是一系列策略和技術，用於管理客戶資料並確保符合適用於資料使用的法規、限制和政策。

由於資料控管與存取資料相關，因此在[!DNL Experience Platform]的各個層級中，資料控管都扮演著關鍵角色：
* 資料使用標籤
* 資料存取原則
* 對行銷動作資料的存取控制

[!DNL Data governance] 在數個點進行管理。這包括決定要將哪些資料內嵌至[!DNL Platform]，以及針對指定行銷動作內嵌後可存取哪些資料。 如需詳細資訊，請從閱讀[資料控管概述](../data-governance/home.md)開始。

### 處理選擇退出與資料隱私權請求

[!DNL Experience Platform] 可讓客戶傳送與資料在內的使用和儲存相關的退出請求 [!DNL Real-time Customer Profile]。如需如何處理選擇退出請求的詳細資訊，請參閱[上的檔案，接受選擇退出請求](../segmentation/consents.md)。

## 後續步驟和其他資源

若要進一步了解如何使用Experience PlatformUI或設定檔API來處理[!DNL Real-time Customer Profile]資料，請先分別閱讀[設定檔UI指南](ui/user-guide.md)或[API開發人員指南](api/overview.md)。
