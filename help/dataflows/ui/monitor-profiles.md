---
keywords: Experience Platform；首頁；熱門主題；監視器設定檔；監視資料流；資料流；設定檔；即時客戶設定檔；
description: 「即時客戶設定檔」可讓您結合來自多個管道的資料，包括線上、離線、CRM和協力廠商，進而全面了解每個客戶。 本教學課程提供有關如何使用Experience Platform用戶介面使用配置式監視資料流的說明。
title: 監視UI中配置檔案的資料流
topic-legacy: overview
type: Tutorial
exl-id: 00b624b2-f6d1-4ef2-abf2-52cede89b684
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1074'
ht-degree: 3%

---

# 監視UI中設定檔的資料流

「即時客戶設定檔」可讓您結合來自多個管道的資料，包括線上、離線、CRM和協力廠商，進而全面了解每個客戶。 個人檔案可讓您將客戶資料合併成統一的檢視畫面，針對每個客戶互動提供可採取行動且附有時間戳記的說明。

監控控制面板提供設定檔中資料活動的視覺表示，包括資料的設定檔狀態。 本教學課程提供相關指示，說明如何使用監控控制面板，透過Experience Platform使用者介面監控您資料的設定檔，讓您追蹤設定檔處理的狀態。

## 快速入門 {#getting-started}

本指南需要妥善了解下列Adobe Experience Platform元件：

- [資料流](../home.md):資料流是跨平台移動資料的資料作業的表示。 資料流可跨不同的服務進行配置，有助於將資料從源連接器移動到目標資料集 [!DNL Identity] 和 [!DNL Profile]和 [!DNL Destinations].
   - [資料流運行](../../sources/notifications.md):資料流運行是基於所選資料流的頻率配置的循環調度作業。
