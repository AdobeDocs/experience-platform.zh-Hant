---
keywords: Experience Platform；首頁；熱門主題；監視器帳戶；監視器資料流；資料流
description: Adobe Experience Platform中的Source聯結器可讓您依排程擷取外部來源資料。 本教學課程提供從來源工作區監控串流資料流的步驟。
title: 在UI中監視串流來源的資料流
exl-id: b080e398-e71f-40bd-aea1-7ea3ce86b55d
source-git-commit: 647f2780798dcf55a68e156af3318924c352a442
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 10%

---

# 在UI中監視串流來源的資料流

本教學課程涵蓋使用[!UICONTROL 來源]工作區監控串流來源資料流的步驟。

## 快速入門

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

* [資料流](../../../dataflows/home.md)：資料流可呈現跨平台行動資料的資料作業。 資料流是跨不同服務設定的，有助於將資料從來源聯結器移至目標資料集、移至[!DNL Identity]和[!DNL Profile]以及移至[!DNL Destinations]。
   * [資料流執行](../../notifications.md)：資料流執行是根據所選資料流的頻率設定所排程的週期性工作。
* [來源](../../home.md)：Experience Platform允許從各種來源擷取資料，同時讓您能夠使用Platform服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../sandboxes/home.md)：Experience Platform提供的虛擬沙箱可將單一Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

## 監控串流來源的資料流

在Platform UI中，從左側導覽列選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取[!UICONTROL 來源]工作區。 [!UICONTROL 目錄]畫面會顯示您可以建立帳戶的各種來源。

若要檢視串流來源的現有資料流，請從頂端標題選取&#x200B;**[!UICONTROL 資料流]**。

![目錄](../../images/tutorials/monitor-streaming/catalog.png)

[!UICONTROL 資料流]頁面包含貴組織中所有現有資料流的清單，包括關於其來源資料、帳戶名稱和資料流執行狀態的資訊。

選取您要檢視的資料流名稱。

![資料流](../../images/tutorials/monitor-streaming/dataflows.png)

下表包含資料流執行狀態的詳細資訊：

| 狀態 | 說明 |
| ------ | ----------- |
| 已完成 | `Completed`狀態表示對應資料流執行的所有記錄都在一小時期間內處理。 `Completed`狀態在資料流執行中仍可能包含錯誤。 |
| 成功 | `Success`狀態表示對應資料流執行的所有記錄都在一小時期間內處理，且在資料流執行期間沒有發生錯誤。 |
| 正在處理 | `Processing`狀態表示資料流尚未啟用。 此狀態通常會在建立新資料流後立即發生。 |
| 錯誤 | `Error`狀態表示資料流程的啟用程式已中斷。 |
| 沒有回合 | `No runs`狀態表示已建立資料流，但未啟動任何資料流執行。 |

[!UICONTROL 資料流活動]頁面會顯示串流資料流的特定資訊。 頂端橫幅包含您所選取日期範圍內所有串流資料流執行的累計擷取記錄和失敗記錄數。

![資料流活動](../../images/tutorials/monitor-streaming/dataflow-activity.png)

依預設，顯示的資料包含過去七天的擷取率。 選取「**[!UICONTROL 最近7天]**」以調整記錄的時間範圍。

此時會出現一個日曆快顯視窗，為您提供替代擷取時間範圍的選項。 您可以設定資料流執行時間範圍，以檢視過去七天或過去30天的資料流執行。 或者，您可以設定互動式行事曆，以設定自訂的時間範圍。 完成後，選取&#x200B;**[!UICONTROL 套用]**。

![行事曆](../../images/tutorials/monitor-streaming/calendar.png)

頁面下半部會顯示每個資料流執行中接收、擷取及失敗的記錄數相關資訊。 每個資料流執行都會記錄在一個每小時的時段內。

![資料流 — 執行](../../images/tutorials/monitor-streaming/dataflow-run.png)

### 資料流執行指標 {#dataflow-run-metrics}

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_received"
>title="已收到的記錄"
>abstract="已收到的記錄量度會顯示資料流中收到的記錄總計數。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_ingested"
>title="已擷取的記錄"
>abstract="已擷取的記錄量度會顯示擷取至資料湖的記錄總計數。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_failed"
>title="失敗的記錄"
>abstract="失敗的記錄量度會顯示由於資料錯誤而未擷取至資料湖的記錄總計數。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_warnings"
>title="包含警告的記錄"
>abstract="包含警告的記錄會顯示包含對應工具轉換警告的記錄總計數。所有的對應工具轉換錯誤都會通報為警告，部分擷取的列則會被視為包含警告的成功"
>text="Learn more in documentation"

每個個別資料流執行會顯示下列詳細資訊：

* **[!UICONTROL 資料流執行開始]**：資料流執行開始的時間。
* **[!UICONTROL 處理時間]**：資料流處理所花的時間。
* **[!UICONTROL 已接收的記錄數]**：從來源聯結器在資料流中接收的記錄總數。
* **[!UICONTROL 個擷取的記錄]**：擷取到[!DNL Data Lake]的記錄總數。
* **[!UICONTROL 含有警告的記錄]**：已擷取的含有警告的記錄總數。 所有對應程式轉換錯誤都會回報為警告，而部分擷取的列會標示為`success`並加上警告。 **注意**：只有串流來源才支援擷取含有警告的記錄。
* **[!UICONTROL 記錄失敗]**：由於資料發生錯誤，未擷取到[!DNL Data Lake]的記錄數。
* **[!UICONTROL 擷取率]**：擷取到[!DNL Data Lake]的記錄成功率。 此量度適用於[!UICONTROL 部分擷取]啟用的情況。
* **[!UICONTROL 狀態]**：代表資料流所處的狀態： [!UICONTROL 已完成]或[!UICONTROL 正在處理]。 [!UICONTROL 已完成]表示對應資料流執行的所有記錄都在一小時內處理。 [!UICONTROL 正在處理]表示資料流執行尚未完成。

[!UICONTROL 資料流執行總覽]頁面包含您資料流的其他資訊，例如其對應的資料流執行ID、目標資料集和組織ID。

含有錯誤的資料流執行也包含[!UICONTROL 資料流執行錯誤]面板，該面板會顯示導致執行失敗的特定錯誤，以及失敗的記錄總數。

![資料流執行總覽](../../images/tutorials/monitor-streaming/dataflow-run-overview.png)

### 檢視含有警告的記錄 {#warnings}

[!UICONTROL 含有警告的記錄]會顯示資料流執行期間發生的對應程式轉換警告清單。 部分擷取的列會被視為成功，如果發現任何對應程式轉換錯誤，則會附加警告。

依預設，所有對應程式轉換錯誤都會被視為警告，除非它們屬於下列任一情況：

* 語法錯誤
* 對不存在屬性的參照
* XDM資料型別不相符

若要檢視錯誤診斷，請選取&#x200B;**[!UICONTROL 預覽錯誤診斷]**。

![個有警告的記錄](../../images/tutorials/monitor-streaming/records-with-warnings.png)

[!UICONTROL 錯誤診斷預覽]視窗可讓您預覽與資料流執行相關的最多100個錯誤和/或警告。 您也可以在此處使用[!DNL Data Access] API下載擷取失敗資訊清單，以取得詳細資訊。

![診斷](../../images/tutorials/monitor-streaming/diagnostics.png)

## 後續步驟

依照此教學課程，您已成功使用[!UICONTROL 來源]工作區來監視您的串流資料流，並識別導致任何失敗資料流的錯誤。 如需詳細資訊，請參閱下列檔案：

* [來源概觀](../../home.md)
* [資料流概觀](../../../dataflows/home.md)
