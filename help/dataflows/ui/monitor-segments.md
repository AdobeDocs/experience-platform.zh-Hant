---
keywords: Experience Platform；首頁；熱門主題；監視器段；監視資料流；資料流；分段
description: 分段允許您根據即時客戶配置檔案資料建立段和受眾。 本教程提供有關如何在使用Experience Platform用戶介面進行分段期間監視資料流的說明。
title: 監視UI中段的資料流
type: Tutorial
exl-id: 32fd2ba1-0ff0-4ea7-8d55-80d53eebc02f
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1919'
ht-degree: 4%

---

# 監視UI中段的資料流

分段服務允許您從Adobe Experience Platform的即時客戶配置檔案資料中建立分段和受眾。 平台提供資料流，以透明地跟蹤從源到目標的資料流。

監控面板可以直觀地表示資料在段內的活動，包括資料分段的狀態。 本教程提供了有關如何使用監控面板使用Experience Platform用戶介面監視資料分段的說明，使您能夠跟蹤段激活、評估和導出作業的狀態。

## 快速入門 {#getting-started}

本指南要求對Adobe Experience Platform的下列組成部分有工作上的理解：

- [資料流](../home.md):資料流是跨平台移動資料的資料作業的表示形式。 資料流是跨不同服務配置的，有助於將資料從源連接器移動到目標資料集 [!DNL Identity] 和 [!DNL Profile], [!DNL Destinations]。
   - [資料流運行](../../sources/notifications.md):資料流運行是基於所選資料流的頻率配置的定期調度作業。
