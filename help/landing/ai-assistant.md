---
title: Adobe Experience Platform的AI助理
description: 瞭解如何使用AI助理來導覽並瞭解Experience Platform和Real-time Customer Data Platform概念，以及有關您物件的使用資訊。
badge: Alpha
hide: true
hidefromtoc: true
exl-id: 8be1c222-3ccd-4a41-978e-33ac9b730f8c
source-git-commit: b1f2d85f5a1cf6bb38344c87496488a919800029
workflow-type: tm+mt
source-wordcount: '2604'
ht-degree: 0%

---

# Adobe Experience Platform的AI助理

>[!NOTE]
>
> 適用於Adobe Experience Platform的AI助理目前Alpha。 功能和檔案可能會有所變更。

AI助理是UI功能，可用來導覽並瞭解Adobe Experience Platform和Real-time Customer Data Platform概念以及有關您物件的使用資訊。

您可以查詢AI助理以取得下列資訊：

* 有關如何執行與資料和受眾相關之工作的指南。
* 貴組織中現有資料物件的狀態和量度。
* 使用案例範例和細微差別，更能瞭解您的資料物件，包括屬性、資料流、資料集、目的地、結構描述、區段和來源。

請閱讀以下指南，瞭解如何使用AI助理來協助導覽並瞭解您的Experience Platform和Real-Time CDP工作流程。

>[!BEGINSHADEBOX]

**AI助理如何運作？**

AI Assistant會查詢資料庫，然後將資料庫中的資料轉譯成人類看得懂的答案，以回應您提交的問題。

這種基礎資料的內部表示法也稱為知識圖表，是一張包含特定答案的概念、資料和中繼資料的完整網路。

「知識圖形」由每次提交查詢時所參考的子圖形組成：

* 客戶使用資料。
* 各種中繼存放區的客戶使用資料。
* Experience League檔案。

在查詢AI Assistant之前，需要考慮兩種型別的問題：

* **概念問題**：概念問題與資料或受眾相關的Adobe概念有關。 概念問題的一些範例包括：
   * 批次和串流區段之間有何差異？
   * 是否有產業資料模型，以及我該如何使用？
   * Real-Time CDP的最佳用途為何？
* **使用問題**：使用問題與組織內的資料物件有關。 使用問題的一些範例包括：
   * 我有多少資料集？
   * 有多少結構描述屬性從未使用過？
   * 已啟用哪些區段？

>[!ENDSHADEBOX]

## 您可以使用AI助理完成的目標

您可以使用AI助理來達成下列目標：

| 目標 | 說明 |
| --- | --- |
| 學習Experience Platform和Real-Time CDP概念 | 您可以詢問AI Assistant的概念問題，這樣您就可以將自己帶入Experience Platform和Real-Time CDP中。 您也可以使用AI Assistant來瞭解您不熟悉的物件和行為。 |
| 確保沙箱中的資料整潔 | 您可以使用AI Assistant來識別任何重複專案或未使用的物件，以便有效地維護沙箱的乾淨。 |
| 協調價值分析 | 您可以使用AI Assistant來識別您最常使用的物件，並評估任何績效指標或尋找最有價值的資料。 |
| 瞭解影響分析 | 您可以使用AI助理來識別某些工作流程中使用的物件，以便評估任何變更的影響。 |
| 監控您的資料 | 您可以使用AI助理來監視任何資料流、擷取或評估工作，以便檢視任何差異或報告進度。 |

## 在Experience PlatformUI中存取AI助理

若要啟動AI助理，請選取 **[!UICONTROL AI助理圖示]** 從Experience PlatformUI的頂端標題。

![Experience Platform首頁，其中已選取AI助理圖示並開啟AI助理介面。](./images/ai-assistant/ai-assistant.png)

AI Assistant介面隨即顯示，立即為您提供開始使用的資訊。 您可以使用下提供的選項 [!UICONTROL 開始使用的概念] 回答下列問題和命令：

* [!UICONTROL 系統會啟用我的哪些區段？]
* [!UICONTROL 什麼是結構描述？]
* [!UICONTROL 告訴我一些Real-Time CDP的常見使用案例]

![AI Assistant的「入門概念」一節。](./images/ai-assistant/ideas-to-get-started.png)

