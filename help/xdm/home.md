---
keywords: Experience Platform；首頁；熱門主題；XDM;XDM系統；XDM個別設定檔；XDM ExperienceEvent;XDM體驗事件；體驗事件；欄位群組；欄位群組；欄位群組；欄位群組；體驗事件；XDM體驗事件；XDM ExperienceEvent；體驗事件；XDM ExperienceEvent；體驗資料模型；體驗資料模型；資料模型；程式庫架構；註冊表；結構；記錄資料；時間序列；時間序列
solution: Experience Platform
title: XDM系統概述
topic-legacy: overview
description: 標準化和互操作性是Adobe Experience Platform背後的重要概念。 由Adobe推動的Experience Data Model(XDM)，旨在標準化客戶體驗資料並定義客戶體驗管理的結構。
exl-id: 294d5f02-850f-47ea-9333-8b94a0bb291e
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '2087'
ht-degree: 2%

---

# XDM系統概觀

標準化和互操作性是Adobe Experience Platform背後的重要概念。 [!DNL Experience Data Model] (XDM)受Adobe推動，致力標準化客戶體驗資料並定義客戶體驗管理的結構。

XDM是公開記錄的規格，旨在改善數位體驗的強大功能。 它提供通用結構和定義，允許任何應用程式用於與Platform服務通信。 遵循XDM標準，所有客戶體驗資料皆可整合至通用表示法中，以更快速、更整合的方式提供深入分析。 您可以從客戶動作中獲得寶貴的深入分析、透過區段定義客戶受眾，以及為個人化目的表達客戶屬性。

XDM是基本架構，可讓Adobe Experience Cloud(由Experience Platform提供技術支援)在適當的時間，透過適當的管道向適當的人員傳遞適當的訊息。 建立Experience Platform的方法， XDM系統，可操作 [!DNL Experience Data Model] 供Platform服務使用的結構。

本檔案概述XDM系統在Experience Platform中的角色。

## XDM結構

Experience Platform 會使用結構，以一致且可重複使用的方式說明資料結構。藉由定義跨系統的一致資料，將可輕易保留意義，而發揮資料應有的價值。

在將資料擷取至Platform之前，必須先建立結構以說明資料的結構，並對每個欄位中可包含的資料類型提供限制。 結構由基類和零個或多個結構欄位組組成。

如需結構構成模型的詳細資訊，包括設計原則和最佳實務，請參閱 [綱要構成基本知識](schema/composition.md).

### 標準XDM元件

XDM提供標準欄位群組和資料類型的強大集合，這些群組旨在擷取不同產業的常見概念和使用案例。 Experience Platform可讓您依產業篩選這些元件，以便快速且放心地建構最能支援您特定業務需求的結構。

在Experience PlatformUI中建構結構時，列出的欄位群組會以人氣量度顯示。 此量度由其他Platform使用者在其結構中採用欄位群組的頻率決定。 數字越高，欄位群組就越受歡迎。 依預設，結果會從最受歡迎到最不受歡迎，讓您了解行業中的資料模型趨勢。

![欄位群組人氣](./images/overview/popularity.png)

### [!DNL Schema Library]

Experience Platform提供使用者介面和RESTful API，您可從中檢視及管理Experience Platform中所有與架構相關的資源 **[!DNL Schema Library]**. 此 [!DNL Schema Library] 包含依Adobe提供給您的標準XDM元件，以及來自您使用應用程式之Experience Platform合作夥伴和廠商的資源。

使用 [!DNL Schema Registry API] 或 [!UICONTROL 結構] workspace在Platform UI中，您也可以建立及管理貴組織特有的新結構和資源。

如需如何管理及與Platform中的結構描述互動的詳細資訊，請參閱下列檔案：

* [XDM UI指南](./ui/overview.md)
* [Schema Registry API指南](./api/overview.md)

## XDM系統中的資料行為 {#data-behaviors}

>[!CONTEXTUALHELP]
>id="platform_schemas_behavior"
>title="資料行為"
>abstract="用於Experience Platform的資料分為三種行為類型：記錄、時間系列和臨機。 記錄結構提供有關主題屬性的資訊，而時間序列結構在執行操作時捕獲系統的快照。 隨選結構會擷取命名空間欄位，僅供單一資料集使用。 如需Platform中資料行為的詳細資訊，請參閱本檔案。"

