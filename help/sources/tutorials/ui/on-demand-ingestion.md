---
title: UI中來源資料流程的隨選擷取
description: 瞭解如何使用Experience Platform使用者介面，依需求為您的來源連線建立資料流程。
exl-id: e5a70044-2484-416a-8098-48e6d99c2d98
source-git-commit: fabacf273fb5774ddcee42d0cdcf12281eb0216b
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 0%

---

# UI中來源資料流程的隨選擷取

您可以使用Adobe Experience Platform使用者介面中的來源工作區，隨選擷取來觸發現有資料流的資料流執行反複專案。

本檔案提供如何依需求建立來源資料流的步驟，以及如何重試已處理或已失敗的資料流執行。

>[!BEGINSHADEBOX]

**什麼是資料流執行？**

流程執行代表資料流執行的例項。 例如，如果資料流排程在早上9:00、10:00、11:00 AM每小時執行，則您會有三個資料流執行個體。 流程執行是您的特定組織所專屬。

>[!ENDSHADEBOX]

## 快速入門

>[!NOTE]
>
>為了建立資料流執行，您必須先擁有排程為單次擷取的資料流的資料流ID。

參閱本檔案前，請先實際瞭解下列Experience Platform元件：

* [來源](../../home.md)： Experience Platform允許從各種來源擷取資料，同時讓您能夠使用Experience Platform服務來建構、加標籤以及增強傳入的資料。
* [資料流](../../../dataflows/home.md)：資料流可呈現跨Experience Platform行動資料的資料作業。 資料流可跨不同服務進行設定，有助於將資料從來源聯結器移至目標資料集、身分服務和即時客戶個人檔案，以及移至目的地。
* [沙箱](../../../sandboxes/home.md)： Experience Platform提供的虛擬沙箱可將單一Experience Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

## 隨選建立資料流 {#create-a-dataflow-on-demand}

導覽至來源工作區的&#x200B;*[!UICONTROL 資料流程]*&#x200B;標籤。 從這裡，尋找您要隨選執行的資料流，然後選取資料流名稱旁邊的省略符號(**`...`**)。

![來源工作區中的資料流清單。](../../images/tutorials/on-demand/select-dataflow.png)

接著，從出現的下拉式功能表中選取&#x200B;**[!UICONTROL 隨選執行]**。

![已選取[隨選執行]選項的下拉式功能表。](../../images/tutorials/on-demand/run-on-demand.png)

設定隨選擷取的排程。 選取&#x200B;**[!UICONTROL 擷取開始時間]**、**[!UICONTROL 日期範圍開始時間]**&#x200B;和&#x200B;**[!UICONTROL 日期範圍結束時間]**。

| 正在排程設定 | 說明 |
| --- | --- |
| [!UICONTROL 擷取開始時間] | 隨選資料流執行的排定時間。 |
| [!UICONTROL 日期範圍開始時間] | 將會從中擷取資料的最早日期和時間。 |
| [!UICONTROL 日期範圍結束時間] | 擷取資料的日期和時間，截止日期為。 |

選取「**[!UICONTROL 排程]**」，並等待一段時間讓您的隨選資料流觸發。

![隨選擷取的排程設定視窗。](../../images/tutorials/on-demand/configure-schedule.png)

選取您的資料流名稱以檢視您的資料流活動。 您將在這裡看到已處理的資料流執行清單。 您可以重新執行資料流執行的個別反複專案，無論它們失敗還是成功。 對於失敗的執行反複專案，您可以在診斷並解決建立過程中可能遇到的任何錯誤之後，使用&#x200B;**[!UICONTROL 重試]**&#x200B;來再次啟動執行。

>[!TIP]
>
>重試資料流執行只會處理時間戳記在原始執行範圍內的檔案。

![所選資料流的已處理資料流執行清單。](../../images/tutorials/on-demand/processed.png)

選取&#x200B;**[!UICONTROL 已排程]**，以檢視排程供未來內嵌的資料流執行清單。

![所選資料流的排程資料流執行清單。](../../images/tutorials/on-demand/scheduled.png)

## 後續步驟

閱讀本檔案後，您已瞭解如何針對現有來源資料流建立依需求執行的流程。 如需來源的詳細資訊，請閱讀[來源概觀](../../home.md)