若要與AI Assistant互動，請使用輸入方塊輸入您的查詢或命令。 您也可以使用(**`+`**)符號，以利用自動完成功能及書籤圖示來存取您的書籤化查詢與命令。

![AI助理輸入方塊會反白顯示。](./images/ai-assistant/interact.png)

## 使用案例範例：使用AI助理加快您的綱要建立流程

>[!NOTE]
>
>以下工作流程是使用Experience Event結構描述建立程式的範例，說明如何使用Experience PlatformUI中的AI Assistant。

考慮您正在建立的使用案例 **裝置交易事件結構描述**. 在體驗事件結構描述建立程式期間，您會 `eventType` 欄位。 「此時，您可以選擇退出工作流程並參閱 [結構描述組合的基本面](../xdm/schema/composition.md) 檔案或您可以使用AI助理來擷取問題的答案，並透過AI助理建議的檔案連結尋找其他資源。」

若要開始，請在提供的文字方塊中輸入您的問題。 在以下範例中，AI Assistant會提供以下問題： &quot;**什麼是ExperienceEvent結構描述中的eventType欄位？**&quot;

![用於Experience Platform的AI助理具有下列準備進行查詢的問題：「什麼是ExperienceEvent結構描述中的eventType欄位？](./images/ai-assistant/question.png)

AI Assistant接著會查詢其知識庫並計算答案。 幾分鐘後，AI Assistant會傳回答案和相關建議，您可將其用作後續提示。

![有上一個查詢答案的Experience PlatformAI助理。](./images/ai-assistant/answer.png)

收到來自AI助理的回應後，您可以從多個選項中進行選取，以決定要如何繼續。

### 儲存查詢 {#save-your-query}

+++選取以檢視如何儲存查詢的範例

若要儲存查詢，請選取問題旁的書籤圖示。

![選取書籤的熒幕擷圖。](./images/ai-assistant/save-your-query.png)

若要存取已儲存的查詢，請選取輸入方塊下方的書籤圖示，然後選取您要執行的查詢。

![書籤圖示的熒幕擷圖和已儲存查詢的清單。](./images/ai-assistant/bookmarks.png)

+++

### 在您的沙箱中檢視資料 {#view-data-in-your-sandbox}

+++選取以檢視範例

根據您的查詢，AI Assistant會提供與沙箱中資料相關的其他資訊。 若要檢視查詢回應如何套用至您的沙箱，請選取 **[!UICONTROL 在您的沙箱中].**

在此步驟中，AI助理可以提供特定問題物件UI頁面的直接連結。 在以下範例中，AI Assistant提供直接連結至 [!UICONTROL 方案] 和 [!UICONTROL 區段] UI頁面。

![「在您的沙箱中」選項的熒幕擷圖。](./images/ai-assistant/in-your-sandbox.png)

+++

### 驗證回應 {#verify-the-response}

+++選取此選項可檢視如何顯示來源的範例

若要檢視引文及驗證AI助理的回應，請選取 **[!UICONTROL 顯示來源]**. AI Assistant提供可證實其回應的檔案連結。 您也可以使用AI Assistant提供的查詢 [!UICONTROL 相關建議] 以進一步探索與原始查詢相關的主題。

![「顯示來源」熒幕擷圖。](./images/ai-assistant/show-sources.png)

+++

### 資料使用情況和視覺效果 {#data-usage-and-visualization}

+++選取此選項可檢視資料使用問題和資料視覺效果的範例

若要讓AI Assistant回應有關您組織內資料使用情況的查詢，您必須處於有效沙箱中。

在以下範例中，AI助理會隨附以下查詢： **「向我顯示含有超過1000個設定檔的區段定義，並包含啟用狀態。」** AI Assistant接著會以圖表回應，將您的區段和設定檔資料視覺化。

![繼續回答有關資料使用的問題。](./images/ai-assistant/data-usage-question.png)

您可以將滑鼠停留在個別長條圖上，以檢視特定資料。 您也可以選取展開圖示，以檢檢視表的大圖。

![繼續回答說明資料視覺化效果的問題。](./images/ai-assistant/data-visualization.png)

