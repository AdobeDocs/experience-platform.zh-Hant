---
description: 瞭解如何使用Experience Platform使用者介面在細分期間監視資料流程。
title: 在UI中監視對象的資料流
type: Tutorial
exl-id: 32fd2ba1-0ff0-4ea7-8d55-80d53eebc02f
source-git-commit: 716c14f29be24d084111864053e3e4ae884003f0
workflow-type: tm+mt
source-wordcount: '1862'
ht-degree: 2%

---

# 在UI中監視對象的資料流

區段服務可讓您透過區段定義或其他來源，從您的網站建立對象。 [!DNL Real-Time Customer Profile] 資料。 Platform提供資料流，透明地追蹤從來源到目的地的資料流程。

使用監控儀表板可檢視對象中資料活動的視覺化表示法，包括資料細分的狀態。 閱讀教學課程，瞭解如何使用監視儀表板來使用Experience Platform使用者介面監視資料分段，讓您追蹤對象啟用、評估和匯出工作的狀態。

## 快速入門 {#getting-started}

本指南需要您深入了解下列 Adobe Experience Platform 元件：

- [資料流](../home.md)：資料流能呈現資料處理作業在Platform上行動資料的情形。 資料流可跨不同服務進行設定，有助於將資料從來源聯結器移至目標資料集，以及 [!DNL Identity] 和 [!DNL Profile]，並至 [!DNL Destinations].
   - [資料流執行](../../sources/notifications.md)：資料流執行是根據所選資料流的頻率設定而定期排程的工作。
