---
keywords: Experience Platform；主題；熱門主題；分段；分段；分段；分段；分段；分段；分段；分段；分段；分段；分段；分段；分段
solution: Experience Platform
title: 分段服務概述
description: 瞭解Adobe Experience Platform細分服務及其在平台生態系統中的作用。
exl-id: 2c18a806-88ed-4659-bdfd-2377f5a09a1a
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1635'
ht-degree: 11%

---

# [!DNL Segmentation Service] 概覽

Adobe Experience Platform [!DNL Segmentation Service] 提供了用戶介面和REST風格的API，允許您生成段並從您的 [!DNL Real-Time Customer Profile] 資料。 這些段在 [!DNL Platform]，並且任何Adobe解決方案都可輕鬆訪問。

此文檔提供 [!DNL Segmentation Service] 以及它在Adobe Experience Platform的作用。

## 入門 [!DNL Segmentation Service]

瞭解本文檔中使用的以下關鍵術語非常重要：

- **分段**:將一大群人（如客戶、潛在客戶、用戶或組織）分成具有相似特性並將對市場營銷策略做出類似反應的較小群體。
- **段定義**:用於描述目標受眾的關鍵特徵或行為的規則集。 一旦概念化，段定義中概述的規則將用於確定段的合格受眾成員。
- **觀眾**:符合段定義條件的結果配置檔案集。

## 分段的工作原理

細分是定義配置檔案子集與配置檔案儲存共用的特定屬性或行為的過程，以區分可銷售的人員組與客戶群。 例如，在一封名為「你忘記買運動鞋了嗎？」的電子郵件中，你可能希望看到過去30天內搜索跑鞋但沒有完成購買的所有用戶的觀眾。

一旦在概念上定義了段，就內置 [!DNL Experience Platform]。 通常，細分由營銷人員或受眾專家構建，儘管一些組織希望由其營銷部門與資料分析員協作建立。 查看要發送到 [!DNL Platform]，資料分析員通過選擇哪些欄位和值將用於構建段的規則或條件來組成段定義。 這是使用UI或API完成的。

## 建立區段

是使用API建立還是使用 [!DNL Segment Builder]，段最終使用 [!DNL Profile Query Language] (PQL)。 在此處，概念段定義將以檢索滿足條件的配置檔案所構建的語言進行描述。 有關詳細資訊，請參見 [PQL概述](./pql/overview.md)。

瞭解如何在 [!DNL Segment Builder] (UI實現 [!DNL Segmentation Service])，請參閱 [段生成器指南](./ui/overview.md)。

有關使用API構建段定義的資訊，請參見上的教程 [使用API建立受眾段](./tutorials/create-a-segment.md)。

>[!NOTE]
>
>在擴展架構時，所有將來的上載都必須相應更新新添加的欄位。 有關自定義的詳細資訊 [!DNL Experience Data Model] (XDM)，訪問 [架構編輯器教程](../xdm/tutorials/create-schema-ui.md)。
>
>此外，如果資料集上啟用了「體驗事件」過期值，則這可能會影響所建立段的成員身份。 請閱讀上的指南 [體驗事件過期](../profile/event-expirations.md) 的子菜單。

## 評估段 {#evaluate-segments}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation"
>title="評估方式"
>abstract="Platform 目前支援三種評估區段的方式：串流分段、批次分段以及邊緣分段。"

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_streaming"
>title="串流評估"
>abstract="串流分段是一種持續的資料選取流程，會根據使用者活動更新您的區段。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/api/streaming-segmentation.html" text="使用串流分段近乎即時地評估事件"

Platform 目前支援三種評估區段的方式：串流分段、批次分段以及邊緣分段。

### 流分段 {#streaming}

串流分段是一種持續的資料選取流程，會根據使用者活動更新您的區段。一旦生成並保存了段，將針對傳入資料應用段定義。 [!DNL Real-Time Customer Profile]。 定期處理段添加和刪除，確保目標受眾保持相關性。

要瞭解有關流分段的詳細資訊，請閱讀 [流分段文檔](./api/streaming-segmentation.md)。

### 批分段 {#batch}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_batch"
>title="批次評估"
>abstract="批次分段是持續資料選取流程的替代方案，會透過區段定義立即移動所有設定檔資料以產生相對應的對象。建立後，會將區段儲存並存放，以便您可以將其匯出使用。"

批次分段是持續資料選取流程的替代方案，會透過區段定義立即移動所有設定檔資料以產生相對應的對象。建立後，將保存並儲存此段，以便導出該段供使用。

每24小時自動評估批段。 如果要按需計算批段，則可以使用段任務。 要瞭解有關段作業的詳細資訊，請閱讀 [段作業文檔](./api/segment-jobs.md)。

### 邊緣分割 {#edge}

>[!CONTEXTUALHELP]
>id="platform_segments_evaluation_edge"
>title="邊緣評估"
>abstract="邊緣分段指在 Experience Edge 上即時評估 Platform 中的區段的能力，可實現同一頁面和下一頁面個人化的使用案例。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/edge-segmentation.html" text="邊緣分段服務 UI 指南"

邊緣分割是即時評估平台中段的能力 [體驗邊緣](../edge/home.md)，啟用同頁和下頁個性化用例。

