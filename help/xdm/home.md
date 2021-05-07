---
keywords: Experience Platform；主題；熱門主題；XDM;XDM系統；XDM個人配置檔案；XDM ExperienceEvent;XDM ExperienceEvent;XDM ExperienceEvent；體驗事件；欄位組；欄位組；欄位組；體驗事件；XDM ExperienceEvent;xdm Experienceevent;experience資料模型；Experience資料模型；Experience Data Model；資料模型；資料模型；模式註冊表；模式庫；模式庫；模式庫；模式庫；模式；記錄資料；時間序列；時間序列
solution: Experience Platform
title: XDM系統概述
topic-legacy: overview
description: 標準化和互操作性是Adobe Experience Platform背後的關鍵概念。 Experience Data Model(XDM)是由Adobe驅動，旨在標準化客戶體驗資料並定義客戶體驗管理的架構。
exl-id: 294d5f02-850f-47ea-9333-8b94a0bb291e
translation-type: tm+mt
source-git-commit: b70e693b4ffeda561de4d4c8dd8fd1adeec489f7
workflow-type: tm+mt
source-wordcount: '1694'
ht-degree: 1%

---

# XDM系統概述

>[!NOTE]
>
>詞語&quot;mixin&quot;已更新為架構&quot;欄位群組&quot;，以增進瞭解。 欄位群組是可重複使用的欄位集，可支援商業使用案例。 此變更現在會反映在「架構註冊表API」、「Adobe Experience PlatformUI」和所有平台檔案中。

標準化和互操作性是Adobe Experience Platform背後的關鍵概念。 [!DNL Experience Data Model] (XDM)由Adobe驅動，旨在標準化客戶體驗資料並定義客戶體驗管理的架構。

XDM是公開記載的規格，旨在改善數位體驗的強大功能。 它為用於與[!DNL Platform]服務通信的任何應用程式提供了通用結構和定義。 遵循XDM標準，所有客戶體驗資料都可整合在共同的呈現方式中，以更快速、更整合的方式提供見解。 您可以從客戶行動中獲得寶貴見解，透過細分定義客戶受眾，並表達客戶屬性以利個人化。

XDM是基礎性的框架，它讓[!DNL Experience Platform]的Adobe Experience Cloud能夠在正確的時刻，在正確的通道上向適當的人傳遞合適的資訊。 構建[!DNL Experience Platform]的方法XDM系統操作[!DNL Experience Data Model]方案，以供[!DNL Platform]服務使用。

本文檔概述了[!DNL Experience Platform]中XDM系統的角色。

## XDM架構

[!DNL Experience Platform] 會使用結構，以一致且可重複使用的方式說明資料結構。藉由定義跨系統的一致資料，將可輕易保留意義，而發揮資料應有的價值。

在將資料收錄到[!DNL Platform]之前，必須構成一個模式，以說明資料的結構並為每個欄位中可包含的資料類型提供約束條件。 方案由基本類和零個或多個方案欄位組組成。

有關架構構成模型（包括設計原則和最佳實踐）的詳細資訊，請參閱[架構構成基礎](schema/composition.md)。

### [!DNL Schema Registry] 和 [!DNL Schema Library]

**[!DNL Schema Registry]**&#x200B;提供了用戶介面和REST風格的API，您可以從中查看和管理Adobe Experience Platform **[!DNL Schema Library]**&#x200B;中所有與模式相關的資源。 [!DNL Schema Library]包含您依Adobe提供的業界標準資源，以及您使用應用程式的[!DNL Experience Platform]合作夥伴和廠商的資源。 Schema Registry UI和API也可用於建立和管理組織特有的新架構和資源。

有關[!DNL Schema Registry]中主要操作的完整指南，請參閱[方案註冊表開發人員指南](api/getting-started.md)。

## XDM系統中的資料行為{#data-behaviors}

用於[!DNL Experience Platform]的資料被分為兩種行為類型：

* **記錄資料**:提供主題屬性的相關資訊。主題可以是組織或個人。
* **時間系列資料**:提供記錄主體直接或間接採取操作時系統的快照。

