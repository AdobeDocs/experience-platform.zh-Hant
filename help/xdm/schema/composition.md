---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 架構構成基礎
topic: overview
translation-type: tm+mt
source-git-commit: d04bf35e49488ab7d5e07de91eb77d0d9921b6fa
workflow-type: tm+mt
source-wordcount: '2628'
ht-degree: 0%

---


# 架構構成基礎

本檔案介紹 [!DNL Experience Data Model] (XDM)架構，以及構成Adobe Experience Platform中要使用之架構的建置區塊、原則和最佳實務。 有關XDM及其在中的使用方式的一般資訊，請 [!DNL Platform]參閱 [XDM系統概述](../home.md)。

## 瞭解結構

架構是一組規則，用於表示和驗證資料的結構和格式。 高層次上，結構描述提供實際物件（例如人）的抽象定義，並概述該物件每個例項中應包含的資料（例如名字、姓氏、生日等）。

除了描述資料的結構外，模式還對資料應用約束和期望，以便在系統之間移動時驗證它。 這些標準定義允許一致地解釋資料，而不論其來源為何，並消除跨應用程式翻譯的需要。

[!DNL Experience Platform] 通過使用模式來維護此語義規範化。 結構描述是描述中資料的標準方法 [!DNL Experience Platform]，允許符合結構的所有資料可以重複使用，而不會在組織間發生衝突，甚至可以在多個組織之間共用。

### 關係表與嵌入對象

使用關係式資料庫時，最佳實務是標準化資料，或將實體分割為離散的部分，然後跨多個表格顯示。 為了整體讀取資料或更新實體，必須使用JOIN對許多單個表執行讀和寫操作。

XDM模式通過嵌入對象的使用，可以直接表示複雜的資料，並將其儲存在具有層次結構的自包含文檔中。 此結構的主要優點之一是，它可讓您查詢資料，而不需透過昂貴的連接來重新建構實體至多個非標準化表格。

### 結構圖和大資料

現代數位系統會產生大量的行為訊號（交易資料、網路記錄、物聯網、展示等等）。 此巨量資料提供了最佳化體驗的絕佳機會，但由於資料的規模和多樣性，使用起來十分困難。 為了從資料中獲取價值，必須標準化其結構、格式和定義，以便能夠一致且有效率地處理。

結構描述可解決此問題，它允許從多個來源整合資料、透過共同結構和定義標準化資料，並跨解決方案共用。 這允許後續的流程和服務回答任何類型的資料問題，從傳統的資料建模方法轉向資料建模方法，在該方法中，將要詢問資料的所有問題都事先已知，並且資料建模以符合這些期望。

### 以架構為基礎的工作流程，位於 [!DNL Experience Platform]

標準化是其背後的一個關鍵概念 [!DNL Experience Platform]。 XDM由Adobe推動，旨在標準化客戶體驗資料，並定義客戶體驗管理的標準架構。

所建立的基 [!DNL Experience Platform] 礎架構(稱為 [!DNL XDM System]架構)有助於架構式工作流程，並包含 [!DNL Schema Registry]、 [!DNL Schema Editor]、架構中繼資料和服務使用模式。 如需詳細 [資訊，請參閱XDM系統概觀](../home.md) 。

## 規劃您的架構

建立架構的第一步是決定您要在架構中擷取的概念或實際物件。 一旦您確定要描述的概念，您就可以開始規劃您的架構，包括資料類型、潛在識別欄位，以及架構未來的演變方式等。

### 資料行為 [!DNL Experience Platform]

要用於的資料會 [!DNL Experience Platform] 分為兩種行為類型：

* **記錄資料**: 提供主題屬性的相關資訊。 主題可以是組織或個人。
* **時間系列資料**: 提供記錄主體直接或間接採取操作時系統的快照。

所有XDM結構描述的資料可以分類為記錄或時間序列。 方案的資料行為由方案的類定 **義**，該類在首次建立方案時被分配給方案。 本文稍後將對XDM類作進一步的詳細說明。

記錄和時間序列模式都包含身份映射(`xdm:identityMap`)。 此欄位包含主題的身分表示法，其取自標示為「身分」的欄位，如下一節所述。

### [!UICONTROL 身份]