- [分段](../../segmentation/home.md):分段允許您根據即時客戶配置檔案資料建立段和受眾。
   - [激活作業](../../destinations/ui/activation-overview.md):激活作業用於將段激活到指定的目標。
   - [評估作業](../../segmentation/tutorials/evaluate-a-segment.md#evaluate-a-segment):評估作業是一個非同步進程，運行該進程會基於指定段建立訪問群體段。
   - [導出作業](../../segmentation/api/export-jobs.md):導出作業是用於將受眾段成員保留到資料集的非同步進程。
- [沙箱](../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙箱，將單個沙箱 [!DNL Platform] 實例到獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

## 監視段儀表板 {#monitoring-segments-dashboard}

>[!CONTEXTUALHELP]
>id="platform_monitoring_segments"
>title="區段"
>abstract="區段檢視包含有關您組織之區段的所有資訊，以及有關其啟動和評估作業的進一步資訊。"

訪問 **[!UICONTROL 段]** 儀表板，選擇 **[!UICONTROL 監視]** 的子菜單。 在 **[!UICONTROL 監視]** ，選擇 **[!UICONTROL 段]** 卡。

![段卡。 將顯示有關上次評估作業和上次導出作業的資訊。](../assets/ui/monitor-segments/segment-card-monitoring.png)

主 **[!UICONTROL 段]** 儀表板， **[!UICONTROL 段]** card顯示上次評估作業和上次導出作業的狀態和日期。

儀表板本身包含段和段作業的度量。 預設情況下，控制板將顯示過去24小時的段度量。 要瞭解有關段作業視圖的詳細資訊，請閱讀 [監視段作業](#monitoring-segment-jobs-dashboard) 的子菜單。

>[!IMPORTANT]
>
>當前，僅激活到 [批處理（基於檔案）目標](../../destinations/destination-types.md#file-based) 支援監視段儀表板。

![段操控板。 將顯示有關組織和沙箱中不同段的資訊。](../assets/ui/monitor-segments/segment-monitoring-dashboard.png)

以下度量可用於此儀表板視圖：

| 量度 | 說明 |
| ------ | ----------- |
| **[!UICONTROL 段名稱]** | 段的名稱。 |
| **[!UICONTROL 上次評估時間戳]** | 段上次評估作業運行的日期和時間。 |
| **[!UICONTROL 上次評估狀態]** | 段上次評估作業的狀態。 可能的值包括 **[!UICONTROL 成功]**。 **[!UICONTROL 無運行]**, **[!UICONTROL 失敗]**。 |
| **[!UICONTROL 上次評估配置檔案]** | 在段的上次評估作業中評估的配置檔案數。 |
| **[!UICONTROL 上次激活時間戳]** | 段上次激活作業運行的日期和時間。 |
| **[!UICONTROL 上次激活狀態]** | 段上次激活作業的狀態。 可能的值包括 **[!UICONTROL 成功]**。 **[!UICONTROL 無運行]**, **[!UICONTROL 失敗]**。 |
| **[!UICONTROL 上次激活標識]** | 在段的上次激活作業中激活的標識數。 |
| **[!UICONTROL 上次激活目標]** | 段上次激活作業所激活的目標的名稱。 |

可以通過選擇篩選器表徵圖(![篩選器表徵圖。](../assets/ui/monitor-segments/filter-icon.png))。段作業按時間順序排序，最新段作業首先出現。

![過濾器表徵圖將突出顯示。 選擇此項可查看指定段的段作業。](../assets/ui/monitor-segments/filter-segment.png)

將出現篩選的段操控板。 的 **[!UICONTROL 段]** card顯示上次評估作業和上次激活作業的狀態和日期。

![段卡。 將顯示有關上次評估作業和上次激活作業的資訊。](../assets/ui/monitor-segments/specified-segment-card.png)

控制面板本身顯示上次評估和激活作業的時間和狀態，顯示段評估的配置檔案計數以及運行的段作業的度量的圖形。 預設情況下，控制面板顯示過去24小時的段作業度量。

![篩選的段操控板。 將顯示有關為此段運行的各個段作業的資訊。](../assets/ui/monitor-segments/filter-specified-segment.png)

以下度量可用於此儀表板視圖：

| 量度 | 說明 |
| ------ | ----------- |
| **[!UICONTROL 作業開始]** | 段作業開始的日期和時間。 |
| **[!UICONTROL 類型]** | 指示段作業的類型。 支援的兩種作業類型是 **激活** 和 **評價** 工作。 |
| **[!UICONTROL 作業完成]** | 段任務完成的日期和時間。 |
| **[!UICONTROL 處理時間]** | 段作業完成所花的時間。 |
| **[!UICONTROL 工作狀態]** | 段作業的狀態。 支援的值包括 **[!UICONTROL 成功]**。 **[!UICONTROL 正在進行]**, **[!UICONTROL 失敗]**。 |
| **[!UICONTROL 設定檔計數]** | 段作業正在評估的配置檔案數。 每個用戶應具有唯一的配置檔案。 |
| **[!UICONTROL 身份計數]** | 段作業正在激活的標識數。 每個配置檔案可以具有多個標識。 例如，配置檔案可以包含電子郵件、電話號碼和會員號碼作為身份。 |
| **[!UICONTROL 目標名稱]** | 將段作業激活到的目標的名稱。 |

您可以進一步篩選特定段作業，並通過選擇篩選器表徵圖(![篩選器表徵圖。](../assets/ui/monitor-segments/filter-icon.png))。可以篩選兩種不同的段作業：激活作業和評估作業。

### 激活作業詳細資訊 {#activation-job-details}

「激活作業資料流運行詳細資料」頁顯示有關運行度量、資料流運行錯誤以及與段作業相關的段的資訊。 激活作業用於激活指定目標的段。 預設情況下，「詳細資訊」頁顯示資料流運行錯誤。

![篩選的段操控板。 將顯示有關為此段運行的各個段作業的資訊。](../assets/ui/monitor-segments/activation-job-details.png)

以下度量可用於此儀表板視圖：

| 量度 | 說明 |
| ------ | ----------- |
| **[!UICONTROL 收到的設定檔]** | 在激活流中接收的配置檔案總數。 |
| **[!UICONTROL 啟用的身分]** | 根據收到的配置檔案成功激活到目標的標識總數。 |
| **[!UICONTROL 排除的身分]** | 根據接收的配置檔案，被排除為無法激活到目標的標識總數。 由於缺少屬性或違反同意，這些身份可能被排除。 |
| **[!UICONTROL 資料大小]** | 正在激活的資料流的大小。 |
| **[!UICONTROL 檔案總數]** | 資料流中正在激活的檔案總數。 |
| **[!UICONTROL 狀態]** | 激活作業的當前狀態。 |
| **[!UICONTROL 資料流運行啟動]** | 激活作業啟動的日期和時間。 |
| **[!UICONTROL 資料流運行結束]** | 激活作業結束的日期和時間。 |
| **[!UICONTROL 資料流運行ID]** | 當前激活作業的ID。 |
| **[!UICONTROL IMS組織ID]** | 激活作業所屬的組織的ID。 |
| **[!UICONTROL 目標名稱]** | 要激活資料的目標的名稱。 |

在度量下面，將顯示一個切換選項，以便在資料流運行錯誤和段之間進行選擇。

![篩選的段操控板。 用於在資料流運行錯誤和段顯示之間切換的切換將突出顯示。](../assets/ui/monitor-segments/activation-job-details-toggle.png)

在資料流運行錯誤部分下，選擇切換以查看標識失敗或標識排除欄位。 錯誤部分包括有關錯誤代碼的詳細資訊以及失敗或排除的身份數。

![篩選的段操控板。 有關失敗或被排除的標識的資訊會突出顯示。](../assets/ui/monitor-segments/activation-job-details.png)

在段部分下，可以看到作為激活作業一部分激活的段的清單。 使用搜索欄按名稱篩選段清單。

![篩選的段操控板。 有關失敗或被排除的標識的資訊會突出顯示。](../assets/ui/monitor-segments/activation-job-details-segments.png)

對於段部分，可以使用以下度量：

| 量度 | 說明 |
| ------ | ----------- |
| **[!UICONTROL 名稱]** | 已激活的段的名稱。 |
| **[!UICONTROL 啟用的身分]** | 根據收到的配置檔案成功激活到目標的標識總數。 |
| **[!UICONTROL 排除的身分]** | 根據接收的配置檔案，被排除為無法激活到目標的標識總數。 由於缺少屬性或違反同意，這些身份可能被排除。 |
| **[!UICONTROL 上次資料流運行狀態]** | 為該段運行的上次激活作業的狀態。 |
| **[!UICONTROL 上次資料流運行日期]** | 為該段運行的上次激活作業的日期和時間。 |

### 評估作業詳細資訊 {#evaluation-job-details}

「評估作業資料流運行詳細資料」頁顯示有關運行度量和與段作業相關的段的資訊。 評估作業是一個非同步過程，它基於指定段建立訪問群體段。 要瞭解有關評估作業的詳細資訊，請閱讀有關 [評估段](../../segmentation/tutorials/evaluate-a-segment.md#evaluate-a-segment)。

![評估作業儀表板。 將顯示有關段評估作業的資訊。](../assets/ui/monitor-segments/evaluation-job-details.png)

以下度量可用於此儀表板視圖：

| 量度 | 說明 |
| ------ | ----------- |
| **[!UICONTROL 配置檔案總數]** | 正在評估的配置檔案總數。 |
| **[!UICONTROL 狀態]** | 評估作業的狀態。 評估作業的可能狀態包括 **[!UICONTROL 成功]** 和 **[!UICONTROL 失敗]**。 |
| **[!UICONTROL 作業開始]** | 評估作業開始的日期和時間。 |
| **[!UICONTROL 作業結束]** | 評估作業結束的日期和時間。 |
| **[!UICONTROL 作業類型]** | 段作業的類型。 在這種情況下，它將始終是一個段評估作業。 |
| **[!UICONTROL 評估類型]** | 正在執行的評估類型。 這可以是 **[!UICONTROL 批]** 或 **[!UICONTROL 流]**。 |
| **[!UICONTROL 作業ID]** | 評估作業的ID。 |
| **[!UICONTROL IMS組織ID]** | 評估作業所屬組織的ID。 |
| **[!UICONTROL 段名稱]** | 正被評估的段的名稱。 |
| **[!UICONTROL 段ID]** | 正在計算的段的ID。 |

在「段」(segments)部分下，可以看到作為評估作業一部分進行評估的段的清單。 可以使用搜索欄按名稱篩選段清單。

>[!IMPORTANT]
>
>此儀表板視圖當前支援多達800個段度量。

對於段部分，可以使用以下度量：

| 量度 | 說明 |
| ------ | ----------- |
| **[!UICONTROL 名稱]** | 正被評估的段的名稱。 |
| **[!UICONTROL 設定檔計數]** | 正在評估的配置檔案數。 |

## 監視段作業控制面板 {#monitoring-segment-jobs-dashboard}

>[!CONTEXTUALHELP]
>id="platform_monitoring_segment_jobs"
>title="區段作業"
>abstract="區段作業視圖會包含有關所有區段的評估和匯出作業的資訊。"

訪問 **[!UICONTROL 段作業]** 儀表板，選擇 **[!UICONTROL 監視]** (![監視表徵圖](../assets/ui/monitor-destinations/monitoring-icon.png))。 在 [!UICONTROL 監視] ，選擇 **[!UICONTROL 段作業]**。 的 [!UICONTROL 監視] 儀表板包含有關段評估和導出作業的度量和資訊。

>[!NOTE]
>
>僅 **段評估任務** 支援每段監視。 段導出作業僅支援組織級監視。

![段作業監視控制面板](../assets/ui/monitor-segments/segment-jobs-dashboard.png)

使用 [!UICONTROL 段作業] 控制面板，以便瞭解配置檔案評估和導出是否按時進行且無任何例外，因此用於目標激活的下游服務可以具有最新評估的配置檔案資料。

以下度量可用於段作業：

| 量度 | 說明 |
---------|----------|
| **[!UICONTROL 段任務]** | 指示段作業的名稱。 |
| **[!UICONTROL 類型]** | 指示段作業的類型 — 導出或評估。 請注意，在這兩種情況下，段任務都會評估或導出 **全部** 屬於組織的段。 要瞭解有關導出作業的詳細資訊，請閱讀 [導出作業終結點](../../segmentation/api/export-jobs.md)。 要瞭解有關評估作業的詳細資訊，請閱讀有關 [評估段](../../segmentation/tutorials/evaluate-a-segment.md#evaluate-a-segment)。 |
| **[!UICONTROL 作業開始]** | 段作業開始的日期和時間。 |
| **[!UICONTROL 作業結束]** | 段任務完成的日期和時間。 |
| **[!UICONTROL 狀態]** | 已完成作業的狀態。 段作業的可能狀態包括成功或失敗。 |
