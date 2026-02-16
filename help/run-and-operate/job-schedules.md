---
description: 瞭解如何使用Adobe Experience Platform中的「工作排程」工具來檢查和疑難排解已排程的批次處理工作。
solution: Experience Platform
title: 檢查工作排程
type: Tutorial
hide: true
source-git-commit: 436ce6843e96b76dac0595ff5ab8a6067fb521ea
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 0%

---


# 檢查工作排程

>[!AVAILABILITY]
>
>[!UICONTROL Job schedules]目前是有限版本，僅適用於下列Real-Time CDP工作：
>
> * 批次資料湖擷取
> * 批次設定檔擷取
> * 批次區段
> * 批次目的地啟用。

[!UICONTROL Job Schedules]提供跨資料管道之所有已排程批次處理工作的統一檢視 — 從擷取到目的地啟用。 檢查執行狀態、識別排程衝突，並在設定問題影響您的業務運作之前診斷這些問題。

使用工作排程來調查失敗、最佳化工作時間，並瞭解資料湖擷取、設定檔處理、細分和目的地啟用之間的相依性。 如需解決常見組態問題的指南，請參閱有關[識別工作排程反模式](job-schedules-anti-patterns.md)的檔案。

## 先決條件 {#prerequisites}

若要存取[!UICONTROL Job Schedules]，您需要&#x200B;**[!UICONTROL View Job Schedules]**&#x200B;與&#x200B;**[!UICONTROL View Profile Management]** [存取控制許可權](/help/access-control/home.md#permissions)。

請聯絡您的系統管理員，以確保您擁有適當的許可權。

## 快速入門 {#getting-started}

在使用[!UICONTROL Job Schedules]之前，您應該熟悉下列Experience Platform概念：

* **[批次內嵌](../ingestion/batch-ingestion/overview.md)**：如何以排定的間隔將資料載入資料湖和設定檔存放區。
* **[分段](../segmentation/home.md)**：如何根據設定檔資料和區段定義來評估及更新對象。
* **[即時客戶設定檔](../profile/home.md)**：如何整合設定檔資料，以及使其可用於細分和啟用。
* **[目的地](../destinations/home.md)**：資料在下游系統和行銷平台上啟用的位置與方式。

瞭解這些元件有助於您解讀工作執行模式，並在問題發生時加以診斷。

## 瞭解工單排程介面 {#understanding-interface}

若要存取[!UICONTROL Job Schedules]：

1. 在Experience Platform UI中，從左側導覽選取&#x200B;**[!UICONTROL Run and Operate]**。
2. 選擇「**[!UICONTROL Job Schedules]**」。

[!UICONTROL Job Schedules]頁面提供您所有已排程批次處理工作的總覽。

![執行並操作左側導覽](assets/job-schedules/run-and-operate-left-nav.png)

### 摘要卡片 {#summary-cards}

在頁面頂端，您可以看到摘要卡片，這些卡片會提供批次處理作業的快速深入分析。

![工作排程摘要卡片顯示批次處理工作的深入分析](assets/job-schedules/job-schedules-cards.png)

* **Lake擷取執行**：已執行的資料湖擷取工作數目。
* **設定檔擷取執行**：已執行的設定檔擷取工作數目。
* **下一個分段**：下一個排定的分段工作執行時間。
* **下一個目的地啟用**：下一個排定的目的地啟用工作將於何時執行。

這些卡片可協助您瞭解資料管道中的活動和近期排程。 **Lake擷取執行**&#x200B;和&#x200B;**設定檔擷取執行**&#x200B;的值會根據選取的時間間隔（今天、昨天或過去7天）而變更；下次執行的卡片（**下一個分段**&#x200B;和&#x200B;**下一個目的地啟用**）不受時間選擇器的影響。

### 時段選擇器 {#time-period}

使用時段選擇器來選擇回顧多久來檢視排程的工作。

![工作排程中時段選擇器UI的動畫範例](assets/job-schedules/time-selector.gif)

* **今天**：檢視排定今天的工作（預設檢視）。
* **昨天**：檢視昨天執行的工作。
* **最近7天**：檢視過去一週的工作。

### 批次工作排程詳細資料 {#job-schedules-details}

主要檢視會顯示批次工作排程在一天中執行的時間。 您可以：

* **依資料集或實體檢視工作**：左欄顯示資料集或處理工作的名稱（例如內嵌資料集或分段工作）。
* **檢視工作計時**：時間表會顯示每個工作排定執行的時間，視覺指示器會標示排定的時間。
* **篩選工作**：使用篩選圖示來縮小要包含在報告中的資料集範圍。
* **瞭解工作型別**：底部的圖例以色彩標示，可協助您識別不同的工作型別：
   * **資料湖擷取** （綠色）：資料擷取至資料湖
   * **個人資料擷取** （粉紅色）：資料擷取至個人資料存放區
   * **分段** （淺藍色）：對象評估工作
   * **設定檔匯出** （藍色）：設定檔資料的匯出
   * **啟動** （深灰色）：目的地啟動工作
   * **進行中** （分段）：目前正在執行或佇列的工作

此時間表檢視可協助您識別排程衝突、瞭解作業之間的相依性，以及最佳化您的批次處理排程。

## 識別設定問題 {#identifying-issues}

當您檢閱工作排程時，可能會注意到指示組態問題的模式。 常見問題包括：

* 排程過於緊密的工作，造成資源爭用
* 在相同時間範圍內執行太多批次
* 每日批次工作過多的個別資料集
* 擷取工作已排程在分段執行前立即執行

這些模式可能會導致工作失敗、資料處理不完整和系統效能不佳。 若要瞭解如何識別及解決這些問題，請參閱有關[識別工作排程反模式](job-schedules-anti-patterns.md)的檔案。

當您需要調查特定資料集或工作執行時，您可以向下展開至詳細檢視，以檢視執行歷史記錄、錯誤訊息、效能測量結果和相依性。 如需有關檢視此詳細資料的資訊，請參閱有關[檢視工作詳細資料](job-schedules-details.md)的檔案。


## 後續步驟 {#next-steps}

瞭解工作排程後，您可能會想要探索下列相關主題：

* [檢視工作詳細資料](job-schedules-details.md)：瞭解如何深入瞭解個別資料集和工作執行，以進行詳細調查。
* [識別工作排程反模式](job-schedules-anti-patterns.md)：瞭解如何找出並解決影響管道效能的常見組態問題。
* [批次擷取](../ingestion/batch-ingestion/overview.md)：瞭解如何使用批次處理將資料擷取到Experience Platform。
* [分段](../segmentation/home.md)：瞭解如何依排程間隔評估和更新對象。
* [監視目的地的資料流](../dataflows/ui/monitor-destinations.md)：瞭解如何監視目的地啟用資料流。
* [排程對象匯出](../destinations/ui/activate-batch-profile-destinations.md)：瞭解如何設定排程的批次目的地啟用。
