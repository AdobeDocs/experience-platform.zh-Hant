---
keywords: Experience Platform；首頁；熱門主題；監控身分；監控資料流程；資料流程；身分；
description: Adobe Experience Platform 身分識別服務透過跨裝置和系統橋接身分，為您提供客戶及其行為的全方位檢視，讓您可即時實現有影響力的個人數位體驗。本教學課程提供如何使用Experience Platform使用者介面監控具有身分的資料流的指示。
title: 監視UI中身分的資料流
type: Tutorial
exl-id: 735b0e52-74f6-47fe-98c6-e12a633b6f57
source-git-commit: 1a7ba52b48460d77d0b7695aa0ab2d5be127d921
workflow-type: tm+mt
source-wordcount: '1149'
ht-degree: 14%

---

# 監視UI中身分的資料流

Adobe Experience Platform 身分識別服務透過跨裝置和系統橋接身分，為您提供客戶及其行為的全方位檢視，讓您可即時實現有影響力的個人數位體驗。

監視儀表板可讓您以視覺化方式呈現身分中的資料活動，包括資料身分的狀態。 本教學課程提供有關如何使用監視儀表板來使用Experience Platform使用者介面監視資料的身分，允許您追蹤身分處理狀態的指示。

## 快速入門 {#getting-started}

- [資料流](../home.md)：資料流能呈現資料處理作業在Platform上行動資料的情形。 資料流可跨不同服務進行設定，有助於將資料從來源聯結器移至目標資料集，以及 [!DNL Identity] 和 [!DNL Profile]，並至 [!DNL Destinations].
   - [資料流執行](../../sources/notifications.md)：資料流執行是根據所選資料流的頻率設定而定期排程的工作。
- [Identity Service](../../identity-service/home.md)：透過跨裝置和系統橋接身分，更能瞭解個別客戶及其行為。
- [沙箱](../../sandboxes/home.md)： [!DNL Experience Platform] 提供分割單一區域的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，協助開發及改進數位體驗應用程式。

## 監視身分儀表板 {#identity-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_identity_processing"
>title="身分識別處理"
>abstract="身分識別處理視圖會包含有關擷取到身分識別服務的記錄的資訊，包括新增的身分識別數量、建立的圖表和更新的圖表。檢閱量度定義指南以了解有關量度和圖表的詳細資訊。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_identity"
>title="資料流執行詳細資訊"
>abstract="資料流執行詳細資訊頁面會顯示有關身分識別資料流執行的詳細資訊，包括其組織 ID 和資料流執行 ID。"

若要存取 **[!UICONTROL 身分]** 儀表板，選取 **[!UICONTROL 監視]** ，位於左側導覽器中。 一旦於 **[!UICONTROL 監視]** 頁面，選取 **[!UICONTROL 身分]** 卡片。

![身分卡。 畫面上會顯示有關已接收記錄數、已擷取記錄數以及成功率的資訊。](../assets/ui/monitor-identities/focus-card.png)

在主要 **[!UICONTROL 身分]** 儀表板， **[!UICONTROL 身分]** 卡片會顯示所接收記錄總數、擷取的記錄數以及記錄擷取成功率的相關資訊。

儀表板本身包含有關身分處理的量度。 預設情況下，儀表板將顯示過去24小時內您組織來源的身分處理詳細資訊。

![身分控制面板。 會顯示每個來源接收之記錄數的相關資訊。](../assets/ui/monitor-identities/sources.png)

此 [!UICONTROL 身分處理中] 頁面包含擷取到的記錄資訊 [!DNL Identity Service]，包括新增的身分數量、建立的圖表和更新的圖表。

下列量度適用於此儀表板檢視：

| 身分量度 | 說明 |
| ---------------- | ----------- |
| **[!UICONTROL 已收到的記錄]** | 從資料湖接收的記錄數。 |
| **[!UICONTROL 失敗的記錄]** | 由於資料錯誤而未擷取到Platform的記錄數。 |
| **[!UICONTROL 略過的記錄]** | 已擷取但未擷取的記錄數 [!DNL Identity Service] 因為記錄列中只有一個識別碼。 |
| **[!UICONTROL 已擷取的記錄]** | 擷取到的記錄數 [!DNL Identity Service]. |
| **[!UICONTROL 身分已新增]** | 新增到的淨新識別碼數目 [!DNL Identity Service]. |
| **[!UICONTROL 建立的圖表]** | 在中建立的淨新身分圖表數目 [!DNL Identity Service]. |
| **[!UICONTROL 已更新的圖表]** | 以新邊更新的現有身分圖表數目。 |
| **[!UICONTROL 失敗的資料流總數]** | 失敗的資料流執行次數。 |

您可以選取篩選器圖示 ![篩選圖示](../assets/ui/monitor-identities/filter.png) 在來源名稱旁邊，可檢視該所選來源資料流程的身分處理資訊。

