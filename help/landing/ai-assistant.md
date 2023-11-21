---
title: Adobe Experience Platform助理
description: 瞭解如何使用助理來導覽並瞭解Experience Platform和Real-time Customer Data Platform概念，以及有關您物件的使用資訊。
badge: Alpha
hide: true
hidefromtoc: true
exl-id: 8be1c222-3ccd-4a41-978e-33ac9b730f8c
source-git-commit: a0395c4d3514693d3200571496eff47768da52ba
workflow-type: tm+mt
source-wordcount: '2183'
ht-degree: 0%

---

# Adobe Experience Platform助理

>[!NOTE]
>
>Adobe Experience Platform的助理目前Alpha。 功能和檔案可能會有所變更。

Adobe Experience Platform的助理是UI功能，可用於導覽並瞭解Experience Platform和Real-time Customer Data Platform概念，以及物件的使用資訊。

您可以查詢「輔助程式」以取得下列資訊：

* 有關如何執行與資料和受眾相關之工作的指南。
* 貴組織中現有資料物件的狀態和量度。
* 使用案例範例和細微差別，以便更清楚瞭解您的資料物件，包括屬性、資料集、目的地、結構描述、區段和來源。

本檔案提供存取和使用助理的相關資訊，讓您瞭解如何提出問題並獲得Experience Platform和Real-Time CDP概念的解答。

>[!BEGINSHADEBOX]

**助理如何運作？**

小幫手會查詢資料庫，然後將資料庫中的資料轉譯成人類看得懂的答案，以回應您提交的問題。

這種基礎資料的內部表示法也稱為知識圖表，是一張包含特定答案的概念、資料和中繼資料的完整網路。

「知識圖形」由每次提交查詢時所參考的子圖形組成：

* 客戶使用資料。
* 各種中繼存放區的客戶使用資料。
* Experience League檔案。

在查詢「助理員」之前，需要考慮兩種型別的問題：

* **概念問題**：概念問題與資料或受眾相關的Adobe概念有關。 概念問題的一些範例包括：
   * 批次和串流區段之間有何差異？
   * 是否有產業資料模型，以及我該如何使用？
   * Real-Time CDP的最佳用途為何？
* **使用問題**：使用問題與組織內的資料物件有關。 使用問題的一些範例包括：
   * 我有多少資料集？
   * 有多少結構描述屬性從未使用過？
   * 已啟用哪些區段？

>[!ENDSHADEBOX]

## 在UI中進行Experience Platform的存取助理

您可以從Experience PlatformUI的標題導覽存取「小幫手」。

選取 **[!UICONTROL 助理圖示]** 從標題到啟動助理面板。

![已選取「助理員」圖示的Experience Platform UI首頁。](./images/ai-assistant/ai-assistant.png)

<!-- +++Use immersive mode

To use [!DNL Immersive mode] select the focus icon in the header navigation of the Assistant.

![select-immersive](./images/ai-assistant/select-immersive.png)

A dedicated pop-up interface for Assistant appears at the center of your screen.

![immersive-mode](./images/ai-assistant/immersive-mode.png)

+++

From here, you can input your question in the text box and query Assistant for concepts regarding data or audiences. You can also ask questions about your data objects to better understand how you can use them for your respective use case.  -->

### 使用案例範例：使用「小幫手」加速您的綱要建立程式 {#example-use-case}

>[!NOTE]
>
>以下範例工作流程使用ExperienceEvent結構描述建立程式來說明在使用Experience PlatformUI時如何使用「助理」。

考慮您正在建立的使用案例 **裝置交易事件結構描述**. 在ExperienceEvent結構描述建立程式期間，您會 `eventType` 欄位。 此時，您可以離開工作流程，並參閱 [結構描述組合的基本面](../xdm/schema/composition.md)，或者您可以使用助理來立即擷取問題的答案。

若要開始，請在提供的文字方塊中輸入您的問題。 在下列範例中，小幫手會詢問問題： &quot;**什麼是ExperienceEvent結構描述中的eventType欄位？**&quot;

![用於Experience Platform的助理已準備好進行查詢，並附帶下列問題：「什麼是ExperienceEvent綱要中的eventType欄位？](./images/ai-assistant/question.png)

然後小幫手查詢其知識庫並計算答案。 幾分鐘後，「小幫手」會傳回答案和相關建議，供您作為後續提示使用。

給定的答案會提供指向任何參照實體的超連結。 在以下範例中，選取 **[!UICONTROL 方案]** 若要檢視參照的結構描述清單，或 **[!UICONTROL 區段]** 以檢視參照區段的清單。

![有上一個查詢答案的Experience Platform助理。](./images/ai-assistant/answer.png)

助理可以檢視其來源，讓您驗證答案。 說明檔案的連結可用於概念問題，而資料使用問題則可使用示範如何計算答案的SQL查詢來驗證。

![傳回答案後助理提供的選項。](./images/ai-assistant/options.png)

### 後續追蹤問題 {#follow-up-question}

+++選取以檢視後續問題的範例

您可以透過提出後續問題，進一步瞭解特定主題的更多資訊。 在下一個範例中，系統會詢問助理員如何在細分中使用eventType。

