---
keywords: Experience Platform；首頁；熱門主題；監視器標識；監視器資料流；資料流；標識；
description: Adobe Experience Platform身份服務通過跨設備和系統橋接身份，讓您能夠全面瞭解客戶及其行為，讓您能夠即時提供有影響的個人數字型驗。 本教程提供了有關如何使用Experience Platform用戶介面使用標識監視資料流的說明。
title: 監視UI中標識的資料流
type: Tutorial
exl-id: 735b0e52-74f6-47fe-98c6-e12a633b6f57
source-git-commit: 1a7ba52b48460d77d0b7695aa0ab2d5be127d921
workflow-type: tm+mt
source-wordcount: '1149'
ht-degree: 8%

---

# 監視UI中標識的資料流

Adobe Experience Platform身份服務通過跨設備和系統橋接身份，讓您能夠全面瞭解客戶及其行為，讓您能夠即時提供有影響的個人數字型驗。

監控面板可以直觀地表示資料在標識內的活動，包括資料標識的狀態。 本教程提供了有關如何使用監視儀表板使用Experience Platform用戶介面監視資料身份的說明，使您能夠跟蹤身份處理的狀態。

## 快速入門 {#getting-started}

- [資料流](../home.md):資料流是跨平台移動資料的資料作業的表示形式。 資料流是跨不同服務配置的，有助於將資料從源連接器移動到目標資料集 [!DNL Identity] 和 [!DNL Profile], [!DNL Destinations]。
   - [資料流運行](../../sources/notifications.md):資料流運行是基於所選資料流的頻率配置的定期調度作業。
