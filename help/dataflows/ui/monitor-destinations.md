---
description: 瞭解如何使用Experience Platform使用者介面監控目的地的資料流。
solution: Experience Platform
title: 在UI中監視目的地的資料流
type: Tutorial
exl-id: 8eb7bb3c-f2dc-4dbc-9cf5-3d5d3224f5f1
source-git-commit: 27802292a7a06f2edaea9efc39d4a63507e0e7e1
workflow-type: tm+mt
source-wordcount: '3542'
ht-degree: 10%

---

# 在UI中監視目的地的資料流

使用Experience Platform目錄中的各種目的地，從Platform向無數的外部合作夥伴啟用您的資料。 Platform藉由提供資料流透明度，讓追蹤資料流向目的地的程式變得更輕鬆。

監視儀表板可讓您以視覺化方式呈現資料流程的歷程，包括資料啟用的目的地、您要檢視的資料型別、每次資料流程執行的匯出資料等等。

本教學課程提供如何直接在目的地Workspace中監視資料流，或使用「監視」控制面板透過Experience Platform使用者介面監視目的地的資料流的說明。

## 快速入門 {#getting-started}

本指南需要您深入了解下列 Adobe Experience Platform 元件：

- [資料流](../home.md)：資料流可呈現跨平台行動資料的資料作業。 資料流是跨不同服務設定的，有助於將資料從來源聯結器移至目標資料集、移至[!DNL Identity]和[!DNL Profile]以及移至[!DNL Destinations]。
   - [資料流執行](../../sources/notifications.md)：資料流執行是根據所選資料流的頻率設定所排程的週期性工作。
- [目的地](../../destinations/home.md)：目的地是預先建置的與常用應用程式的整合，可讓您順暢地從Platform啟用資料，以用於跨管道行銷活動、電子郵件行銷活動、目標定位廣告和許多其他使用案例。
- [沙箱](../../sandboxes/home.md)： [!DNL Experience Platform]提供可將單一[!DNL Platform]執行個體分割成個別虛擬環境的虛擬沙箱，以利開發及改進數位體驗應用程式。

## 監視目的地工作區中的資料流 {#monitor-dataflows-in-the-destinations-workspace}

在Platform UI的&#x200B;**[!UICONTROL 目的地]**&#x200B;工作區中，導覽至&#x200B;**[!UICONTROL 瀏覽]**&#x200B;標籤，並選取您要檢視的目的地的名稱。

![選取目的地連線反白顯示的目的地檢視](../assets/ui/monitor-destinations/select-destination.png)

現有資料流清單隨即顯示。 此頁面是可檢視資料流的清單，包括有關其目的地、使用者名稱、資料流數量和狀態的資訊。

請參閱下表以取得狀態的詳細資訊：

| 狀態 | 說明 |
| ------ | ----------- |
| 啟用 | `Enabled`狀態表示資料流作用中，而且正在根據提供的排程匯出資料。 |
| 停用 | `Disabled`狀態表示資料流為非作用中且未匯出任何資料。 |
| 正在處理 | `Processing`狀態表示資料流尚未啟用。 此狀態通常會在建立新資料流後立即發生。 |
| 錯誤 | `Error`狀態表示資料流程的啟用程式已中斷。 |

### 用於串流目的地的資料流執行 {#dataflow-runs-for-streaming-destinations}

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_activation_streaming"
>title="資料流執行詳細資訊"
>abstract="目標資料流執行詳細資訊包含客群啟用狀態的資訊，以及取自即時客戶輪廓以產生唯一身分的量度。若要深入了解，請檢閱量度定義指南。"

>[!CONTEXTUALHELP]
>id="platform_monitoring_profiles_received_streaming"
>title="收到的設定檔"
>abstract="資料流中收到的設定檔總數。此值每 60 分鐘更新一次。"

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesactivated_streaming"
>title="啟用的身分"
>abstract="成功啟用到所選目的地之個別設定檔身分的計數。此量度包括從匯出的客群中建立、更新和刪除的身分。"

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesexcluded_streaming"
>title="排除的身分"
>abstract="根據缺少的屬性和違規行為，從所選目的地的啟用中排除的個別設定檔記錄的計數。"

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesfailed_streaming"
>title="失敗的身分"
>abstract="針對所選目的地失敗的個別設定檔身分的計數。請檢查錯誤診斷以取得詳細資料。"

