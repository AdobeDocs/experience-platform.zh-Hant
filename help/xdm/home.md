---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 體驗資料模型(XDM)系統
topic: overview
translation-type: tm+mt
source-git-commit: d04bf35e49488ab7d5e07de91eb77d0d9921b6fa
workflow-type: tm+mt
source-wordcount: '1606'
ht-degree: 0%

---


# XDM系統概述

標準化和互操作性是Adobe Experience Platform的主要概念。 [!DNL Experience Data Model] (XDM)是由Adobe推動，旨在標準化客戶體驗資料並定義客戶體驗管理的架構。

XDM是公開記載的規格，旨在改善數位體驗的強大功能。 它為用於與服務通訊的任何應用程式提供通用結構和 [!DNL Platform] 定義。 遵循XDM標準，所有客戶體驗資料都可整合在共同的呈現方式中，以更快速、更整合的方式提供見解。 您可以從客戶行動中獲得寶貴見解，透過細分定義客戶受眾，並表達客戶屬性以利個人化。

XDM是基礎架構，可讓Adobe Experience Cloud在適當的時機，在適當的通道上，在適當的時機，向適當的人傳遞適當的訊息。 [!DNL Experience Platform]構建的方 [!DNL Experience Platform] 法— **XDM System**—操作模式 [!DNL Experience Data Model] 供服務 [!DNL Platform] 使用。

本文檔概述了XDM系統在中的角色 [!DNL Experience Platform]。

## XDM架構

[!DNL Experience Platform] 使用結構描述以一致且可重複使用的方式來描述資料結構。 透過跨系統一致地定義資料，保留意義並從資料中獲取價值變得更容易。

在將資料收入 [!DNL Platform]之前，必須構成一個模式以描述資料的結構，並為每個欄位中可包含的資料類型提供約束。 結構描述由基類和零個或多個混合組成。

如需架構構成模型的詳細資訊，包括設計原則和最佳實務，請參閱架構 [構成的基本資訊](schema/composition.md)。

### [!DNL Schema Registry] 和 [!DNL Schema Library]

提 **[!DNL Schema Registry]** 供使用者介面和REST風格的API，您可從中檢視和管理Adobe Experience Platform中所有與架構相關的資源 **[!DNL Schema Library]**。 本 [!DNL Schema Library] 文包含Adobe提供給您的業界標準資源，以及您所使用應用程式的合作夥伴 [!DNL Experience Platform] 和廠商所提供的資源。 Schema Registry UI和API也可用於建立和管理組織特有的新架構和資源。

如需有關中主要操作的完整指南，請參 [!DNL Schema Registry]閱「方案注 [冊表開發人員指南」](api/getting-started.md)。

## XDM系統中的資料行為 {#data-behaviors}

要用於的資料會 [!DNL Experience Platform] 分為兩種行為類型：

* **記錄資料**: 提供主題屬性的相關資訊。 主題可以是組織或個人。
* **時間系列資料**: 提供記錄主體直接或間接採取操作時系統的快照。

所有XDM結構描述的資料可以分類為記錄或時間序列。 方案的資料行為由方案的類定 **義**，該類在首次建立方案時被分配給方案。 XDM類描述了模式必須包含的最小屬性數，以表示特定資料行為。

雖然您可以在中定義自己的類 [!DNL Schema Registry]，但建議您分別使用首選類 **[!DNL XDM Individual Profile]****[!DNL XDM ExperienceEvent]** 和記錄和時間序列資料。 下面將詳細說明這些類別。

### [!DNL XDM Individual Profile]

[!DNL XDM Individual Profile] 是基於記錄的類，它對已識別和部分已識別的主題的屬性形成奇異表示。 高度識別的個人檔案可用於個人通訊或目標互動，且可包含詳細的個人資訊，例如姓名、性別、出生日期、地點和聯絡資訊，包括電話號碼和電子郵件地址。

