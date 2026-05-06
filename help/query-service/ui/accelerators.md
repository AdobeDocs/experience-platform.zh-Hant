---
keywords: Experience Platform；查詢服務；資料Distiller；加速器；引數化查詢；SQL範本
solution: Experience Platform
title: 資料Distiller加速器
description: 使用Data Distiller加速器在查詢服務UI中執行並排程Adobe核准的引數化SQL範本。 加速器是唯讀且由Adobe管理；請使用**[!UICONTROL Create custom template]**來複製及編輯它們。
source-git-commit: 5ee579c15fc2d9954673062b08280d9060b5205a
workflow-type: tm+mt
source-wordcount: '1300'
ht-degree: 0%

---

# 資料Distiller加速器 {#data-distiller-accelerators}

資料Distiller加速器是由Adobe編寫、引數化的SQL範本，專為常見分析案例而設計。 使用加速器來執行常見分析，而不需從頭開始寫入SQL。 加速器是唯讀狀態，並由Adobe進行維護，確保整個組織的一致性。 如果您需要修改範本，可以將其復製為自訂範本。

請閱讀本指南，瞭解如何在[!UICONTROL Queries]工作區中執行、排程和複製加速器。

>[!AVAILABILITY]
>
>資料Distiller加速器僅適用於擁有資料Distiller SKU的組織。 [!UICONTROL Accelerators]標籤和相關工作流程需要Data Distiller附加元件。 請參閱[資料Distiller概觀](../data-distiller/overview.md)或聯絡您的Adobe代表以取得更多資訊。

## 先決條件 {#prerequisites}

開始之前，請確認您符合下列需求：

* 您有權存取Experience Platform中的[!UICONTROL Queries]工作區。
* 您瞭解[如何使用查詢編輯器並執行查詢](./user-guide.md)。
* 您熟悉[引數化查詢](./parameterized-queries.md) （在執行階段取代SQL中的預留位置）。

## 何時使用加速器 {#when-to-use}