用於Experience Platform的資料分為三種行為類型：

* **記錄**:提供主題屬性的相關資訊。 主題可以是組織或個人。
* **時間序列**:提供記錄主體直接或間接執行操作時系統的快照。
* **臨機**:僅透過單一資料集擷取與使用命名相同的欄位。 臨機結構用於各種資料擷取工作流程中，以供Experience Platform使用，包括擷取CSV檔案和建立特定類型的來源連線。

所有XDM結構都說明可分類為記錄或時間序列的資料。 架構的資料行為由架構的類定義，該類在首次建立時分配給架構。 XDM類別說明結構必須包含的屬性數量最小，才能代表特定資料行為。

雖然您可以在 [!DNL Schema Registry]，建議您使用標準類別 **[!UICONTROL XDM個別設定檔]** 和 **[!UICONTROL XDM ExperienceEvent]** 用於記錄資料和時間序列資料。 以下將更詳細地介紹這些類。

>[!NOTE]
>
>沒有基於臨機行為的標準類。 採用臨機結構的平台程式會自動產生這些結構，但也可以 [使用方案註冊表API手動建立](./tutorials/ad-hoc.md).

### [!UICONTROL XDM個別設定檔] {#xdm-individual-profile}

[!UICONTROL XDM個別設定檔] 是基於記錄的類，它對已識別和部分已識別的主題的屬性形成奇異的表示。 高度識別的配置檔案可用於個人通信或目標性參與，並且可以包含詳細的個人資訊，如姓名、性別、出生日期、位置和聯繫資訊，包括電話號碼和電子郵件地址。

未識別的設定檔可能僅包含匿名行為訊號，例如瀏覽器Cookie。 在這種情況下，稀疏配置檔案資料用於構建資訊庫，在該資訊庫中整理和儲存匿名配置檔案的興趣和首選項。 隨著主體註冊通知、訂閱、購買等，這些識別碼可能會隨著時間而變得更詳細。 設定檔屬性的增加最終可能會產生已識別的主題，並允許更高度的目標參與。

隨著設定檔的持續成長，它會成為個人個人資訊、身分識別資訊、聯絡資訊和通訊偏好設定的強大存放庫。

請參閱 [[!UICONTROL XDM個別設定檔] 參考指南](./classes/individual-profile.md) ，以了解類別所提供欄位的結構和使用案例。

### [!UICONTROL XDM ExperienceEvent] {#xdm-experience-event}

XDM ExperienceEvent是以時間序列為基礎的類別，用於在發生事件（或一組事件）時擷取系統狀態，包括相關主體的時間點和身分。 體驗事件是不可變的、事實記錄，記錄在該時間點發生的事件，代表所發生的事件，且未進行匯總或解釋。 它們對於時域分析至關重要，因為它們可用於分析指定時間窗口中發生的更改，以及比較多個時間窗口以跟蹤趨勢。

體驗事件可以是明確或隱含的。 明確事件是直接可觀察的人類行動，在歷程的某個時間點發生。 隱含事件是指在沒有直接人為行動的情況下引發，但仍與個人相關的事件。 隱式事件的範例包括排程傳送電子郵件快訊或達到特定臨界值的電池電壓。

雖然並非所有事件都可輕鬆分類到所有資料來源，但在可能的情況下將類似事件協調為類似類型以供處理，是極有價值的。

![ExperienceEvent客戶歷程](images/overview/experience-event-journey.png)

請參閱 [[!UICONTROL XDM ExperienceEvent] 參考指南](./classes/experienceevent.md) ，以了解類別所提供欄位的結構和使用案例。

## XDM結構與Experience Platform服務

Experience Platform不受結構限制，這表示任何符合XDM標準的結構皆可供Platform服務使用。 以下將詳細說明不同Platform服務使用結構的方式。

### 目錄服務、資料擷取和Data Lake

目錄服務是Experience Platform資產及其相關結構的記錄系統。 目錄不包含實際的資料檔案或目錄，而是包含這些檔案和目錄的元資料和說明。

目錄資料會儲存在Data Lake中，這是一個高度精細的資料存放區，包含由Platform管理的所有資料，不論來源或檔案格式為何。