識別不詳的描述檔可能只包含匿名行為訊號，例如瀏覽器Cookie。 在這種情況下，稀疏的配置檔案資料被用於構建一個資訊庫，其中收集和儲存匿名配置檔案的興趣和偏好。 隨著主體註冊通知、訂閱、購買等，這些識別碼可能會隨著時間變得更詳細。 這種描述檔屬性的增加可能最終導致已識別的主題，並可提高目標參與度。

隨著消費者個人檔案的不斷成長，它成為個人個人資訊、身分識別資訊、聯絡資訊和通訊偏好的強穩儲存庫。

### [!DNL XDM ExperienceEvent]

XDM ExperienceEvent是以時間序列為基礎的類別，用於在發生事件（或事件集）時擷取系統狀態，包括所涉主題的時間點和身分。 「體驗事件」是所發生事件的事實記錄，因此它們是不可變的，不經匯總或解譯即代表所發生的事件。 它們對於時域分析至關重要，因為它們可用於分析特定時段內發生的變更，以及比較多個時段以追蹤趨勢。

「體驗事件」可以是明確或隱含的。 明確事件是直接觀察到的人類行為在旅程的某個時刻發生。 隱含事件是指在沒有直接人類行動的情況下引發，但仍與個人有關的事件。 隱式事件的範例包括排程傳送電子郵件電子報或電池電壓達到特定臨界值。

雖然並非所有事件都可輕鬆分類至所有資料來源，但在可能的情況下將類似事件協調為類似類型以進行處理是非常有價值的。

![ExperienceEvent客戶歷程](images/overview/experience-event-journey.png)

## XDM架構和服 [!DNL Experience Platform] 務

[!DNL Experience Platform] 是模式不可知的，這意味著任何符合XDM標準的模式都可供服務使 [!DNL Platform] 用。 下面將詳細說明不 [!DNL Platform] 同服務使用結構描述的方式。

### [!DNL Catalog Service], [!DNL Data Ingestion] &amp; [!DNL Data Lake]

[!DNL Catalog Service] 是資產及其相關結 [!DNL Experience Platform] 構的記錄系統。 [!DNL Catalog] 不是包含資料的實際檔案或目錄，而是包含這些檔案和目錄的元資料和說明。

[!DNL Catalog] 資料會儲存在高度 [!DNL Data Lake]精細的資料儲存區中，其中包含所有由管理的資料，不 [!DNL Platform]論來源或檔案格式為何。

若要開始將資料收 [!DNL Experience Platform]入資料，請使用建立資料集 [!DNL Catalog Service]。 該資料集引用描述要攝取的資料的結構的XDM模式。 如果建立的資料集沒有模式， [!DNL Experience Platform] 將通過檢查所收錄資料欄位的類型和內容來導出「觀察到的模式」。 然後，資料集將被跟 [!DNL Catalog] 蹤並與其所基 [!DNL Data Lake] 於的模式和觀察到的模式一起儲存在中。

如需詳細資訊， [!DNL Catalog]請參閱目錄 [服務概觀](../catalog/home.md)。 如需Adobe Experience Platform資料擷取的詳細資訊，請參閱資料擷取 [概觀](../ingestion/home.md)。

### [!DNL Query Service]

Adobe Experience Platform可 [!DNL Query Service] 讓您使用標準SQL來查詢資料， [!DNL Experience Platform] 以支援許多不同的使用案例。

在構成模式並建立引用該模式的資料集後，資料隨後被提取並儲存在中 [!DNL Data Lake]。 使用 [!DNL Query Service]時，您可以將任何資料集連結在中， [!DNL Data Lake] 並將查詢結果擷取為新資料集，以用於報告、機器學習或擷取 [!DNL Real-time Customer Profile]。

若要進一步了 [!DNL Query Service]解，請參閱查 [詢服務簡介](../query-service/home.md)。

### [!DNL Real-time Customer Profile]

即時客戶個人檔案提供集中的消費者個人檔案，以進行針對性的個人化體驗管理。 每個描述檔都包含匯總至所有系統的資料，以及與您使用的任何系統中發生之個別事件相關的可操作時間戳記帳戶 [!DNL Experience Platform]。

