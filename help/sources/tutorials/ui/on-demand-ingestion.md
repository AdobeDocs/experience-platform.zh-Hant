---
title: UI中來源資料流程的隨選擷取
description: 瞭解如何使用Experience Platform使用者介面，依需求為來源連線建立資料流程。
hide: true
hidefromtoc: true
source-git-commit: 812aa0bb0ec9199ef575ac972038115afc2fa647
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 0%

---

# UI中來源資料流程的隨選擷取

您可以使用Adobe Experience Platform使用者介面中的來源工作區，隨選擷取來觸發現有資料流的資料流執行反複專案。

本檔案提供如何依需求建立來源資料流的步驟，以及如何重試已處理或已失敗的資料流執行。

>[!BEGINSHADEBOX]

**什麼是資料流執行？**

流程執行代表資料流執行的例項。 例如，如果資料流排程在每小時的上午9:00、上午10:00及上午11:00執行，則您會有三個資料流執行個體。 流程執行是您的特定組織所專屬。

>[!ENDSHADEBOX]

## 快速入門

本檔案需要您實際瞭解下列Experience Platform元件：

* [來源](../../home.md)：Experience Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。
* [資料流](../../../dataflows/home.md)：資料流可呈現跨平台行動資料的資料作業。 資料流可跨不同服務進行設定，有助於將資料從來源聯結器移至目標資料集、身分服務和即時客戶個人檔案，以及移至目的地。
* [沙箱](../../../sandboxes/home.md)：Experience Platform提供可將單一Platform執行個體分割成個別虛擬環境的虛擬沙箱，以利開發及改進數位體驗應用程式。

## 隨選建立資料流 {#create-a-dataflow-on-demand}

導覽至 *[!UICONTROL 資料流]* 「來源」工作區的標籤。 從這裡，尋找您要隨選執行的資料流，然後選取省略符號(**`...`**)。

![來源工作區中的資料流清單。](../../images/tutorials/on-demand/select-dataflow.png)

接下來，選取 **[!UICONTROL 隨選執行]** 從出現的下拉式功能表中。

![已選取隨選執行選項的下拉式功能表。](../../images/tutorials/on-demand/run-on-demand.png)

設定隨選擷取的排程。 選取 **[!UICONTROL 擷取開始時間]**，則 **[!UICONTROL 日期範圍開始時間]**，以及 **[!UICONTROL 日期範圍結束時間]**.

| 正在排程設定 | 說明 |
| --- | --- |
| [!UICONTROL 擷取開始時間] | 排程的開始時間（以UTC表示），表示隨選資料流將開始的時間。 |
| [!UICONTROL 日期範圍開始時間] | 開始提取資料的日期和時間。 |
| [!UICONTROL 日期範圍結束時間] | 提取資料的結束日期和時間，直到為止。 |

選取 **[!UICONTROL 排程]** 並提供一些時間，讓您的隨選資料流觸發。

![隨選擷取的排程設定視窗。](../../images/tutorials/on-demand/configure-schedule.png)

選取您的資料流名稱以檢視您的資料流活動。 您將在這裡看到已處理的資料流執行清單。 選取資料流執行，然後選取 **[!UICONTROL 重試]** 從右側邊欄重新嘗試擷取所選的資料流執行反複專案。

![針對所選資料流執行的已處理流程清單。](../../images/tutorials/on-demand/processed.png)

選取 **[!UICONTROL 已排程]** 檢視排程供未來內嵌使用的資料流執行清單。

![針對所選資料流執行的排程流程清單。](../../images/tutorials/on-demand/scheduled.png)

## 後續步驟

閱讀本檔案後，您已瞭解如何針對現有來源資料流建立依需求執行的流程。 如需有關來源的詳細資訊，請閱讀 [來源概觀](../../home.md)