![「助理」上顯示的後續問題與答案，以進行Experience Platform。](./images/ai-assistant/follow-up-question.png)

+++

### 資料使用問題 {#data-usage-question}

+++選取此選項可檢視資料使用問題的範例

您也可以向「小幫手」詢問有關資料使用的問題。 查詢資料使用情況時，您必須處於作用中沙箱中，小幫手才能回答您的查詢。

對於涉及資料使用資訊的回應，「助理員」會提供相關實體的連結。 此外，「小幫手」會提供您如何計算其答案的說明。

![一個資料使用問題，詢問使用者擁有多少區段。](./images/ai-assistant/data-usage-question.png)

+++

### 多圈 {#multi-turn}

+++選取以檢視多圈範例

您可以使用「小幫手」的多圈功能，在體驗期間進行更自然的交談。 助理可以回答後續的問題，因為上下文可以從先前的互動中推斷。

在下列範例中，系統會要求「助理」列出組織中現有的區段，作為先前有關區段總數的查詢的後續作業。

![](./images/ai-assistant/multi-turn-one.png)

接著，助理會收到另一個後續追蹤要求。 此時，「助理員」會列出依其各自大小排序的現有區段，以進行回應。

![](./images/ai-assistant/multi-turn-two.png)

+++

### 使用自動完成 {#use-auto-complete}

+++選取以檢視自動完成的範例

您可以使用自動完成函式來接收沙箱中存在之資料物件的清單。 自動完成建議適用於下列網域：區段、結構描述、資料集、來源和目的地。

若要使用自動完成，請輸入加號(**`+`**)作為問題的一部分。 或者，您也可以選取加號(**`+`**)。 接著會出現一個視窗，內含存在於沙箱中的建議資料物件清單。

![](./images/ai-assistant/autocomplete-options.png)

接著，選取您要查詢的資料物件以完成問題，然後提交問題。

![](./images/ai-assistant/autocomplete-question.png)

+++

## 範圍 {#scope}

助理可以回答有關Real-Time CDP和Experience Platform概念的問題，以及您的使用者帳戶特有的資料使用問題。 助理也可以根據您所在的UI頁面推斷內容。 它可以識別：

* 您正在使用的使用者帳戶。
* 您所屬的組織。
* 您在熒幕上檢視的頁面。
* 您在畫面上檢視的資源（包括型別和ID）。
* 假設您正在處理特定Experience Platform或Real-Time CDP工作流程，助理可以推斷您的意圖。

### 文件 {#documentation}

目前，檔案索引涵蓋Adobe Experience Platform (Real-Time CDP和受眾)。 索引會定期更新。

說明檔案擷取模型已針對Experience Platform(Real-Time CDP和受眾)接受訓練。 Adobe Experience Platform範圍以外的問題，例如，關於其他Adobe產品(如Adobe Target)和Creative Cloud套裝的問題，無法回答。

### 資料使用情況 {#data-usage}

您也可以向「小幫手」詢問下列網域中資料使用的相關問題：

* 屬性
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

## 驗證回應 {#verify-the-response}

您可以使用多種不同方式來驗證「小幫手」傳回的回應。

### 檔案引文 {#citations}

每次回應時，「小幫手」都會提供引文，供您參考以取得驗證或詳細資訊。

選取 **[!UICONTROL 顯示來源]** 取得「助理」參考以計算其回應的檔案連結清單。 當您選取參照檔案的連結時，會前往該特定頁面的相關區段，並反白顯示特定資訊。

![「助理員」中顯示的來源連結。](./images/ai-assistant/show-sources.png)

## 提供意見反應 {#feedback}

>[!BEGINSHADEBOX]

**您的意見回饋已要求**

在此Alpha階段，請您針對從助理收到的回應提供意見反應。 所有回應和提交的意見都會經過稽核，以繼續改善「助理員」的使用體驗。

若要提供意見回饋，請在收到「小幫手」的回應後，選取向上或向下拇指，然後在提供的文字方塊中輸入您的意見回饋。 接下來，選取 **[!UICONTROL 提交意見]** 以提交。

>[!ENDSHADEBOX]

+++提供意見反應

>[!BEGINTABS]

>[!TAB 豎起大拇指]

選取向上拇指圖示，對使用助理時表現良好的專案提供意見回饋。

![正面意見回饋視窗。](./images/ai-assistant/thumbs-up.png)

>[!TAB 向下拇指]

選取按住拇指的圖示，根據您使用助理的經驗，提供可以改善的意見反應。 在此步驟中，您也可以提供關於體驗的特定註解。 評論中提供的意見回饋會每天稽核。

![負面意見回饋視窗。](./images/ai-assistant/thumbs-down.png)

>[!TAB 標幟]

選取旗標圖示，即可提供進一步的使用助理員體驗報告。

![報表結果視窗。](./images/ai-assistant/flag.png)

>[!ENDTABS]

+++

## 其他資訊 {#additional-information}

請參閱本節以取得有關「Experience Platform助理」的其他資訊。

### 警告和限制 {#caveats-and-limitations}

下節概述使用「小幫手」時應考量的目前注意事項和限制。
<!-- 
#### Conversational experience