所有XDM結構描述的資料可以分類為記錄或時間序列。 架構的資料行為由架構的類定義，該類在初次建立時被分配給架構。 XDM類描述了模式必須包含的最小屬性數，以表示特定資料行為。

雖然您可以在[!DNL Schema Registry]中定義自己的類，但建議您分別使用首選的類&#x200B;**[!DNL XDM Individual Profile]**&#x200B;和&#x200B;**[!DNL XDM ExperienceEvent]**&#x200B;用於記錄和時間系列資料。 下面將詳細說明這些類別。

### [!DNL XDM Individual Profile] {#xdm-individual-profile}

[!DNL XDM Individual Profile] 是基於記錄的類，它對已識別和部分已識別的主題的屬性形成奇異表示。高度識別的個人檔案可用於個人通訊或目標互動，且可包含詳細的個人資訊，例如姓名、性別、出生日期、地點和聯絡資訊，包括電話號碼和電子郵件地址。

識別不詳的描述檔可能只包含匿名行為訊號，例如瀏覽器Cookie。 在這種情況下，稀疏的配置檔案資料被用於構建一個資訊庫，其中收集和儲存匿名配置檔案的興趣和偏好。 隨著主體註冊通知、訂閱、購買等，這些識別碼可能會隨著時間變得更詳細。 這種描述檔屬性的增加可能最終導致已識別的主題，並可提高目標參與度。

隨著消費者個人檔案的不斷成長，它成為個人個人資訊、身分識別資訊、聯絡資訊和通訊偏好的強穩儲存庫。

### [!DNL XDM ExperienceEvent] {#xdm-experience-event}

XDM ExperienceEvent是以時間序列為基礎的類別，用於在發生事件（或事件集）時擷取系統狀態，包括所涉主題的時間點和身分。 「體驗事件」是所發生事件的事實記錄，因此它們是不可變的，不經匯總或解譯即代表所發生的事件。 它們對於時域分析至關重要，因為它們可用於分析特定時間範圍內發生的變更，以及比較多個時間窗口以追蹤趨勢。

「體驗事件」可以是明確或隱含的。 明確事件是直接觀察到的人類行為在旅程的某個時刻發生。 隱含事件是指在沒有直接人類行動的情況下引發，但仍與個人有關的事件。 隱式事件的範例包括排程傳送電子郵件電子報或電池電壓達到特定臨界值。

雖然並非所有事件都可輕鬆分類至所有資料來源，但在可能的情況下將類似事件協調為類似類型以進行處理是非常有價值的。

![ExperienceEvent客戶歷程](images/overview/experience-event-journey.png)

## XDM方案和[!DNL Experience Platform]服務

[!DNL Experience Platform] 是模式不可知的，這意味著任何符合XDM標準的模式都可供服務使 [!DNL Platform] 用。以下詳細說明了不同[!DNL Platform]服務使用結構描述的方式。

### [!DNL Catalog Service], [!DNL Data Ingestion] &amp; [!DNL Data Lake]

[!DNL Catalog Service] 是資產及其相關結 [!DNL Experience Platform] 構的記錄系統。[!DNL Catalog] 不是包含資料的實際檔案或目錄，而是包含這些檔案和目錄的元資料和說明。

[!DNL Catalog] 資料會儲存在高度 [!DNL Data Lake]精細的資料儲存區中，其中包含所有由管理的資料，不 [!DNL Platform]論來源或檔案格式為何。

若要開始將資料擷取至[!DNL Experience Platform]，請使用[!DNL Catalog Service]建立資料集。 該資料集引用描述要攝取的資料的結構的XDM模式。 如果建立的資料集沒有模式， [!DNL Experience Platform]將通過檢查所收錄資料欄位的類型和內容來導出「觀察到的模式」。 然後，在[!DNL Catalog]中跟蹤資料集，並將其與它們所基於的方案和觀察到的方案一起儲存在[!DNL Data Lake]中。

有關[!DNL Catalog]的詳細資訊，請參閱[目錄服務概述](../catalog/home.md)。 有關Adobe Experience Platform資料提取的詳細資訊，請參閱[資料提取概述](../ingestion/home.md)。

### [!DNL Query Service]