視覺效果的展開檢視隨即顯示。 您可以使用展開的強制回應視窗來進一步檢查資料，且在視覺化傳回大量欄時特別實用。

![展開的圖表。](./images/ai-assistant/chart-expanded.png)

出現資料使用問題提示時，AI Assistant會提供如何計算答案的說明。 在以下範例中，AI Assistant概述其顯示的區段定義及其超過1000個設定檔和各自啟用狀態所採取步驟。

![繼續回答有關區段的問題，以說明AI Assistant如何計算答案。](./images/ai-assistant/results-explained.png)

您還可以提供篩選器和修改查詢，並可以指示AI助理根據您包含的篩選器呈現其結果。 例如，您可以要求AI助理按照區段建立的日期順序，顯示計數區段定義的趨勢；移除總設定檔為零的區段定義；以及在顯示資料時，使用月份名稱而非整數。

+++

### 使用自動完成 {#use-auto-complete}

+++選取以檢視自動完成的範例

您可以使用自動完成函式來接收沙箱中存在之資料物件的清單。 自動完成建議適用於下列網域：區段、結構描述、資料集、來源和目的地。

加入加號(**`+`**)。 您也可以選取加號(**`+`**)，位於文字輸入方塊底部。 隨即顯示一個視窗，其中包含沙箱中建議的資料物件清單。

![自動完成範例](./images/ai-assistant/auto-complete-one.png)

接著，選取您要查詢的資料物件以完成問題，然後提交問題。

![自動完成並附上問答的範例](./images/ai-assistant/auto-complete-two.png)

+++

### 使用多圈 {#use-multi-turn}

+++選取以檢視多圈範例

您可以使用AI Assistant的多圈功能，在體驗期間進行更自然的交談。 AI Assistant能夠回答後續的問題。 該上下文可從先前的互動中推斷。

在以下範例中，會要求AI助理取得目前組織中資料流程的總數。

![多圈範例](./images/ai-assistant/multi-turn-one.png)

接著，AI助理會收到另一個後續追蹤要求。 這次，AI Assistant會列出組織中目前存在的資料流來進行回應。

![包含問答的多圈範例](./images/ai-assistant/multi-turn-two.png)

+++

## 文件 {#documentation}

目前，檔案索引涵蓋Adobe Experience Platform (Real-Time CDP和受眾)。 索引會定期更新。

說明檔案擷取模型已針對Experience Platform(Real-Time CDP和受眾)接受訓練。 Adobe Experience Platform範圍以外的問題，例如，關於其他Adobe產品(如Adobe Target)和Creative Cloud套裝的問題，無法回答。

## 資料使用情況 {#data-usage}

您也可以向AI Assistant詢問有關下列網域中資料使用情況的問題：

* 屬性
* 資料流
* 資料集
* 目的地 _（關於帳戶的問題和資料流的一些問題目前無法回答。）_
* 方案 _（目前無法回答有關欄位群組的問題。）_
* 區段
* 來源 _（目前無法回答有關帳戶的問題。）_

對於使用資料查詢，答案可能不會反映UI的目前狀態。 支援這些問題的資料每24小時更新一次。 例如，使用者白天在Real-Time CDP中所做的變更會在夜間與資料存放區同步，然後早上就可供使用者提問。 您可能需要將問題的格式設定為：「標題為的區段是什麼時候 {TITLE} 建立時間？」 而非「何時會 {TITLE} 區段已建立？」

您需要登入沙箱，查詢與物件（例如結構描述、資料集、屬性、目的地和區段）相關的特定資料。

### 範例資料使用問題 {#example-data-usage-questions}

+++選取以檢視範例資料使用問題清單

