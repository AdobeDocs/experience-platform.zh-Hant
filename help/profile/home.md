---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: 即時客戶個人檔案總覽
topic: guide
translation-type: tm+mt
source-git-commit: fa439ebb9d02d4a08c8ed92b18f2db819d089174
workflow-type: tm+mt
source-wordcount: '1665'
ht-degree: 1%

---


# [!DNL Real-time Customer Profile]概述

Adobe Experience Platform可讓您為客戶推動協調、一致且相關的體驗，不論客戶在何處或何時與您的品牌互動。 透過 [!DNL Real-time Customer Profile]此功能，您可以全面瞭解每個客戶，並結合來自多個通道的資料，包括線上、離線、CRM和第三方資料。 [!DNL Profile] 可讓您將分散的客戶資料整合為統一的檢視，提供每個客戶互動的可操作、時間戳記帳戶。 此概述將幫助您瞭解中的角色和 [!DNL Real-time Customer Profile] 使用 [!DNL Experience Platform]。

## 瞭解 [!DNL Real-time Customer Profile]

[!DNL Real-time Customer Profile] 是一般查閱實體儲存，可合併來自各種企業資料資產的資料，然後以個別客戶個人檔案和相關時間系列事件的形式提供對該資料的存取。 此功能可讓行銷人員跨多個通道，推動與受眾之間協調、一致且相關的體驗。

### [!DNL Profile] 資料儲存

雖然 [!DNL Real-time Customer Profile] 會處理擷取的資料並使用Adobe Experience Platform透過身分對 [!DNL Identity Service] 應來合併相關資料，但它會在商店中維護其專屬的 [!DNL Profile] 資料。 換言之，儲存 [!DNL Profile] 區與資料( [!DNL Catalog][!DNL Data Lake])和資料 [!DNL Identity Service] （識別圖）分開。

### [!DNL Profile] 和服 [!DNL Platform] 務

下圖中 [!DNL Real-time Customer Profile] 強調了內 [!DNL Experience Platform] 部和其他服務的關係：

![設定檔與其他Experience Platform服務之間的關係。](images/profile-overview/profile-in-platform.png)

### 設定檔和記錄資料

描述檔是主體、組織或個人的表示，也稱為記錄資料。 例如，產品的描述檔可能包含SKU和說明，而人員的描述檔則包含名字、姓氏和電子郵件地址等資訊。 使用 [!DNL Experience Platform]時，您可以自訂個人檔案，以使用與您的業務相關的資料類型。 標準 [!DNL Experience Data Model] (XDM)類 [!DNL Individual Profile] 是在描述客戶記錄資料時構建模式的首選類，並為平台服務之間的許多交互提供資料的完整性。 有關在中使用方案的詳細信 [!DNL Experience Platform]息，請從閱讀 [XDM系統概述開始](../xdm/home.md)。

### 時間系列事件

時間序列資料提供了對象直接或間接採取操作時系統的快照，以及詳細描述事件本身的資料。 由標準架構類別XDM ExperienceEvent表示，時間系列資料可說明事件，例如新增至購物車的項目、被點按的連結和檢視的視訊。 時間系列資料可用來建立區段規則，而事件則可在描述檔的內容中個別存取。

### 身份

每家企業都想以個人化的方式與客戶溝通。 不過，為客戶提供相關數位體驗的其中一項挑戰，是瞭解如何將互不相連的資料連結在一起，這通常會跨不同的數位通道（例如平板電腦、行動電話和筆記型電腦）傳播。 [!DNL Identity Service] 可讓您從多個通道連結身分，為每個客戶建立身份圖表，以便更好地瞭解客戶，從而將客戶的完整形象拼湊在一起。 如需詳細 [資訊，請造訪Identity Service](../identity-service/home.md) 總覽。

### 區段

Adobe Experience Platform可 [!DNL Segmentation Service] 為個別客戶提供體驗所需的受眾。 建立觀眾區段時，該區段的ID會新增至所有符合資格的設定檔的區段成員資格清單。 區段規則是使用REST風格的API [!DNL Real-time Customer Profile] 和「區段產生器」使用者介面建立並套用至資料。 若要進一步瞭解區段，請先閱讀區段服務 [概觀](../segmentation/home.md)。

### 描述檔片段和結合結構描述 {#profile-fragments-and-union-schemas}

多通道資料的統 [!DNL Real-time Customer Profile] 一性是其關鍵特點之一。 當用 [!DNL Real-time Customer Profile] 於訪問實體時，它可以為您提供該實體跨資料集的所有配置檔案片段的合併視圖（稱為聯合視圖），並通過稱為聯合模式實現。 [!DNL Real-time Customer Profile] 當實體或描述檔透過其ID存取或匯出為區段時，資料會跨來源合併。 若要進一步瞭解如何使用 [!DNL Real-time Customer Profile] API存取描述檔和工會檢視，請造訪 [實體端點指南](api/entities.md)。

