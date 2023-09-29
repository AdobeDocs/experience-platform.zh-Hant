---
keywords: Experience Platform；首頁；熱門主題；監控區段；監控資料流程；資料流程；分段
description: 區段可讓您從即時客戶個人檔案資料建立區段和對象。 本教學課程提供如何使用Experience Platform使用者介面在細分期間監視資料流的指示。
title: 監視UI中區段的資料流
type: Tutorial
exl-id: 32fd2ba1-0ff0-4ea7-8d55-80d53eebc02f
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1919'
ht-degree: 4%

---

# 監視UI中區段的資料流

區段服務可讓您從Adobe Experience Platform中的即時客戶設定檔資料建立區段和對象。 Platform提供資料流，透明地追蹤從來源到目的地的資料流程。

監視儀表板可讓您以視覺化方式呈現區段內的資料活動，包括資料細分的狀態。 本教學課程說明如何使用監視儀表板，透過Experience Platform使用者介面監視資料的區段，讓您追蹤區段啟用、評估和匯出工作的狀態。

## 快速入門 {#getting-started}

本指南需要您深入瞭解下列Adobe Experience Platform元件：

- [資料流](../home.md)：資料流能呈現資料處理作業在Platform上行動資料的情形。 資料流可跨不同服務進行設定，有助於將資料從來源聯結器移至目標資料集，以及 [!DNL Identity] 和 [!DNL Profile]，並至 [!DNL Destinations].
   - [資料流執行](../../sources/notifications.md)：資料流執行是根據所選資料流的頻率設定而定期排程的工作。
