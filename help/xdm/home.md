---
keywords: Experience Platform；主題；熱門主題；XDM;XDM系統；XDM個人概況；XDM體驗事件；XDM體驗事件；XDM體驗事件；體驗事件；欄位組；欄位組；欄位組；體驗事件；XDM體驗事件；XDM體驗事件；體驗事件；體驗事件；XDM體驗事件XDM體驗資料模型；體驗資料模型；體驗資料模型；資料模型；資料模型；資料模型；模式註冊；模式註冊；模式庫；模式庫；模式庫；模式庫；記錄資料；時間序列；時間序列
solution: Experience Platform
title: XDM系統概述
description: 標準化和互操作性是Adobe Experience Platform背後的關鍵概念。 體驗資料模型(XDM)由Adobe驅動，旨在規範客戶體驗資料並定義客戶體驗管理模式。
exl-id: 294d5f02-850f-47ea-9333-8b94a0bb291e
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '2087'
ht-degree: 5%

---

# XDM 系統概觀

標準化和互操作性是Adobe Experience Platform背後的關鍵概念。 [!DNL Experience Data Model] (XDM)在Adobe的推動下，致力於標準化客戶體驗資料並定義客戶體驗管理模式。

XDM是一種公開記錄的規範，旨在提高數字型驗的威力。 它提供了通用的結構和定義，允許任何應用程式使用它們與平台服務通信。 通過遵守XDM標準，所有客戶體驗資料都可以納入到一種通用的表示形式中，這種表示形式能夠以更快、更整合的方式提供洞察力。 您可以從客戶操作中獲得有價值的見解，通過細分市場定義客戶受眾，並為個性化目的表達客戶屬性。

XDM是一個基礎框架，它讓Adobe Experience Cloud在Experience Platform的支援下，在正確的時間，在正確的渠道向正確的人傳遞正確的資訊。 構建Experience Platform的方法XDM系統 [!DNL Experience Data Model] 平台服務使用的架構。

本文檔概述了XDM系統在Experience Platform中的角色。

## XDM架構

Experience Platform 會使用結構，以一致且可重複使用的方式說明資料結構。藉由定義跨系統的一致資料，將可輕易保留意義，而發揮資料應有的價值。

在將資料引入平台之前，必須構建一個架構來描述資料的結構，並對每個欄位中可以包含的資料類型提供約束。 架構由基類和零個或多個架構欄位組組成。

有關架構組成模型（包括設計原則和最佳做法）的詳細資訊，請參見 [架構組合基礎](schema/composition.md)。

### 標準XDM元件

XDM提供了標準欄位組和資料類型的強健集合，這些類型旨在捕獲不同行業中的常見概念和使用案例。 Experience Platform允許您按行業篩選這些元件，使您能夠快速而自信地構建最能支援您特定業務需求的架構。

在Experience PlatformUI中構造架構時，將使用流行度量顯示列出的欄位組。 此度量由其他平台用戶在其架構中使用欄位組的頻率決定。 數字越高，欄位組就越受歡迎。 預設情況下，結果從最流行到最不流行，讓您隨時瞭解行業中的資料建模趨勢。

![欄位組受歡迎程度](./images/overview/popularity.png)

### [!DNL Schema Library]

Experience Platform提供用戶介面和REST風格的API，您可以從中查看和管理Experience Platform中所有與架構相關的資源 **[!DNL Schema Library]**。 的 [!DNL Schema Library] 包含通過Adobe提供給您的標準XDM元件，以及來自Experience Platform合作夥伴和供應商的資源，這些供應商的應用程式是您使用的。

使用 [!DNL Schema Registry API] 或 [!UICONTROL 架構] 工作區，您還可以建立和管理組織特有的新架構和資源。

有關如何管理平台中的架構並與其進行交互的詳細資訊，請參閱以下文檔：

* [XDM UI指南](./ui/overview.md)
* [架構註冊API指南](./api/overview.md)

## XDM系統中的資料行為 {#data-behaviors}

>[!CONTEXTUALHELP]
>id="platform_schemas_behavior"
>title="資料行為"
>abstract="用於 Experience Platform 的資料分為三種行為類型：記錄、時間序列和臨時。記錄方案會提供有關主體屬性的資訊，而時間序列方案則會在採取動作時擷取系統的快照。臨時方案會擷取僅供單一資料集使用的命名空間的欄位。如需有關 Platform 中資料行為的詳細資訊，請查看此文件。"