| 問題型別 | 說明 | 範例 |
| --- | --- | --- | 
| 資料譜系 | 追蹤其他Experience Platform物件中一或多個物件的使用情況 | <ul><li>使用哪些資料集 {SCHEMA_NAME} 綱要？</li><li>使用相同結構描述擷取了多少資料集？</li><li>已啟用區段中已使用哪些資料集？</li><li>列出具有用於已啟動區段之屬性的結構描述。</li><li>顯示啟用的區段 {DESTINATION_ACCOUNT_NAME} 和超過1000個設定檔。</li><li>顯示已啟動區段（在2023年1月之後已修改）中使用的屬性。</li><li>什麼是資料集透過擷取 {SOURCE_NAME}？</li><li>哪些資料流相關聯 {DATAFLOW_NAME}</li><li>列出與已啟動區段相關且建立於過去1年的結構描述。</li></ul> |
| 分佈與彙總 | 關於Experience Platform物件使用情況的摘要式問題 | <ul><li>已啟動區段的百分比為何？</li><li>區段中使用了多少欄位？</li><li>啟用至最多目的地的區段有哪些？</li><li>列出重複的區段。</li><li>顯示啟用的區段 {DESTINATION_ACCOUNT_NAME} 並按設定檔大小排名。</li><li>尚未啟動但設定檔超過100個的區段百分比為何？ 顯示他們的姓名。</li><li>列出將資料擷取到我的資料集中的3個來源聯結器。</li><li>根據已啟動區段中的出現次數，列出前5個用於已啟動區段的屬性。</li></ul> |
| 物件查詢 | 擷取或存取Experience Platform物件或其屬性。 | <ul><li>哪些資料集沒有任何相關聯的結構描述</li><li>列出用於以下專案的屬性： {SEGMENT_NAME}？</li><li>給我已啟用設定檔但自建立以來未修改的結構描述清單。</li><li>上週修改了哪些區段？</li><li>列出具有相同區段定義的區段及其建立日期。</li><li>哪些資料集已啟用設定檔，並且包括已從每個資料集建立多少區段。</li><li>哪些來源帳戶與資料集XYZ相關聯？</li><li>顯示區段定義和修改日期 {SEGMENT_NAME}.</li></ul> |

+++

## 提供意見反應 {#feedback}

>[!BEGINSHADEBOX]

**您的意見回饋已要求**

在此Alpha階段，請您針對從AI助理收到的回應提供意見反應。 所有回應和提交的意見都會經過稽核，以繼續改善AI助理體驗。

若要提供意見回饋，請在收到AI助理的回應後選取向上或向下拇指，然後在提供的文字方塊中輸入您的意見回饋。 接下來，選取 **[!UICONTROL 提交意見]** 以提交。

>[!ENDSHADEBOX]

+++提供意見回饋

>[!BEGINTABS]

>[!TAB 豎起大拇指]

選取向上拇指圖示，提供您對於AI助理的良好體驗的反饋。

![正面意見回饋視窗。](./images/ai-assistant/thumbs-up.png)

>[!TAB 向下拇指]

選取向下縮圖圖示，即可根據您使用AI助理的經驗，提供哪些可改善的意見回饋。 在此步驟中，您也可以提供關於體驗的特定註解。 評論中提供的意見回饋會每天稽核。

![負面意見回饋視窗。](./images/ai-assistant/thumbs-down.png)

>[!TAB 標幟]

選取標幟圖示以提供關於您使用AI助理體驗的進一步報告。

![報表結果視窗。](./images/ai-assistant/flag.png)

>[!ENDTABS]

+++

## 其他資訊 {#additional-information}

請參閱本節以取得有關AI Assistant forExperience Platform的更多資訊。

### 警告和限制 {#caveats-and-limitations}

以下章節概述使用AI助理時應考量的目前注意事項和限制。
<!-- 
#### Conversational experience

You must consider several nuances regarding the conversational experience when querying the AI Assistant.

>[!NOTE]
>
>These limitations are temporary and are being improved upon throughout the course of the alpha.

>[!BEGINTABS]

>[!TAB Unable to infer context from prior discussion]

The AI Assistant currently cannot reference prior discussions as context for a given question. See the table below for examples:

| Ambiguous question | Clear question | Note |
| --- | --- | --- |
| <ul><li>First question: "What is a segment?"</li><li>Follow up question: "Are there different types of them?"</li></ul>| <ul><li>First question: "What is a segment?"</li><li>Follow up question: "Are there different types of **segments**?"</li></ul> | The AI Assistant cannot infer what "them" means. |
| <ul><li>First question: "What is a segment?"</li><li>Follow up question: "Can you elaborate more?"</li></ul> | <ul><li>First question: "What is a segment?"</li><li>Follow up question: "Explain what a segment is in depth"</li></ul> | The AI Assistant cannot intelligently reference documentation based on "more". |
| <ul><li>First question: "What is a segment?"</li><li>Follow up question: "Can you give me an example of one?"</li></ul> | <ul><li>First question: "What is a segment?"</li><li>Follow up question: "Can you give me an example of a segment?"</li></ul> | The AI Assistant cannot infer what you want an example of.|
| <ul><li>First question: "What is a batch segment?"</li><li>Follow up question: "How does it compare to a streaming segment?"</li></ul> | <ul><li>First question: "What is a batch segment?"</li><li>Follow up question: "Can you compare a streaming segment to a batch segment?"</li></ul> | The AI Assistant cannot infer what "it" is referring to and thus cannot compare the streaming segment. |
| <ul><li>First question: "How many segments do I have?"</li><li>Follow up question: "How many of them use Facebook as a destination?"</li></ul> | <ul><li>First question: "How many segments do I have?"</li><li>Follow up question: "How many of the segments that I have are using Facebook as a destination?"</li></ul> | The AI Assistant is cannot infer what "them" is referring to. |

{style="table-layout:auto"}

>[!TAB Unable to infer context from a page]

When asking the AI Assistant about a particular element of the Experience Platform UI page that you are on, you must clearly define the specific element within your question. 

| Ambiguous question | Clear question | Note |
| --- | --- | --- |
| "What does this do?" | "What does {PAGE_NAME} do? | The AI Assistant cannot infer what "this" is referring to. You must provide the specific page element that you are querying about. |
| "Why won't it save?" | "Why can't I save a new sandbox called {NAME}?" | The AI Assistant cannot infer what "it" is referring to and cannot know that you are having issues with an entity. |

{style="table-layout:auto"}

Furthermore, the AI Assistant can only answer questions regarding error messages, given that the error is documented in Experience League.

>[!TAB Ambiguity]

You must phrase your questions clearly and scope them within a product, application, or domain, as the AI Assistant currently cannot disambiguate questions.

| Ambiguous question | Clear question | Note |
| --- | --- | --- |
| "How do I create a filter? | How do I create a filter in Profile Query Language? | You must specify the feature that which you are filtering for because a variety of Experience Platform features support filtering. |
| "How do I get started? | How do I get started using destinations? | You must provide clarity on your goals and use case because overly broad concepts may result in generic or unnecessarily specific answers. |

{style="table-layout:auto"}

>[!ENDTABS] -->

#### 有限的閒聊

您可以與AI助理進行交談，但此容量目前有限。

#### 功能問題

AI Assistant可能會提供其功能的錯誤印象。 它可能會錯誤地回答以下型別的問題：

| 範例問題 | 注意 |
| --- | --- |
| 「您可以回答有關以下方面的問題 {ENTITY}？」 | 只要「AI助理」能夠在索引中找到參照指定實體的單一頁面，就會回答「是」。 |
| 「您知道嗎 **x** 語言？」 | AI助理目前僅支援英文，但因為基礎模型可以支援，所以可能會回答「是」。 |
| 「您可以……？」 | AI助理可能會回答「是」，即使它無法回答。 |

### 提示 {#tips}

以下章節概述使用AI助理時應考慮的一些提示和解決方法。

#### 問題可能會以錯誤的資訊來源來回答

在某些情況下，您關於使用情況資料的問題可能會根據檔案得出答案。 這是因為AI助理可能會將您的問題錯誤地路由到錯誤的資訊來源。 您可以透過以下方式防止此情況：

* 改寫您的問題以使用類似SQL的語言
* 明確呼叫要使用的資訊來源。

請閱讀下表的範例：

| 錯誤的問題 | 好問題 | 附註 |
| --- | --- | --- |
| 我最大的區段是什麼？ | 我最大的區段是什麼？ 使用資料。 | 明確告知AI助理，您希望答案以資料為基礎。 |
| 我最大的區段是什麼？ | 列出我最大的區段。 | 在某些情況下，「什麼……」問題可能會被誤認為檔案型問題。 使用類似「list」的命令是較強化的指標，表示您對上下文中的資料存有疑問。 |
| 我有多少資料集？ | 計算我的資料集。 | 原始問題適用於區段，但可能不適用於資料集。 |