- [細分](../../segmentation/home.md)：分段可讓您從即時客戶設定檔資料建立區段和對象。
   - [啟動工作](../../destinations/ui/activation-overview.md)：啟用工作用於將區段啟用至指定目的地。
   - [評估工作](../../segmentation/tutorials/evaluate-a-segment.md#evaluate-a-segment)：評估工作為非同步程式，會根據指定區段執行建立對象區段。
   - [匯出工作](../../segmentation/api/export-jobs.md)：匯出作業是用來將對象區段成員保留至資料集的非同步程式。
- [沙箱](../../sandboxes/home.md)： [!DNL Experience Platform] 提供分割單一區域的虛擬沙箱 [!DNL Platform] 將執行個體整合至個別的虛擬環境中，協助開發及改進數位體驗應用程式。

## 監控區段控制面板 {#monitoring-segments-dashboard}

>[!CONTEXTUALHELP]
>id="platform_monitoring_segments"
>title="區段"
>abstract="區段檢視包含有關您組織之區段的所有資訊，以及有關其啟動和評估作業的進一步資訊。"

若要存取 **[!UICONTROL 區段]** 儀表板，選取 **[!UICONTROL 監視]** ，位於左側導覽器中。 一旦於 **[!UICONTROL 監視]** 頁面，選取 **[!UICONTROL 區段]** 卡片。

![區段卡片。 最後評估工作和最後匯出工作的相關資訊隨即顯示。](../assets/ui/monitor-segments/segment-card-monitoring.png)

在主要 **[!UICONTROL 區段]** 儀表板， **[!UICONTROL 區段]** 卡片會顯示上次評估工作和上次匯出工作的狀態和日期。

儀表板本身包含區段和區段作業的量度。 預設情況下，控制面板會顯示過去24小時的區段量度。 若要深入瞭解區段作業檢視，請參閱 [監視區段工作](#monitoring-segment-jobs-dashboard) 區段。

>[!IMPORTANT]
>
>目前，僅限啟用的區段 [批次（以檔案為基礎）目的地](../../destinations/destination-types.md#file-based) 監控區段儀表板支援。

![區段控制面板。 有關您組織和沙箱中不同區段的資訊隨即顯示。](../assets/ui/monitor-segments/segment-monitoring-dashboard.png)

下列量度適用於此儀表板檢視：

| 量度 | 說明 |
| ------ | ----------- |
| **[!UICONTROL 區段名稱]** | 區段名稱。 |
| **[!UICONTROL 上次評估時間戳記]** | 區段的上次評估工作執行的日期和時間。 |
| **[!UICONTROL 上次評估狀態]** | 區段最後評估工作的狀態。 可能的值包括 **[!UICONTROL 成功]**， **[!UICONTROL 沒有回合]**、和 **[!UICONTROL 已失敗]**. |
| **[!UICONTROL 上次評估設定檔]** | 在區段的上次評估工作中評估的設定檔數。 |
| **[!UICONTROL 上次啟用時間戳記]** | 區段的上次啟用工作執行的日期和時間。 |
| **[!UICONTROL 上次啟用狀態]** | 區段最後啟用工作的狀態。 可能的值包括 **[!UICONTROL 成功]**， **[!UICONTROL 沒有回合]**、和 **[!UICONTROL 已失敗]**. |
| **[!UICONTROL 上次啟用身分]** | 在區段的上次啟用工作中啟用的身分數。 |
| **[!UICONTROL 上次啟用目的地]** | 區段的上次啟用工作所啟用的目的地名稱。 |

您可以篩選特定區段的結果，並透過選取篩選圖示(![篩選圖示。](../assets/ui/monitor-segments/filter-icon.png))。區段作業會依時間順序排序，最近的區段作業會先出現。

![篩選器圖示會反白顯示。 選取此選項可讓您檢視指定區段的區段作業。](../assets/ui/monitor-segments/filter-segment.png)

篩選的區段控制面板隨即出現。 此 **[!UICONTROL 區段]** 卡片會顯示上次評估工作和上次啟用工作的狀態和日期。

![區段卡片。 最後評估工作和上次啟用工作的相關資訊隨即顯示。](../assets/ui/monitor-segments/specified-segment-card.png)

儀表板本身會顯示上次評估與啟用工作的時間和狀態、顯示區段評估的設定檔計數的圖形，以及執行之區段工作的量度。 依預設，控制面板會顯示過去24小時的區段工作量度。

![篩選的區段控制面板。 會顯示已針對此區段執行之各種區段工作的相關資訊。](../assets/ui/monitor-segments/filter-specified-segment.png)

下列量度適用於此儀表板檢視：

| 量度 | 說明 |
| ------ | ----------- |
| **[!UICONTROL 工作開始]** | 區段作業開始的日期和時間。 |
| **[!UICONTROL 類型]** | 表示區段作業的型別。 兩種支援的工作型別為 **啟用** 和 **評估** 個工作。 |
| **[!UICONTROL 工作完成]** | 區段作業完成的日期和時間。 |
| **[!UICONTROL 處理時間]** | 完成區段作業所需的時間。 |
| **[!UICONTROL 工作狀態]** | 區段工作的狀態。 支援的值包括 **[!UICONTROL 成功]**， **[!UICONTROL 進行中]**、和 **[!UICONTROL 已失敗]**. |
| **[!UICONTROL 設定檔計數]** | 區段工作正在評估的設定檔數。 每個使用者都應該有唯一的設定檔。 |
| **[!UICONTROL 身分計數]** | 正在啟用區段工作的身分數。 每個設定檔都可以有多個身分。 例如，個人資料可以包含電子郵件、電話號碼和忠誠度編號作為身分。 |
| **[!UICONTROL 目的地名稱]** | 區段作業啟動的目標目的地名稱。 |

您可以進一步篩選至特定區段作業，並藉由選取篩選圖示(![篩選圖示。](../assets/ui/monitor-segments/filter-icon.png))。有兩種不同型別的區段作業可供篩選：啟動作業和評估作業。

### 啟用工作詳細資料 {#activation-job-details}

「啟動工作資料流執行詳細資料」頁面會顯示執行專案的測量結果、資料流執行錯誤，以及與區段工作相關的區段資訊。 啟用工作可用來啟用指定目的地的區段。 依預設，「詳細資訊」頁面會顯示資料流執行錯誤。

![篩選的區段控制面板。 會顯示已針對此區段執行之各種區段工作的相關資訊。](../assets/ui/monitor-segments/activation-job-details.png)

下列量度適用於此儀表板檢視：

| 量度 | 說明 |
| ------ | ----------- |
| **[!UICONTROL 收到的設定檔]** | 啟動流程中接收的設定檔總數。 |
| **[!UICONTROL 啟用的身分]** | 根據收到的設定檔，成功啟用至目的地的身分總數。 |
| **[!UICONTROL 排除的身分]** | 根據收到的設定檔，從啟用至目的地排除的身分總數。 由於缺少屬性或違反同意，這些身分可能會被排除。 |
| **[!UICONTROL 資料大小]** | 正在啟用的資料流的大小。 |
| **[!UICONTROL 檔案總數]** | 在資料流中啟用的檔案總數。 |
| **[!UICONTROL 狀態]** | 啟動工作的目前狀態。 |
| **[!UICONTROL 資料流執行開始]** | 啟動工作開始的日期和時間。 |
| **[!UICONTROL 資料流執行結束]** | 啟動工作結束的日期和時間。 |
| **[!UICONTROL 資料流執行ID]** | 目前啟用工作的ID。 |
| **[!UICONTROL IMS組織ID]** | 啟動工作所屬的組織ID。 |
| **[!UICONTROL 目的地名稱]** | 資料啟用的目的地名稱。 |

在量度下方，會在資料流執行錯誤與區段之間顯示一個可供選取的切換按鈕。

![篩選的區段控制面板。 用於切換資料流執行錯誤和區段顯示的切換會反白顯示。](../assets/ui/monitor-segments/activation-job-details-toggle.png)

在資料流執行錯誤區段下，選取切換以檢視失敗的身分或排除的身分欄位。 錯誤區段包含有關錯誤代碼和失敗或排除的身分數量的詳細資訊。

![篩選的區段控制面板。 失敗或排除的身分相關資訊會醒目提示。](../assets/ui/monitor-segments/activation-job-details.png)

在區段區段底下，您可以看到已啟動作為啟動工作一部分的區段清單。 使用搜尋列依名稱篩選區段清單。

![篩選的區段控制面板。 失敗或排除的身分相關資訊會醒目提示。](../assets/ui/monitor-segments/activation-job-details-segments.png)

在「區段」區段，可使用下列量度：

| 量度 | 說明 |
| ------ | ----------- |
| **[!UICONTROL 名稱]** | 已啟用的區段名稱。 |
| **[!UICONTROL 啟用的身分]** | 根據收到的設定檔，成功啟用至目的地的身分總數。 |
| **[!UICONTROL 排除的身分]** | 根據收到的設定檔，從啟用至目的地排除的身分總數。 由於缺少屬性或違反同意，這些身分可能會被排除。 |
| **[!UICONTROL 上次資料流執行狀態]** | 針對該區段執行的最後一次啟用工作的狀態。 |
| **[!UICONTROL 上次資料流執行日期]** | 針對該區段執行的上次啟用工作的日期和時間。 |

### 評估工作詳細資料 {#evaluation-job-details}

「評估工作資料流執行詳細資料」頁面會顯示與區段工作相關的執行量度和區段資訊。 評估工作是依據指定區段建立對象區段的非同步程式。 若要進一步瞭解評估工作，請閱讀以下教學課程： [評估區段](../../segmentation/tutorials/evaluate-a-segment.md#evaluate-a-segment).

![評估工作儀表板。 會顯示區段評估工作的相關資訊。](../assets/ui/monitor-segments/evaluation-job-details.png)

下列量度適用於此儀表板檢視：

| 量度 | 說明 |
| ------ | ----------- |
| **[!UICONTROL 設定檔總數]** | 正在評估的設定檔總數。 |
| **[!UICONTROL 狀態]** | 評估工作的狀態。 評估工作的可能狀態包括 **[!UICONTROL 成功]** 和 **[!UICONTROL 已失敗]**. |
| **[!UICONTROL 工作開始]** | 評估工作開始的日期和時間。 |
| **[!UICONTROL 工作結束]** | 評估工作結束的日期和時間。 |
| **[!UICONTROL 工作型別]** | 區段工作的型別。 在此情況下，一律會是區段評估工作。 |
| **[!UICONTROL 評估型別]** | 正在完成的評估型別。 這可以是 **[!UICONTROL 批次]** 或 **[!UICONTROL 串流]**. |
| **[!UICONTROL 工作ID]** | 評估工作的ID。 |
| **[!UICONTROL IMS組織ID]** | 評估工作所屬組織的識別碼。 |
| **[!UICONTROL 區段名稱]** | 正在評估的區段名稱。 |
| **[!UICONTROL 區段ID]** | 正在評估的區段的ID。 |

在區段區段底下，您可以看到作為評估工作的一部分進行評估的區段清單。 您可以使用搜尋列依名稱篩選區段清單。

>[!IMPORTANT]
>
>此儀表板檢視目前支援最多800個區段量度。

在「區段」區段，可使用下列量度：

| 量度 | 說明 |
| ------ | ----------- |
| **[!UICONTROL 名稱]** | 正在評估的區段名稱。 |
| **[!UICONTROL 設定檔計數]** | 正在評估的設定檔數。 |

## 監視區段作業儀表板 {#monitoring-segment-jobs-dashboard}

>[!CONTEXTUALHELP]
>id="platform_monitoring_segment_jobs"
>title="區段作業"
>abstract="區段作業視圖會包含有關所有區段的評估和匯出作業的資訊。"

若要存取 **[!UICONTROL 區段工作]** 儀表板，選取 **[!UICONTROL 監視]** (![監檢視示](../assets/ui/monitor-destinations/monitoring-icon.png))中。 一旦於 [!UICONTROL 監視] 頁面，選取 **[!UICONTROL 區段工作]**. 此 [!UICONTROL 監視] 控制面板包含區段評估和匯出作業的量度和資訊。

>[!NOTE]
>
>僅限 **區段評估工作** 支援每個區段監控。 區段匯出作業僅支援組織層級的監控。

![區段作業監視儀表板](../assets/ui/monitor-segments/segment-jobs-dashboard.png)

使用 [!UICONTROL 區段工作] 控制面板以瞭解設定檔評估與匯出是否準時發生，且無任何例外，因此目的地啟用的下游服務可以有評估過的最新設定檔資料。

以下量度適用於區段作業：

| 量度 | 說明 |
---------|----------|
| **[!UICONTROL 區段工作]** | 表示區段工作的名稱。 |
| **[!UICONTROL 類型]** | 指示區段工作的型別 — 匯出或評估。 請注意，在這兩種情況下，區段作業都會評估或匯出 **全部** 屬於組織的區段。 若要進一步瞭解匯出作業，請閱讀 [匯出作業端點](../../segmentation/api/export-jobs.md). 若要進一步瞭解評估工作，請閱讀以下教學課程： [評估區段](../../segmentation/tutorials/evaluate-a-segment.md#evaluate-a-segment). |
| **[!UICONTROL 工作開始]** | 區段作業開始的日期和時間。 |
| **[!UICONTROL 工作結束]** | 區段作業完成的日期和時間。 |
| **[!UICONTROL 狀態]** | 已完成工作的狀態。 區段作業的可能狀態包括成功或失敗。 |
