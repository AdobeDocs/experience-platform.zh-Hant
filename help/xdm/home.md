---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 體驗資料模型(XDM)系統
topic: overview
translation-type: tm+mt
source-git-commit: c07f926a71447e840c692ed15e85c9e02f1106ab

---


# XDM系統概述

標準化和互操作性是Adobe Experience Platform的主要概念。 Adobe推動的Experience Data Model(XDM)旨在標準化客戶體驗資料並定義客戶體驗管理的架構。

XDM是公開記載的規格，旨在改善數位體驗的強大功能。 它為用於與平台服務通訊的任何應用程式提供通用結構和定義。 遵循XDM標準，所有客戶體驗資料都可整合在共同的呈現方式中，以更快速、更整合的方式提供見解。 您可以從客戶行動中獲得寶貴見解，透過細分定義客戶受眾，並表達客戶屬性以利個人化。

XDM是基礎架構，可讓採用Experience Platform的Adobe Experience Cloud在適當的時機，透過適當的通道向適當的人傳遞適當的訊息。 建立Experience Platform的方法- **XDM System**，可操作Experience Data Model架構，供Platform服務使用。

本檔案概述XDM系統在Experience Platform中的角色。

## XDM架構

Experience Platform使用結構描述，以一致且可重複使用的方式來描述資料結構。 透過跨系統一致地定義資料，保留意義並從資料中獲取價值變得更容易。

在將資料引入平台之前，必須構建一個模式來描述資料的結構，並為每個欄位中可包含的資料類型提供約束。 結構描述由基類和零個或多個混合組成。

如需架構構成模型的詳細資訊，包括設計原則和最佳實務，請參閱架構 [構成的基本資訊](schema/composition.md)。

### 架構註冊表和架構庫

架構注 **冊表提供使用者介面和REST風格的API** ，您可從中檢視並管理Adobe Experience Platform **Schema Library中所有與架構相關的資**&#x200B;源。 架構庫包含Adobe提供給您的業界標準資源，以及Experience Platform合作夥伴和您使用應用程式的廠商所提供的資源。 Schema Registry UI和API也可用於建立和管理組織特有的新架構和資源。

有關「架構註冊表」中可用主要操作的完整指南，請參 [閱「架構註冊表」開發人員指南](api/getting-started.md)。

## XDM系統中的資料行為 {#data-behaviors}

用於Experience Platform的資料分為兩種行為類型：

* **記錄資料**:提供主題屬性的相關資訊。 主題可以是組織或個人。
* **時間系列資料**:提供記錄主體直接或間接採取操作時系統的快照。

所有XDM結構描述的資料可以分類為記錄或時間序列。 方案的資料行為由方案的類定 **義**，該類在首次建立方案時被分配給方案。 XDM類描述了模式必須包含的最小屬性數，以表示特定資料行為。

雖然您可以在架構註冊表中定義自己的類，但建議您分別使用偏好的類 **XDM Individual Profile** 和 **XDM ExperienceEvent** ，來記錄和時間序列資料。 下面將詳細說明這些類別。

### XDM個人資料

XDM Individual Profile是基於記錄的類，它對已識別和部分識別的主體的屬性形成奇異表示。 高度識別的個人檔案可用於個人通訊或目標互動，且可包含詳細的個人資訊，例如姓名、性別、出生日期、地點和聯絡資訊，包括電話號碼和電子郵件地址。

識別不詳的描述檔可能只包含匿名行為訊號，例如瀏覽器Cookie。 在這種情況下，稀疏的配置檔案資料被用於構建一個資訊庫，其中收集和儲存匿名配置檔案的興趣和偏好。 隨著主體註冊通知、訂閱、購買等，這些識別碼可能會隨著時間變得更詳細。 這種描述檔屬性的增加可能最終導致已識別的主題，並可提高目標參與度。

隨著消費者個人檔案的不斷成長，它成為個人個人資訊、身分識別資訊、聯絡資訊和通訊偏好的強穩儲存庫。

### XDM ExperienceEvent

XDM ExperienceEvent是以時間序列為基礎的類別，用於在發生事件（或事件集）時擷取系統狀態，包括所涉主題的時間點和身分。 「體驗事件」是所發生事件的事實記錄，因此它們是不可變的，不經匯總或解譯即代表所發生的事件。 它們對於時域分析至關重要，因為它們可用於分析特定時段內發生的變更，以及比較多個時段以追蹤趨勢。

「體驗事件」可以是明確或隱含的。 明確事件是直接觀察到的人類行為在旅程的某個時刻發生。 隱含事件是指在沒有直接人類行動的情況下引發，但仍與個人有關的事件。 隱式事件的範例包括排程傳送電子郵件電子報或電池電壓達到特定臨界值。

雖然並非所有事件都可輕鬆分類至所有資料來源，但在可能的情況下將類似事件協調為類似類型以進行處理是非常有價值的。

![ExperienceEvent客戶歷程](images/overview/experience-event-journey.png)

## XDM架構和Experience Platform服務

