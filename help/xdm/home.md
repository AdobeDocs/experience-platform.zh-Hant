---
keywords: Experience Platform；首頁；熱門主題；XDM；XDM系統；XDM個人設定檔；XDM ExperienceEvent；XDM體驗事件；體驗事件；欄位群組；欄位群組；欄位群組；體驗事件；XDM ExperienceEvent；XDM Experienceevent；XDM Experienceevent；體驗資料模型；體驗資料模型；資料模型；結構描述登入；結構描述庫；結構描述庫；記錄時間序列
solution: Experience Platform
title: XDM系統概覽
description: 標準化和互通性是Adobe Experience Platform背後的重要概念。 體驗資料模型(XDM)由Adobe驅動，致力於標準化客戶體驗資料並定義客戶體驗管理的結構。
exl-id: 294d5f02-850f-47ea-9333-8b94a0bb291e
source-git-commit: 8113b5298120f710f43c5a02504f19ca3af67c5a
workflow-type: tm+mt
source-wordcount: '2117'
ht-degree: 4%

---

# XDM系統概覽

標準化和互通性是Adobe Experience Platform背後的重要概念。 體驗資料模型(XDM)由Adobe驅動，致力於標準化客戶體驗資料並定義客戶體驗管理的結構。

XDM是公開記錄的規格，旨在改善數位體驗的效能。 它提供通用結構和定義，可讓任何應用程式使用來與Platform服務通訊。 只要遵循XDM標準，所有客戶體驗資料都可整合到共同表現中，以更快、更整合的方式提供深入分析。 您可以從客戶動作中獲得有價值的深入分析、透過區段定義客戶對象，以及表達客戶屬性以進行個人化。

XDM是基礎架構，可讓Adobe Experience Cloud在Experience Platform的支援下，於正確的時間在正確的頻道將正確的訊息傳遞給正確的人。 建立Experience Platform所根據的方法XDM系統可將Experience Data Model結構描述可操作化，以供Platform服務使用。

瞭解XDM系統在Experience Platform中的角色。

## XDM結構描述 {#xdm-schemas}

Experience Platform 會使用結構，以一致且可重複使用的方式說明資料結構。藉由定義跨系統的一致資料，將更容易保留意義，進而從資料中獲得價值。

在將資料擷取到Platform之前，必須組成結構描述資料的結構並對可包含在每個欄位中的資料型別提供限制。 結構描述包含一個基底類別和零個或多個結構描述欄位群組。

如需結構描述組合模型的詳細資訊，包括設計原則和最佳實務，請參閱 [結構描述組合的基本面](schema/composition.md).

### 標準XDM元件 {#Standard-xdm-components}

XDM提供標準欄位群組和資料型別的強大集合，旨在擷取不同產業的共同概念和使用案例。 Experience Platform可讓您依產業篩選這些元件，讓您快速自信地建構最能支援您特定業務需求的結構描述。

在Experience Platform UI中建構結構描述時，列出的欄位群組會顯示人氣量度。 此量度取決於其他Platform使用者在其結構描述中使用欄位群組的頻率。 數字越高，欄位群組就越受歡迎。 依預設，會顯示從最受歡迎到最不受歡迎的結果，讓您隨時掌握業界的資料模型化趨勢。

![的人氣欄 [!UICONTROL 新增欄位群組] 對話方塊。](./images/overview/popularity.png)

### [!DNL Schema Library] {#schema-library}

Experience Platform提供使用者介面和RESTful API，您可以從中檢視和管理Experience Platform中所有結構描述相關的資源 **[!DNL Schema Library]**. 此 [!DNL Schema Library] 包含依Adobe向您提供的標準XDM元件，以及來自您使用之應用程式的Experience Platform合作夥伴和廠商的資源。

您也可以使用建立和管理組織專屬的新方案和資源 [!DNL Schema Registry API]，或 [!UICONTROL 方案] Platform UI中的工作區。

如需如何在Platform中管理方案和與之互動的詳細資訊，請參閱下列檔案：

* [XDM UI指南](./ui/overview.md)
* [結構描述登入API指南](./api/overview.md)

## XDM 系統中的資料行為 {#data-behaviors}

>[!CONTEXTUALHELP]
>id="platform_schemas_behavior"
>title="資料行為"
>abstract="用於 Experience Platform 的資料分為三種行為類型：記錄、時間序列和臨時。記錄方案會提供有關主體屬性的資訊，而時間序列方案則會在採取動作時擷取系統的快照。臨時方案會擷取僅供單一資料集使用的命名空間欄位。如需有關 Platform 中資料行為的詳細資訊，請查看此文件。"