若要開始將資料內嵌至Experience Platform中，您可以使用目錄服務來建立資料集。 資料集會參照XDM結構，說明要擷取的資料結構。 如果建立資料集時沒有結構，Experience Platform會檢查所擷取資料欄位的類型和內容，以衍生出「觀察的結構」。 接著，資料集會在目錄中受到追蹤，並與資料集所依據的結構和觀察的結構一起儲存在資料湖中。

如需目錄的詳細資訊，請參閱 [目錄服務概述](../catalog/home.md). 如需Adobe Experience Platform資料擷取的詳細資訊，請參閱 [資料擷取概觀](../ingestion/home.md).

### 查詢服務

Adobe Experience Platform Query Service可讓您使用標準SQL來查詢Experience Platform資料，以支援許多不同的使用案例。

建立結構並建立參照該結構的資料集後，資料便會內嵌並儲存在Data Lake中。 使用Query Service，您可以加入Data Lake中的任何資料集，並將查詢結果擷取為新資料集，以用於報表、機器學習或內嵌至即時客戶設定檔。

請參閱 [查詢服務概述](../query-service/home.md) 以取得服務的詳細資訊。

### 即時客戶個人檔案

「即時客戶設定檔」提供集中的消費者設定檔，以便進行目標式和個人化的體驗管理。 每個設定檔都包含所有系統中匯總的資料，以及涉及個人事件的可操作的時間戳記帳戶，這些事件發生在您搭配Experience Platform使用的任何系統中。

即時客戶設定檔會根據 [!UICONTROL XDM個別設定檔] 和 [!UICONTROL XDM ExperienceEvent] 類，並根據該資料響應查詢。 設定檔不支援使用以其他類別為基礎的結構描述。

系統會維護每個客戶設定檔的例項，將資料合併在一起，為個人形成「單一真相來源」。 此統一資料會使用所謂的「聯合結構」（有時稱為「聯合檢視」）來表示。 聯合架構會將實施相同類別之所有架構的欄位匯總至單一架構中。  使用UI或API撰寫結構時，您可以啟用結構以與即時客戶設定檔搭配使用，並加上標籤以納入聯合中。 接著，標籤的結構將參與饋送至「設定檔」的結構定義。

As [!UICONTROL XDM個別設定檔] 和 [!UICONTROL XDM ExperienceEvent] 資料會內嵌至資料湖，即時客戶設定檔會內嵌已啟用供其使用的任何資料。 擷取的互動和詳細資訊越多，個別設定檔就越健全。

[!UICONTROL XDM個別設定檔] 資料有助於通知及啟用任何管道或Adobe產品整合中的動作。 與豐富的行為和互動資料記錄搭配使用時，這些資料可用來推動機器學習。 即時客戶設定檔API也可用來豐富協力廠商解決方案、CRM和專屬解決方案的功能。

請參閱 [即時客戶個人檔案概觀](../profile/home.md) 以取得更多資訊。

### Data Science Workspace

Adobe Experience Platform Data Science Workspace使用機器學習和人工智慧，從儲存在Experience Platform中的資料中獲得深入分析。 Data Science Workspace可讓資料科學家根據 [!UICONTROL XDM個別設定檔] 和 [!UICONTROL XDM ExperienceEvent] 關於客戶及其活動的資料，有助於進行預測，例如購買傾向，以及建議個人可能欣賞和使用的選件。

透過Data Science Workspace，資料科學家可輕鬆建立由機器學習提供技術支援的智慧服務API。 這些服務可與其他Adobe解決方案(包括Adobe Target和Adobe Analytics Cloud)搭配使用，協助您自動化個人化、鎖定目標的數位體驗。

如需使用Experience Platform資料強化深入分析的詳細資訊，請參閱 [Data Science Workspace概觀](../data-science-workspace/home.md).

## 後續步驟和其他資源

現在，您更清楚了解結構在整個Experience Platform中的角色，您就可以開始自行撰寫了。

若要了解合成結構以與Experience Platform搭配使用的設計原則和最佳實務，請先閱讀 [綱要構成基本知識](schema/composition.md). 如需如何建立結構的逐步指示，請參閱建立結構的教學課程 [使用API](tutorials/create-schema-api.md) 或 [使用使用者介面](tutorials/create-schema-ui.md).

強化您對 [!DNL XDM System] 在Experience Platform中，觀看下列影片：

>[!VIDEO](https://video.tv.adobe.com/v/27105?quality=12&learn=on)
