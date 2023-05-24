---
keywords: Experience Platform；首頁；熱門主題；監視器配置檔案；監視資料流；資料流；配置檔案；即時客戶配置檔案；
description: 即時客戶概要檔案通過組合來自多個渠道的資料（包括線上、離線、CRM和第三方），讓您可以查看每個客戶的整體視圖。 本教程提供有關如何使用Experience Platform用戶介面使用配置檔案監視資料流的說明。
title: 監視UI中配置檔案的資料流
type: Tutorial
exl-id: 00b624b2-f6d1-4ef2-abf2-52cede89b684
source-git-commit: 1a7ba52b48460d77d0b7695aa0ab2d5be127d921
workflow-type: tm+mt
source-wordcount: '1074'
ht-degree: 9%

---

# 監視UI中配置檔案的資料流

即時客戶概要檔案通過組合來自多個渠道的資料（包括線上、離線、CRM和第三方），讓您可以查看每個客戶的整體視圖。 個人檔案可讓您將客戶資料合併成統一的檢視畫面，針對每個客戶互動提供可採取行動且附有時間戳記的說明。

監控面板可以直觀地表示資料在配置檔案內的活動，包括資料配置檔案的狀態。 本教程提供了有關如何使用監視儀表板使用Experience Platform用戶介面監視資料的配置檔案的說明，使您能夠跟蹤配置檔案處理的狀態。

## 快速入門 {#getting-started}

本指南要求對Adobe Experience Platform的下列組成部分有工作上的理解：

- [資料流](../home.md):資料流是跨平台移動資料的資料作業的表示形式。 資料流是跨不同服務配置的，有助於將資料從源連接器移動到目標資料集 [!DNL Identity] 和 [!DNL Profile], [!DNL Destinations]。
   - [資料流運行](../../sources/notifications.md):資料流運行是基於所選資料流的頻率配置的定期調度作業。
