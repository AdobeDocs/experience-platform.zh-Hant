---
keywords: Experience Platform；首頁；熱門主題；監視器設定檔；監視器資料流程；資料流程；設定檔；即時客戶設定檔；
description: 即時客戶設定檔可讓您透過合併來自多個管道（包括線上、離線、CRM和協力廠商）的資料，檢視每個個別客戶的整體檢視。 本教學課程提供如何使用Experience Platform使用者介面監控設定檔資料流的指示。
title: 在UI中監視設定檔的資料流
type: Tutorial
exl-id: 00b624b2-f6d1-4ef2-abf2-52cede89b684
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1077'
ht-degree: 7%

---

# 在UI中監視設定檔的資料流

即時客戶設定檔可讓您透過合併來自多個管道（包括線上、離線、CRM和協力廠商）的資料，檢視每個個別客戶的整體檢視。 設定檔可讓您將客戶資料合併成統一的檢視畫面，針對每個客戶互動提供可採取行動且附有時間戳記的說明。

監控儀表板可讓您以視覺化方式呈現設定檔中的資料活動，包括資料設定檔的狀態。 本教學課程提供如何使用Experience Platform使用者介面監控資料設定檔的監控儀表板，讓您追蹤設定檔處理狀態的說明。

## 快速入門 {#getting-started}

本指南需要您深入了解下列 Adobe Experience Platform 元件：

- [資料流](../home.md)：資料流可呈現跨Experience Platform行動資料的資料作業。 資料流是跨不同服務設定的，有助於將資料從來源聯結器移至目標資料集、移至[!DNL Identity]和[!DNL Profile]以及移至[!DNL Destinations]。
   - [資料流執行](../../sources/notifications.md)：資料流執行是根據所選資料流的頻率設定所排程的週期性工作。
