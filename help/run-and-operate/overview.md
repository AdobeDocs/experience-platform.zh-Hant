---
title: 執行與操作概觀
description: 使用執行和操作工具檢查、疑難排解並最佳化Experience Platform實施。 瞭解已排程的批次啟用、識別設定問題，並改善系統可靠性。
hide: true
source-git-commit: 4733fae23c5029f4bc2c405376b1a52212dc0440
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 1%

---


# 執行與操作概觀

>[!AVAILABILITY]
>
>「執行與操作」功能目前以限量版提供。

當批次工作失敗或傳遞不完整的資料時，您需要快速瞭解導致問題的原因。 根本原因可能是資料可用性問題、計時錯誤、設定問題或系統容量限制。 如果沒有明確的可見度，您可能會花費數小時調查多個系統，才能找到答案。

透過[!UICONTROL Run and Operate]工具，您可以：

* **檢查您的資料作業**：取得所有工作流程中工作執行狀態與健全狀態的完整檢視。
* **加速疑難排解**：存取詳細的診斷資訊和執行歷程記錄，以快速找出根本原因，並減少解決問題的平均時間。
* **主動預防問題**：分析工作模式，在設定問題導致失敗之前偵測問題，並最佳化您的資料作業。

## 目標客群 {#target-audiences}

[!UICONTROL Run and Operate]工具的設計可在您的組織中提供多個對象：

* **資料與IT團隊**：系統管理員與資料工程師，負責維護可靠的資料管道，並疑難排解技術問題。
* **行銷作業**：檢查資料傳送至行銷平台並解決啟用問題的行銷技術人員。
* **實作人員**：驗證實作效率、可靠性及疑難排解技術問題的從業人員。

## 先決條件 {#prerequisites}

若要存取[執行與操作]工具，您需要&#x200B;**[!UICONTROL View Job Schedules]**&#x200B;與&#x200B;**[!UICONTROL View Profile Management]** [存取控制許可權](/help/access-control/home.md#permissions)。
[!UICONTROL Job Schedules]頁面提供您所有已排程批次處理工作的總覽。
請聯絡您的系統管理員，以確保您擁有適當的許可權。

## 快速入門 {#getting-started}

若要從Experience Platform UI存取「執行與操作」工具：

1. 登入您的Experience Platform帳戶，並從左側導覽中選取&#x200B;**[!UICONTROL Run and Operate]**。
2. 選取符合檢查或疑難排解需求的工具。

   >[!NOTE]
   >
   >目前唯一可用的功能是[工作排程](job-schedules.md)。

![Experience Platform UI顯示[執行並操作]左側導覽。](assets/overview/run-and-operate.png)

## 可用的工具 {#available-tools}

下列工具可協助您檢查並最佳化資料作業。

### 工作排程 {#job-schedules}

>[!IMPORTANT]
>
>[!UICONTROL Job schedules]目前僅適用於下列Real-Time CDP工作：
>
> * 批次資料湖擷取
> * 批次設定檔擷取
> * 批次區段
> * 批次目的地啟用。

透過[工作排程](job-schedules.md)，您可以檢查組織內每個沙箱的所有已排程批次作業，包括資料湖擷取、設定檔擷取、細分和目的地啟用。 檢視工作執行狀態、效能測量結果和執行歷史記錄，以識別模式並診斷影響可靠性的組態問題。

![Experience Platform UI顯示[工作排程]畫面。](assets/overview/job-schedules-interface.png)

「工單排程」提供三種調查層次：

* **[檢查工作排程](job-schedules.md)**：檢視時間軸中的所有資料集及其排程工作，以識別整個管道的模式和排程衝突。
* **[識別反模式](job-schedules-anti-patterns.md)**：瞭解如何發現並解決常見的組態問題，例如排程重疊、密集批次棧疊和過度批次處理，這些都會影響效能。
* **[檢視工作詳細資料](job-schedules-details.md)**：深入研究特定資料集和個別工作執行，以調查失敗、檢查時間並驗證已處理的記錄。

您也可以瞭解資料處理階段之間的相依性，協助您確保在Experience Platform工作流程中穩定傳輸資料。

## 後續步驟 {#next-steps}

現在您已瞭解[!UICONTROL Run and Operate]工具的用途和功能，請探索下列資源以深化您的知識：

* 瞭解[批次擷取](../ingestion/batch-ingestion/overview.md)，瞭解如何將資料擷取到Experience Platform
* 瞭解如何[檢查批次擷取和啟用的工作排程](job-schedules.md)
* 瞭解如何為批次目的地[設定排定的啟用](../destinations/ui/activate-batch-profile-destinations.md)
* 探索目的地[資料流監視](../dataflows/ui/monitor-destinations.md)