針對串流目的地，[!UICONTROL 資料流執行]索引標籤會提供資料流執行上量度資料的每小時更新。 標示為最顯著的統計資料是用於身分。

身分代表設定檔的不同面向。 例如，如果設定檔同時包含電話號碼和電子郵件地址，則該設定檔有兩個身分。

接著會顯示個別執行及其特定量度的清單，以及身分的下列總計：

- **[!UICONTROL 已啟用的身分]**：已成功啟用至所選目的地的設定檔身分總數。 此量度包括從匯出的客群中建立、更新和刪除的身分。
- **[!UICONTROL 排除的身分]**：根據遺失的屬性和同意違規，略過用於啟用的設定檔身分總數。
- **[!UICONTROL 身分失敗]**：由於錯誤而未啟用到目的地的設定檔身分總數。

![串流目的地的資料流執行詳細資料。](../assets/ui/monitor-destinations/dataflow-runs-stream.png)

每個個別資料流執行會顯示下列詳細資訊：

- **[!UICONTROL 資料流執行開始]**：資料流執行開始的時間。 對於串流資料流執行，Experience Platform會以每小時量度的形式，根據資料流執行的開始擷取量度。 這表示對於串流資料流執行，如果資料流執行在例如晚上10:30開始，量度會在UI中將開始時間顯示為晚上10:00。
- **[!UICONTROL 處理時間]**：資料流執行處理所花的時間。
   - 對於&#x200B;**[!UICONTROL 已完成]**&#x200B;個執行，處理時間量度一律顯示一個小時。
   - 針對仍處於&#x200B;**[!UICONTROL 處理]**&#x200B;狀態的資料流執行，擷取所有量度的視窗會保持開啟超過一小時，以處理對應至資料流執行的所有量度。 例如，上午9:30開始的資料流執行可能會維持處理狀態1小時30分鐘，以擷取及處理所有量度。 接著，在處理視窗關閉且資料流執行更新為&#x200B;**已完成**&#x200B;的狀態後，顯示的處理時間就會變更為一小時。
- **[!UICONTROL 已接收的設定檔]**：資料流中接收的設定檔總數。
- **[!UICONTROL 已啟用的身分]**：在資料流執行過程中成功啟用至所選目的地的設定檔身分總數。 此量度包括從匯出的客群中建立、更新和刪除的身分。
- **[!UICONTROL 排除的身分]**：根據遺失的屬性和同意違規，從啟用中排除的設定檔身分總數。
- **[!UICONTROL 身分失敗]**&#x200B;由於錯誤而未啟用到目的地的設定檔身分總數。
- **[!UICONTROL 啟用率]**：已順利啟用或略過的接收身分百分比。 下列公式示範如何計算此值：
  ![啟用率公式。](../assets/ui/monitor-destinations/activation-rate-formula.png)
- **[!UICONTROL 狀態]**：代表資料流所處的狀態： [!UICONTROL 已完成]或[!UICONTROL 正在處理]。 [!UICONTROL 已完成]表示已在一小時內匯出對應資料流執行的所有身分。 [!UICONTROL 正在處理]表示資料流執行尚未完成。

若要檢視特定資料流執行的詳細資訊，請從清單中選取執行的開始時間。

資料流執行的詳細資訊頁面包含其他資訊，例如收到的設定檔數、啟用的身分數量、失敗的身分數量和排除的身分數量。

![串流目的地的資料流詳細資料。](../assets/ui/monitor-destinations/dataflow-details-stream.png)

詳細資訊頁面也會顯示失敗的身分和排除的身分清單。 會顯示失敗和已排除的身分的相關資訊，包括錯誤代碼、身分計數和說明。 依預設，清單會顯示失敗的身分。 若要顯示跳過的身分，請選取&#x200B;**[!UICONTROL 排除的身分]**&#x200B;切換。