當您需要針對常見分析模式（例如funnel分析、移動平均或對象重疊）預先建立的SQL時，請使用加速器。 如果沒有符合您使用案例的加速器，請[在查詢編輯器](./user-guide.md#query-authoring)中撰寫自訂查詢，或要求新的加速器（請參閱[要求新的加速器](#request-accelerator)）。

一小部分加速器會開啟為控制面板，以供立即分析，有些加速器則會在「查詢編輯器」中開啟，讓您執行、排程或調整邏輯。 請參閱[控制面板連結的加速器](#dashboard-accelerators)區段，瞭解這些預先設定的視覺效果如何提供對象資料的深入分析。

若要開始使用加速器，請導覽至&#x200B;**[!UICONTROL Queries]**&#x200B;工作區並開啟「**[!UICONTROL Accelerators]**」標籤或「**[!UICONTROL Overview]**」標籤。

## 加速器探索路徑 {#discovery-paths}

您可以透過兩種方式從查詢工作區存取加速器，這取決於您想要完整目錄還是建議的範本。

### 使用「加速器」標籤

當您想要瀏覽所有可用的加速器時，請使用此路徑。 若要開啟完整的加速器目錄，請在左側導覽中選取&#x200B;**[!UICONTROL Queries]**，然後選取&#x200B;**[!UICONTROL Accelerators]**&#x200B;索引標籤。

工作區會顯示一個包含名稱、SQL預覽和時間戳記的加速器表格。 選取加速器名稱，以在「查詢編輯器」中將其開啟。

>[!NOTE]
>
>從&#x200B;**[!UICONTROL Accelerators]**&#x200B;索引標籤選取的所有加速器都會在查詢編輯器中開啟。

![已選取[加速器]索引標籤的[查詢]工作區會顯示加速器表格。](../images/ui/accelerators/accelerators-tab-table.png)

### 使用「概述」標籤

當您想要快速存取強烈建議的加速器時，請使用此路徑。 導覽至&#x200B;**[!UICONTROL Queries]**，然後選取&#x200B;**[!UICONTROL Overview]**&#x200B;索引標籤。 接著，從&#x200B;**[!UICONTROL Recommended Data Distiller accelerators]**&#x200B;區段選取卡片。

大部分的加速器會在「查詢編輯器」中開啟。 一小部分加速器會開啟為具有預先建立視覺效果的儀表板。 如果卡片開啟的是儀表板而不是查詢編輯器，請參閱[儀表板連結的加速器](#dashboard-accelerators)。

![已選取[概觀]索引標籤的[查詢]工作區會顯示建議的[資料Distiller加速器]清單。](../images/ui/accelerators/queries-overview-accelerators.png)

## 在查詢編輯器中開啟加速器 {#open-accelerator}

本節說明當您在「查詢編輯器」中開啟加速器時會發生什麼情況，以及您接下來可以執行的動作，包括執行加速器、排程加速器或建立自訂範本。

開啟加速器之後，您可以&#x200B;**執行**&#x200B;加速器以檢視結果，**排程**&#x200B;加速器以自動執行，或&#x200B;**建立自訂範本**&#x200B;以修改SQL。

>[!NOTE]
>
>當您在查詢編輯器中開啟加速器時，SQL會以唯讀狀態預先載入，且工具列動作（例如[!UICONTROL Show results]、[!UICONTROL Undo text]、[!UICONTROL Format text]）會停用。

右側面板會顯示中繼資料，例如&#x200B;**[!UICONTROL Accelerator ID]**、**[!UICONTROL Name]**&#x200B;和修改詳細資料，並提供透過&#x200B;**[!UICONTROL Add schedule]**&#x200B;排程的存取權。

![已開啟加速器的[查詢編輯器]，顯示SQL區域、[查詢引數]索引標籤和右側面板。](../images/ui/accelerators/accelerator-query-editor.png)

### 提供引數並執行加速器 {#provide-parameters-execute}

若要執行加速器，您必須先提供所有必要引數的值。 引數使用`${PARAMETER_NAME}`語法，並出現在編輯器下方的&#x200B;**[!UICONTROL Query parameters]**&#x200B;索引標籤中。 例如，`${START_DATE}`需要`YYYY-MM-DD`格式的日期值（例如，`2024-01-01`），而`${AUDIENCE_ID}`需要特定的對象識別碼。

若要執行加速器，請執行下列動作：

1. 選取&#x200B;**[!UICONTROL Query parameters]**&#x200B;並為每個引數輸入值。
2. 選取播放圖示（![播放圖示。](../../images/icons/play.png)） （在工具列中）。

加速器會在&#x200B;**[!UICONTROL Results]**&#x200B;索引標籤中執行並顯示結果。 除非您使用&#x200B;**[!UICONTROL Run as CTAS]**&#x200B;或排程加速器，否則這些結果不會保留在資料集中。

如需引數化查詢的詳細資訊，請參閱查詢編輯器中的[引數化查詢](./parameterized-queries.md)。

## 保留來自加速器的結果 {#persist-results}

執行加速器並確認結果後，您可以將輸出保留到資料集。

若要從結果中建立資料集，請選取&#x200B;**[!UICONTROL Save]**&#x200B;以將加速器儲存為範本，然後選取&#x200B;**[!UICONTROL Run as CTAS]**。 **[!UICONTROL Enter output dataset details]**&#x200B;對話方塊隨即顯示。 輸入資料集名稱和選用的說明，然後確認以建立資料集。 此動作會建立新資料集並將結果寫入其中。

![已填入資料集名稱和描述的[!UICONTROL Enter output dataset details]對話方塊。](../images/ui/accelerators/output-dataset-details-dialog.png)

## 排程加速器 {#schedule-accelerator}

若要排程使用固定引數值自動執行的加速器，請在右側面板中選取&#x200B;**[!UICONTROL Add schedule]**。

>[!TIP]
>
>在排程之前，請確定您瞭解必要的引數值。 請先執行加速器以驗證結果。

排程組態對話方塊隨即顯示。

![顯示頻率、日期範圍、輸出資料集和引數欄位的排程設定對話方塊。](../images/ui/accelerators/schedule-details.png)

在排程設定對話方塊中，您必須再次提供頻率、時間範圍、輸出資料集和引數值。 在查詢編輯器中輸入的引數值不會執行至排程設定。 在&#x200B;**[!UICONTROL Dataset details]**&#x200B;區段中，您可以選擇&#x200B;**[!UICONTROL Append into existing dataset]**&#x200B;或&#x200B;**[!UICONTROL Create and append into new dataset]**。 設定排程後，加速器會根據您的設定自動執行，並將結果寫入所選的資料集。

如需完整的逐步指示，請參閱[建立查詢排程](./query-schedules.md#create-schedule)指南。

## 從加速器建立自訂範本 {#create-custom-template}

如果您需要修改SQL或重複使用自己組態下的邏輯，可以從加速器建立自訂範本。 首先，在查詢編輯器中開啟加速器，然後選取&#x200B;**[!UICONTROL Create custom template]**。 視需要修改SQL和詳細資料，並選取&#x200B;**[!UICONTROL Save]**&#x200B;或&#x200B;**[!UICONTROL Save and close]**&#x200B;以儲存範本。

儲存後，範本即可編輯，並可執行、排程或搭配CTA使用。 範本會儲存至&#x200B;**[!UICONTROL Templates]**&#x200B;標籤，您可以在其中像管理任何其他範本一樣管理範本。 如需詳細資訊，請參閱[查詢範本](./query-templates.md)。

### 建立自訂範本時會有哪些變更 {#custom-template-differences}

複製範本與原始加速器不同，因為SQL可以編輯，您可以儲存變更、刪除範本及排程範本。 **[!UICONTROL Modified by]**&#x200B;欄位會顯示您的名稱。 在&#x200B;**[!UICONTROL Templates]**&#x200B;索引標籤中找到的是範本，而非&#x200B;**[!UICONTROL Accelerators]**。

## 控制面板連結的加速器 {#dashboard-accelerators}

**[!UICONTROL Overview]**&#x200B;標籤上的部分加速器會開啟為儀表板，而不是SQL查詢。 這些加速器提供用於分析受眾資料的預先建立視覺效果，並且不需要引數輸入或手動執行。

下列加速器會在&#x200B;**[!UICONTROL Dashboards]**&#x200B;工作區中開啟：

**[!UICONTROL Advanced Audience Overlaps]**&#x200B;會分析所選對象之間或整個對象集的交集，以識別重疊模式。 利用這些見解來調整細分並減少多餘的鎖定。

**[!UICONTROL Audience Comparison]**&#x200B;會並排比較兩個對象之間的關鍵量度，包括大小、身分構成及隨時間的變更。 使用此檢視來評估效能差異，並告知目標定位決策。

**[!UICONTROL Audience Trends]**&#x200B;追蹤對象量度在一段時間內的變化，包括對象人數和身分計數。 使用這些趨勢來監控成長並評估細分策略的影響。

**[!UICONTROL Audience Identity Overlaps]**&#x200B;會檢視身分型別在選取的對象中如何重疊，以瞭解身分關係。 使用此分析來改善身分拼接和分段準確性。

![儀表板檢視顯示具有圖表和篩選器的對象分析視覺效果。](../images/ui/accelerators/dashboard-accelerator-template-example.png)

控制面板開啟後，使用可用的控制項和篩選器來探索和比較對象資料。 如需詳細資訊，請參閱[儀表板範本](../../dashboards/sql-insights-query-pro-mode/templates/overview.md)。

## 要求新的加速器 {#request-accelerator}

如果您有現有加速服務未涵蓋的週期性使用案例，請透過您的Adobe支援頻道提交請求。 Adobe會根據常見使用模式和產業適用性來評估請求。

## 後續步驟 {#next-steps}

您現在可以使用加速器來執行並自動化常見分析查詢。

若要擴充工作流程，請建立並瀏覽[查詢範本](./query-templates.md#browse)、作者[引數化查詢](./parameterized-queries.md)、排程[查詢](./query-schedules.md)，或探索[查詢服務工作流程](./user-guide.md)。
