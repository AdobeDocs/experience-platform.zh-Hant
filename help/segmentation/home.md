---
keywords: Experience Platform；首頁；熱門主題；分段；分段；區段服務；區段；區段；區段；區段
solution: Experience Platform
title: 區段服務概述
topic-legacy: overview
description: 了解Adobe Experience Platform細分服務及其在Platform生態系統中的角色。
exl-id: 2c18a806-88ed-4659-bdfd-2377f5a09a1a
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1635'
ht-degree: 0%

---

# [!DNL Segmentation Service] 概覽

Adobe Experience Platform [!DNL Segmentation Service] 提供使用者介面和RESTful API，可讓您建立區段，並從中產生對象 [!DNL Real-Time Customer Profile] 資料。 這些區段是在 [!DNL Platform]，任何Adobe解決方案都可輕鬆存取。

本檔案提供 [!DNL Segmentation Service] 以及它在Adobe Experience Platform的作用。

## 開始使用 [!DNL Segmentation Service]

請務必了解本檔案中使用的下列主要術語：

- **區段**:將大量個人（例如客戶、潛在客戶、使用者或組織）分成具有類似特徵且對行銷策略有類似反應的較小群組。
- **區段定義**:用來說明目標對象之關鍵特性或行為的規則集。 概念化後，區段定義中概述的規則將用於決定區段的合格受眾成員。
- **對象**:符合區段定義條件的產生設定檔集。

## 區段的運作方式

區段是定義設定檔存放區中一組設定檔子集所共用的特定屬性或行為的程式，以區分可行銷的一組人員和您的客戶群。 例如，在名為「您忘記購買運動鞋嗎？」的電子郵件行銷活動中，您可能想要有過去30天內搜尋跑鞋，但未完成購買的所有使用者的對象。

在概念上定義區段後，就會內建區段 [!DNL Experience Platform]. 通常，區段是由行銷人員或受眾專員建立，不過有些組織偏好由行銷部門與資料分析人員共同建立。 檢閱要傳送至的資料時 [!DNL Platform]，資料分析師會選取將用來建立區段規則或條件的欄位和值，以構成區段定義。 這是使用UI或API來完成。

## 建立區段

使用API建立或使用 [!DNL Segment Builder]，區段最終會使用 [!DNL Profile Query Language] (PQL)。 這是擷取符合條件之設定檔所建置語言中描述概念區段定義的地方。 如需詳細資訊，請參閱 [PQL概述](./pql/overview.md).

若要了解如何在 [!DNL Segment Builder] （UI實作） [!DNL Segmentation Service])，請參閱 [區段產生器指南](./ui/overview.md).

如需使用API建立區段定義的相關資訊，請參閱 [使用API建立受眾區段](./tutorials/create-a-segment.md).

>[!NOTE]
>
>在架構擴展時，所有將來的上載必須相應地更新新添加的欄位。 如需自訂的詳細資訊 [!DNL Experience Data Model] (XDM)，請造訪 [結構編輯器教學課程](../xdm/tutorials/create-schema-ui.md).
>
>此外，如果資料集上已啟用「體驗事件」過期值，這可能會影響所建立區段的成員資格。 請閱讀指南 [體驗事件過期](../profile/event-expirations.md) 以取得此功能如何影響區段的詳細資訊。

## 評估區段 {#evaluate-segments}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation"
>title="評價方法"
>abstract="Platform目前支援三種評估區段的方法：串流分段、批次分段和邊緣分段。"

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_streaming"
>title="流評估"
>abstract="串流區段是持續進行的資料選取程式，會根據使用者活動更新您的區段。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html" text="透過串流細分以近乎即時的方式評估事件"

Platform目前支援三種評估區段的方法：串流分段、批次分段和邊緣分段。

### 串流細分 {#streaming}

串流區段是持續進行的資料選取程式，會根據使用者活動更新您的區段。 建立並儲存區段後，會對傳入的資料套用區段定義至 [!DNL Real-Time Customer Profile]. 會定期處理區段新增和移除，確保目標受眾仍具相關性。

若要進一步了解串流細分，請閱讀 [串流細分檔案](./api/streaming-segmentation.md).

### 批次分段 {#batch}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_batch"
>title="批次評估"
>abstract="作為持續資料選取程式的替代方法，批次區段會透過區段定義一次移動所有設定檔資料，以產生對應的對象。 區段一經建立便會儲存，供您匯出使用。"

作為持續資料選取程式的替代方法，批次區段會透過區段定義一次移動所有設定檔資料，以產生對應的對象。 建立後，會儲存此區段，供您匯出使用。

每24小時會自動評估批次區段。 如果要按需評估批段，則可以使用段任務。 若要進一步了解區段作業，請參閱 [區段工作檔案](./api/segment-jobs.md).

### 邊緣分割 {#edge}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_edge"
>title="邊緣評估"
>abstract="邊緣分段是在Experience Edge上即時評估Platform中區段的功能，可啟用同頁和下一頁個人化使用案例。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/edge-segmentation.html" text="Edge劃分UI指南"

邊緣分割是即時評估Platform中區段的功能 [在Experience Edge上](../edge/home.md)，啟用同頁和下一頁個人化的使用案例。