![串流目的地的資料流記錄中反白顯示錯誤訊息。](../assets/ui/monitor-destinations/dataflow-records-stream.png)

#### (Beta)適用於串流目的地的受眾層級資料流執行監控 {#audience-level-dataflow-runs-for-streaming-destinations}

您可以檢視在對象層級劃分的啟用、排除或失敗身分的相關資訊，瞭解屬於資料流的每個對象。 串流目的地的對象層級監視目前僅適用於[[!DNL Google Customer Match + Display & Video 360] 目的地](/help/destinations/catalog/advertising/google-customer-match-dv360.md)。

![串流目的地的對象層級監視。](/help/dataflows/assets/ui/monitor-destinations/audience-level-monitoring-streaming.png)

>[!NOTE]
>
>**[!UICONTROL 受眾]**&#x200B;索引標籤中的&#x200B;**[!UICONTROL 已接收設定檔]**&#x200B;編號不一定與資料流執行已接收的設定檔數量相符。 這是因為指定的設定檔可能包含在資料流執行中啟用的多個對象。

### 用於批次目標的資料流執行 {#dataflow-runs-for-batch-destinations}

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_activation"
>title="資料流執行詳細資訊"
>abstract="目標資料流執行詳細資訊包含客群啟用狀態的資訊，以及取自即時客戶輪廓以產生唯一身分的量度。若要深入了解，請檢閱量度定義指南。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dataflows/ui/monitor-destinations.html?lang=zh-Hant#dataflow-runs-for-streaming-destinations" text="用於串流目的地的資料流執行"

>[!CONTEXTUALHELP]
>id="platform_monitoring_profiles_received_batch"
>title="收到的設定檔"
>abstract="資料流中收到的設定檔總數。此值每 60 分鐘更新一次。"

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesactivated_batch"
>title="啟用的身分"
>abstract="成功啟用到所選目的地之個別設定檔身分的計數。此量度包括從匯出的客群中建立、更新和刪除的身分。"

>[!CONTEXTUALHELP]
>id="platform_destinations_dataflow_identitiesexcluded_batch"
>title="排除的身分"
>abstract="根據缺少的屬性和違規行為，從所選目的地的啟用中排除的個別設定檔記錄的計數。"

針對批次目的地，[!UICONTROL 資料流執行]索引標籤會提供資料流執行上的量度資料。 接著會顯示個別執行及其特定量度的清單，以及身分的下列總計：

- **[!UICONTROL 已啟用的身分]**：已成功啟用至所選目的地的設定檔身分總數。 此量度包括從匯出的客群中建立、更新和刪除的身分。
- **[!UICONTROL 排除的身分]**：根據遺失的屬性和同意違規，從選取的目的地啟用中排除的個別設定檔身分計數。

![批次目的地的資料流執行檢視。](../assets/ui/monitor-destinations/dataflow-runs-batch.png)

每個個別資料流執行會顯示下列詳細資訊：

- **[!UICONTROL 資料流執行開始]**：資料流執行開始的時間。
- **[!UICONTROL 對象]**：與每個資料流執行相關聯的對象名稱。
- **[!UICONTROL 處理時間]**：資料流執行處理所花費的時間。
- **[!UICONTROL 已接收的設定檔]**：資料流中接收的設定檔總數。 此值每 60 分鐘更新一次。
- **[!UICONTROL 已啟用的身分]**：在資料流執行過程中成功啟用至所選目的地的設定檔身分總數。 此量度包括從匯出的客群中建立、更新和刪除的身分。
- **[!UICONTROL 排除的身分]**：根據遺失的屬性和同意違規，從啟用中排除的設定檔身分總數。
- **[!UICONTROL 狀態]**：代表資料流所處的狀態。 這可以是下列三種狀態之一： [!UICONTROL 成功]、[!UICONTROL 失敗]和[!UICONTROL 處理]。 [!UICONTROL 成功]表示資料流作用中且正在根據其提供的排程匯出資料。 [!UICONTROL 失敗]表示資料啟用已因錯誤而暫停。 [!UICONTROL 處理中]表示資料流尚未作用中，通常會在建立新資料流時遇到。

