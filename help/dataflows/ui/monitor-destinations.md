---
keywords: Experience Platform；首頁；熱門主題；監視帳戶；監視資料流；資料流；目標
description: 目標允許您將資料從Adobe Experience Platform激活到無數外部合作夥伴。 本教程提供有關如何使用Experience Platform用戶介面監視目標的資料流的說明。
solution: Experience Platform
title: 監視UI中目標的資料流
topic-legacy: overview
type: Tutorial
exl-id: 8eb7bb3c-f2dc-4dbc-9cf5-3d5d3224f5f1
source-git-commit: b66c39016b2ccd4a4e24899f9e59f9a80cdc531b
workflow-type: tm+mt
source-wordcount: '2085'
ht-degree: 0%

---

# 監視UI中目標的資料流

目標允許您將資料從Adobe Experience Platform激活到無數外部合作夥伴。 平台通過提供資料流的透明性，使跟蹤資料流到目標的過程更加輕鬆。

監視面板可以直觀地表示資料流的行程，包括資料被激活到的目標。 本教程提供了有關如何直接在目標工作區中監視資料流，或使用監視面板使用Experience Platform用戶介面監視目標的資料流的說明。

## 快速入門

本指南要求對Adobe Experience Platform的下列組成部分有工作上的理解：

- [資料流](../home.md):資料流是跨平台移動資料的資料作業的表示形式。 資料流是跨不同服務配置的，有助於將資料從源連接器移動到目標資料集 [!DNL Identity] 和 [!DNL Profile], [!DNL Destinations]。
   - [資料流運行](../../sources/notifications.md):資料流運行是基於所選資料流的頻率配置的定期調度作業。
