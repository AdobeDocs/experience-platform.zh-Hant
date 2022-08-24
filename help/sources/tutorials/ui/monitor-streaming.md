---
keywords: Experience Platform；首頁；熱門主題；監視帳戶；監視資料流；資料流
description: Adobe Experience Platform的源連接器提供了定期接收外部源資料的能力。 本教程提供了從源工作區監視流資料流的步驟。
title: 監視UI中流源的資料流
exl-id: b080e398-e71f-40bd-aea1-7ea3ce86b55d
source-git-commit: 647f2780798dcf55a68e156af3318924c352a442
workflow-type: tm+mt
source-wordcount: '1034'
ht-degree: 0%

---

# 監視UI中流源的資料流

本教程介紹使用 [!UICONTROL 源] 工作區。

## 快速入門

本教程需要對Adobe Experience Platform的以下部分進行有效的理解：

* [資料流](../../../dataflows/home.md):資料流是跨平台移動資料的資料作業的表示形式。 資料流是跨不同服務配置的，有助於將資料從源連接器移動到目標資料集 [!DNL Identity] 和 [!DNL Profile], [!DNL Destinations]。
   * [資料流運行](../../notifications.md):資料流運行是基於所選資料流的頻率配置的定期調度作業。
* [源](../../home.md):Experience Platform允許從各種源接收資料，同時讓您能夠使用平台服務構建、標籤和增強傳入資料。
* [沙箱](../../../sandboxes/home.md):Experience Platform提供虛擬沙箱，將單個平台實例分區為獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

## 監視流源的資料流

在平台UI中，選擇 **[!UICONTROL 源]** 從左導航欄訪問 [!UICONTROL 源] 工作區。 的 [!UICONTROL 目錄] 螢幕顯示可為其建立帳戶的各種源。

要查看流源的現有資料流，請選擇 **[!UICONTROL 資料流]** 的下界。

![目錄](../../images/tutorials/monitor-streaming/catalog.png)

的 [!UICONTROL 資料流] 頁包含組織中所有現有資料流的清單，包括有關其源資料、帳戶名和資料流運行狀態的資訊。

選擇要查看的資料流的名稱。

![資料流](../../images/tutorials/monitor-streaming/dataflows.png)

下表包含有關資料流運行狀態的詳細資訊：

| 狀態 | 說明 |
| ------ | ----------- |
| 已完成 | 的 `Completed` status表示在1小時內處理了相應資料流運行的所有記錄。 A `Completed` 狀態仍可能包含資料流運行中的錯誤。 |
| 成功 | 的 `Success` 狀態表示在一小時內處理了相應資料流運行的所有記錄，在資料流運行過程中沒有遇到錯誤。 |
| 正在處理 | 的 `Processing` 狀態表示資料流尚未處於活動狀態。 建立新資料流後，通常會立即遇到此狀態。 |
| 錯誤 | 的 `Error` 狀態表示資料流的激活過程已中斷。 |
| 無運行 | 的 `No runs` 狀態表示已建立資料流，但未啟動資料流運行。 |

的 [!UICONTROL 資料流活動] 頁顯示有關流資料流的特定資訊。 頂部標題包含所選日期範圍內所有流資料流運行所接收和失敗記錄的累計數量。

![資料流活動](../../images/tutorials/monitor-streaming/dataflow-activity.png)

預設情況下，顯示的資料包含過去七天的攝取率。 選擇 **[!UICONTROL 最後七天]** 來調整顯示的記錄的時間範圍。

此時將出現一個日曆彈出窗口，為您提供了替代接收時間框架的選項。 您可以配置資料流運行時間框架，以查看前七天或過去30天內的流運行。 或者，您可以配置互動式日曆以設定您選擇的自定義時間框架。 完成後，選擇 **[!UICONTROL 應用]**。

![日曆](../../images/tutorials/monitor-streaming/calendar.png)