- [即時客戶個人檔案](../../profile/home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。
- [沙箱](../../sandboxes/home.md): [!DNL Experience Platform] 提供可分割單一沙箱的虛擬沙箱 [!DNL Platform] 例項放入個別的虛擬環境，以協助開發及改進數位體驗應用程式。

## 監控設定檔控制面板 {#profile-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_profile_processing"
>title="設定檔處理"
>abstract="設定檔處理檢視包含擷取至設定檔服務的記錄相關資訊，包括建立的設定檔片段數、更新的設定檔片段數，以及設定檔片段總數。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_profile"
>title="資料流運行詳細資訊"
>abstract="「資料流運行詳細資訊」頁顯示了有關配置檔案資料流運行的詳細資訊，包括其組織ID和資料流運行ID。"

若要存取 **[!UICONTROL 設定檔]** 控制面板，選取 **[!UICONTROL 監控]** 的下一頁。 一次 **[!UICONTROL 監控]** 頁面，選擇 **[!UICONTROL 設定檔]** 卡片。

![設定檔卡。 會顯示接收的記錄數、建立和更新的設定檔片段數，以及成功率的相關資訊。](../assets/ui/monitor-profiles/focus-card.png)

主要 **[!UICONTROL 設定檔]** 控制面板、 **[!UICONTROL 設定檔]** 「 」卡片顯示接收的記錄總數、建立和更新的設定檔片段數，以及建立和更新的設定檔片段成功率的相關資訊。

控制面板本身包含關於設定檔處理的量度。 依預設，控制面板會顯示貴組織過去24小時來源的設定檔處理詳細資料。

![設定檔控制面板。 系統會顯示每個來源收到的設定檔記錄數的相關資訊。](../assets/ui/monitor-profiles/sources.png)

此 [!UICONTROL 設定檔處理] 頁面包含擷取至的記錄資訊 [!DNL Profile]，包括建立的設定檔片段數、更新的設定檔片段數，以及設定檔片段總數。

此控制面板檢視可使用下列量度：

| 量度 | 說明 |
| -------| ----------- |
| **[!UICONTROL 源名稱]** | 源的名稱。 |
| **[!UICONTROL 收到的記錄]** | 從資料湖接收的記錄數。 |
| **[!UICONTROL 記錄失敗]** | 已擷取但未擷取至 [!DNL Profile] 錯誤。 |
| **[!UICONTROL 建立的設定檔片段]** | 新淨數 [!DNL Profile] 新增片段。 |
| **[!UICONTROL 已更新設定檔片段]** | 現有的 [!DNL Profile] 片段已更新。 |
| **[!UICONTROL 設定檔片段總計]** | 寫入的記錄總數 [!DNL Profile]，包括所有現有 [!DNL Profile] 片段已更新並新增 [!DNL Profile] 已建立片段。 |
| **[!UICONTROL 失敗的資料流總數]** | 失敗的資料流運行數。 |

您可以選取篩選圖示 ![篩選圖示](../assets/ui/monitor-profiles/filter.png) ，查看所選源資料流的配置檔案處理資訊。

![篩選器圖示會反白顯示。 選中此表徵圖可讓您查看所選源的資料流。](../assets/ui/monitor-profiles/sources-filter.png)

或者，您也可以選取 **[!UICONTROL 資料流]** 切換，查看組織過去24小時資料流的設定檔處理詳細資料。

![設定檔控制面板。 將顯示有關每個資料流接收的配置檔案記錄數的資訊。](../assets/ui/monitor-profiles/dataflows.png)

此控制面板檢視可使用下列量度：

| 量度 | 說明 |
| -------| ----------- |
| **[!UICONTROL 資料流]** | 資料流的名稱。 |
| **[!UICONTROL 資料集]** | 資料流要插入的資料集的名稱。 |
| **[!UICONTROL 源名稱]** | 資料流所屬的源的名稱。 |
| **[!UICONTROL 收到的記錄**] | 從資料湖接收的記錄數。 |
| **[!UICONTROL 記錄失敗]** | 已擷取但未擷取至 [!DNL Profile] 錯誤。 |
| **[!UICONTROL 建立的設定檔片段]** | 新淨數 [!DNL Profile] 新增片段。 |
| **[!UICONTROL 已更新設定檔片段]** | 現有的 [!DNL Profile] 更新片段 |
| **[!UICONTROL 設定檔片段總計]** | 寫入的記錄總數 [!DNL Profile]，包括所有現有 [!DNL Profile] 片段已更新並新增 [!DNL Profile] 已建立片段。 |
| **[!UICONTROL 失敗流運行總數]** | 失敗的資料流運行數。 |
| **[!UICONTROL 上次活動]** | 上次運行資料流的時間戳。 |

選取篩選圖示 ![篩選](../assets/ui/monitor-profiles/filter.png) 資料流運行開始時間旁邊，查看有關 [!DNL Profile] 資料流運行。

![篩選器圖示會反白顯示。 選擇此表徵圖可讓您查看有關所選資料流的詳細資訊。](../assets/ui/monitor-profiles/dataflows-filter.png)

此 [!UICONTROL 資料流運行詳細資訊] 頁面會顯示您 [!DNL Profile] 資料流運行，包括其組織ID和資料流運行ID。 此頁還顯示相應的錯誤代碼和提供的錯誤消息 [!DNL Profile]，則擷取程式中會發生任何錯誤。

![將顯示一個儀表板，其中顯示有關所選資料流的詳細資訊。](../assets/ui/monitor-profiles/dataflow-run-details.png)

此控制面板檢視可使用下列量度：

| 量度 | 說明 |
| -------| ----------- |
| **[!UICONTROL 收到的記錄]** | 從資料湖接收的記錄數。 |
| **[!UICONTROL 記錄失敗]** | 已擷取但未擷取至 [!DNL Profile] 錯誤。 |
| **[!UICONTROL 建立的設定檔片段]** | 新淨數 [!DNL Profile] 新增片段。 |
| **[!UICONTROL 已更新設定檔片段]** | 現有的 [!DNL Profile] 片段已更新。 |
| **[!UICONTROL 狀態]** | 定義資料流的總體狀態。 可能的狀態值為： <ul><li>`Success`:指示資料流處於活動狀態，並正在根據資料流提供的計畫來接收資料。</li><li>`Failed`:表示資料流的激活過程因錯誤而中斷。 </li><li>`Processing`:指示資料流尚未處於活動狀態。 建立新資料流後，通常會立即出現此狀態。</li></ul> |
| **[!UICONTROL 資料流運行開始]** | 資料流開始運行的日期和時間。 |
| **[!UICONTROL 上次更新時間]** | 上次更新資料流的日期和時間。 |
| **[!UICONTROL 錯誤摘要]** | 如果資料流運行失敗，則顯示錯誤代碼和資料流運行失敗原因的摘要。 |
| **[!UICONTROL 資料流運行ID]** | 資料流運行的ID。 |
| **[!UICONTROL IMS組織ID]** | 資料流運行所屬的組織ID。 |

此外，您可以選取切換來檢視失敗記錄或已略過記錄。 「錯誤」部分包括有關錯誤代碼的詳細資訊以及失敗或排除的記錄數。