Experience Platform與架構無關，這表示符合XDM標準的任何架構都可供平台服務使用。 以下將詳細說明不同平台服務使用結構描述的方式。

### 型錄服務、資料擷取與資料湖

目錄服務是Experience Platform資產及其相關架構的記錄系統。 目錄不是包含資料的實際檔案或目錄，而是包含這些檔案和目錄的元資料和說明。

目錄資料會儲存在資料湖中，這是高度精細的資料存放區，包含平台管理的所有資料，不論來源或檔案格式為何。

若要開始將資料擷取至Experience Platform，請使用Catalog Service建立資料集。 該資料集引用描述要攝取的資料的結構的XDM模式。 如果建立資料集時沒有架構，Experience Platform會透過檢查所擷取資料欄位的類型和內容來衍生「觀察到的架構」。 資料集隨後在目錄中被跟蹤並儲存在資料湖中，與它們所基於的模式和觀察到的模式一起儲存。

如需目錄的詳細資訊，請參閱目錄 [服務概觀](../catalog/home.md)。 如需Adobe Experience Platform資料擷取的詳細資訊，請參閱資料擷取 [概觀](../ingestion/home.md)。

### 查詢服務

Adobe Experience Platform查詢服務可讓您使用標準SQL來查詢Experience Platform資料，以支援許多不同的使用案例。

在構成模式並建立引用該模式的資料集後，資料隨後被提取並儲存在資料湖中。 使用查詢服務，您可以加入資料湖中的任何資料集，並將查詢結果擷取為新資料集，以用於報告、機器學習或擷取至即時客戶個人檔案。

若要進一步瞭解查詢服務，請參閱查詢 [服務簡介](../query-service/home.md)。

### 即時客戶個人檔案

即時客戶個人檔案提供集中的消費者個人檔案，以進行針對性的個人化體驗管理。 每個描述檔都包含匯總至所有系統的資料，以及與您使用Experience Platform的任何系統中發生之個人相關之事件的可操作時間戳記帳戶。

即時客戶描述檔會根據XDM個人描述檔或XDM ExperienceEvent類別，使用架構格式化資料，並根據該資料回應查詢。 配置檔案不支援基於其他類使用方案。

描述檔會維護每個客戶描述檔的例項，將資料合併為個人的「單一真相來源」。 此統一資料使用所謂的「聯合檢視」來表示。 聯合視圖將實施相同類的所有方案的欄位聚合到單個方案中。  使用UI或API合成架構時，您可以啟用該架構以便與即時客戶描述檔搭配使用，並標籤它以便加入聯合檢視中。 然後，標籤的架構將參與提供給Profile的架構定義。

當XDM個人資料和XDM ExperienceEvent資料由Catalog擷取和管理時，它會觸發即時客戶資料，開始擷取已啟用使用的資料。 所擷取的互動與詳細資訊越多，個別描述檔就越強穩。

XDM個人設定檔資料有助於透過任何通道或Adobe解決方案整合，為行動提供資訊並賦予其能力，而且，當行為與互動資料的豐富歷史記錄搭配使用時，這些資料將用來推動機器學習。 即時客戶個人檔案API也可用來豐富協力廠商解決方案、CRM和專屬解決方案的功能。

如需詳 [細資訊，請參閱即時客戶個人檔案](../profile/home.md) 。

### 資料科學工作區

Adobe Experience Platform Data Science Workspace使用機器學習和人工智慧，從Experience Platform中儲存的資料獲取見解。 Data Science Workspace讓資料科學家能夠根據XDM個人資料和XDM ExperienceEvent客戶及其活動的資料來建立配方，以利預測購買傾向，並推薦個人可能喜歡和使用的優惠。

有了Data Science Workspace，資料科學家就可輕鬆建立以機器學習為基礎的智慧服務API。 這些服務可與其他Adobe解決方案搭配使用，包括Adobe Target和Adobe Analytics Cloud，協助您自動化個人化、針對性的數位體驗。

如需使用Experience Platform資料強化見解的詳細資訊，請參閱資料科 [學工作區概觀](../data-science-workspace/home.md)。

### 決策服務

決策服務提供在平台整合應用程式中設定個人化優惠決策的功能。 選件可以是產品建議、網頁體驗的內容元件、對話指令碼和要採取的動作。

決策服務利用即時客戶配置檔案資料，因此僅與基於實施XDM單個配置檔案或XDM ExperienceEvent類的方案的資料集相容。

如需詳細 [資訊，請參閱決策服務](../decisioning-service/home.md) 概觀。

## 後續步驟

現在，您已更清楚瞭解整個Experience Platform中結構描述的角色，因此，您已準備好開始自行撰寫。

若要瞭解構圖的設計原則和最佳範例，以便與Experience Platform搭配使用，請先閱讀架構構 [成的基本概念](schema/composition.md)。 如需如何建立架構的逐步指示，請參閱使用API或使用使用者介 [面建立架構](tutorials/create-schema-api.md)[的教學課程](tutorials/create-schema-ui.md)。