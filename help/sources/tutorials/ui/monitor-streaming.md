---
keywords: Experience Platform；首頁；熱門主題；監視器帳戶；監視器資料流；資料流
description: Adobe Experience Platform中的來源連接器可讓您依排程內嵌外部來源資料。 本教學課程提供從來源工作區監控串流資料流的步驟。
solution: Experience Platform
title: 在UI中監視流源的資料流
topic-legacy: overview
type: Tutorial
source-git-commit: 58761cbe8465f4a00f07f33f751f481d34493cf7
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 1%

---


# 在UI中監視流源的資料流

本教學課程涵蓋使用[!UICONTROL Sources]工作區監控串流來源的資料流的步驟。

## 快速入門

本教學課程需要妥善了解下列Adobe Experience Platform元件：

* [資料流](../../../dataflows/home.md):資料流是跨平台移動資料的資料作業的表示。資料流可跨不同的服務進行配置，有助於將資料從源連接器移動到目標資料集、到[!DNL Identity]和[!DNL Profile]以及到[!DNL Destinations]。
   * [資料流運行](../../notifications.md):資料流運行是基於所選資料流的頻率配置的循環調度作業。
* [來源](../../home.md):Experience Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。
* [沙箱](../../../sandboxes/home.md):Experience Platform提供可將單一Platform執行個體分割成個別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

## 監視流源的資料流

在平台UI中，從左側導覽列選取&#x200B;**[!UICONTROL Sources]**&#x200B;以存取[!UICONTROL Sources]工作區。 [!UICONTROL 目錄]螢幕顯示了各種源，您可以用這些源建立帳戶。

要查看流源的現有資料流，請從頂部標頭中選擇&#x200B;**[!UICONTROL 資料流]**。

![目錄](../../images/tutorials/monitor-streaming/catalog.png)

「[!UICONTROL 資料流]」頁包含組織中所有現有資料流的清單，包括有關其源資料、帳戶名和資料流運行狀態的資訊。

選擇要查看的資料流的名稱。

![資料流](../../images/tutorials/monitor-streaming/dataflows.png)

下表包含有關資料流運行狀態的更多資訊：

| 狀態 | 說明 |
| ------ | ----------- |
| 已完成 | `Completed`狀態指示相應資料流運行的所有記錄都在1小時內處理。 `Completed`狀態仍可包含資料流運行中的錯誤。 |
| 正在處理 | `Processing`狀態表示資料流尚未處於活動狀態。 建立新資料流後，通常會立即出現此狀態。 |
| 錯誤 | `Error`狀態表示資料流的激活過程已中斷。 |

「[!UICONTROL 資料流活動]」頁顯示流資料流的特定資訊。 頂端橫幅包含所有串流資料流在所選日期範圍內執行時，擷取的記錄數和失敗的記錄數。

頁面的下半部顯示每個流程執行所接收、擷取和失敗的記錄數。 每個流運行都記錄在每小時窗口中。

![dataflow-activity](../../images/tutorials/monitor-streaming/dataflow-activity.png)

每個資料流運行都顯示以下詳細資訊：

* **[!UICONTROL 資料流運行開始]**:資料流運行的開始時間。
* **[!UICONTROL 處理時間]**:資料流處理所花費的時間。
* **[!UICONTROL 收到的記錄]**:資料流中從源連接器接收的記錄總數。
* **[!UICONTROL 擷取的記錄]**:擷取到的記錄總數 [!DNL Data Lake]。
* **[!UICONTROL 記錄失敗]**:因資料中的錯誤而未 [!DNL Data Lake] 擷取的記錄數。
* **[!UICONTROL 擷取率]**:擷取到的記錄成功率 [!DNL Data Lake]。當[!UICONTROL 部分擷取]啟用時，此量度即適用。
* **[!UICONTROL 狀態]**:表示資料流的狀態：完成  或處 [!UICONTROL 理]。 Completed表示在一小時內處理了相應資料流運行的所有記錄。 Processing表示資料流運行尚未完成。

依預設，顯示的資料包含過去七天的擷取率。 選擇「**[!UICONTROL 最近7天]**」以調整顯示的記錄時間範圍。

![變更時間](../../images/tutorials/monitor-streaming/change-time.png)

此時將出現一個日曆彈出窗口，為您提供可選的獲取時間範圍選項。 選擇&#x200B;**[!UICONTROL 最近30天]**，然後選擇&#x200B;**[!UICONTROL 應用]**。

![日曆](../../images/tutorials/monitor-streaming/calendar.png)

要查看特定資料流運行的詳細資訊（包括其錯誤），請從清單中選擇運行的開始時間。

![選擇失敗](../../images/tutorials/monitor-streaming/select-fail.png)

「[!UICONTROL 資料流運行概述]」頁包含有關資料流的其他資訊，如相應的資料流運行ID、目標資料集和IMS組織ID。

包含錯誤的流運行還包含[!UICONTROL 資料流運行錯誤]面板，該面板顯示導致運行失敗的特定錯誤以及失敗的記錄總數。

![失敗](../../images/tutorials/monitor-streaming/failure.png)

## 後續步驟

按照本教程，您已成功使用[!UICONTROL 源]工作區監視流資料流並識別導致任何失敗資料流的錯誤。 如需詳細資訊，請參閱下列檔案：

* [來源概觀](../../home.md)
* [資料流概述](../../../dataflows/home.md)