---
solution: Experience Platform
title: 分段服務總覽
description: 瞭解Adobe Experience Platform劃分服務及其在Experience Platform生態系統中所扮演的角色。
exl-id: 2c18a806-88ed-4659-bdfd-2377f5a09a1a
source-git-commit: 0a9028beca36b46d6228c0038366bbac5d32603c
workflow-type: tm+mt
source-wordcount: '1679'
ht-degree: 12%

---

# [!DNL Segmentation Service] 概觀

Adobe Experience Platform [!DNL Segmentation Service]提供使用者介面和RESTful API，可讓您透過[!DNL Real-Time Customer Profile]資料的區段定義或其他來源建立對象。 這些客群會在 [!DNL Experience Platform] 上集中設定及維護，並可透過任何 Adobe 解決方案輕鬆存取。

本檔案概述[!DNL Segmentation Service]及其在Adobe Experience Platform中扮演的角色。

## 快速入門：[!DNL Segmentation Service]

您應瞭解本檔案中使用的下列主要辭彙：

- **對象**：一組具有類似行為和/或特徵的人。 此人員集合可由Adobe Experience Platform使用區段定義（Experience Platform產生的對象）產生，或由外部來源（外部產生的對象）產生。
- **區段定義**： Adobe Experience Platform用來描述目標對象關鍵特性或行為的規則集。
- **區段**：將設定檔分隔成對象的動作。

## 區段的運作方式

區段是定義特定屬性或行為的程式，這些屬性或行為由您的個人資料存放區中的個人資料子集共用，以便區分可行銷人群組和您的客戶群。 例如，在名為「您忘記購買運動鞋嗎？」的電子郵件行銷活動中，您可能想要一個受眾，其中包含過去30天內搜尋跑鞋但未完成購買的所有使用者。

在概念定義對象後，即會在[!DNL Experience Platform]中建置對象。 一般而言，對象是由行銷人員或對象專家建立，不過有些組織偏好由行銷部門與資料分析師合作建立。 檢閱傳送至[!DNL Experience Platform]的資料後，資料分析人員可以兩種方式建立對象：透過選取將用於建立對象規則或條件的欄位和值來建立區段定義，或使用對象構成來構成對象。

## 建立對象

您可以在Adobe Experience Platform上以多種方式建立受眾，包括透過組合、區段定義、同盟資料和資料Distiller。

### 客群構成

在Experience Platform上直接構成受眾時，您可以使用受眾構成。 若要瞭解如何使用對象構成來建立對象，請參閱[對象構成指南](./ui/audience-composition.md)以取得詳細資訊。

### 區段定義

不論是使用API或使用[!DNL Segment Builder]建立，區段定義最終都是使用[!DNL Profile Query Language] (PQL)定義。 這是以建立用來擷取符合條件的設定檔的語言描述概念區段定義的地方。 如需詳細資訊，請參閱[PQL概觀](./pql/overview.md)。

若要瞭解如何在[!DNL Segment Builder] （[!DNL Segmentation Service]的UI實作）中建立和使用區段，請參閱[區段產生器指南](./ui/segment-builder.md)。

如需有關使用API建立區段定義的資訊，請參閱有關[使用API建立區段定義](./tutorials/create-a-segment.md)的教學課程。

>[!NOTE]
>
>在擴展結構描述時，所有未來上傳都必須據此更新新新增的欄位。 如需自訂[!DNL Experience Data Model] (XDM)的詳細資訊，請造訪[結構描述編輯器教學課程](../xdm/tutorials/create-schema-ui.md)。
>
>此外，如果資料集已啟用體驗事件到期值，這可能會影響已建立區段定義的成員資格。 請閱讀[體驗事件有效期](../profile/event-expirations.md)的指南，瞭解此功能如何影響分段的詳細資訊。

### 聯合客群構成 {#fac}