Adobe Experience Platform[!DNL Query Service]允許您使用標準SQL查詢[!DNL Experience Platform]資料以支援許多不同的使用案例。

構成模式並建立引用該模式的資料集後，資料會被收錄並儲存在[!DNL Data Lake]中。 使用[!DNL Query Service]，您可以將[!DNL Data Lake]中的任何資料集連接起來，並將查詢結果擷取為新資料集，以用於報告、機器學習或擷取至[!DNL Real-time Customer Profile]。

若要進一步瞭解[!DNL Query Service]，請參閱[查詢服務簡介](../query-service/home.md)。

### [!DNL Real-time Customer Profile]

即時客戶個人檔案提供集中化的消費者個人檔案，以進行針對性的個人化體驗管理。 每個描述檔都包含所有系統匯總的資料，以及與您使用[!DNL Experience Platform]的任何系統中發生的個別事件相關的可操作時間戳記帳戶。

[!DNL Real-time Customer Profile] 根據或類來使用模式格式 [!DNL XDM Individual Profile] 化 [!DNL XDM ExperienceEvent] 資料，並基於該資料響應查詢。[!DNL Profile] 不支援基於其他類的方案使用。

[!DNL Profile] 維護每個客戶個人檔案的例項，將資料合併在一起，為個人形成「單一真相來源」。此統一資料使用所謂的「聯合檢視」來表示。 聯合視圖將實施相同類的所有方案的欄位聚合到單個方案中。  使用UI或API合成架構時，可以啟用該架構以與[!DNL Real-time Customer Profile]一起使用，並將其標籤為包含在聯合視圖中。 然後，標籤的架構將參與被饋送到[!DNL Profile]的架構定義。

當[!DNL XDM Individual Profile]和[!DNL XDM ExperienceEvent]資料由[!DNL Catalog]收錄和管理時，會觸發[!DNL Real-time Customer Profile]開始收錄已啟用使用的資料。 所擷取的互動與詳細資訊越多，個別描述檔就越強穩。

[!DNL XDM Individual Profile] 資料有助於通過任何通道或Adobe解決方案整合，為行動提供資訊並賦予其能力，而且當資料與行為與互動資料的豐富歷史記錄搭配使用時，這些資料將用來推動機器學習。[!DNL Real-time Customer Profile] API也可用來豐富協力廠商解決方案、CRM和專屬解決方案的功能。

如需詳細資訊，請參閱[即時客戶個人資料概觀](../profile/home.md)。

### [!DNL Data Science Workspace]

Adobe Experience Platform[!DNL Data Science Workspace]使用機器學習和人工智慧，從儲存在[!DNL Experience Platform]中的資料獲得見解。 [!DNL Data Science Workspace] 讓資料科學家根據XDM個人和客戶及其活動 [!DNL Profile] 的 [!DNL XDM ExperienceEvent] 資料來建立食譜，以促進購買傾向等預測，並推薦個人可能喜歡和使用的優惠。

有了[!DNL Data Science Workspace]，資料科學家就可輕鬆建立由機器學習提供支援的智慧服務API。 這些服務可與其他Adobe解決方案(包括Adobe Target和Adobe Analytics Cloud)搭配使用，協助您自動化個人化、針對性的數位體驗。

有關使用[!DNL Experience Platform]資料強化見解的詳細資訊，請參閱[資料科學工作區概觀](../data-science-workspace/home.md)。

## 後續步驟和其他資源

現在，您已更清楚瞭解架構在[!DNL Experience Platform]中的角色，您就可以開始自行撰寫。 若要繼續補充您的學習，請先閱讀建議的檔案，然後觀看以下影片。

要瞭解構建方案的設計原則和最佳做法，請首先閱讀方案構建的[基礎知識](schema/composition.md)。 [!DNL Experience Platform]有關如何建立架構的逐步說明，請參閱有關使用API](tutorials/create-schema-api.md)或[使用用戶介面](tutorials/create-schema-ui.md)建立架構[的教程。

若要進一步瞭解[!DNL Experience Platform]中的[!DNL XDM System]，請觀看以下影片：

>[!VIDEO](https://video.tv.adobe.com/v/27105?quality=12&learn=on)