- [目標](../../destinations/home.md):目標是預構建的與常用應用程式的整合，這些整合允許從平台無縫激活資料，用於跨渠道營銷活動、電子郵件活動、目標廣告和許多其他使用案例。
- [沙箱](../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙箱，將單個沙箱 [!DNL Platform] 實例到獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

## 監視目標工作區中的資料流 {#monitor-dataflows-in-the-destinations-workspace}

在 **[!UICONTROL 目標]** 工作區，導航到 **[!UICONTROL 瀏覽]** 頁籤，然後選擇要查看的目標名稱。

![](../assets/ui/monitor-destinations/select-destination.png)

此時將顯示現有資料流的清單。 此頁上是可查看資料流的清單，包括有關其目標、用戶名、資料流數和狀態的資訊。

有關狀態的詳細資訊，請參閱下表：

| 狀態 | 說明 |
| ------ | ----------- |
| 啟用 | 的 `Enabled` 狀態表示資料流處於活動狀態，並正在根據提供的計畫導出資料。 |
| 停用 | 的 `Disabled` 狀態表示資料流處於非活動狀態，且未導出任何資料。 |
| 正在處理 | 的 `Processing` 狀態表示資料流尚未處於活動狀態。 建立新資料流後，通常會立即遇到此狀態。 |
| 錯誤 | 的 `Error` 狀態表示資料流的激活過程已中斷。 |

### 流目標的資料流運行 {#dataflow-runs-for-streaming-destinations}

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesactivated"
>title="已激活身份"
>abstract="已成功激活到選定目標的單個配置檔案標識的計數。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesexcluded"
>title="排除的身份"
>abstract="基於丟失的屬性和同意違規而從選定目標的激活中排除的單個配置檔案記錄的計數。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesfailed"
>title="標識失敗"
>abstract="所選目標失敗的單個配置檔案標識的計數。 有關詳細資訊，請檢查錯誤診斷。"
>additional-url="https://adobe.com/go/destinations-monitor-dataflows-batch-en" text="瞭解有關文檔的詳細資訊"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_activation_streaming"
>title="資料流運行詳細資訊"
>abstract="目標資料流運行詳細資訊包含有關段的激活狀態和從即時客戶配置檔案獲取的度量的資訊，以生成唯一標識。 要瞭解更多資訊，請查看度量定義指南。"

>[!CONTEXTUALHELP]
>id="platform_monitoring_profiles_received_streaming"
>title="收到的配置檔案"
>abstract="在資料流中接收的配置檔案總數。 此值每60分鐘更新一次。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesactivated_streaming"
>title="已激活身份"
>abstract="已成功激活到選定目標的單個配置檔案標識的計數。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesexcluded_streaming"
>title="排除的身份"
>abstract="基於丟失的屬性和同意違規而從選定目標的激活中排除的單個配置檔案記錄的計數。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesfailed_streaming"
>title="標識失敗"
>abstract="所選目標失敗的單個配置檔案標識的計數。 有關詳細資訊，請檢查錯誤診斷。"
>text="Learn more in documentation"

對於流目標， [!UICONTROL 資料流運行] 頁籤為資料流運行上的度量資料提供每小時更新。 標有標識的最顯赫統計資料是身份。

標識表示輪廓的不同小平面。 例如，如果配置檔案同時包含電話號碼和電子郵件地址，則該配置檔案將具有兩個身份。

將顯示單個運行及其特定度量的清單，以及以下標識總計：

- **[!UICONTROL 已激活身份]**:為激活而建立或更新的配置檔案標識的總數。
- **[!UICONTROL 排除的身份]**:基於缺少屬性和同意違規而跳過用於激活的配置檔案標識總數。
- **[!UICONTROL 標識失敗]**:由於錯誤而未激活到目標的配置檔案標識總數。

![](../assets/ui/monitor-destinations/dataflow-runs-stream.png)

每個資料流運行都顯示以下詳細資訊：

- **[!UICONTROL 資料流運行啟動]**:資料流運行於的時間。
- **[!UICONTROL 處理時間]**:資料流處理所花費的時間。
- **[!UICONTROL 收到的配置檔案]**:在資料流中接收的配置檔案總數。
- **[!UICONTROL 已激活身份]**:成功激活到選定目標的配置檔案標識總數。
- **[!UICONTROL 排除的身份]**:基於缺少屬性和同意違規而被排除在激活中的配置檔案標識總數。
- **[!UICONTROL 標識失敗]** 由於錯誤而未激活到目標的配置檔案標識總數。
- **[!UICONTROL 激活率]**:已成功激活或跳過的已接收標識的百分比。 以下公式說明如何計算此值：
   ![](../assets/ui/monitor-destinations/activation-rate-formula.png)
- **[!UICONTROL 狀態]**:表示資料流的狀態：或 [!UICONTROL 已完成] 或 [!UICONTROL 處理]。 [!UICONTROL 已完成] 表示在1小時內導出了相應資料流運行的所有標識。 [!UICONTROL 處理] 表示資料流運行尚未完成。

要查看特定資料流運行的詳細資訊，請從清單中選擇運行的開始時間。

資料流運行的詳細資訊頁包含其他資訊，如接收的配置檔案數、激活的標識數、失敗的標識數和排除的標識數。

![](../assets/ui/monitor-destinations/dataflow-details-stream.png)

詳細資訊頁面還顯示失敗的標識清單和排除的標識。 將顯示失敗和排除身份的資訊，包括錯誤代碼、身份計數和說明。 預設情況下，清單顯示失敗的標識。 要顯示跳過的標識，請選擇 **[!UICONTROL 排除的身份]** 切換。

![](../assets/ui/monitor-destinations/dataflow-records-stream.png)

### 為批處理目標運行資料流 {#dataflow-runs-for-batch-destinations}

>[!CONTEXTUALHELP]
>id="platform_monitoring_profiles_received"
>title="收到的配置檔案"
>abstract="在資料流中接收的配置檔案總數。 此值每60分鐘更新一次。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_activation"
>title="資料流運行詳細資訊"
>abstract="目標資料流運行詳細資訊包含有關段的激活狀態和從即時客戶配置檔案獲取的度量的資訊，以生成唯一標識。 要瞭解更多資訊，請查看度量定義指南。"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_activation_batch"
>title="資料流運行詳細資訊"
>abstract="目標資料流運行詳細資訊包含有關段的激活狀態和從即時客戶配置檔案獲取的度量的資訊，以生成唯一標識。 要瞭解更多資訊，請查看度量定義指南。"

>[!CONTEXTUALHELP]
>id="platform_monitoring_profiles_received_batch"
>title="收到的配置檔案"
>abstract="在資料流中接收的配置檔案總數。 此值每60分鐘更新一次。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesactivated_batch"
>title="已激活身份"
>abstract="已成功激活到選定目標的單個配置檔案標識的計數。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesexcluded_batch"
>title="排除的身份"
>abstract="基於丟失的屬性和同意違規而從選定目標的激活中排除的單個配置檔案記錄的計數。"
>text="Learn more in documentation"

對於批目標， [!UICONTROL 資料流運行] 頁籤提供資料流運行的度量資料。 將顯示單個運行及其特定度量的清單，以及以下標識總計：

- **[!UICONTROL 已激活身份]**:已成功激活到選定目標的單個配置檔案標識的計數。
- **[!UICONTROL 排除的身份]**:基於缺少的屬性和同意違規，從選定目標的激活中排除的單個配置檔案標識的計數。

![](../assets/ui/monitor-destinations/dataflow-runs-batch.png)

每個資料流運行都顯示以下詳細資訊：

- **[!UICONTROL 資料流運行啟動]**:資料流運行於的時間。
- **[!UICONTROL 處理時間]**:處理資料流運行所花費的時間。
- **[!UICONTROL 收到的配置檔案]**:在資料流中接收的配置檔案總數。 此值每60分鐘更新一次。
- **[!UICONTROL 已激活身份]**:成功激活到選定目標的配置檔案標識總數。
- **[!UICONTROL 排除的身份]**:基於缺少屬性和同意違規而被排除在激活中的配置檔案標識總數。
- **[!UICONTROL 狀態]**:表示資料流處於的狀態。 這可以是三個狀態之一： [!UICONTROL 成功]。 [!UICONTROL 失敗], [!UICONTROL 處理]。 [!UICONTROL 成功] 表示資料流處於活動狀態，並正在根據其提供的時間表導出資料。 [!UICONTROL 失敗] 表示由於錯誤而暫停了資料的激活。 [!UICONTROL 處理] 表示資料流尚未處於活動狀態，並且通常在建立新資料流時遇到。

要查看特定資料流運行的詳細資訊，請從清單中選擇運行的開始時間。

>[!NOTE]
>
>根據目標資料流的調度頻率生成資料流運行。 對應用於段的每個合併策略執行單獨的資料流運行。

資料流的「詳細資訊」頁除了資料流清單中顯示的詳細資訊之外，還顯示了有關資料流的更具體資訊：

- **[!UICONTROL 資料大小]**:正在導出的資料流的大小。
- **[!UICONTROL 檔案總數]**:資料流中導出的檔案總數。
- **[!UICONTROL 上次更新時間]**:上次更新資料流運行的時間。

![](../assets/ui/monitor-destinations/dataflow-batch.png)

詳細資訊頁面還顯示失敗的標識清單和排除的標識。 將顯示失敗標識和排除標識的資訊，包括錯誤代碼和說明。 預設情況下，清單顯示失敗的標識。 要顯示排除的身份，請選擇 **[!UICONTROL 排除的身份]** 切換。

![](../assets/ui/monitor-destinations/dataflow-records-batch.png)

## 監視目標儀表板 {#monitoring-destinations-dashboard}

>[!CONTEXTUALHELP]
>id="platform_monitoring_activation"
>title="啟用"
>abstract="目標激活包含有關段的激活狀態和從即時客戶配置檔案獲取的度量的資訊，以生成唯一標識。"

>[!CONTEXTUALHELP]
>id="platform_monitoring_segment_jobs"
>title="段作業"
>abstract="段作業控制面板包含有關所有段的評估和導出作業的資訊。"

訪問 [!UICONTROL 監視] 儀表板，選擇 **[!UICONTROL 監視]** (![監視表徵圖](../assets/ui/monitor-destinations/monitoring-icon.png))。 在 [!UICONTROL 監視] ，選擇 [!UICONTROL 目標]。 的 [!UICONTROL 監視] 儀表板包含有關目標運行作業的度量和資訊。

儀表板的中心是「激活」面板，其中包含用於顯示導出到目的地的資料激活速率資料的度量和圖形。

![](../assets/ui/monitor-destinations/dashboard-graph.png)


預設情況下，顯示的資料包含過去24小時的激活率。 選擇 **[!UICONTROL 過去24小時]** 來調整顯示的記錄的時間範圍。 可用選項包括 **[!UICONTROL 過去24小時]**。 **[!UICONTROL 最後七天]**, **[!UICONTROL 最後三十天]**。 或者，您也可以在顯示的日曆彈出窗口中選擇日期。 選擇日期後，選擇 **[!UICONTROL 應用]** 來調整顯示的資訊的時間框。

>[!NOTE]
>
>以下螢幕快照顯示了過去30天而不是過去24小時的激活率。 通過選擇 **[!UICONTROL 最後三十天]**。

![](../assets/ui/monitor-destinations/dashboard-graph-change-date-range.png)

預設情況下，圖形會顯示，您可以禁用它以展開下面的目標清單。 選擇 **[!UICONTROL 度量和圖形]** 切換以禁用圖形。

的 **[!UICONTROL 激活]** 面板顯示至少包含一個現有帳戶的目標清單。 此清單還包括有關接收的配置檔案、激活的配置檔案記錄、失敗的配置檔案記錄、跳過的配置檔案記錄、失敗的資料流總數以及這些目標的上次更新日期的資訊。

![](../assets/ui/monitor-destinations/dashboard-destinations.png)

您還可以過濾目標清單，以僅顯示選定的目標類別。 選擇 **[!UICONTROL 我的目的地]** 下拉，然後選擇要篩選的目標類型。

![](../assets/ui/monitor-destinations/dashboard-destinations-filter-dropdown.png)

此外，您可以在搜索欄中輸入目標，以隔離到單個目標。 如果要查看目標的資料流，可以選擇篩選器 ![濾波器](../assets/ui/monitor-destinations/filter.png) 清單。

![](../assets/ui/monitor-destinations/filtered-destinations.png)

如果要查看所有目標中的所有現有資料流，請選擇 **[!UICONTROL 資料流]**。

此時將顯示資料流清單，按目標分組。 通過查找要監視的目標，選擇篩選器，可以查看特定資料流的其他詳細資訊 ![濾波器](../assets/ui/monitor-destinations/filter.png) 旁邊，然後選取 ![濾波器](../assets/ui/monitor-destinations/filter.png) 的子目錄。

![](../assets/ui/monitor-destinations/dashboard-dataflows.png)


「資料流運行」頁顯示有關資料流運行的資訊，包括資料流運行開始時間、處理時間、接收的配置檔案、激活的標識、排除的標識、標識失敗、激活率和狀態。 要查看有關特定資料流運行的詳細資訊，請選擇篩選器 ![濾波器](../assets/ui/monitor-destinations/filter.png) 資料流運行開始時間旁邊。

![](../assets/ui/monitor-destinations/dashboard-dataflows-filter.png)

「資料流詳細資料」頁除了資料流清單中顯示的詳細資料外，還顯示有關資料流的更具體資訊：

- **[!UICONTROL 資料流運行ID]**:資料流的ID。
- **[!UICONTROL IMS組織ID]**:資料流所屬的IMS組織。
- **[!UICONTROL 上次更新時間]**:上次更新資料流運行的時間。

詳細資訊頁面還顯示失敗的標識清單和排除的標識。 將顯示失敗和排除身份的資訊，包括錯誤代碼、身份計數和說明。 預設情況下，清單顯示失敗的標識。 要顯示跳過的標識，請選擇 **[!UICONTROL 排除的身份]** 切換。

![](../assets/ui/monitor-destinations/identities-excluded.png)

## 後續步驟

通過遵循本指南，您現在知道如何監視批處理和流式處理目標的資料流，包括處理時間、激活率和狀態等所有相關資訊。 要瞭解有關平台中資料流的詳細資訊，請閱讀 [資料流概述](../home.md)。 要瞭解有關目標的詳細資訊，請閱讀 [目標概述](../../destinations/home.md)。