要瞭解有關邊緣分割的詳細資訊，請閱讀 [API文檔](./api/edge-segmentation.md) 或 [UI文檔](./ui/edge-segmentation.md)。

## 訪問分段結果

要瞭解如何訪問導出的段，請參閱 [段評估教程](./tutorials/evaluate-a-segment.md)。

## 段元資料

段元資料有助於在任何段被重用和/或組合時進行索引。

合成段(通過API或 [!DNL Segment Builder])要求您定義段名和合併策略。

### 段名稱

建立新段時，需要提供段名稱。 段名稱用於標識由 [!DNL Segmentation Service]。 因此，段名稱應具有描述性、簡潔性和唯一性。

>[!NOTE]
>
>在規劃段時，請記住，可以從任何其它段參照段，並與其組合。 選擇名稱時，請考慮段可能包含可重用部分。

### 合併策略

合併策略是使用的規則 [!DNL Profile] 確定資料在特定條件下如何排定優先順序並合併為統一視圖。
如果未定義合併策略，則預設 [!DNL Platform] 使用合併策略。 如果您希望使用特定於組織的合併策略，則可以建立自己的合併策略並將其標籤為組織的預設策略。

有關合併策略的詳細資訊，請參閱 [合併策略指南](../profile/api/merge-policies.md)。

>[!NOTE]
>
>受眾規模的估計基於組織的預設配置檔案合併策略。

### 其他段元資料

除段名和合併策略外， [!DNL Segment Builder] 為您提供了一個附加的「段說明」元資料欄位，您可以在該欄位中總結段定義的用途。

## 高級分段特徵

可將段配置為通過組合持續地生成受眾 [流資料接收](../ingestion/streaming-ingestion/overview.md) 具有以下任何高級分割功能：
- [序貫分割](#sequential)
- [動態分割](#dynamic)
- [多實體分割](#multi-entity)

以下各節將更詳細地討論這些高級功能。

## 序貫分割 {#sequential}

標準用戶行程在性質上是連續的。 Adobe Experience Platform允許您定義一系列有序的段以反映此行程，從而在事件發生時捕獲事件序列。 通過使用中的可視事件時間軸，可以將事件排列為所需的順序 [!DNL Segment Builder]。

需要按順序分段的客戶行程示例為產品視圖>產品添加>結帳>無購買。

## 動態分割 {#dynamic}

動態細分解決了營銷活動構建細分市場時營銷人員傳統上面臨的可擴充性問題。

與靜態分割不同，動態分割需要顯式並重複捕獲每個可能的使用案例，而動態分割則使用變數來構建規則邏輯並動態表達關係。

### 用例：尋找在本國以外購買的客戶

為了說明此高級細分功能的價值，請考慮一個資料架構師與一個營銷人員協作，以確定在其本國之外進行採購的客戶。

**問題**

靜態分段要求您使用唯一的家庭狀態屬性定義單個段，然後篩選不等於家庭狀態的購買事件。 此類型的明確部分將寫成「我在尋找來自猶他州的人，而他們購買的產品不在猶他州」。 使用此方法建立受眾要求您為每個美國州定義一個段，共50個段。

由於縮放時不可避免地會出現不同的段組合，因此靜態分割所需的手動過程會更加耗時，從而降低整體效率。

**解決方案**

通過將變數賦給採購狀態屬性，您的動態段可簡化為「在採購狀態不等於客戶家庭狀態的情況下查找採購」。 這樣，您就可以將50個靜態段合併到一個動態段中。

## 多實體分割 {#multi-entity}

使用高級多實體分割特徵，可以擴展 [!DNL Real-Time Customer Profile] 帶有基於產品、儲存或其他非人員的附加資料的資料，也稱為「維」實體。 因此， [!DNL Segmentation Service] 可以在段定義期間訪問其他欄位，就好像這些欄位是本地的 [!DNL Profile] 資料儲存。 當根據與您的獨特業務需要相關的資料識別受眾時，多實體細分提供了靈活性。 有關更多資訊（包括使用案例和工作流），請參閱 [多實體分割指南](multi-entity-segmentation.md)。

## [!DNL Segmentation Service] 資料類型

[!DNL Segmentation Service] 支援各種原始和複雜的資料類型。 詳細資訊，包括支援的資料類型清單，請參見 [支援的資料類型指南](./data-types.md)。

## 後續步驟

[!DNL Segmentation Service] 提供了一個整合的工作流，以從 [!DNL Real-Time Customer Profile] 資料。 總之：

- [!DNL Segmentation] 是從配置檔案儲存中定義配置檔案子集的過程，允許您表徵所需有價組的行為或屬性。 [!DNL Segmentation Service] 使這個過程成為可能。
- 在規劃段時，請記住可以從任何其他段參照段並將其組合。
- 可以基於配置檔案資料、相關時間序列資料或兩者的規則構建段。
- 段可以按需評估，也可以連續評估。 按需評估時，所有配置檔案資料都會一次通過段定義。 連續評估時，資料流會通過段定義進入 [!DNL Platform]。

要瞭解如何在UI中定義段，請參閱 [段生成器指南](./ui/overview.md)。 有關使用API構建段定義的資訊，請參見上的教程 [使用API建立段](./tutorials/create-a-segment.md)。