打算用於Experience Platform的資料分為三種行為型別：

* **記錄**：提供主旨屬性的相關資訊。 主旨可以是組織或個人。
* **時間序列**：提供記錄主體直接或間接執行動作時的系統快照。
* **臨機**：擷取已名稱空間的欄位，以供單一資料集使用。 臨機結構用於各種資料擷取工作流程中以進行Experience Platform，包括擷取CSV檔案和建立特定型別的來源連線。

所有XDM結構描述都說明可歸類為記錄或時間序列的資料。 結構描述的資料行為由結構描述的類別定義，該類別在首次建立時指派給結構描述。 XDM類別說明結構描述必須包含的最小屬性數量，才能代表特定的資料行為。

雖然您能在 [!DNL Schema Registry]，建議您使用標準類別 **[!UICONTROL XDM個別設定檔]** 和 **[!UICONTROL XDM ExperienceEvent]** 用於記錄及時間序列資料。 這些類別將於下文詳細說明。

>[!NOTE]
>
>沒有基於臨機行為的標準類別。 臨時結構會由使用它們的平台程式自動產生，但也可以 [使用結構描述登入API手動建立](./tutorials/ad-hoc.md).

### [!UICONTROL XDM 個別設定檔] {#xdm-individual-profile}

[!UICONTROL XDM個別設定檔] 是以記錄為基礎的類別，可形成已識別和部分識別之主體的屬性的單一表示法。 高度識別的設定檔可用於個人通訊或目標參與。 高度識別的設定檔可包含詳細的個人資訊，例如，姓名、性別、出生日期、地點，以及聯絡資訊，包括電話號碼和電子郵件地址。

較少識別的設定檔可能僅由匿名行為訊號（如瀏覽器Cookie）組成。 在這種情況下，會使用稀疏設定檔資料來建立資訊庫，匿名設定檔的興趣和偏好設定會在該資訊庫中整理和儲存。 隨著主體註冊接收通知、訂閱、購買等，這些識別碼可能會隨著時間變得更詳細。 設定檔屬性的這種增加最終可能會導致識別的主題，並允許更高程度的目標參與。

隨著個人檔案持續成長，會成為個人個人資訊、身分資訊、聯絡詳細資料和通訊偏好設定的健全存放庫。

請參閱 [[!UICONTROL XDM個別設定檔] 參考指南](./classes/individual-profile.md) 有關類別所提供的欄位結構和使用案例的詳細資訊。

### [!UICONTROL XDM ExperienceEvent] {#xdm-experience-event}

XDM ExperienceEvent是一種以時間序列為基礎的類別，用於在事件（或一組事件）發生時擷取系統的狀態，包括時間點和所涉及主體的身分。 體驗事件是指在該時間點所發生之情況的不可變、真實記錄，代表在沒有彙總或詮釋的情況下所發生的情況。 它們對於時間網域分析至關重要，因為它們可用於分析指定時段內發生的變化，並用於比較多個時段以追蹤趨勢。

體驗事件可以是明確或隱含的。 明確事件是指在歷程中某個時間點發生的直接可觀察的人類行為。 隱含事件是在沒有直接人類動作的情況下引發，但仍與個人相關的事件。 隱含事件的範例包括排程傳送電子郵件電子報或電池電壓達到特定臨界值。

雖然並非所有事件都可輕鬆跨所有資料來源分類，但儘可能將類似事件統一為類似型別以進行處理極具價值。

![客戶歷程的資訊圖，以一段時間的體驗事件加以視覺化。](images/overview/experience-event-journey.png)

請參閱 [[!UICONTROL XDM ExperienceEvent] 參考指南](./classes/experienceevent.md) 有關類別所提供的欄位結構和使用案例的詳細資訊。

## XDM結構描述和Experience Platform服務 {#schemas-and-platform-services}

Experience Platform與結構無關，這表示任何符合XDM標準的結構均可供Platform服務使用。 不同Platform服務使用結構描述的方式將詳述於下。

### 目錄服務、資料擷取和資料湖 {#ingestion-catalog-and-storage}

目錄服務是Experience Platform資產及其相關結構描述的記錄系統。 目錄並不包含實際的資料檔案或目錄，而是包含這些檔案和目錄的中繼資料和說明。

目錄資料會儲存在Data Lake中，這是高度精細的資料存放區，包含Platform管理的所有資料，無論來源或檔案格式為何。

若要開始將資料擷取到Experience Platform中，您可以使用目錄服務建立資料集。 資料集參考描述要擷取之資料結構的XDM結構描述。 如果在沒有結構描述的情況下建立資料集，Experience Platform會透過檢查所擷取資料欄位的型別和內容來衍生「觀察到的結構描述」。 資料集接著會在目錄服務中受到追蹤，並與資料集所根據的結構描述和觀察的結構描述一起儲存在資料湖中。