頁面的下半部分顯示有關每個流運行接收、接收和失敗的記錄數的資訊。 每個流運行都記錄在一個小時窗口內。

![資料流運行](../../images/tutorials/monitor-streaming/dataflow-run.png)

### 資料流運行度量 {#dataflow-run-metrics}

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_received"
>title="收到的記錄"
>abstract="「已接收記錄」度量指示在資料流中接收的記錄總數。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_ingested"
>title="攝取的記錄"
>abstract="「Records Ingested」度量指示已接收到資料湖的記錄總數。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_failed"
>title="記錄失敗"
>abstract="「記錄失敗」度量指示由於資料中的錯誤而未被攝取到資料湖的記錄總數。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_sources_dataflow_records_warnings"
>title="帶警告的記錄"
>abstract="「帶警告的記錄」指示使用映射器轉換警告接收的記錄總數。 所有映射器轉換錯誤都會報告為警告，而部分攝取的行被視為成功且有警告"
>text="Learn more in documentation"

每個資料流運行都顯示以下詳細資訊：

* **[!UICONTROL 資料流運行啟動]**:資料流運行於的時間。
* **[!UICONTROL 處理時間]**:資料流處理所花費的時間。
* **[!UICONTROL 接收的記錄]**:從源連接器在資料流中接收的記錄總數。
* **[!UICONTROL 已接收的記錄]**:接收到的記錄總數 [!DNL Data Lake]。
* **[!UICONTROL 帶警告的記錄]**:已接收警告的記錄總數。 所有映射器轉換錯誤都會報告為警告，而部分攝取的行則標籤為 `success` 警告你。 **注釋**:只有流源才能支援插入帶有警告的記錄。
* **[!UICONTROL 記錄失敗]**:未攝取到的記錄數 [!DNL Data Lake] 因為資料中的錯誤。
* **[!UICONTROL 攝取率]**:接收到的記錄的成功率 [!DNL Data Lake]。 此度量適用於 [!UICONTROL 部分攝取] 的子菜單。
* **[!UICONTROL 狀態]**:表示資料流的狀態：或 [!UICONTROL 已完成] 或 [!UICONTROL 處理]。 [!UICONTROL 已完成] 表示在1小時內處理了相應資料流運行的所有記錄。 [!UICONTROL 處理] 表示資料流運行尚未完成。

的 [!UICONTROL 資料流運行概述] 頁包含有關資料流的其他資訊，如相應的資料流運行ID、目標資料集和組織ID。

包含錯誤的流運行還包含 [!UICONTROL 資料流運行錯誤] 面板，顯示導致運行失敗的特定錯誤以及失敗的記錄總數。

![資料流運行概述](../../images/tutorials/monitor-streaming/dataflow-run-overview.png)

### 查看帶警告的記錄 {#warnings}

[!UICONTROL 帶警告的記錄] 顯示在流運行期間發生的映射器轉換警告的清單。 部分攝取的行被視為成功，如果發現映射器轉換錯誤，將附加警告。

預設情況下，所有映射器轉換錯誤都被視為警告，除非它們是下列任何錯誤：

* 語法錯誤
* 對不存在的屬性的引用
* XDM資料類型不匹配

要查看錯誤診斷，請選擇 **[!UICONTROL 預覽錯誤診斷]**。

![帶警告的記錄](../../images/tutorials/monitor-streaming/records-with-warnings.png)

的 [!UICONTROL 錯誤診斷預覽] 窗口允許您預覽與資料流運行相關的最多100個錯誤和/或警告。 從此處，您還可以使用 [!DNL Data Access] API。

![診斷](../../images/tutorials/monitor-streaming/diagnostics.png)

## 後續步驟

按照本教程，您已成功使用 [!UICONTROL 源] 工作區，用於監視流資料流並識別導致任何失敗資料流的錯誤。 有關詳細資訊，請參閱以下文檔：

* [源概述](../../home.md)
* [資料流概述](../../../dataflows/home.md)