You must consider several nuances regarding the conversational experience when querying the Assistant.

>[!NOTE]
>
>These limitations are temporary and are being improved upon throughout the course of the alpha.

>[!BEGINTABS]

>[!TAB Unable to infer context from prior discussion]

The Assistant currently cannot reference prior discussions as context for a given question. See the table below for examples:

| Ambiguous question | Clear question | Note |
| --- | --- | --- |
| <ul><li>First question: "What is a segment?"</li><li>Follow up question: "Are there different types of them?"</li></ul>| <ul><li>First question: "What is a segment?"</li><li>Follow up question: "Are there different types of **segments**?"</li></ul> | The Assistant cannot infer what "them" means. |
| <ul><li>First question: "What is a segment?"</li><li>Follow up question: "Can you elaborate more?"</li></ul> | <ul><li>First question: "What is a segment?"</li><li>Follow up question: "Explain what a segment is in depth"</li></ul> | The Assistant cannot intelligently reference documentation based on "more". |
| <ul><li>First question: "What is a segment?"</li><li>Follow up question: "Can you give me an example of one?"</li></ul> | <ul><li>First question: "What is a segment?"</li><li>Follow up question: "Can you give me an example of a segment?"</li></ul> | The Assistant cannot infer what you want an example of.|
| <ul><li>First question: "What is a batch segment?"</li><li>Follow up question: "How does it compare to a streaming segment?"</li></ul> | <ul><li>First question: "What is a batch segment?"</li><li>Follow up question: "Can you compare a streaming segment to a batch segment?"</li></ul> | The Assistant cannot infer what "it" is referring to and thus cannot compare the streaming segment. |
| <ul><li>First question: "How many segments do I have?"</li><li>Follow up question: "How many of them use Facebook as a destination?"</li></ul> | <ul><li>First question: "How many segments do I have?"</li><li>Follow up question: "How many of the segments that I have are using Facebook as a destination?"</li></ul> | The Assistant is cannot infer what "them" is referring to. |

{style="table-layout:auto"}

>[!TAB Unable to infer context from a page]

When asking the Assistant about a particular element of the Experience Platform UI page that you are on, you must clearly define the specific element within your question. 

| Ambiguous question | Clear question | Note |
| --- | --- | --- |
| "What does this do?" | "What does {PAGE_NAME} do? | The Assistant cannot infer what "this" is referring to. You must provide the specific page element that you are querying about. |
| "Why won't it save?" | "Why can't I save a new sandbox called {NAME}?" | The Assistant cannot infer what "it" is referring to and cannot know that you are having issues with an entity. |

{style="table-layout:auto"}

Furthermore, the Assistant can only answer questions regarding error messages, given that the error is documented in Experience League.

>[!TAB Ambiguity]

You must phrase your questions clearly and scope them within a product, application, or domain, as the Assistant currently cannot disambiguate questions.

| Ambiguous question | Clear question | Note |
| --- | --- | --- |
| "How do I create a filter? | How do I create a filter in Profile Query Language? | You must specify the feature that which you are filtering for because a variety of Experience Platform features support filtering. |
| "How do I get started? | How do I get started using destinations? | You must provide clarity on your goals and use case because overly broad concepts may result in generic or unnecessarily specific answers. |

{style="table-layout:auto"}

>[!ENDTABS] -->

#### 有限的閒聊

您可以與「小幫手」進行交談，但目前的容量有限。

#### 功能問題

助理員可能會對其功能產生不準確的印象。 它可能會錯誤地回答以下型別的問題：

| 範例問題 | 注意 |
| --- | --- |
| 「您可以回答有關以下方面的問題 {ENTITY}？」 | 只要「助理員」能夠在索引中找到參照指定實體的單一頁面，就會回答「是」。 |
| 「您知道嗎 **x** 語言？」 | 助理目前僅支援英文，但因為基礎模型能夠支援它，所以可能會回答「是」。 |
| 「您可以……？」 | 助理可能會回答「是」，即使它無法回答。 |

### 提示 {#tips}

以下章節概述使用「小幫手」時應考慮的一些秘訣和解決方法。

#### 問題可能會以錯誤的資訊來源來回答

在某些情況下，您關於使用情況資料的問題可能會根據檔案得出答案。 這是因為「小幫手」可能會將您的問題錯誤地路由到錯誤的資訊來源。 您可以透過以下方式防止此情況：

* 改寫您的問題以使用類似SQL的語言
* 明確呼叫要使用的資訊來源。

請閱讀下表的範例：

| 錯誤的問題 | 好問題 | 附註 |
| --- | --- | --- |
| 我最大的區段是什麼？ | 我最大的區段是什麼？ 使用資料。 | 明確告知小幫手，您希望答案以資料為基礎。 |
| 我最大的區段是什麼？ | 列出我最大的區段。 | 在某些情況下，「什麼……」問題可能會被誤認為檔案型問題。 使用類似「list」的命令是較強化的指標，表示您對上下文中的資料存有疑問。 |
| 我有多少資料集？ | 計算我的資料集。 | 原始問題適用於區段，但可能不適用於資料集。 |