請參閱 [目錄服務總覽](../catalog/home.md) 以取得詳細資訊。 請參閱 [資料擷取概觀](../ingestion/home.md) 以取得有關Adobe Experience Platform資料擷取的詳細資訊。

### 查詢服務 {#query-service}

您可以使用標準SQL來查詢Experience Platform資料，以透過Adobe Experience Platform查詢服務支援許多不同的使用案例。

在撰寫結構描述並建立參考該結構描述的資料集後，系統就會擷取資料並儲存在Data Lake中。 然後，您可以使用查詢服務來聯結Data Lake中的任何資料集，並將查詢結果擷取為新資料集，以用於報表、機器學習或內嵌到即時客戶個人檔案中。

請參閱 [查詢服務總覽](../query-service/home.md) 以取得服務的詳細資訊。

### 即時客戶設定檔 {#real-time-customer-profile}

即時客戶設定檔提供集中式消費者設定檔，用於針對性和個人化的體驗管理。 每個設定檔都包含跨所有系統彙總的資料，並包含涉及設定檔主旨之事件的可行時間戳記帳戶。 這些事件可能發生在您與Experience Platform搭配使用的任何系統中。

即時客戶設定檔會根據 [!UICONTROL XDM個別設定檔] 和 [!UICONTROL XDM ExperienceEvent] 類別，以及根據該資料回應查詢。

>[!NOTE]
>
>即時客戶個人檔案可以 **非** 根據類別以外的支援結構描述 [!UICONTROL XDM ExperienceEvent] 類別。

系統會維護每個客戶設定檔的一個例項，將資料合併在一起，形成個人的「單一信任來源」。 此統一資料使用所謂的「聯合結構描述」（有時稱為「聯合檢視」）來表示。 聯合結構描述會將實施相同類別的所有結構描述的欄位彙總到單一結構描述中。 使用UI或API構成結構描述時，您可以啟用結構描述以與即時客戶個人檔案搭配使用，並標籤它以包含在聯合中。 然後，標籤的結構描述將參與要提供給設定檔的結構描述定義。

作為 [!UICONTROL XDM個別設定檔] 和 [!UICONTROL XDM ExperienceEvent] 資料會擷取至Data Lake，即時客戶設定檔會擷取任何已啟用以供使用的資料。 內嵌的互動和詳細資訊越多，個別設定檔就越健全。

[!UICONTROL XDM個別設定檔] 資料可協助您瞭解所有管道或Adobe產品整合中的動作並強化動作。 如果搭配豐富的行為和互動資料歷史，這些資料可用於推動機器學習。 即時客戶設定檔API也可用來擴充協力廠商解決方案、CRM和專有解決方案的功能。

請參閱 [即時客戶個人檔案總覽](../profile/home.md) 以取得詳細資訊。

### Data Science Workspace {#data-science-workspace}

Adobe Experience Platform Data Science Workspace使用機器學習和人工智慧，從Experience Platform中儲存的資料中獲得深入分析。 資料科學工作區可讓資料科學家根據以下專案建置配方 [!UICONTROL XDM個別設定檔] 和 [!UICONTROL XDM ExperienceEvent] 有關客戶及其活動的資料。 這些配方有助於進行預測，例如購買傾向和建議個人可能會讚賞和使用的選件。

藉由Data Science Workspace，資料科學家可以輕鬆建立由機器學習提供支援的智慧型服務API。 這些服務可與其他Adobe解決方案搭配使用，包括Adobe Target和Adobe Analytics Cloud，協助您自動化個人化、鎖定目標的數位體驗。

如需使用Experience Platform資料強化深入分析的詳細資訊，請參閱 [資料科學工作區概觀](../data-science-workspace/home.md).

## 後續步驟和其他資源

現在您更能瞭解結構描述在整個Experience Platform中的角色，您已準備好開始撰寫自己的結構描述。

若要瞭解構成要與Experience Platform搭配使用的結構描述的設計原則和最佳實務，請從閱讀 [結構描述組合的基本面](schema/composition.md). 如需如何建立綱要的逐步指示，請參閱建立綱要教學課程 [使用API](tutorials/create-schema-api.md) 或 [使用使用者介面](tutorials/create-schema-ui.md).

加強您的理解 [!DNL XDM System] 在Experience Platform中，觀看以下影片：

>[!VIDEO](https://video.tv.adobe.com/v/27105?quality=12&learn=on)
