---
keywords: Experience Platform；首頁；熱門主題；分段；分段；分段服務；分段；分段；分段；分段；分段；分段；分段；分段；分段；分段；分段；分段
solution: Experience Platform
title: 區段服務概觀
topic: 概述
description: 瞭解Adobe Experience Platform細分服務及其在平台生態系統中的作用。
translation-type: tm+mt
source-git-commit: 7eadb14dc71792174dfd750775148763f55834dd
workflow-type: tm+mt
source-wordcount: '1449'
ht-degree: 0%

---


# [!DNL Segmentation Service] 概觀

Adobe Experience Platform[!DNL Segmentation Service]提供使用者介面和RESTful API，可讓您建立區段並從您的[!DNL Real-time Customer Profile]資料產生觀眾。 這些區段是集中設定並維護在[!DNL Platform]上，任何Adobe解決方案都可輕鬆存取。

本檔案概述[!DNL Segmentation Service]及其在Adobe Experience Platform的作用。

## [!DNL Segmentation Service]快速入門

請務必瞭解本檔案中使用的下列主要術語：

- **區段**:將大量個人（例如客戶、潛在客戶、使用者或組織）分成具有相似特性且回應類似行銷策略的較小群組。
- **區段定義**:用於描述目標對象的關鍵特性或行為的規則集。概念化後，區段定義中概述的規則會用來決定區段的合格讀者成員。
- **觀眾**:符合區段定義條件的結果描述檔集。

## 區段的運作方式

區段是定義描述檔商店中描述檔子集所共用的特定屬性或行為，以區分適銷人員群組和客戶群的程式。 例如，在名為「您忘記購買運動鞋嗎？」的電子郵件促銷活動中，您可能希望擁有在過去30天內搜尋跑鞋但未完成購買的所有使用者的觀眾。

在概念上定義區段後，會內建在[!DNL Experience Platform]中。 通常，區段是由行銷人員或受眾專員建立，但有些組織希望由行銷部門與資料分析人員共同建立。 在檢視傳送至[!DNL Platform]的資料時，資料分析人員會選擇將用來建立區段規則或條件的欄位和值，以建立區段定義。 這是使用UI或API來完成的。

## 建立區段

無論是使用API建立還是使用[!DNL Segment Builder]，區段最終都會使用[!DNL Profile Query Language](PQL)來定義。 在此處，概念區段定義會以擷取符合標準的描述檔所建立的語言加以說明。 有關詳細資訊，請參閱[PQL概述](./pql/overview.md)。

若要瞭解如何在[!DNL Segment Builder]（[!DNL Segmentation Service]的UI實作）中建立和使用區段，請參閱[區段產生器指南](./ui/overview.md)。

如需有關使用API建立區段定義的詳細資訊，請參閱[使用API](./tutorials/create-a-segment.md)建立觀眾區段的教學課程。

>[!NOTE]
>
>在模式被擴展時，所有以後的上載都必須相應地更新新添加的欄位。 有關自定義[!DNL Experience Data Model](XDM)的詳細資訊，請訪問[方案編輯器教程](../xdm/tutorials/create-schema-ui.md)。

## 評估區段

平台目前支援兩種評估區段的方法：串流分段和批次分段。

### 串流區段

串流區段是持續不斷的資料選擇程式，可因應使用者活動而更新區段。 建立並儲存區段後，區段定義會套用至[!DNL Real-time Customer Profile]的傳入資料。 區段新增和移除作業會定期處理，確保目標受眾保持相關性。

若要進一步瞭解串流分段，請閱讀[串流分段檔案](./api/streaming-segmentation.md)。

### 批次分段

作為持續資料選擇程式的替代選擇，批次分段會透過區段定義一次移動所有描述檔資料，以產生對應的觀眾。 建立後，會儲存此區段，以便匯出以供使用。

若要瞭解如何評估區段，請參閱[區段評估教學課程](./tutorials/evaluate-a-segment.md)。

### 邊緣分割

邊緣區段是指能夠即時在邊緣上評估平台中的區段，讓相同的頁面和下一頁個人化使用案例。

若要進一步瞭解邊緣區段，請閱讀[API檔案](./api/edge-segmentation.md)或[UI檔案](./ui/edge-segmentation.md)。

## 存取區段結果

要瞭解如何訪問導出的段，請參閱[段評估教程](./tutorials/evaluate-a-segment.md)。

## 區段中繼資料

區段中繼資料可協助您在任何區段重複使用及／或組合時建立索引。

合成區段（透過API或[!DNL Segment Builder]）需要您定義區段名稱並合併原則。

### 區段名稱

建立新區段時，您必須提供區段名稱。 區段名稱用於識別由[!DNL Segmentation Service]建立之系列中的特定區段。 因此，區段名稱應具有說明性、簡明和獨特性。