用於Experience Platform的資料分為三種行為類型：

* **記錄**:提供有關主題屬性的資訊。 主題可以是組織或個人。
* **時間序列**:提供記錄主題直接或間接執行操作時系統的快照。
* **臨時**:捕獲僅由單個資料集使用的同名欄位。 Ad-hoc模式用於各種資料接收工作流以進行Experience Platform，包括接收CSV檔案和建立某些類型的源連接。

所有XDM架構都描述可以分類為記錄或時間序列的資料。 架構的資料行為由架構的類定義，該類在首次建立架構時分配給該架構。 XDM類描述模式必須包含的最小屬性數以表示特定資料行為。

雖然您可以在 [!DNL Schema Registry]，建議使用標準類 **[!UICONTROL XDM個人配置檔案]** 和 **[!UICONTROL XDM體驗事件]** 記錄資料和時間序列資料。 下面將詳細介紹這些類。

>[!NOTE]
>
>沒有基於即席行為的標準類。 Ad-hoc模式由使用它們的平台進程自動生成，但也可以 [使用架構註冊表API手動建立](./tutorials/ad-hoc.md)。

### [!UICONTROL XDM 個別設定檔] {#xdm-individual-profile}

[!UICONTROL XDM個人配置檔案] 是基於記錄的類，它對已識別和部分識別的主題的屬性形成單一表示。 高度識別的配置檔案可用於個人通信或目標預訂，並且可以包含詳細的個人資訊，例如姓名、性別、出生日期、地點和聯繫資訊，包括電話號碼和電子郵件地址。

識別較少的配置檔案可能只包括諸如瀏覽器cookie之類的匿名行為信號。 在這種情況下，稀疏簡檔資料被用於構建資訊庫，在該資訊庫中整理和儲存匿名簡檔的興趣和偏好。 隨著主題註冊通知、訂閱、購買等，這些標識符可能會隨著時間的推移而變得更加詳細。 配置檔案屬性的這種增加最終可能導致已識別的主題，並允許更高程度的目標接觸。

隨著配置檔案的不斷增長，它將成為個人個人資訊、標識資訊、聯繫資訊和通信首選項的可靠儲存庫。

查看 [[!UICONTROL XDM個人配置檔案] 參考指南](./classes/individual-profile.md) 的子菜單。

### [!UICONTROL XDM體驗事件] {#xdm-experience-event}

XDM ExperienceEvent是基於時間序列的類，用於在發生事件（或事件集）時捕獲系統的狀態，包括所涉及主題的時間點和標識。 經驗事件是不可改變的，記錄當時發生的事實，代表所發生的事情，而不進行聚合或解釋。 它們對於時域分析至關重要，因為它們可用於分析給定時間窗口中發生的更改，以及在多個時間窗口之間進行比較以跟蹤趨勢。

「體驗事件」可以是顯式的，也可以是隱式的。 顯性事件是直接觀察到的人類行動，發生在旅途中的某一點。 隱含事件是指在沒有直接人類行動的情況下引發但仍然與個人有關的事件。 隱式事件的示例可包括預定發送電子郵件新聞稿或達到特定閾值的電池電壓。

雖然並非所有事件都可以在所有資料源中輕鬆分類，但在可能的情況下將類似事件協調為類似類型以供處理是極其有價值的。

![ExperienceEvent客戶行程](images/overview/experience-event-journey.png)

查看 [[!UICONTROL XDM體驗事件] 參考指南](./classes/experienceevent.md) 的子菜單。

## XDM架構和Experience Platform服務

Experience Platform與模式無關，這意味著任何符合XDM標準的模式都可供平台服務使用。 下面將詳細介紹不同平台服務使用架構的方式。

### 目錄服務、資料接收和資料湖

目錄服務是Experience Platform資產及其相關架構的記錄系統。 目錄不包含實際的資料檔案或目錄，而是包含這些檔案和目錄的元資料和說明。

目錄資料儲存在資料湖中，這是一個高度精細的資料儲存庫，它包含平台管理的所有資料，而不考慮源或檔案格式。