- [細分](../../segmentation/home.md)：分段可讓您從即時客戶設定檔資料建立對象。
   - [啟動工作](../../destinations/ui/activation-overview.md)：啟用工作用於將對象啟用至指定目的地。
   - [評估工作](../../segmentation/tutorials/evaluate-a-segment.md#evaluate-a-segment)：評估作業是評估受眾的非同步程式。
   - [匯出工作](../../segmentation/api/export-jobs.md)：匯出作業為非同步程式，用於儲存資料集的對象成員。
- [沙箱](../../sandboxes/home.md)： [!DNL Experience Platform] 提供分割單一區域的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，協助開發及改進數位體驗應用程式。

## 監視受眾控制面板 {#monitoring-audiences-dashboard}

>[!CONTEXTUALHELP]
>id="platform_monitoring_segments"
>title="對象"
>abstract="對象檢視包含貴組織所有對象的相關資訊，以及這些對象的啟用和評估工作的相關進一步資訊。"

若要存取 **[!UICONTROL 受眾]** 儀表板，選取 **[!UICONTROL 監視]** ，位於左側導覽器中。 一旦於 **[!UICONTROL 監視]** 頁面，選取 **[!UICONTROL 受眾]** 卡片。

![受眾卡。 最後評估工作和最後匯出工作的相關資訊隨即顯示。](../assets/ui/monitor-audiences/audience-card.png)

在主要 **[!UICONTROL 受眾]** 儀表板， **[!UICONTROL 受眾]** 卡片會顯示上次評估工作和上次匯出工作的狀態和日期。

儀表板本身包含對象和細分作業的量度。 依預設，控制面板會顯示過去24小時的對象量度。 若要進一步瞭解分段作業檢視，請參閱 [監視分段工作](#monitoring-segmentation-jobs-dashboard) 區段。

>[!IMPORTANT]
>
>目前，僅限啟用的對象 [批次（以檔案為基礎）目的地](../../destinations/destination-types.md#file-based) 監控對象控制面板支援。

![受眾控制面板。 有關您組織和沙箱中不同對象的資訊隨即顯示。](../assets/ui/monitor-audiences/audience-dashboard.png)

下列量度適用於此儀表板檢視：

| 量度 | 說明 |
| ------ | ----------- |
| **[!UICONTROL 對象名稱]** | 對象名稱。 |
| **[!UICONTROL 資料型別]** | 對象的資料型別。 可能的值包括 **[!UICONTROL 客戶]**， **[!UICONTROL 帳戶]**、和 **[!UICONTROL 潛在客戶]**. 您可以使用檢視特定資料型別的對象 [!UICONTROL 資料型別] 在卡片帶狀上方篩選。 |
| **[!UICONTROL 上次評估時間戳記]** | 對象上次執行評估工作的日期和時間。 |
| **[!UICONTROL 上次評估狀態]** | 對象最後評估工作的狀態。 可能的值包括 **[!UICONTROL 成功]**， **[!UICONTROL 沒有回合]**、和 **[!UICONTROL 已失敗]**. |
| **[!UICONTROL 上次評估方法]** | 對象的評估方法。 由於僅支援批次分段，因此唯一可能的值為 **[!UICONTROL 批次]**. |
| **[!UICONTROL 上次評估設定檔]** | 在對象的上次評估工作中評估的設定檔數。 |
| **[!UICONTROL 上次啟用時間戳記]** | 對象上次執行啟用工作的日期和時間。 |
| **[!UICONTROL 上次啟用狀態]** | 對象上次啟用工作的狀態。 可能的值包括 **[!UICONTROL 成功]**， **[!UICONTROL 沒有回合]**、和 **[!UICONTROL 已失敗]**. |
| **[!UICONTROL 上次啟用身分]** | 在對象的上次啟用工作中啟用的身分數量。 |
| **[!UICONTROL 上次啟用目的地]** | 對象上次啟用工作的目的地名稱。 |

您可以篩選結果給特定對象，並藉由選取篩選圖示(![篩選圖示。](../assets/ui/monitor-audiences/filter-icon.png))。區段作業會依時間順序排序，而最近的區段作業會先出現。

![篩選器圖示會反白顯示。 選取此項可讓您檢視指定對象的細分工作。](../assets/ui/monitor-audiences/filter-audience.png)

篩選的對象控制面板隨即顯示。 此 **[!UICONTROL 受眾]** 卡片會顯示上次評估工作和上次啟用工作的狀態和日期。

![受眾卡。 最後評估工作和上次啟用工作的相關資訊隨即顯示。](../assets/ui/monitor-audiences/specified-audience-card.png)

儀表板本身會顯示上次評估和啟用工作的時間和狀態、顯示對象評估的設定檔計數的圖表，以及執行之區段工作的量度。 依預設，控制面板會顯示過去24小時的分段工作量度。

![篩選的對象控制面板。 畫面上會顯示為此對象執行的各種分段工作相關資訊。](../assets/ui/monitor-audiences/filter-audience.png)

下列量度適用於此儀表板檢視：

| 量度 | 說明 |
| ------ | ----------- |
| **[!UICONTROL 工作開始]** | 分段工作開始的日期和時間。 |
| **[!UICONTROL 類型]** | 表示細分工作的型別。 兩種支援的工作型別為 **啟用** 和 **評估** 個工作。 |
| **[!UICONTROL 工作完成]** | 分段工作完成的日期和時間。 |
| **[!UICONTROL 處理時間]** | 完成細分工作所需的時間。 |
| **[!UICONTROL 工作狀態]** | 分段工作的狀態。 支援的值包括 **[!UICONTROL 成功]**， **[!UICONTROL 進行中]**、和 **[!UICONTROL 已失敗]**. |
| **[!UICONTROL 設定檔計數]** | 分段工作正在評估的設定檔數。 每個使用者都應該有唯一的設定檔。 |
| **[!UICONTROL 身分已啟用]** | 正在啟用細分工作的身分數。 每個設定檔都可以有多個身分。 例如，個人資料可以包含電子郵件、電話號碼和忠誠度編號作為身分。 |
| **[!UICONTROL 目的地名稱]** | 分段工作啟動的目標目的地名稱。 |

您可以進一步篩選至特定分段工作，並透過選取篩選器圖示(![篩選圖示。](../assets/ui/monitor-audiences/filter-icon.png))。有兩種不同型別的細分工作可供篩選：啟動工作和評估工作。

### 啟用工作詳細資料 {#activation-job-details}

「啟動工作資料流執行詳細資料」頁面會顯示執行專案的量度、資料流執行錯誤，以及與細分工作相關的對象資訊。 啟用工作可針對指定目的地啟用您的對象。

![啟動工作儀表板。 畫面上會顯示為此對象執行的各種分段工作相關資訊。](../assets/ui/monitor-audiences/activation-job-dashboard.png)

下列量度適用於此儀表板檢視：

| 量度 | 說明 |
| ------ | ----------- |
| **[!UICONTROL 已接收的設定檔]** | 啟動流程中接收的設定檔總數。 |
| **[!UICONTROL 身分已啟用]** | 根據收到的設定檔，成功啟用至目的地的身分總數。 |
| **[!UICONTROL 身分已排除]** | 根據收到的設定檔，從啟用至目的地排除的身分總數。 由於缺少屬性或違反同意，這些身分可能會被排除。 |
| **[!UICONTROL 資料大小]** | 正在啟用的資料流的大小。 |
| **[!UICONTROL 檔案總數]** | 在資料流中啟用的檔案總數。 |
| **[!UICONTROL 狀態]** | 啟動工作的目前狀態。 |
| **[!UICONTROL 資料流執行開始]** | 啟動工作開始的日期和時間。 |
| **[!UICONTROL 資料流執行結束]** | 啟動工作結束的日期和時間。 |
| **[!UICONTROL 資料流執行ID]** | 目前啟用工作的ID。 |
| **[!UICONTROL IMS組織ID]** | 啟動工作所屬的組織ID。 |
| **[!UICONTROL 目的地名稱]** | 資料啟用的目的地名稱。 |

在受眾區段底下，您可以看到啟動工作中啟動的受眾清單。

![啟動工作儀表板。 失敗或排除的身分相關資訊會醒目提示。](../assets/ui/monitor-audiences/activation-job-audiences.png)

在「對象」區段，可使用下列量度：

| 量度 | 說明 |
| ------ | ----------- |
| **[!UICONTROL 名稱]** | 已啟用的對象名稱。 |
| **[!UICONTROL 身分已啟用]** | 根據收到的設定檔，成功啟用至目的地的身分總數。 |
| **[!UICONTROL 身分已排除]** | 根據收到的設定檔，從啟用至目的地排除的身分總數。 由於缺少屬性或違反同意，這些身分可能會被排除。 |
| **[!UICONTROL 上次資料流執行狀態]** | 針對該對象執行的最後一次啟用工作的狀態。 |
| **[!UICONTROL 上次資料流執行日期]** | 針對該對象執行的上次啟用工作的日期和時間。 |

此外，您也可以檢視資料流執行錯誤的詳細資料。 在資料流執行錯誤區段下，您可以檢視失敗的身分或排除的身分。 錯誤區段包含有關錯誤代碼和失敗或排除的身分數量的詳細資訊。

![啟動工作儀表板。 失敗或排除的身分相關資訊會醒目提示。](../assets/ui/monitor-audiences/activation-job-errors.png)

### 評估工作詳細資料 {#evaluation-job-details}

「評估工作資料流執行詳細資料」頁面會顯示與細分工作相關的執行量度和對象資訊。

![評估工作儀表板。 畫面上會顯示對象評估工作的相關資訊。](../assets/ui/monitor-audiences/evaluation-job-details.png)

下列量度適用於此儀表板檢視：

| 量度 | 說明 |
| ------ | ----------- |
| **[!UICONTROL 設定檔總數]** | 正在評估的設定檔總數。 |
| **[!UICONTROL 狀態]** | 評估工作的狀態。 評估工作的可能狀態包括 **[!UICONTROL 成功]** 和 **[!UICONTROL 已失敗]**. |
| **[!UICONTROL 工作開始]** | 評估工作開始的日期和時間。 |
| **[!UICONTROL 工作結束]** | 評估工作結束的日期和時間。 |
| **[!UICONTROL 工作型別]** | 細分工作的型別。 在此情況下，永遠是 **[!UICONTROL 區段評估]** 工作。 |
| **[!UICONTROL 評估型別]** | 正在完成的評估型別。 這可以是 **[!UICONTROL 批次]** 或 **[!UICONTROL 串流]**. |
| **[!UICONTROL 工作ID]** | 評估工作的ID。 |
| **[!UICONTROL IMS組織ID]** | 評估工作所屬組織的識別碼。 |
| **[!UICONTROL 對象名稱]** | 正在評估的對象名稱。 |
| **[!UICONTROL 對象ID]** | 正在評估的對象的ID。 |

在 [!UICONTROL 受眾] 區段，您可以看到作為評估工作的一部分進行評估的對象清單。 您可以使用搜尋列依名稱篩選對象清單。

>[!IMPORTANT]
>
>此儀表板檢視目前支援最多800個對象量度。

對於 [!UICONTROL 受眾] 區段，可使用下列量度：

| 量度 | 說明 |
| ------ | ----------- |
| **[!UICONTROL 名稱]** | 正在評估的對象名稱。 |
| **[!UICONTROL 設定檔計數]** | 正在評估的設定檔數。 |

## 監視分段工作儀表板 {#monitoring-segmentation-jobs-dashboard}

>[!CONTEXTUALHELP]
>id="platform_monitoring_segment_jobs"
>title="分段工作"
>abstract="分段作業檢視包含有關所有對象之評估和匯出作業的資訊。"

若要存取 **[!UICONTROL 分段工作]** 儀表板，選取 **[!UICONTROL 分段工作]** 在 [!UICONTROL 受眾] 儀表板。 此 [!UICONTROL 監視] 儀表板包含有關評估和匯出作業的量度和資訊。

>[!NOTE]
>
>僅限 **區段評估工作** 支援用於每個對象監控。 區段匯出作業僅支援組織層級的監控。

![隨即顯示分段工作監視儀表板。 會強調顯示在「對象」和「細分」工作之間切換的切換按鈕。](../assets/ui/monitor-audiences/segmentation-jobs-dashboard.png)

使用 [!UICONTROL 分段工作] 控制面板以瞭解設定檔評估與匯出是否準時發生，且無任何例外，因此目的地啟用的下游服務可以有評估過的最新設定檔資料。

下列量度可用於細分工作：

| 量度 | 說明 |
| ------ | ----------- |
| **[!UICONTROL 分段工作]** | 表示細分工作的名稱。 |
| **[!UICONTROL 類型]** | 指示分段工作的型別 — 匯出或評估。 請注意，在這兩種情況下，分段工作都會評估或匯出 **全部** 屬於組織的對象。 若要進一步瞭解匯出作業，請閱讀 [匯出作業端點](../../segmentation/api/export-jobs.md). 若要進一步瞭解評估工作，請閱讀以下教學課程： [評估區段定義](../../segmentation/tutorials/evaluate-a-segment.md#evaluate-a-segment). |
| **[!UICONTROL 工作開始]** | 分段工作開始的日期和時間。 |
| **[!UICONTROL 工作結束]** | 分段工作完成的日期和時間。 |
| **[!UICONTROL 狀態]** | 已完成工作的狀態。 分段工作可能的狀態包括成功或失敗。 |