- [即時客戶個人檔案](../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時客戶個人檔案。
- [沙箱](../../sandboxes/home.md)： [!DNL Experience Platform]提供可將單一[!DNL Experience Platform]執行個體分割成個別虛擬環境的虛擬沙箱，以利開發及改進數位體驗應用程式。

## 監視設定檔儀表板 {#profile-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_profile_processing"
>title="設定檔處理"
>abstract="設定檔處理視圖會包含有關擷取至設定檔服務的記錄的資訊，包括建立的設定檔片段數、更新的設定檔片段數以及設定檔片段總數。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_profile"
>title="資料流執行詳細資訊"
>abstract="資料流執行詳細資訊頁面會顯示有關設定檔資料流執行的詳細資訊，包括其組織 ID 和資料流執行 ID。"

若要存取&#x200B;**[!UICONTROL 設定檔]**&#x200B;儀表板，請在左側導覽中選取&#x200B;**[!UICONTROL 監視]**。 在&#x200B;**[!UICONTROL 監視]**&#x200B;頁面上，選取&#x200B;**[!UICONTROL 設定檔]**&#x200B;卡片。

![設定檔卡。 顯示關於已接收記錄數、已建立和已更新設定檔片段數以及成功率的資訊。](../assets/ui/monitor-profiles/focus-card.png)

在主要&#x200B;**[!UICONTROL 設定檔]**&#x200B;儀表板上，**[!UICONTROL 設定檔]**&#x200B;卡片會顯示所接收記錄總數、已建立和已更新設定檔片段數目，以及建立和已更新設定檔片段的成功率等相關資訊。

儀表板本身包含有關設定檔處理的量度。 預設情況下，儀表板將顯示過去24小時內您組織來源的設定檔處理細節。

![設定檔儀表板。 顯示每個來源接收之設定檔記錄數目的相關資訊。](../assets/ui/monitor-profiles/sources.png)

[!UICONTROL 設定檔處理]頁面包含擷取至[!DNL Profile]的記錄資訊，包括已建立的設定檔片段數、已更新的設定檔片段數，以及設定檔片段總數。

下列量度適用於此儀表板檢視：

| 量度 | 說明 |
| -------| ----------- |
| **[!UICONTROL Source名稱]** | 來源的名稱。 |
| 已接收&#x200B;**[!UICONTROL 筆記錄]** | 從資料湖接收的記錄數。 |
| **[!UICONTROL 個記錄失敗]** | 已擷取但由於錯誤而未擷取到[!DNL Profile]中的記錄數。 |
| **[!UICONTROL 已建立的設定檔片段]** | 已新增的淨新[!DNL Profile]片段數目。 |
| **[!UICONTROL 已更新設定檔片段]** | 已更新現有[!DNL Profile]片段的數量。 |
| **[!UICONTROL 設定檔片段總數]** | 寫入[!DNL Profile]的記錄總數，包括所有已更新的現有[!DNL Profile]片段以及已建立的新[!DNL Profile]片段。 |
| **[!UICONTROL 失敗的資料流總數]** | 失敗的資料流執行次數。 |

您可以選取來源名稱旁的篩選圖示![篩選圖示](/help/images/icons/filter.png)，以檢視該所選來源資料流程的設定檔處理資訊。

![篩選圖示會醒目提示。 選取此圖示可讓您檢視所選來源的資料流。](../assets/ui/monitor-profiles/sources-filter.png)

或者，您可以在切換時選取「**[!UICONTROL 資料流]**」，以檢視貴組織過去24小時資料流的設定檔處理詳細資料。

![設定檔儀表板。 顯示有關每個資料流接收的設定檔記錄數目的資訊。](../assets/ui/monitor-profiles/dataflows.png)

下列量度適用於此儀表板檢視：

| 量度 | 說明 |
| -------| ----------- |
| **[!UICONTROL 資料流]** | 資料流的名稱。 |
| **[!UICONTROL 資料集]** | 資料流所插入的資料集名稱。 |
| **[!UICONTROL Source名稱]** | 資料流所屬的來源名稱。 |
| 已接收&#x200B;**[!UICONTROL 筆記錄**] | 從資料湖接收的記錄數。 |
| **[!UICONTROL 個記錄失敗]** | 已擷取但由於錯誤而未擷取到[!DNL Profile]中的記錄數。 |
| **[!UICONTROL 已建立的設定檔片段]** | 已新增的淨新[!DNL Profile]片段數目。 |
| **[!UICONTROL 已更新設定檔片段]** | 已更新現有[!DNL Profile]片段的數量 |
| **[!UICONTROL 設定檔片段總數]** | 寫入[!DNL Profile]的記錄總數，包括所有已更新的現有[!DNL Profile]片段以及已建立的新[!DNL Profile]片段。 |
| **[!UICONTROL 失敗的資料流執行總數]** | 失敗的資料流執行次數。 |
| **[!UICONTROL 上次使用中]** | 上次執行資料流的時間戳記。 |

選取資料流執行開始時間旁的篩選圖示![篩選](/help/images/icons/filter.png)，檢視有關您的[!DNL Profile]資料流執行的詳細資訊。

![篩選圖示會醒目提示。 選取此圖示可讓您檢視所選資料流的詳細資訊。](../assets/ui/monitor-profiles/dataflows-filter.png)

[!UICONTROL 資料流執行詳細資料]頁面會顯示您[!DNL Profile]資料流執行的詳細資訊，包括其組織ID和資料流執行ID。 此頁面也會顯示[!DNL Profile]提供的對應錯誤碼和錯誤訊息（如果擷取程式發生任何錯誤）。

![會顯示一個儀表板，顯示所選資料流的詳細資訊。](../assets/ui/monitor-profiles/dataflow-run-details.png)

下列量度適用於此儀表板檢視：

| 量度 | 說明 |
| -------| ----------- |
| 已接收&#x200B;**[!UICONTROL 筆記錄]** | 從資料湖接收的記錄數。 |
| **[!UICONTROL 個記錄失敗]** | 已擷取但由於錯誤而未擷取到[!DNL Profile]中的記錄數。 |
| **[!UICONTROL 已建立的設定檔片段]** | 已新增的淨新[!DNL Profile]片段數目。 |
| **[!UICONTROL 已更新設定檔片段]** | 已更新現有[!DNL Profile]片段的數量。 |
| **[!UICONTROL 狀態]** | 定義資料流的整體狀態。 可能的狀態值包括： <ul><li>`Success`：表示資料流作用中，而且正在根據提供的排程擷取資料。</li><li>`Failed`：指出資料流程的啟用程式已因錯誤而中斷。 </li><li>`Processing`：表示資料流尚未啟用。 此狀態通常會在建立新資料流後立即發生。</li></ul> |
| **[!UICONTROL 資料流執行開始]** | 資料流開始執行的日期和時間。 |
| **[!UICONTROL 上次更新時間]** | 資料流上次更新的日期和時間。 |
| **[!UICONTROL 錯誤摘要]** | 如果資料流執行失敗，這會顯示錯誤代碼以及資料流執行失敗原因的摘要。 |
| **[!UICONTROL 資料流執行ID]** | 資料流執行的識別碼。 |
| **[!UICONTROL IMS組織ID]** | 資料流執行所屬的組織ID。 |

此外，您可以選取切換來檢視失敗的記錄或略過的記錄。 錯誤區段包含有關錯誤代碼和失敗或排除的記錄數的詳細資訊。