>[!NOTE]
>
>在規劃區段時，請記住，區段可從任何其他區段參考，並與之結合。 選取名稱時，請考慮您的群體可能包含可重複使用的部分。

### 合併原則

合併策略是[!DNL Profile]用於確定資料在特定條件下如何按優先順序排列並合併為統一視圖的規則。
如果未定義合併策略，則使用預設的[!DNL Platform]合併策略。 如果您想要使用組織專屬的合併原則，可以建立自己的合併原則，並將其標示為組織的預設值。

有關合併策略的詳細資訊，請參閱[合併策略指南](../profile/api/merge-policies.md)。

>[!NOTE]
>
>觀眾人數的估計是根據組織的預設描述檔合併原則。

### 其他區段中繼資料

除了區段名稱和合併原則外，[!DNL Segment Builder]還提供您額外的「區段說明」中繼資料欄位，供您概述區段定義的用途。

## 進階細分功能

可將區段設定為結合[串流資料擷取](../ingestion/streaming-ingestion/overview.md)與下列任何進階區段功能，持續產生觀眾：
- [循序分段](#sequential)
- [動態細分](#dynamic)
- [多實體分段](#multi-entity)

以下幾節將更詳細地討論這些進階功能。

## 循序分段{#sequential}

標準的使用者歷程在本質上是循序的。 Adobe Experience Platform可讓您定義一系列有序的區段，以反映此歷程，從而在事件發生時擷取事件的序列。 您可以使用[!DNL Segment Builder]中的視覺化事件時間軸，依所需順序排列事件。

需要循序劃分的客戶歷程範例包括產品檢視>產品新增>結帳>無購買。

## 動態分段{#dynamic}

動態細分可解決行銷人員在建立行銷宣傳的細分時，傳統上所面臨的可擴充性問題。

與靜態分段不同，動態分段需要明確且重複擷取每個可能的使用案例，動態分段使用變數來建立規則邏輯並動態表達關係。

### 使用案例：尋找在家庭以外購買的客戶

為了說明此進階細分功能的價值，請考慮由資料架構師與行銷人員協作，以識別在其祖國以外進行採購的客戶。

**問題**

靜態區段需要您先定義具有唯一首頁狀態屬性的個別區段，然後再篩選不等於首頁狀態的購買事件。 此類型的明確區段會是「我在尋找來自猶他州的人，他們購買的州並非猶他州」。 使用此方法建立觀眾時，您必須為每個美國州定義一個區段，共50個區段。

由於不同的區段組合不可避免地會隨著您的縮放而產生，因此靜態區段所需的手動程式變得更耗時，降低整體效率。

**解決方案**

透過將變數指派至購買狀態屬性，您的動態區段可簡化為「在購買狀態不等於客戶首頁狀態的情況下尋找購買」。 如此可讓您將50個靜態區段合併為單一動態區段。

## 多實體分段{#multi-entity}

透過進階的多實體分段功能，您可以根據產品、商店或其他非人（亦稱為「維度」實體），以額外資料擴充[!DNL Real-time Customer Profile]資料。 因此，[!DNL Segmentation Service]可在區段定義期間存取其他欄位，就像這些欄位是[!DNL Profile]資料存放區的原生欄位。 多實體區隔可讓您根據與您獨特業務需求相關的資料來識別受眾時，有彈性。 如需詳細資訊，包括使用案例和工作流程，請參閱[多實體分段指南](multi-entity-segmentation.md)。

## [!DNL Segmentation Service] 資料類型

[!DNL Segmentation Service] 支援多種原始和複雜的資料類型。如需詳細資訊，包括支援的資料類型清單，請參閱[支援的資料類型指南](./data-types.md)。

## 後續步驟

[!DNL Segmentation Service] 提供整合的工作流程，從資料建立 [!DNL Real-time Customer Profile] 區段。總之：

- [!DNL Segmentation] 是從描述檔商店定義描述檔子集的程式，可讓您描述所需有價群組的行為或屬性。[!DNL Segmentation Service] 使這個過程成為可能。
- 規劃區段時，請記住，區段可從任何其他區段參考，並與之結合。
- 您可以根據描述檔資料、相關時間系列資料或兩者，從規則建立區段。
- 區段可依需求或持續評估。 在隨選評估時，所有描述檔資料都會一次傳遞至區段定義。 持續評估時，當資料串流進入[!DNL Platform]時，會透過區段定義。

若要瞭解如何在UI中定義區段，請參閱[區段產生器指南](./ui/overview.md)。 如需有關使用API建立區段定義的詳細資訊，請參閱有關使用API](./tutorials/create-a-segment.md)建立區段的教學課程。[