- [即時客戶配置檔案](../../profile/home.md):基於來自多個源的聚合資料提供統一、即時的用戶配置檔案。
- [沙箱](../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙箱，將單個沙箱 [!DNL Platform] 實例到獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

## 監視配置檔案儀表板 {#profile-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_profile_processing"
>title="設定檔處理"
>abstract="設定檔處理視圖會包含有關擷取至設定檔服務的記錄的資訊，包括建立的設定檔片段數、更新的設定檔片段數以及設定檔片段總數。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_profile"
>title="資料流執行詳細資訊"
>abstract="資料流執行詳細資訊頁面會顯示有關設定檔資料流執行的詳細資訊，包括其組織 ID 和資料流執行 ID。"

訪問 **[!UICONTROL 配置檔案]** 儀表板，選擇 **[!UICONTROL 監視]** 的子菜單。 在 **[!UICONTROL 監視]** ，選擇 **[!UICONTROL 配置檔案]** 卡。

![配置式卡。 顯示有關接收的記錄數、建立和更新的配置檔案片段數以及成功率的資訊。](../assets/ui/monitor-profiles/focus-card.png)

主 **[!UICONTROL 配置檔案]** 儀表板， **[!UICONTROL 配置檔案]** 該卡顯示有關已接收記錄總數、建立和更新的配置檔案片段數以及建立和更新的配置檔案片段成功率的資訊。

儀表板本身包含有關配置檔案處理的度量。 預設情況下，控制面板將顯示組織過去24小時來源的配置檔案處理詳細資訊。

![配置式操控板。 將顯示有關每個源接收的配置檔案記錄數的資訊。](../assets/ui/monitor-profiles/sources.png)

的 [!UICONTROL 配置檔案處理] 頁面包含接收到的記錄的資訊 [!DNL Profile]包括建立的配置檔案片段數、更新的配置檔案片段數和配置檔案片段總數。

以下度量可用於此儀表板視圖：

| 量度 | 說明 |
| -------| ----------- |
| **[!UICONTROL 源名稱]** | 源的名稱。 |
| **[!UICONTROL 已收到的記錄]** | 從資料湖接收的記錄數。 |
| **[!UICONTROL 失敗的記錄]** | 攝入但未進入的記錄數 [!DNL Profile] 錯誤。 |
| **[!UICONTROL 已建立配置檔案片段]** | 淨新數 [!DNL Profile] 已添加片段。 |
| **[!UICONTROL 已更新配置檔案片段]** | 現有數量 [!DNL Profile] 片段已更新。 |
| **[!UICONTROL 配置檔案碎片總數]** | 寫入的記錄總數 [!DNL Profile]，包括所有現有 [!DNL Profile] 片段更新和新 [!DNL Profile] 已建立片段。 |
| **[!UICONTROL 失敗的資料流總數]** | 失敗的資料流運行數。 |

可以選擇篩選器表徵圖 ![「篩選器」表徵圖](../assets/ui/monitor-profiles/filter.png) 在源名稱旁邊，查看該選定源的資料流的配置檔案處理資訊。

![過濾器表徵圖將突出顯示。 選擇此表徵圖可以查看所選源的資料流。](../assets/ui/monitor-profiles/sources-filter.png)

或者，可以選擇 **[!UICONTROL 資料流]** 在切換時查看組織過去24小時資料流的配置檔案處理詳細資訊。

![配置式操控板。 將顯示有關每個資料流接收的配置檔案記錄數的資訊。](../assets/ui/monitor-profiles/dataflows.png)

以下度量可用於此儀表板視圖：

| 量度 | 說明 |
| -------| ----------- |
| **[!UICONTROL 資料流]** | 資料流的名稱。 |
| **[!UICONTROL 資料集]** | 資料流要插入的資料集的名稱。 |
| **[!UICONTROL 源名稱]** | 資料流所屬的源的名稱。 |
| **[!UICONTROL 已收到的記錄**] | 從資料湖接收的記錄數。 |
| **[!UICONTROL 失敗的記錄]** | 攝入但未進入的記錄數 [!DNL Profile] 錯誤。 |
| **[!UICONTROL 已建立配置檔案片段]** | 淨新數 [!DNL Profile] 已添加片段。 |
| **[!UICONTROL 已更新配置檔案片段]** | 現有數量 [!DNL Profile] 片段更新 |
| **[!UICONTROL 配置檔案碎片總數]** | 寫入的記錄總數 [!DNL Profile]，包括所有現有 [!DNL Profile] 片段更新和新 [!DNL Profile] 已建立片段。 |
| **[!UICONTROL 失敗的流運行總數]** | 失敗的資料流運行數。 |
| **[!UICONTROL 上次活動]** | 上次運行資料流的時間戳。 |

選擇篩選器表徵圖 ![濾波器](../assets/ui/monitor-profiles/filter.png) 在資料流運行開始時間旁邊，查看有關 [!DNL Profile] 資料流運行。

![過濾器表徵圖將突出顯示。 選擇此表徵圖可查看有關所選資料流的詳細資訊。](../assets/ui/monitor-profiles/dataflows-filter.png)

的 [!UICONTROL 資料流運行詳細資訊] 頁面顯示有關 [!DNL Profile] 資料流運行，包括其組織ID和資料流運行ID。 此頁還顯示由提供的相應錯誤代碼和錯誤消息 [!DNL Profile]，是否在攝取過程中出現任何錯誤。

![將顯示一個顯示有關所選資料流的詳細資訊的儀表板。](../assets/ui/monitor-profiles/dataflow-run-details.png)

以下度量可用於此儀表板視圖：

| 量度 | 說明 |
| -------| ----------- |
| **[!UICONTROL 已收到的記錄]** | 從資料湖接收的記錄數。 |
| **[!UICONTROL 失敗的記錄]** | 攝入但未進入的記錄數 [!DNL Profile] 錯誤。 |
| **[!UICONTROL 已建立配置檔案片段]** | 淨新數 [!DNL Profile] 已添加片段。 |
| **[!UICONTROL 已更新配置檔案片段]** | 現有數量 [!DNL Profile] 片段已更新。 |
| **[!UICONTROL 狀態]** | 定義資料流的總體狀態。 可能的狀態值為： <ul><li>`Success`:指示資料流處於活動狀態，並且正在根據提供的計畫接收資料。</li><li>`Failed`:指示資料流的激活過程因錯誤而中斷。 </li><li>`Processing`:指示資料流尚未處於活動狀態。 建立新資料流後，通常會立即遇到此狀態。</li></ul> |
| **[!UICONTROL 資料流運行啟動]** | 資料流開始運行的日期和時間。 |
| **[!UICONTROL 上次更新時間]** | 上次更新資料流的日期和時間。 |
| **[!UICONTROL 錯誤摘要]** | 如果資料流運行失敗，則顯示錯誤代碼和資料流運行失敗原因的摘要。 |
| **[!UICONTROL 資料流運行ID]** | 資料流運行的ID。 |
| **[!UICONTROL IMS組織ID]** | 資料流運行所屬的組織ID。 |

此外，您可以選擇切換來查看記錄失敗或跳過記錄。 錯誤部分包括有關錯誤代碼的詳細資訊以及失敗或排除的記錄數。