若要進一步了解邊緣區段，請閱讀 [API檔案](./api/edge-segmentation.md) 或 [UI檔案](./ui/edge-segmentation.md).

## 存取區段結果

若要了解如何存取匯出的區段，請參閱 [區段評估教學課程](./tutorials/evaluate-a-segment.md).

## 區段中繼資料

區段中繼資料有助於在您的任何區段重複使用和/或合併時建立索引。

撰寫區段(透過API或 [!DNL Segment Builder])需要您定義區段名稱及合併原則。

### 區段名稱

建立新區段時，您必須提供區段名稱。 區段名稱可用來識別所建立集合中的特定區段 [!DNL Segmentation Service]. 因此，區段名稱應具有描述性、簡潔明瞭且獨特。

>[!NOTE]
>
>規劃區段時，請記住，可從任何其他區段參考區段，並加以結合。 選取名稱時，請考量區段可能包含可重複使用的部分。

### 合併策略

合併策略是用於 [!DNL Profile] 以決定在特定條件下，如何將資料排定優先順序並合併成統一檢視。
如果未定義合併策略，則預設 [!DNL Platform] 使用合併原則。 如果您想使用貴組織專屬的合併原則，可以建立自己的合併原則，並將其標示為貴組織的預設原則。

有關合併策略的詳細資訊，請參見 [合併策略指南](../profile/api/merge-policies.md).

>[!NOTE]
>
>對象大小的估計是根據組織的預設設定檔合併原則。

### 其他區段中繼資料

除了區段名稱和合併政策外， [!DNL Segment Builder] 提供您額外的「區段說明」中繼資料欄位，供您概述區段定義的用途。

## 進階區段功能

您可以透過結合來設定區段，以持續產生受眾 [串流資料內嵌](../ingestion/streaming-ingestion/overview.md) 搭配下列任何進階區段功能：
- [循序細分](#sequential)
- [動態細分](#dynamic)
- [多實體細分](#multi-entity)

以下幾節將更詳細地討論這些高級功能。

## 循序細分 {#sequential}

標準的使用者歷程是循序的。 Adobe Experience Platform可讓您定義一系列有序的區段，以反映此歷程，因此可在事件發生時擷取事件順序。 您可以使用 [!DNL Segment Builder].

需要依序分段的客戶歷程範例為產品檢視>產品新增>結帳>無購買。

## 動態細分 {#dynamic}

動態細分解決了行銷人員在建立行銷活動區段時，傳統上面臨的可擴充性問題。

靜態分段需要您明確且重複地擷取每個可能的使用案例，而動態分段則使用變數來建立規則邏輯並動態表達關係。

### 使用案例：尋找在家之外購買的客戶

為了說明此進階細分功能的價值，請考慮由資料架構師與行銷人員合作，識別在母州以外進行購買的客戶。

**問題**

靜態分段需要您先定義具有唯一首頁狀態屬性的個別區段，然後才篩選不等於首頁狀態的購買事件。 此類型的明確區段會顯示「我正在尋找來自猶他州的人，而他們的購買狀態並非猶他州」。 使用此方法建立對象時，您必須為每個美國州定義一個區段，共50個區段。

由於您在擴展時不可避免地會出現不同的區段組合，因此靜態細分所需的手動過程會更加耗時，從而降低您的整體效率。

**解決方案**

借由將變數指派給購買狀態屬性，您的動態區段將簡化為「尋找購買狀態不等於客戶家庭狀態的購買」。 如此一來，您便能將50個靜態區段併入單一動態區段。

## 多實體細分 {#multi-entity}

透過進階的多實體分段功能，您可以擴充 [!DNL Real-Time Customer Profile] 以產品、商店或其他非人員為基礎的其他資料（也稱為「維度」實體）的資料。 因此， [!DNL Segmentation Service] 可在區段定義期間存取其他欄位，就像這些欄位是原生欄位 [!DNL Profile] 資料儲存。 多實體細分可根據與您獨特業務需求相關的資料，靈活地識別對象。 如需詳細資訊，包括使用案例和工作流程，請參閱 [多實體分段指南](multi-entity-segmentation.md).

## [!DNL Segmentation Service] 資料類型

[!DNL Segmentation Service] 支援多種原始和複雜的資料類型。 如需詳細資訊，包括支援的資料類型清單，請參閱 [支援的資料類型指南](./data-types.md).

## 後續步驟

[!DNL Segmentation Service] 提供整合的工作流程，以便從 [!DNL Real-Time Customer Profile] 資料。 總之：

- [!DNL Segmentation] 是從您的設定檔存放區定義設定檔子集的程式，可讓您描述所需有價群組的行為或屬性。 [!DNL Segmentation Service] 使這個過程成為可能。
- 規劃區段時，請記得可從任何其他區段參考區段，並加以結合。
- 您可以根據設定檔資料、相關時間序列資料或兩者，從規則建立區段。
- 區段可依需求或持續評估。 隨需評估時，所有設定檔資料會一次透過區段定義傳遞。 持續評估時，資料流會在進入時透過區段定義進行 [!DNL Platform].

若要了解如何在UI中定義區段，請參閱 [區段產生器指南](./ui/overview.md). 如需使用API建立區段定義的相關資訊，請參閱 [使用API建立區段](./tutorials/create-a-segment.md).