除了受眾構成和區段定義之外，您還可以使用Adobe同盟受眾構成從企業資料集建立新受眾，無需複製基礎資料即可將這些受眾儲存至Adobe Experience Platform受眾入口網站。 您也可以利用從企業資料倉儲已同盟的構成對象資料，讓Adobe Experience Platform中的現有對象更為豐富。 請閱讀[同盟對象構成](https://experienceleague.adobe.com/zh-hant/docs/federated-audience-composition/using/home)的指南。

## 評估對象 {#evaluate-segments}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation"
>title="評估方式"
>abstract="Experience Platform 目前支援三種評估客群的方式：串流分段、批次分段以及邊緣分段。"

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_streaming"
>title="串流評估"
>abstract="串流分段是持續進行的資料選擇流程；此功能會根據使用者活動來更新對象。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/methods/streaming-segmentation.html?lang=zh-Hant" text="使用串流分段近乎即時地評估事件"

Experience Platform 目前支援三種評估客群的方式：串流分段、批次分段以及邊緣分段。

### 串流區段 {#streaming}

串流細分是持續進行的資料選擇流程，其會根據使用者活動來更新客群。 建立並儲存對象後，區段定義就會套用至對[!DNL Real-Time Customer Profile]傳入的資料。 會定期處理對象的新增和移除，確保您的目標對象仍然相關。

若要深入瞭解串流區段，請閱讀[串流區段檔案](./methods/streaming-segmentation.md)。

### 批次分段 {#batch}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_batch"
>title="批次評估"
>abstract="批次分段是持續資料選取流程的替代方案，會透過區段定義立即移動所有設定檔資料以產生相對應的對象。建立後，系統會儲存並存放該對象，以便您可以將對象匯出使用。"

批次分段是持續資料選取流程的替代方案，會透過區段定義立即移動所有設定檔資料以產生相對應的對象。建立後，會儲存並儲存產生的對象，以便您將其匯出以供使用。

每24小時自動評估批次對象。 如果您想要依需求評估批次對象，則可以使用區段工作。 若要深入瞭解區段作業，請參閱[區段作業檔案](./api/segment-jobs.md)。

### 邊緣分段 {#edge}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_edge"
>title="邊緣評估"
>abstract="邊緣分段指在 Edge Network 上即時評估 Experience Platform 中區段的能力，可實現同一頁面和下一頁面個人化的使用案例。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/methods/edge-segmentation.html?lang=zh-Hant" text="邊緣分段服務指南"

Edge區段能在Edge Network[&#128279;](../landing/edge-and-hub-comparison.md)上即時評估Experience Platform中的區段，啟用相同頁面和下一頁個人化使用案例。

若要深入瞭解邊緣細分，請閱讀[邊緣細分概觀](./methods/edge-segmentation.md)。

## 存取區段結果

若要瞭解如何存取匯出的對象，請參閱[區段定義評估教學課程](./tutorials/evaluate-a-segment.md)。

## 區段定義中繼資料

區段定義中繼資料可在您的任何對象要重複使用和/或結合時協助編制索引。

構成區段定義（透過API或[!DNL Segment Builder]）需要您定義名稱和合併原則。

### 區段定義名稱

建立新區段定義時，您必須提供名稱。 區段定義名稱是用來識別由[!DNL Segmentation Service]建立的集合中的特定區段定義。 因此，區段定義名稱應具描述性、簡潔且獨特。

>[!NOTE]
>
>規劃區段定義時，請記住，區段定義可從任何其他區段定義中參照並與之結合。 選取名稱時，請考量您的區段定義可能包含可重複使用的部分的可能性。

### 合併原則

合併原則是[!DNL Profile]用來決定資料在特定條件下如何優先並合併到統一檢視中的規則。

如果未定義合併原則，則會使用預設的[!DNL Experience Platform]合併原則。 若您想使用組織專屬的合併原則，您可以建立自己的原則，並將其標示為組織的預設原則。

您可以在[合併原則指南](../profile/api/merge-policies.md)中找到有關合併原則的更多資訊。

>[!NOTE]
>
>預估對象人數是根據組織的預設設定檔合併原則。

### 其他區段定義中繼資料

除了名稱和合併原則之外，[!DNL Segment Builder]還提供您額外的說明中繼資料欄位，您可以在其中摘要您區段定義的用途。

## 進階分段功能

區段定義可設定為結合[串流資料擷取](../ingestion/streaming-ingestion/overview.md)以及下列任何進階分段功能，以持續產生對象：

- [循序分段](#sequential)
- [動態細分](#dynamic)
- [多實體分段](#multi-entity)

以下各節將更詳細地討論這些進階功能。

### 循序分段 {#sequential}

標準使用者歷程本質上為循序性質。 Adobe Experience Platform可讓您定義一系列有序的對象來反映此歷程，因此能擷取事件發生的順序。 您可以使用[!DNL Segment Builder]中的視覺事件時間軸，將事件依所需順序排列。

需要循序分段的客戶歷程範例為產品檢視>產品新增>結帳>不購買。

### 動態細分 {#dynamic}

動態細分可解決行銷人員在傳統上為行銷活動建立受眾時面臨的可擴充性問題。

靜態細分需要您明確並重複擷取每個可能的使用案例，而動態細分則會使用變數來建立規則邏輯及動態地表達關係。

為了說明此進階細分功能的價值，請考慮讓資料架構師與行銷人員合作，以識別在家庭狀態以外進行購買的客戶。

靜態區段會要求您先以唯一的首頁狀態屬性定義個別區段，再篩選不等於首頁狀態的購買事件。 若是此型別的明確區段定義，會顯示「我正在猶他州尋找購買狀態並非猶他州的人」。 使用此方法建立受眾時，需要您為每個美國州定義一個區段定義，一共有50個區段。

隨著規模增加，不可避免地會出現不同的區段定義組合，導致靜態區段所需的手動程式變得更加耗時，進而降低您的整體效率。

將變數指派給購買狀態屬性，您的動態區段定義簡化為「在該購買狀態不等於客戶居住狀態的情況下尋找我的購買」。 如此一來，您就可以將50個靜態區段合併為單一動態區段定義。

### 多實體分段 {#multi-entity}

使用進階多實體分段功能，您可以根據產品、商店或其他非人員（也稱為「維度」實體）的其他資料來擴充[!DNL Real-Time Customer Profile]資料。 因此，[!DNL Segmentation Service]可以在區段定義期間存取其他欄位，就好像這些欄位是[!DNL Profile]資料存放區的原生欄位一樣。 根據與您獨特業務需求相關的資料，多實體細分在識別對象時可提供彈性。 如需詳細資訊，包括使用案例和工作流程，請參閱[多實體分段指南](./tutorials/multi-entity-segmentation.md)。

## [!DNL Segmentation Service]資料型別

[!DNL Segmentation Service]支援各種基本和複雜的資料型別。 您可以在[支援的資料型別指南](./data-types.md)中找到詳細資訊，包括支援的資料型別清單。

## 後續步驟

[!DNL Segmentation Service]提供合併的工作流程，以從[!DNL Real-Time Customer Profile]資料建立對象。

如需使用Segmentation Service UI的詳細資訊，請參閱[Segmentation Service UI概觀](./ui/overview.md)。

若要瞭解如何在UI中撰寫對象，請閱讀[對象撰寫指南](./ui/audience-composition.md)。 若要瞭解如何在UI中定義區段定義，請參閱[區段產生器指南](./ui/overview.md)。 如需有關使用API建立區段定義的資訊，請參閱有關[使用API建立區段定義](./tutorials/create-a-segment.md)的教學課程。