結構描述用於將資料吸收到中 [!DNL Experience Platform]。 此資料可跨多個服務使用，以建立個別實體的單一統一檢視。 因此，在考慮結構時，請務必考慮「[!UICONTROL Identity]」，以及哪些欄位可用來識別主體，而不論資料來自何處。

為協助處理此程式，關鍵欄位可標示為「[!UICONTROL Identity]」。 資料擷取時，這些欄位中的資料會插入該個人的「[!UICONTROL 身分圖表]」中。 圖形資料隨後可由和其他服 [!DNL Real-time Customer Profile](../../profile/home.md) 務訪問， [!DNL Experience Platform] 以提供每個客戶的拼接視圖。

通常標示為「[!UICONTROL Identity]」的欄位包括： 電子郵件地址、電話號碼、 [!DNL Experience Cloud ID (ECID)](https://docs.adobe.com/content/help/zh-Hant/id-service/using/home.html)CRM ID或其他唯一ID欄位。 您也應考慮組織專屬的任何唯一識別碼，因為這些識別碼可能也是[!UICONTROL 好的「Identity]」欄位。

在方案規劃階段，務必考慮客戶身份，以協助確保資料匯整在一起，以建立最強穩的個人檔案。 請參閱 [Identity Service總覽](../../identity-service/home.md) ，進一步瞭解身分資訊如何協助您為客戶提供數位體驗。

### 模式演化原則 {#evolution}

隨著數位體驗的性質不斷演變，用來代表體驗的架構也必須不斷演變。 因此，精心設計的架構能夠根據需要調整和演化，而不會對舊版架構造成破壞性的改變。

由於維持向後相容性對架構演化至關重要，因此 [!DNL Experience Platform] 會執行純粹的加性版本修訂原則，以確保架構的任何修訂只會產生非破壞性的更新和變更。 換言之，不支 **援中斷變更。**

| 支援的變更 | 中斷變更（不支援） |
|------------------------------------|---------------------------------|
| <ul><li>將新欄位添加到現有模式</li><li>將強制欄位設為選填</li></ul> | <ul><li>移除先前定義的欄位</li><li>推出新的必填欄位</li><li>更名或重定義現有欄位</li><li>移除或限制先前支援的欄位值</li><li>將屬性移動到樹中的不同位置</li></ul> |

>[!NOTE]
>
>如果尚未使用架構將資料嵌入，則 [!DNL Experience Platform]可能會對該架構引入斷開更改。 但是，一旦在中使用了架構， [!DNL Platform]它就必須遵循附加的版本控制策略。

### 結構描述與資料擷取

為了將資料內嵌至 [!DNL Experience Platform]中，必須先建立資料集。 資料集是資料轉換和追蹤的建置區塊， [!DNL Catalog Service](../../catalog/home.md)通常代表包含收錄資料的表格或檔案。 所有資料集都基於現有的XDM模式，這為所提取的資料應包含的內容以及其結構提供了約束。 如需詳細資訊，請 [參閱Adobe Experience Platform資料擷取概觀](../../ingestion/home.md) 。

## 架構的構建塊

[!DNL Experience Platform] 使用組合方法，其中組合標準構建塊以建立模式。 此方法可提升現有元件的可重複使用性，並推動業界標準化，以支援廠商架構和元件 [!DNL Platform]。

方案使用下列公式組成：

**類+ Mixin&amp;ast; = XDM方案**

&amp;ast；模式由類和零個或多個 _混合組成_ 。 這表示您完全不需使用mixin就可以合成資料集架構。

### 類別

構成模式的開始方法是分配類。 類定義模式將包含的資料的行為方面（記錄或時間序列）。 此外，類還描述了基於該類的所有方案需要包含的最小公共屬性數，並為合併多個相容資料集提供了一種方法。

類別也會決定哪些混音符合在架構中使用的資格。 在下面的mixin部分中將更詳細 [地討論](#mixin) 此問題。

每次整合都提供標準類別， [!DNL Experience Platform]稱為「產業」類別。 業界類別是公認的業界標準，適用於廣泛的使用案例。 產業類別的範例包括 [!DNL XDM Individual Profile] Adobe提 [!DNL XDM ExperienceEvent] 供的和類別。

[!DNL Experience Platform] 還允許「供應商」類，這些類由合作夥伴定義，並 [!DNL Experience Platform] 提供給所有使用該供應商服務或應用程式的客戶 [!DNL Platform]。

還有一些類用於描述內部單個組織（稱為「客戶」類）的更 [!DNL Platform]多特定使用案例。 當沒有可用於描述獨特使用案例的行業或供應商類時，客戶類由組織定義。

例如，代表忠誠度方案成員的結構描述個人的記錄資料，因此可以基於類別(由Adobe定義的標 [!DNL XDM Individual Profile] 準產業類別)。

### Mixin {#mixin}

混音是可重複使用的元件，其定義可實作特定功能（例如個人詳細資料、飯店偏好設定或位址）的一或多個欄位。 Mixin是作為實現相容類的模式的一部分而包括的。

Mixins會根據所代表資料的行為（記錄或時間系列）來定義與哪些類別相容。 這表示並非所有混音都可用於所有類別。

Mixin的範圍和定義與類相同： 有由個別組織使用定義的產業混合、廠商混合和客戶混合 [!DNL Platform]。 [!DNL Experience Platform] 包括許多標準的業界混搭，同時允許廠商為其使用者定義混搭，以及個別使用者為其特定概念定義混搭。

例如，若要擷取「忠誠會員[!UICONTROL 」結構的詳細資訊，例如「名字]」和「首位地址」，您可以使用定義這些常見概念的標準混音。 但是，針對較不常見使用案例(例如「[!UICONTROL Loyalty Program Level]」)的特定概念通常沒有預先定義的混音。 在這種情況下，您必須定義自己的混音，才能擷取此資訊。

請記住，結構描述是由「零個或更多」混合組成，因此這表示您無需使用任何混合即可合成有效結構描述。

### Data type {#data-type}

資料類型與基本常值欄位的使用方式相同，在類或方案中用作參考欄位類型。 關鍵區別在於資料類型可以定義多個子欄位。 與混音類似，資料類型允許一致地使用多欄位結構，但比混音更具靈活性，因為通過將資料類型添加為欄位的「資料類型」，資料類型可以包括在模式中的任意位置。

[!DNL Experience Platform] 提供了一些常用資料類型作為的一部分，以 [!DNL Schema Registry] 支援使用標準模式來描述常用資料結構。 這在教學課程中會有更詳細的說 [!DNL Schema Registry] 明，當您逐步執行定義資料類型的步驟時，將會更清楚。

### 欄位

欄位是架構最基本的建置區塊。 欄位可定義特定資料類型，以限制其可包含的資料類型。 這些基本資料類型會定義單一欄位，而前述的資 [料類型](#data-type) ，可讓您定義多個子欄位，並在各種結構中重複使用相同的多欄位結構。 因此，除了將欄位的「資料類型」定義為註冊表中定義的其中一種資料類型外，還支援基 [!DNL Experience Platform] 本標量類型，例如：

* 字串
* 整數
* 數字
* 布林值
* 陣列
* 物件

這些標量類型的有效範圍可以進一步限制為某些模式、格式、最小值／最大值或預定義值。 使用這些約束，可以表示各種更具體的欄位類型，包括：

* Enum
* 長
* 簡短
* 位元組
* 日期
* 日期時間
* 地圖

>[!NOTE]
>
>「映射」欄位類型允許鍵值對資料，包括單個鍵的多個值。 映射只能在系統級別定義，這表示您可能在行業或供應商定義的方案中遇到映射，但無法用於您定義的欄位。 Schema Registry [API開發人員指南包含有關定義欄位類型的詳細資訊](../api/getting-started.md) 。

下游服務和應用程式使用的某些資料操作對特定欄位類型強制執行限制。 受影響的服務包括但不限於：

* [!DNL Real-time Customer Profile](../../profile/home.md)
* [!DNL Identity Service](../../identity-service/home.md)
* [!DNL Segmentation](../../segmentation/home.md)
* [!DNL Query Service](../../query-service/home.md)
* [!DNL Data Science Workspace](../../data-science-workspace/home.md)

在建立用於下游服務的架構之前，請先閱讀這些服務的適當檔案，以便更好地瞭解該架構用於資料操作的現場要求和限制。

### XDM欄位

除了基本欄位和定義您自己的資料類型的能力外，XDM還提供一套標準的欄位和資料類型，這些欄位和資料類型會由服務隱含地理解，並在跨元件使用時提供 [!DNL Experience Platform] 更一致 [!DNL Platform] 性。

這些欄位（例如「名字」和「電子郵件地址」）除了基本標量欄位類型之外，還包含其他附加含義，告訴 [!DNL Platform] 任何共用相同XDM資料類型的欄位將以相同的方式運作。 無論資料來自何處，或資料使用於何種服務，都可信 [!DNL Platform] 任此行為一致。

如需可用 [XDM欄位的完整清單](field-dictionary.md) ，請參閱XDM欄位字典。 建議盡可能使用XDM欄位和資料類型，以支援跨領域的一致性和標準化 [!DNL Experience Platform]。

## 合成示例

結構描述表示將被收錄到的資料的格式和結構 [!DNL Platform]，並使用合成模型構建。 如前所述，這些模式由類和與該類相容的零個或多個混合組成。

例如，描述在零售商店購買的方案稱為「商店[!UICONTROL 交易]」。 該模式實現 [!DNL XDM ExperienceEvent] 與標準 [!UICONTROL Commerce] mixin和用戶定義的 [!UICONTROL Product Info] mixin組合的類。

追蹤網站流量的另一個架構可能稱為「[!UICONTROL 網站造訪]」。 它也實現了類 [!DNL XDM ExperienceEvent] 別，但這次結合了標準 [!UICONTROL Web] mixin。

下圖顯示了這些方案以及每個混音所貢獻的欄位。 它還包含基於類的兩個方 [!DNL XDM Individual Profile] 案，包括本指南中提[!UICONTROL 及的「忠誠成員]」方案。

![](../images/schema-composition/composition.png)

### 聯集 {#union}

雖然 [!DNL Experience Platform] 允許您為特定使用案例合成方案，但它也允許您查看特定類型方案的「聯合」。 上圖顯示基於XDM ExperienceEvent類的兩個模式和基於類的兩個模 [!DNL XDM Individual Profile] 式。 The union（如下所示）匯總了共用相同類的所有方案([!DNL XDM ExperienceEvent] 和 [!DNL XDM Individual Profile]分別)的欄位。

![](../images/schema-composition/union.png)

通過啟用與一起使用的 [!DNL Real-time Customer Profile]模式，它將包含在該類型的union中。 [!DNL Profile] 提供強穩、集中的客戶屬性描述檔，以及客戶在與之整合的任何系統上所發生之每個事件的時間戳記帳戶 [!DNL Platform]。 [!DNL Profile] 使用聯合檢視來呈現此資料，並提供每位客戶的全面檢視。

如需使用的詳細資訊 [!DNL Profile]，請參 [閱即時客戶個人檔案總覽](../../profile/home.md)。

## 將資料檔案映射到XDM模式

所有被收錄到的數 [!DNL Experience Platform] 據檔案都必須符合XDM架構的結構。 有關如何格式化資料檔案以符合XDM層次（包括示例檔案）的詳細資訊，請參見有關示例ETL轉換 [的文檔](../../etl/transformations.md)。 有關將資料檔案收錄到的一般信 [!DNL Experience Platform]息，請參見 [批處理概述](../../ingestion/batch-ingestion/overview.md)。

## 後續步驟

現在，您瞭解了架構構成的基本知識，可以開始使用構建架構 [!DNL Schema Registry]。

此 [!DNL Schema Registry] 程式可用來存取Adobe Experience Platform中 [!DNL Schema Library] 的，並提供使用者介面和RESTful API，讓您存取所有可用的程式庫資源。 本 [!DNL Schema Library] 軟體包含由Adobe定義的產業資源、由合作夥伴定義的廠商資 [!DNL Experience Platform] 源，以及由您組織成員組成的類別、混合、資料類型和結構。

若要開始使用UI編寫架構，請遵循「架構編輯器」教學課程 [](../tutorials/create-schema-ui.md) ，以建立本檔案中提及的「忠誠成員」架構。

若要開始使用 [!DNL Schema Registry] API，請先閱讀 [Schema Registry API開發人員指南](../api/getting-started.md)。 閱讀開發人員指南後，請依照教學課程中說明的步驟， [使用架構註冊表API建立架構](../tutorials/create-schema-api.md)。