### 合併原則

當從多個來源匯整資料並加以合併，以瞭解每個客戶的完整檢視時，合併原則是用來判斷資料的優先順序以及將哪些資料合併以建立統一檢視的規則。 [!DNL Platform] 使用REST風格的API或用戶介面，您可以建立新的合併策略、管理現有策略，並為組織設定預設的合併策略。 有關使用 [!DNL Real-time Customer Profile] API使用合併策略的詳細資訊，請參 [閱合併策](api/merge-policies.md)略端點指南。 要使用 [!DNL Experience Platform] UI處理合併策略，請參閱合 [並策略使用手冊](ui/merge-policies.md)。

### (Alpha)設定計算屬性

>[!IMPORTANT]
>本文中概述的計算屬性功能為alpha。 文件和功能可能會有所變更。

計算屬性可讓您根據其他值、計算和運算式自動計算欄位的值。 計算屬性在描述檔層級上運作，這表示您可以匯總所有記錄和事件的值。 每個計算屬性都包含一個運算式（或「規則」），可評估傳入的資料，並將產生的值儲存在描述檔屬性或事件中。 這些計算可協助您輕鬆回答與期限購買值、購買間隔時間或應用程式開啟次數等相關的問題，而不需在每次需要資訊時手動執行複雜的計算。 有關計算屬性的詳細資訊，以及使用 [!DNL Real-time Customer Profile] API使用這些屬性的逐步指示，請參閱計 [算屬性端點指南](api/computed-attributes.md)。 本指南將協助您進一步瞭解Adobe Experience Platform中計算屬性的角色，並包含執行基本CRUD作業的範例API呼叫。

## 即時元件

本節介紹可即時更 [!DNL Real-time Customer Profile] 新和監控記錄和時間序列資料的元件。

### 串流擷取與串流分段

透過稱為串流擷取的程式，即可進行即時輸入。 當擷取描述檔和時間系列資料時， [!DNL Real-time Customer Profile] 會自動決定透過稱為串流分段的持續程式，將該資料加入或排除區段中，然後將其與現有資料合併並更新聯合檢視。 因此，您可以即時執行計算並做出決策，以便客戶在與品牌互動時提供增強的個人化體驗。 在攝取資料時，也經過驗證，以確保正確攝取資料，並符合資料集所依據的架構。 如需擷取期間執行驗證的詳細資訊，請先閱讀資料擷取品質 [概觀](../ingestion/quality/overview.md)。

### 邊緣投影配置和目標

為即時跨多個通道為客戶提供協調、一致且個人化的體驗，需要隨時提供適當的資料，並在變更時持續更新。 Adobe Experience Platform可讓您透過使用所謂的邊緣，即時存取資料。 邊緣是地理位置優越的伺服器，可儲存資料，讓應用程式可輕鬆存取。 例如，Adobe Target和Adobe Campaign等Adobe應用程式會利用優勢，即時提供個人化客戶體驗。 資料通過投影被路由到邊，投影目的地定義資料要發送到的邊，投影配置定義將在邊上提供的特定資訊。 若要進一步瞭解並開始使用 [!DNL Real-time Customer Profile] API處理投影，請參閱 [邊緣投影端點指南](api/edge-projections.md)。

## 新增資料至 [!DNL Real-time Customer Profile]

[!DNL Platform] 可設定成將記錄和時間系列資料傳送至 [!DNL Profile]，以支援即時串流擷取和批次擷取。 如需詳細資訊，請參閱教學課程，其中說明如 [何將資料新增至即時客戶個人檔案](tutorials/add-profile-data.md)。

>[!NOTE]
>
>透過Adobe解決方案收集的資 [!DNL Analytics Cloud]料，包括 [!DNL Marketing Cloud]、 [!DNL Advertising Cloud]和，會流入 [!DNL Experience Platform] 並吸收到中 [!DNL Profile]。

### [!DNL Profile] 擷取量度

可觀性洞察可讓您在Adobe Experience Platform中公開關鍵指標。 除了各種功 [!DNL Platform] 能的使用統計資料和效能指標 [!DNL Platform][!DNL Profile]，還有特定的相關量度可讓您深入瞭解傳入請求率、成功擷取率、收錄的記錄大小等。 若要進一步瞭解，請先閱讀「可觀 [性洞察」概觀](../observability/home.md)，並取得完整的量度清單， [!DNL Profile] 請參閱可用量度 [的檔案](../observability/metrics.md)。