要開始將資料插入Experience Platform中，可以使用目錄服務建立資料集。 資料集引用描述要接收的資料結構的XDM模式。 如果建立資料集時沒有模式，則Experience Platform通過檢查所攝取資料欄位的類型和內容來導出「觀察模式」。 然後，資料集被跟蹤到目錄中，並儲存在資料湖中與它們所基於的模式和觀察的模式一起儲存。

有關目錄的詳細資訊，請參見 [目錄服務概述](../catalog/home.md)。 有關Adobe Experience Platform資料接收的詳細資訊，請參見 [資料接收概述](../ingestion/home.md)。

### 查詢服務

Adobe Experience Platform查詢服務允許您使用標準SQL查詢Experience Platform資料以支援許多不同的使用案例。

在構建模式並建立引用該模式的資料集後，資料隨後被攝取並儲存在資料湖中。 使用Query Service，您可以加入Data Lake中的任何資料集，並將查詢結果捕獲為新資料集，用於報告、機器學習或接收到即時客戶配置檔案。

請參閱 [查詢服務概述](../query-service/home.md) 的子菜單。

### 即時客戶設定檔

Real-Time Customer Profile（即時客戶配置檔案）為有針對性的個性化體驗管理提供集中的消費者配置檔案。 每個配置檔案都包含所有系統之間聚合的資料，以及可操作的時間戳事件帳戶，這些事件涉及您使用的任何系統中與Experience Platform一起發生的個人。

即時客戶配置檔案使用基於 [!UICONTROL XDM個人配置檔案] 和 [!UICONTROL XDM體驗事件] 類，並基於該資料響應查詢。 配置檔案不支援基於其他類的架構的使用。

該系統維護每個客戶概要檔案的實例，將資料合併在一起，為個人形成「單一真相源」。 此統一資料使用稱為「聯合架構」（有時稱為「聯合視圖」）來表示。 聯合架構將實現相同類的所有架構的欄位聚合到單個架構中。  使用UI或API合成架構時，可以啟用該架構以與即時客戶配置檔案一起使用，並將其標籤以包含在聯合中。 然後，標籤的架構將參與饋送到配置檔案的架構定義。

作為 [!UICONTROL XDM個人配置檔案] 和 [!UICONTROL XDM體驗事件] 資料會被引入資料湖，即時客戶配置檔案會接收任何已啟用以供使用的資料。 所攝取的交互和細節越多，個體輪廓就變得越強健。

[!UICONTROL XDM個人配置檔案] 資料有助於通過任何渠道或Adobe產品整合來通知和支援操作。 當與豐富的行為和交互資料歷史配對時，此資料可用於推動機器學習。 即時客戶配置檔案API還可用於豐富第三方解決方案、 CRM和專有解決方案的功能。

查看 [即時客戶概要資訊概述](../profile/home.md) 的子菜單。

### Data Science Workspace

Adobe Experience Platform資料科學工作區利用機器學習和人工智慧從儲存在Experience Platform中的資料中獲得洞見。 資料科學工作區允許資料科學家根據 [!UICONTROL XDM個人配置檔案] 和 [!UICONTROL XDM體驗事件] 有關客戶及其活動的資料，促進了購買傾向等預測，並推薦了個人可能會升值和使用的產品。

借助資料科學工作區，資料科學家可以輕鬆建立由機器學習提供動力的智慧服務API。 這些服務與其他Adobe解決方案(包括Adobe Target和Adobe Analytics Cloud)協作，幫助您自動化個性化、有針對性的數字型驗。

有關使用Experience Platform資料來增強洞察力的詳細資訊，請參閱 [資料科學工作區概述](../data-science-workspace/home.md)。

## 後續步驟和其他資源

現在，您更好地瞭解了整個Experience Platform中架構的角色，現在，您已準備好開始編寫自己的架構。

要瞭解構成方案與Experience Platform一起使用的設計原則和最佳做法，請首先閱讀 [架構組合基礎](schema/composition.md)。 有關如何建立架構的逐步說明，請參見建立架構的教程 [使用API](tutorials/create-schema-api.md) 或 [使用用戶介面](tutorials/create-schema-ui.md)。

強化你對 [!DNL XDM System] 在Experience Platform中，觀看以下視頻：

>[!VIDEO](https://video.tv.adobe.com/v/27105?quality=12&learn=on)