[!DNL Real-time Customer Profile] 根據或類來取用模式格 [!DNL XDM Individual Profile] 式化 [!DNL XDM ExperienceEvent] 資料，並基於該資料響應查詢。 [!DNL Profile] 不支援基於其他類的方案使用。

[!DNL Profile] 維護每個客戶個人檔案的例項，將資料合併在一起，為個人形成「單一真相來源」。 此統一資料使用所謂的「聯合檢視」來表示。 聯合視圖將實施相同類的所有方案的欄位聚合到單個方案中。  使用UI或API合成架構時，可以啟用該架構以便與一起使用，並 [!DNL Real-time Customer Profile] 將其標籤為包含在聯合視圖中。 然後，標籤的模式將參與要饋送到的模式定義 [!DNL Profile]。

當資 [!DNL XDM Individual Profile] 料被 [!DNL XDM ExperienceEvent] 擷取及管理時，會觸發 [!DNL Catalog][!DNL Real-time Customer Profile] 開始擷取已啟用其使用功能的資料。 所擷取的互動與詳細資訊越多，個別描述檔就越強穩。

[!DNL XDM Individual Profile] 資料有助於透過任何通道或Adobe解決方案整合，為行動提供資訊並賦予其能力，當資料與豐富的行為與互動資料記錄搭配使用時，此資料可協助機器學習。 此 [!DNL Real-time Customer Profile] API也可用來豐富協力廠商解決方案、CRM和專屬解決方案的功能。

如需詳 [細資訊，請參閱即時客戶個人檔案](../profile/home.md) 。

### [!DNL Data Science Workspace]

Adobe Experience Platform使用 [!DNL Data Science Workspace] 機器學習和人工智慧，從儲存在內部的資料獲得見解 [!DNL Experience Platform]。 [!DNL Data Science Workspace] 讓資料科學家根據XDM個人和客戶及其活動的 [!DNL Profile] 資料 [!DNL XDM ExperienceEvent] ，來建立食譜，以促進購買傾向等預測，並建議個人可能會欣賞和使用的優惠。

有了這 [!DNL Data Science Workspace]項功能，資料科學家就可以輕鬆建立以機器學習為基礎的智慧型服務API。 這些服務可與其他Adobe解決方案搭配使用，包括Adobe Target和Adobe Analytics Cloud，協助您自動化個人化、針對性的數位體驗。

如需使用資料強化見 [!DNL Experience Platform] 解的詳細資訊，請參閱資 [料科學工作區概觀](../data-science-workspace/home.md)。

### [!DNL Decisioning Service]

[!DNL Decisioning Service] 提供在整合式應用程式中設定個人化優惠決策 [!DNL Platform]的能力。 選件可以是產品建議、網頁體驗的內容元件、對話指令碼和要採取的動作。

[!DNL Decisioning Service] 利用 [!DNL Real-time Customer Profile] 資料，因此僅與基於實作或類的架構的資料集 [!DNL XDM Individual Profile] 相 [!DNL XDM ExperienceEvent] 容。

如需詳細 [資訊，請參閱決策服務](../decisioning-service/home.md) 概觀。

## 後續步驟和其他資源

現在，您已更清楚瞭解架構在整個 [!DNL Experience Platform]過程中的角色，您已準備好開始自行編寫。 若要繼續補充您的學習，請先閱讀建議的檔案，然後觀看以下影片。

要瞭解合成要使用的架構的設計原則和最佳做法， [!DNL Experience Platform]請首先閱讀架構 [合成的基本知識](schema/composition.md)。 如需如何建立架構的逐步指示，請參閱使用API或使用使用者介 [面建立架構](tutorials/create-schema-api.md)[的教學課程](tutorials/create-schema-ui.md)。

若要強化您對中的 [!DNL XDM System] 了 [!DNL Experience Platform]解，請觀看以下影片：

>[!VIDEO](https://video.tv.adobe.com/v/27105?quality=12&learn=on)