![篩選器圖示會反白顯示。 選取此圖示可讓您檢視所選來源的資料流。](../assets/ui/monitor-identities/sources-filter.png)

或者，您可以選取 **[!UICONTROL 資料流]** 在切換上，可檢視貴組織過去24小時資料流程的身分處理詳細資料。

![身分控制面板。 顯示有關每個資料流接收的身分數目的資訊。](../assets/ui/monitor-identities/dataflows.png)

下列量度適用於此儀表板檢視：

| 量度 | 說明 |
| -------| ----------- |
| **[!UICONTROL 資料流]** | 資料流的名稱。 |
| **[!UICONTROL 資料集]** | 資料流所插入的資料集名稱。 |
| **[!UICONTROL 來源名稱]** | 資料流所屬的來源名稱。 |
| **[!UICONTROL 已收到的記錄]** | 從資料湖接收的記錄數。 |
| **[!UICONTROL 失敗的記錄]** | 由於資料錯誤而未擷取到Platform的記錄數。 |
| **[!UICONTROL 略過的記錄]** | 已擷取但未擷取的記錄數 [!DNL Identity Service] 因為記錄列中只有一個識別碼。 |
| **[!UICONTROL 已擷取的記錄]** | 擷取到的記錄數 [!DNL Identity Service]. |
| **[!UICONTROL 記錄總數]** | 所有記錄的總數，包括失敗的記錄、略過的記錄、新增的身分和重複的記錄。 |
| **[!UICONTROL 身分已新增]** | 新增到的淨新識別碼數目 [!DNL Identity Service]. |
| **[!UICONTROL 建立的圖表]** | 在中建立的淨新身分圖表數目 [!DNL Identity Service]. |
| **[!UICONTROL 已更新的圖表]** | 以新邊更新的現有身分圖表數目。 |
| **[!UICONTROL 失敗的資料流總數]** | 失敗的資料流執行次數。 |

選取篩選器圖示 ![篩選](../assets/ui/monitor-identities/filter.png) 資料流執行開始時間旁邊，可檢視有關您的詳細資訊 [!DNL Identity] 資料流執行。

![篩選器圖示會反白顯示。 選取此圖示可讓您檢視所選資料流的詳細資訊。](../assets/ui/monitor-identities/dataflows-filter.png)

此 [!UICONTROL 資料流執行詳細資料] 頁面會顯示您網站上的 [!DNL Identity] 資料流執行，包括其組織ID和資料流執行ID。 此頁面也會顯示提供的對應錯誤碼和錯誤訊息。 [!DNL Identity Service]，以瞭解擷取過程中是否發生任何錯誤。

![此時會顯示一個控制面板，顯示所選資料流的詳細資訊。](../assets/ui/monitor-identities/dataflow-run-details.png)

下列量度適用於此儀表板檢視：

| 量度 | 說明 |
| -------| ----------- |
| **[!UICONTROL 已收到的記錄]** | 從資料湖接收的記錄數。 |
| **[!UICONTROL 失敗的記錄]** | 由於資料錯誤而未擷取到Platform的記錄數。 |
| **[!UICONTROL 略過的記錄]** | 已擷取但未擷取的記錄數 [!DNL Identity Service] 因為記錄列中只有一個識別碼。 |
| **[!UICONTROL 已擷取的記錄]** | 擷取到的記錄數 [!DNL Identity Service]. |
| **[!UICONTROL 身分已新增]** | 新增到的淨新識別碼數目 [!DNL Identity Service]. |
| **[!UICONTROL 建立的圖表]** | 在中建立的淨新身分圖表數目 [!DNL Identity Service]. |
| **[!UICONTROL 已更新的圖表]** | 以新邊更新的現有身分圖表數目。 |
| **[!UICONTROL 狀態]** | 定義資料流的整體狀態。 可能的狀態值包括： <ul><li>`Success`：指出資料流作用中，且正在根據其提供的排程擷取資料。</li><li>`Failed`：指出資料流程的啟用程式已因錯誤而中斷。 </li><li>`Processing`：指出資料流尚未啟用。 此狀態通常會在建立新資料流後立即發生。</li></ul> |
| **[!UICONTROL 資料流執行開始]** | 資料流開始執行的日期和時間。 |
| **[!UICONTROL 上次更新時間]** | 資料流上次更新的日期和時間。 |
| **[!UICONTROL 錯誤摘要]** | 如果資料流執行失敗，這會顯示錯誤代碼以及資料流執行失敗原因的摘要。 |
| **[!UICONTROL 資料流執行ID]** | 資料流執行的識別碼。 |
| **[!UICONTROL IMS組織ID]** | 資料流執行所屬的組織ID。 |

此外，您可以選取切換來檢視失敗的記錄或略過的記錄。 錯誤區段包含有關錯誤代碼和失敗或排除的記錄數的詳細資訊。