- [身份服務](../../identity-service/home.md):通過跨設備和系統橋接身份，更好地瞭解單個客戶及其行為。
- [沙箱](../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙箱，將單個沙箱 [!DNL Platform] 實例到獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

## 監視身份儀表板 {#identity-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_identity_processing"
>title="身分識別處理"
>abstract="身分識別處理視圖會包含有關擷取到身分識別服務的記錄的資訊，包括新增的身分識別數量、建立的圖表和更新的圖表。檢閱量度定義指南以了解有關量度和圖表的詳細資訊。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_identity"
>title="資料流執行詳細資訊"
>abstract="資料流執行詳細資訊頁面會顯示有關身分識別資料流執行的詳細資訊，包括其組織 ID 和資料流執行 ID。"

訪問 **[!UICONTROL 身份]** 儀表板，選擇 **[!UICONTROL 監視]** 的子菜單。 在 **[!UICONTROL 監視]** ，選擇 **[!UICONTROL 身份]** 卡。

![身份證。 顯示有關已接收記錄數、已接收記錄數和成功率的資訊。](../assets/ui/monitor-identities/focus-card.png)

主 **[!UICONTROL 身份]** 儀表板， **[!UICONTROL 身份]** 卡顯示了有關已接收記錄總數、已接收記錄數以及記錄接收成功率的資訊。

儀表板本身包含有關身份處理的度量。 預設情況下，控制面板將顯示組織過去24小時的源的身份處理詳細資訊。

![標識儀表板。 顯示有關每個源接收的記錄數的資訊。](../assets/ui/monitor-identities/sources.png)

的 [!UICONTROL 身份處理] 頁面包含接收到的記錄的資訊 [!DNL Identity Service]，包括添加的標識數、建立的圖形和更新的圖形數。

以下度量可用於此儀表板視圖：

| 標識度量 | 說明 |
| ---------------- | ----------- |
| **[!UICONTROL 已收到的記錄]** | 從資料湖接收的記錄數。 |
| **[!UICONTROL 失敗的記錄]** | 由於資料中的錯誤而未接收到平台的記錄數。 |
| **[!UICONTROL 略過的記錄]** | 攝入但未進入的記錄數 [!DNL Identity Service] 因為記錄行中只有一個標識符。 |
| **[!UICONTROL 已擷取的記錄]** | 接收到的記錄數 [!DNL Identity Service]。 |
| **[!UICONTROL 已添加標識]** | 添加到的淨新標識符數 [!DNL Identity Service]。 |
| **[!UICONTROL 已建立圖形]** | 在中建立的淨新標識圖數 [!DNL Identity Service]。 |
| **[!UICONTROL 圖形已更新]** | 使用新邊更新的現有標識圖形的數量。 |
| **[!UICONTROL 失敗的資料流總數]** | 失敗的資料流運行數。 |

可以選擇篩選器表徵圖 ![「篩選器」表徵圖](../assets/ui/monitor-identities/filter.png) 在源名稱旁邊，查看該選定源的資料流的身份處理資訊。

![過濾器表徵圖將突出顯示。 選擇此表徵圖可以查看所選源的資料流。](../assets/ui/monitor-identities/sources-filter.png)

或者，可以選擇 **[!UICONTROL 資料流]** 在切換時查看組織過去24小時資料流的身份處理詳細資訊。

![標識儀表板。 顯示有關每個資料流接收的標識數的資訊。](../assets/ui/monitor-identities/dataflows.png)

以下度量可用於此儀表板視圖：

| 量度 | 說明 |
| -------| ----------- |
| **[!UICONTROL 資料流]** | 資料流的名稱。 |
| **[!UICONTROL 資料集]** | 資料流要插入的資料集的名稱。 |
| **[!UICONTROL 源名稱]** | 資料流所屬的源的名稱。 |
| **[!UICONTROL 已收到的記錄]** | 從資料湖接收的記錄數。 |
| **[!UICONTROL 失敗的記錄]** | 由於資料中的錯誤而未接收到平台的記錄數。 |
| **[!UICONTROL 略過的記錄]** | 攝入但未進入的記錄數 [!DNL Identity Service] 因為記錄行中只有一個標識符。 |
| **[!UICONTROL 已擷取的記錄]** | 接收到的記錄數 [!DNL Identity Service]。 |
| **[!UICONTROL 記錄總數]** | 所有記錄（包括失敗的記錄、跳過的記錄、添加的標識和重複的記錄）的總數。 |
| **[!UICONTROL 已添加標識]** | 添加到的淨新標識符數 [!DNL Identity Service]。 |
| **[!UICONTROL 已建立圖形]** | 在中建立的淨新標識圖數 [!DNL Identity Service]。 |
| **[!UICONTROL 圖形已更新]** | 使用新邊更新的現有標識圖形的數量。 |
| **[!UICONTROL 失敗的資料流總數]** | 失敗的資料流運行數。 |

選擇篩選器表徵圖 ![濾波器](../assets/ui/monitor-identities/filter.png) 在資料流運行開始時間旁邊，查看有關 [!DNL Identity] 資料流運行。

![過濾器表徵圖將突出顯示。 選擇此表徵圖可查看有關所選資料流的詳細資訊。](../assets/ui/monitor-identities/dataflows-filter.png)

的 [!UICONTROL 資料流運行詳細資訊] 頁面顯示有關 [!DNL Identity] 資料流運行，包括其組織ID和資料流運行ID。 此頁還顯示由提供的相應錯誤代碼和錯誤消息 [!DNL Identity Service]，是否在攝取過程中出現任何錯誤。

![將顯示一個顯示有關所選資料流的詳細資訊的儀表板。](../assets/ui/monitor-identities/dataflow-run-details.png)

以下度量可用於此儀表板視圖：

| 量度 | 說明 |
| -------| ----------- |
| **[!UICONTROL 已收到的記錄]** | 從資料湖接收的記錄數。 |
| **[!UICONTROL 失敗的記錄]** | 由於資料中的錯誤而未接收到平台的記錄數。 |
| **[!UICONTROL 略過的記錄]** | 攝入但未進入的記錄數 [!DNL Identity Service] 因為記錄行中只有一個標識符。 |
| **[!UICONTROL 已擷取的記錄]** | 接收到的記錄數 [!DNL Identity Service]。 |
| **[!UICONTROL 已添加標識]** | 添加到的淨新標識符數 [!DNL Identity Service]。 |
| **[!UICONTROL 已建立圖形]** | 在中建立的淨新標識圖數 [!DNL Identity Service]。 |
| **[!UICONTROL 圖形已更新]** | 使用新邊更新的現有標識圖形的數量。 |
| **[!UICONTROL 狀態]** | 定義資料流的總體狀態。 可能的狀態值為： <ul><li>`Success`:指示資料流處於活動狀態，並且正在根據提供的計畫接收資料。</li><li>`Failed`:指示資料流的激活過程因錯誤而中斷。 </li><li>`Processing`:指示資料流尚未處於活動狀態。 建立新資料流後，通常會立即遇到此狀態。</li></ul> |
| **[!UICONTROL 資料流運行啟動]** | 資料流開始運行的日期和時間。 |
| **[!UICONTROL 上次更新時間]** | 上次更新資料流的日期和時間。 |
| **[!UICONTROL 錯誤摘要]** | 如果資料流運行失敗，則顯示錯誤代碼和資料流運行失敗原因的摘要。 |
| **[!UICONTROL 資料流運行ID]** | 資料流運行的ID。 |
| **[!UICONTROL IMS組織ID]** | 資料流運行所屬的組織ID。 |

此外，您可以選擇切換來查看記錄失敗或跳過記錄。 錯誤部分包括有關錯誤代碼的詳細資訊以及失敗或排除的記錄數。