## [!DNL Data governance] 和 [!DNL Privacy]

[!DNL Data governance] 是用於管理客戶資料並確保遵守適用於資料使用的法規、限制和政策的一系列策略和技術。

由於與訪問資料有關，資料治理在各個級別 [!DNL Experience Platform] 中起關鍵作用：
* 資料使用標籤
* 資料存取策略
* 對行銷動作資料的存取控制

[!DNL Data governance] 在幾個點進行管理。 這包括決定在擷取特定行 [!DNL Platform] 銷動作之後，要擷取哪些資料，以及可存取哪些資料。 如需詳細資訊，請先閱讀資料管 [理概觀](../data-governance/home.md)。

### 處理退出和資料隱私權要求

[!DNL Experience Platform] 可讓客戶傳送與其資料使用和儲存相關的退出要求 [!DNL Real-time Customer Profile]。 如需如何處理退出要求的詳細資訊，請參閱有關執行退出 [要求的檔案](../segmentation/honoring-opt-outs.md)。

## [!DNL Profile] 准則

[!DNL Experience Platform] 有一系列的指導方針，以便有效使用 [!DNL Profile]。

| 章節 | 邊界 |
| ------- | -------- |
| [!DNL Profile] 聯合模式 | 最多可以 **為** 20個資料集貢獻聯合 [!DNL Profile] 模式。 |
| 多實體關係 | 最多可以 **建立** 5個多實體關係。 |
| 多實體關聯的JSON深度 | JSON深度上限為 **4**。 |
| 時間序列資料 | 非人員實體 **不** 允 [!DNL Profile] 許使用時間系列資料。 |
| 非人員結構關係 | 不允許非人員結構關係 **** 。 |
| 描述檔片段 | 建議的描述檔片段大小上限為 **10kB**。<br><br> 描述檔片段的絕對最大大小 **為1MB**。 |
| 非人員實體 | 單一非人員實體的最大總大小為 **200MB**。 |
| 每個非人實體的資料集 | 最多可以 **將** 1個資料集關聯到非人實體。 |

<!--
| Section | Boundary | Enforcement |
| ------- | -------- | ----------- |
| Profile union schema | A maximum of **20** datasets can contribute to the Profile union schema. | A message stating you've reached the maximum number of datasets appears. You must either disable or clean up other obsolete datasets in order to create a new dataset. |
| Multi-entity relationships | A maximum of **5** multi-entity relationship can be created. | A message stating all available mappings have been used appears when the fifth relationship is mapped. An error message letting you know you have exceeded the number of available mappings appears when attempting to map a sixth relationship. | 
| JSON depth for multi-entity association | The maximum JSON depth is **4**. | When trying to use the relationship selector with a field that is more than four levels deep, an error message appears, stating it is ineligible for multi-entity association. |
| Time series data | Time-series data is **not** permitted in Profile for non-people entities. | A message stating that this data cannot be enabled for Profile because it is of an unsupported type appears. |
| Non-people schema relationships | Non-people schema relationships are **not** permitted. | Relationships between two non-people schemas cannot be created. The relationships checkbox will be disabled. |
| Profile fragment | The recommended maximum size of a profile fragment is **10kB**.<br><br> The absolute maximum size of a profile fragment is **1MB**. | If you upload a fragment that is larger than 10kB, a warning appears, stating that performance may be degraded since the fragment exceeds the recommended maximum working size.<br><br> If you upload a fragment that is larger than 1MB, ingestion will fail, and an alert letting you know that records have failed will be sent. |
| Non-person entity | The maximum total size for a single non-person entity is **200MB**. | If you load an object as a non-person entity that is larger than 200MB, an alert will appear, stating that the entity has exceeded the maximum allowable size and will not be useable for segmentation. |
| Datasets per non-person entity | A maximum of **1** dataset can be associated to a non-person entity. | If you try to create a second dataset that is associated to the same non-person entity, an error appears, stating that only one dataset can be active per non-person entity. |

--->

>[!NOTE]
>
>
>非人員實體是指不屬於的任 **何** XDM類 [!DNL Profile]。

## 後續步驟和其他資源

若要進一步了 [!DNL Real-time Customer Profile]解，請繼續閱讀檔案，並透過觀看以下影片或探索其他 [Experience Platform教學課程，來補充您的學習](https://docs.adobe.com/content/help/en/platform-learn/tutorials/overview.html)。

>[!WARNING]
>下 [!DNL Platform] 列視訊中顯示的UI已過期。 如需最新的UI熒 [幕擷取和功能](ui/user-guide.md) ，請參閱即時客戶個人檔案使用指南。

>[!VIDEO](https://video.tv.adobe.com/v/27251?quality=12)