若要檢視特定資料流執行的詳細資訊，請從清單中選取執行的開始時間。

>[!NOTE]
>
>根據目的地資料流的排程頻率產生資料流執行。 已針對套用至對象的每個[合併原則](../../profile/merge-policies/overview.md)執行個別的資料流執行。

除了資料流清單上顯示的詳細資訊之外，資料流的詳細資訊頁面還會顯示更多關於資料流的特定資訊：

- **[!UICONTROL 資料的大小]**：正在匯出的資料流的大小。
- **[!UICONTROL 檔案總數]**：資料流中匯出的檔案總數。
- **[!UICONTROL 上次更新時間]**：上次更新資料流執行的時間。

![批次目的地的資料流執行詳細資料。](../assets/ui/monitor-destinations/dataflow-batch.png)

詳細資訊頁面也會顯示失敗的身分和排除的身分清單。 會顯示失敗和已排除的身分資訊，包括錯誤代碼和說明。 依預設，清單會顯示失敗的身分。 若要顯示排除的身分，請選取&#x200B;**[!UICONTROL 排除的身分]**&#x200B;切換。

![批次目的地的資料流記錄，錯誤訊息已反白顯示。](../assets/ui/monitor-destinations/dataflow-records-batch.png)

### 在監視中檢視 {#view-in-monitoring}

您也可以選取在監視控制面板中檢視特定資料流及其資料流執行的豐富資訊。 若要在監視控制面板中檢視資料流的相關資訊：

1. 導覽至&#x200B;**[!UICONTROL 連線]** > **[!UICONTROL 目的地]** > **[!UICONTROL 瀏覽]**&#x200B;索引標籤
2. 導覽至您要檢查的資料流。
3. 選取省略符號和![監檢視示](/help/images/icons/monitoring.png) **[!UICONTROL 在監視中檢視]**。

![在目的地工作流程中選取監視中的檢視，以取得資料流的詳細資訊。](/help/dataflows/assets/ui/monitor-destinations/view-in-monitoring.png)

>[!SUCCESS]
>
>您現在可以在監視控制面板中檢視資料流及其相關資料流執行的資訊。 如需詳細資訊，請閱讀以下章節。

## 監視目標儀表板 {#monitoring-destinations-dashboard}

>[!NOTE]
>
>Experience Platform *中除* [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md)和[自訂個人化](/help/destinations/catalog/personalization/custom-personalization.md)目的地以外的所有目的地目前都支援目的地監視功能。

>[!CONTEXTUALHELP]
>id="platform_monitoring_activation"
>title="啟用"
>abstract="目標啟用視圖包含客群啟用狀態的資訊，以及取自即時客戶輪廓以產生唯一身分的量度。"

若要存取[!UICONTROL 監視]儀表板，請在左側導覽中選取&#x200B;**[!UICONTROL 監視]** （![監檢視示](/help/images/icons/monitoring.png)）。 在[!UICONTROL 監視]頁面上，選取[!UICONTROL 目的地]。 [!UICONTROL 監視]儀表板包含目的地執行工作的度量和資訊。

使用[!UICONTROL Destinations]儀表板來取得您啟動流程整體狀況的資訊。 首先，您可以針對所有批次和串流目的地取得彙總層級的深入分析，然後深入研究資料流、資料流執行和已啟動對象的詳細檢視，以深入瞭解您的啟動資料。 [!UICONTROL 監視]儀表板中的畫面會透過量度和錯誤說明提供可操作的深入分析，以協助您疑難排解啟用情況下可能發生的任何問題。

您可以依資料型別篩選顯示的資訊：客戶、帳戶(僅適用於Adobe Real-Time CDP B2B版本)、潛在客戶和帳戶擴充。 請在[監視儀表板指南](/help/dataflows/ui/monitor.md#monitoring-dashboard-overview)中進一步瞭解這些選項。

![監視儀表板檢視中反白顯示的資料型別篩選器。](/help/dataflows/assets/ui/monitor-destinations/add-data-filter.png)

控制面板的中心是[!UICONTROL 啟用]面板，其中包含量度和圖形，可顯示匯出至串流目的地的資料啟用率，以及匯出至批次目的地的失敗批次資料流執行資料。

![在監視檢視中反白顯示的串流和批次啟用圖表。](../assets/ui/monitor-destinations/dashboard-graph.png)


依預設，顯示的資料包含過去24小時的啟用資訊。 選取&#x200B;**[!UICONTROL 最近24小時]**&#x200B;以調整記錄的時間範圍。 可用選項包括&#x200B;**[!UICONTROL 最近24小時]**、**[!UICONTROL 最近7天]**&#x200B;和&#x200B;**[!UICONTROL 最近30天]**。 或者，您可以在出現的行事曆快顯視窗中選取日期。 選取日期後，選取&#x200B;**[!UICONTROL 套用]**&#x200B;以調整顯示資訊的時間範圍。

>[!NOTE]
>
>下列熒幕擷圖顯示過去30天（而非過去24小時）的啟用率和批次資料流執行。 您可以選取&#x200B;**[!UICONTROL 最近30天]**&#x200B;來調整時間範圍。

![變更已啟用的目的地反白顯示的回顧日期範圍控制項](../assets/ui/monitor-destinations/dashboard-graph-change-date-range.png)

使用箭頭圖示（![箭頭圖示](/help/images/icons/chevron-up.png)）來展開或關閉熒幕頂端的卡片，這些卡片會根據目的地型別（串流或批次）顯示啟動詳細資訊的簡單資訊：

- **[!UICONTROL 串流啟用率]**：代表已順利啟用或略過的接收身分百分比。 用於計算此百分比的公式已在此頁面的[資料流執行於串流目的地](#dataflow-runs-for-streaming-destinations)區段中進一步說明。
- **[!UICONTROL 批次失敗的資料流執行]**：代表在選取的時間間隔內失敗的資料流執行次數。

![在頁面頂端顯示或解除卡片。](../assets/ui/monitor-destinations/monitoring-destinations-toggle-arrow.gif)

預設會顯示&#x200B;**[!UICONTROL 啟用]**&#x200B;圖表，您可以停用它以展開底下的目的地清單。 選取&#x200B;**[!UICONTROL 度量與圖形]**&#x200B;切換以停用圖形。

**[!UICONTROL 啟用]**&#x200B;面板會顯示至少包含一個現有帳戶的目的地清單。 此清單也包含接收的個人檔案、啟用的身分、失敗的身分、排除的身分、啟用率、失敗的資料流總數以及這些目的地上次更新日期的相關資訊。 並非所有量度都適用於所有目的地型別。 下表概述每種目的地型別的可用量度和資訊。

| 量度 | 目的地型別 |
|--------------------------------------|-----------------------|
| 已接收&#x200B;**[!UICONTROL 筆記錄]** | 串流和批次 |
| **[!UICONTROL 記錄已啟用]** | 串流和批次 |
| **[!UICONTROL 個記錄失敗]** | 串流 |
| **[!UICONTROL 個略過的記錄]** | 串流和批次 |
| **[!UICONTROL 資料型別]** | 串流和批次 |
| **[!UICONTROL 啟用率]** | 串流 |
| **[!UICONTROL 失敗的資料流總數]** | 批次 |
| **[!UICONTROL 上次更新時間]** | 串流和批次 |

{style="table-layout:auto"}

![所有啟用目的地皆強調的監視儀表板。](../assets/ui/monitor-destinations/dashboard-destinations.png)

您也可以篩選目的地清單，以僅顯示選取的目的地類別。 選取&#x200B;**[!UICONTROL 我的目的地]**&#x200B;下拉式清單，並選取您要篩選的[目的地類別](/help/destinations/destination-types.md#categories)。

![使用下拉式選擇器篩選目的地](../assets/ui/monitor-destinations/dashboard-destinations-filter-dropdown.png)

此外，您可以在搜尋列中輸入目的地，以隔離至單一目的地。 如果您想要檢視目的地的資料流，可以選取該目的地旁邊的篩選器![篩選器](/help/images/icons/filter-add.png)，以檢視其作用中資料流的清單。

![使用監視檢視中反白顯示的搜尋列來篩選目的地。](../assets/ui/monitor-destinations/filtered-destinations.png)

如果您想要檢視所有目的地的所有現有資料流，請選取&#x200B;**[!UICONTROL 資料流]**。

系統隨即顯示資料流清單，依上次資料流執行排序。 您可以尋找要監視的目的地，選取資料流旁邊的篩選器![篩選器](/help/images/icons/filter-add.png)，接著選取資料流旁邊的篩選器![篩選器](/help/images/icons/filter-add.png)，以檢視特定資料流的其他詳細資料。

![監視儀表板中反白顯示的所有資料流。](../assets/ui/monitor-destinations/dashboard-dataflows.png)

選取資料流以進行進一步檢查後，「資料流詳細資料」頁面會包含切換功能，可讓您檢視資料流中已啟動的資料，並按照資料流執行或對象進行劃分。

### 資料流執行檢視 {#dataflow-runs-view}

選取&#x200B;**[!UICONTROL 資料流執行]**&#x200B;時，您可以看到所選資料流的資料流執行清單，以及有關每次執行的進一步資訊。

>[!INFO]
>
>對於要串流目的地的資料流，資料流執行會劃分為每小時時段。 每個每小時視窗都會產生對應的資料流執行ID。
>
>針對批次目的地的資料流，每個對象都會根據對象啟用排程頻率產生相對應的資料流執行。 例如，如果您為相同目的地資料流中的五個對象設定每日排程啟動，則每天將會產生五個個別的資料流執行。

![資料流執行面板，反白顯示數個執行。](../assets/ui/monitor-destinations/dashboard-flow-runs-view.png)

使用&#x200B;**[!UICONTROL 僅顯示失敗]**&#x200B;切換按鈕，僅顯示資料流的失敗執行。

![資料流執行檢視，只顯示failures的切換反白顯示](../assets/ui/monitor-destinations/dataflow-runs-show-failures-only.gif)

### 對象層級檢視 {#segment-level-view}

選取&#x200B;**[!UICONTROL 對象]**&#x200B;時，您會在選取的時間範圍內看到啟用至選取之資料流的對象清單。 此畫麵包含受眾層級資訊，瞭解啟用的記錄、排除的記錄，以及上次資料流執行的狀態和時間。 您可以檢閱排除和啟動記錄的量度，以確認對象是否已成功啟動。

例如，您正在將名為「加州忠誠會員」的受眾啟用至Amazon S3目的地「加州十二月的忠誠會員」。 假設在選取的對象中有100個設定檔，但100筆記錄中只有80筆包含「忠誠度ID」屬性，而且您已將匯出對應規則定義為必要`loyalty.id`。 在此案例中，在對象層級，您會看到80筆記錄已啟用，20筆記錄已排除。

>[!IMPORTANT]
>
>請注意與對象層級量度相關的目前限制：
>- 對象層級檢視目前僅適用於批次（檔案式）目的地和[Google Customer Match DV 360](/help/destinations/catalog/advertising/google-customer-match-dv360.md)串流目的地。 已計畫推出更多串流目的地。
>- 對於批次目的地，目前僅針對成功的資料流執行記錄對象層級量度。 失敗的資料流執行和排除的記錄不會記錄這些事件。 對於串流目的地的資料流執行，會擷取並顯示已啟用和排除的記錄的量度。

![資料流面板中反白顯示的對象。](../assets/ui/monitor-destinations/dashboard-segments-view.png)

在對象層級檢視中，這些量度會在所選時間範圍內跨多個資料流執行進行彙總。 如果有多個資料流執行，您可以從對象層級向下展開，以檢視每個資料流執行的劃分（依選取的對象篩選）。
使用篩選按鈕![篩選器](/help/images/icons/filter-add.png)，針對資料流中的每個對象，向下展開資料流執行檢視。

### 資料流執行頁面 {#dataflow-runs-page}

「資料流執行」頁面會顯示您的資料流執行的相關資訊，包括資料流執行開始時間、處理時間、收到的記錄、啟用的記錄、排除的記錄、失敗的記錄、啟用率和狀態。

當您從[對象層級檢視](#segment-level-view)向下鑽研資料流執行頁面時，您可以選擇透過下列選項來篩選資料流執行：

- **[!UICONTROL 含有失敗記錄的資料流執行]**：對於選取的對象，此選項會列出所有無法啟用的資料流執行。 若要檢查特定資料流執行中記錄失敗的原因，請參閱該資料流執行的[資料流執行詳細資訊頁面](#dataflow-run-details-page)。
- **[!UICONTROL 包含排除記錄的資料流執行]**：對於選取的對象，此選項會列出所有資料流執行，其中部分記錄未完全啟動且部分設定檔被略過。 若要檢查某個資料流執行中的記錄為何被略過，請參閱該資料流執行的[資料流執行詳細資訊頁面](#dataflow-run-details-page)。
- **[!UICONTROL 具有已啟動記錄的資料流執行]**：對於選取的對象，此選項會列出具有已成功啟動記錄的所有資料流執行。

![顯示如何篩選對象資料流執行的選項按鈕。](/help/dataflows/assets/ui/monitor-destinations/dataflow-runs-segment-filter.png)

若要檢視特定資料流執行的詳細資訊，請選取資料流執行開始時間旁的篩選器![篩選器](/help/images/icons/filter-add.png)，以檢視資料流執行詳細資訊頁面。

![資料流在監視儀表板中執行篩選，以深入瞭解特定資料流執行的更多資訊。](../assets/ui/monitor-destinations/dataflow-runs-filter.png)

### 資料流執行詳細資訊頁面 {#dataflow-run-details-page}

除了顯示在資料流執行清單上的詳細資訊之外，「資料流執行詳細資料」頁面還顯示有關資料流的更多特定資訊：

- **[!UICONTROL 資料流執行ID]**：資料流的識別碼。
- **[!UICONTROL IMS組織識別碼]**：資料流所屬的組織。
- **[!UICONTROL 上次更新時間]**：上次更新資料流執行的時間。

詳細資訊頁面也會進行切換，以在資料流執行錯誤和對象之間切換。 此選項僅適用於批次目的地中的資料流執行，以及[Google Customer Match DV 360](/help/destinations/catalog/advertising/google-customer-match-dv360.md)串流目的地。

資料流執行錯誤檢視會顯示失敗的記錄清單和略過的記錄清單。 顯示失敗和略過的記錄資訊，包括錯誤代碼、身分計數和說明。 依預設，清單會顯示失敗的記錄。 若要顯示略過的記錄，請選取&#x200B;**[!UICONTROL 略過的記錄]**&#x200B;切換按鈕。

![排除的身分切換在監視檢視中反白顯示](../assets/ui/monitor-destinations/identities-excluded.png)

選取&#x200B;**[!UICONTROL 對象]**&#x200B;時，您會看到在選取的資料流執行中啟用的對象清單。 此畫麵包含受眾層級資訊，瞭解啟用的記錄、排除的記錄，以及上次資料流執行的狀態和時間。

![資料流執行詳細資訊畫面中的對象檢視。](../assets/ui/monitor-destinations/dataflow-run-segments-view.png)

## 後續步驟 {#next-steps}

依照本指南，您現在瞭解如何監控批次和串流目的地的資料流，包括所有相關資訊，例如處理時間、啟用率和狀態。 若要深入瞭解Platform中的資料流，請閱讀[資料流概觀](../home.md)。 若要深入瞭解目的地，請閱讀[目的地概觀](../../destinations/home.md)。