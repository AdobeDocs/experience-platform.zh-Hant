---
keywords: Experience Platform；首頁；熱門主題；監視器身分；監視資料流；資料流；身分；
description: Adobe Experience Platform Identity Service可跨裝置和系統橋接身分，提供客戶及其行為的全面檢視，讓您即時提供具影響力的個人數位體驗。 本教學課程提供如何使用Experience Platform使用者介面，以身分監視資料流的相關指示。
title: 在UI中監視身分資料流
type: Tutorial
exl-id: 735b0e52-74f6-47fe-98c6-e12a633b6f57
source-git-commit: 1a7ba52b48460d77d0b7695aa0ab2d5be127d921
workflow-type: tm+mt
source-wordcount: '1149'
ht-degree: 1%

---

# 在UI中監視身分資料流

Adobe Experience Platform Identity Service可跨裝置和系統橋接身分，提供客戶及其行為的全面檢視，讓您即時提供具影響力的個人數位體驗。

監控控制面板可以以視覺化方式呈現資料在身分內的活動，包括資料身分的狀態。 本教學課程提供相關指示，說明如何使用監控控制面板，透過Experience Platform使用者介面監控您資料的身分識別，讓您追蹤身分處理狀態。

## 快速入門 {#getting-started}

- [資料流](../home.md):資料流是跨平台移動資料的資料作業的表示。 資料流可跨不同的服務進行配置，有助於將資料從源連接器移動到目標資料集 [!DNL Identity] 和 [!DNL Profile]和 [!DNL Destinations].
   - [資料流運行](../../sources/notifications.md):資料流運行是基於所選資料流的頻率配置的循環調度作業。
- [Identity服務](../../identity-service/home.md):跨裝置和系統橋接身分，以更全面了解個別客戶及其行為。
- [沙箱](../../sandboxes/home.md): [!DNL Experience Platform] 提供可分割單一沙箱的虛擬沙箱 [!DNL Platform] 例項放入個別的虛擬環境，以協助開發及改進數位體驗應用程式。

## 監控身分控制面板 {#identity-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_identity_processing"
>title="身分處理"
>abstract="「身分處理」檢視包含擷取至身分服務之記錄的相關資訊，包括新增的身分數、建立的圖形，以及更新的圖形。 檢閱量度定義指南，以進一步了解量度和圖形。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_dataflow_run_details_identity"
>title="資料流執行詳細資訊"
>abstract="「資料流運行詳細資訊」頁顯示了有關身份資料流運行的詳細資訊，包括其組織ID和資料流運行ID。"

若要存取 **[!UICONTROL 身分]** 控制面板，選取 **[!UICONTROL 監控]** 的下一頁。 一次 **[!UICONTROL 監控]** 頁面，選擇 **[!UICONTROL 身分]** 卡片。

![身分卡。 會顯示接收的記錄數、擷取的記錄數，以及成功率的相關資訊。](../assets/ui/monitor-identities/focus-card.png)

主要 **[!UICONTROL 身分]** 控制面板、 **[!UICONTROL 身分]** 卡片會顯示已接收記錄總數、已擷取記錄數，以及記錄擷取成功率的相關資訊。

控制面板本身包含有關身分處理的量度。 依預設，控制面板會顯示貴組織過去24小時來源的身分處理詳細資訊。

![身分控制面板。 將顯示有關每個源接收的記錄數的資訊。](../assets/ui/monitor-identities/sources.png)

此 [!UICONTROL 身分處理] 頁面包含擷取至的記錄資訊 [!DNL Identity Service]，包括新增的身分數、建立的圖形，以及更新的圖形。

此控制面板檢視可使用下列量度：

| 身分量度 | 說明 |
| ---------------- | ----------- |
| **[!UICONTROL 收到的記錄]** | 從資料湖接收的記錄數。 |
| **[!UICONTROL 記錄失敗]** | 因資料錯誤而未擷取至Platform的記錄數。 |
| **[!UICONTROL 略過的記錄]** | 已擷取但未擷取至 [!DNL Identity Service] 因為記錄列中只有一個標識符。 |
| **[!UICONTROL 擷取的記錄]** | 擷取到的記錄數 [!DNL Identity Service]. |
| **[!UICONTROL 已新增身分]** | 新增至的新識別碼淨數 [!DNL Identity Service]. |
| **[!UICONTROL 建立的圖表]** | 在中建立的淨新標識圖數 [!DNL Identity Service]. |
| **[!UICONTROL 圖形已更新]** | 已用新邊更新的現有標識圖形的數量。 |
| **[!UICONTROL 失敗的資料流總數]** | 失敗的資料流運行數。 |

您可以選取篩選圖示 ![篩選圖示](../assets/ui/monitor-identities/filter.png) 源名稱旁邊，查看所選源資料流的身份處理資訊。

![篩選器圖示會反白顯示。 選中此表徵圖可讓您查看所選源的資料流。](../assets/ui/monitor-identities/sources-filter.png)

或者，您也可以選取 **[!UICONTROL 資料流]** 開啟切換，查看貴組織過去24小時資料流的身分處理詳細資料。

![身分控制面板。 將顯示有關每個資料流接收的標識數的資訊。](../assets/ui/monitor-identities/dataflows.png)

此控制面板檢視可使用下列量度：

| 量度 | 說明 |
| -------| ----------- |
| **[!UICONTROL 資料流]** | 資料流的名稱。 |
| **[!UICONTROL 資料集]** | 資料流要插入的資料集的名稱。 |
| **[!UICONTROL 源名稱]** | 資料流所屬的源的名稱。 |
| **[!UICONTROL 收到的記錄]** | 從資料湖接收的記錄數。 |
| **[!UICONTROL 記錄失敗]** | 因資料錯誤而未擷取至Platform的記錄數。 |
| **[!UICONTROL 略過的記錄]** | 已擷取但未擷取至 [!DNL Identity Service] 因為記錄列中只有一個標識符。 |
| **[!UICONTROL 擷取的記錄]** | 擷取到的記錄數 [!DNL Identity Service]. |
| **[!UICONTROL 記錄總數]** | 所有記錄的總計數，包括失敗的記錄、已跳過的記錄、已添加的身份和重複的記錄。 |
| **[!UICONTROL 已新增身分]** | 新增至的新識別碼淨數 [!DNL Identity Service]. |
| **[!UICONTROL 建立的圖表]** | 在中建立的淨新標識圖數 [!DNL Identity Service]. |
| **[!UICONTROL 圖形已更新]** | 已用新邊更新的現有標識圖形的數量。 |
| **[!UICONTROL 失敗的資料流總數]** | 失敗的資料流運行數。 |

選取篩選圖示 ![篩選](../assets/ui/monitor-identities/filter.png) 資料流運行開始時間旁邊，查看有關 [!DNL Identity] 資料流運行。

![篩選器圖示會反白顯示。 選擇此表徵圖可讓您查看有關所選資料流的詳細資訊。](../assets/ui/monitor-identities/dataflows-filter.png)

此 [!UICONTROL 資料流運行詳細資訊] 頁面會顯示您 [!DNL Identity] 資料流運行，包括其組織ID和資料流運行ID。 此頁還顯示相應的錯誤代碼和提供的錯誤消息 [!DNL Identity Service]，則擷取程式中會發生任何錯誤。

![將顯示一個儀表板，其中顯示有關所選資料流的詳細資訊。](../assets/ui/monitor-identities/dataflow-run-details.png)

此控制面板檢視可使用下列量度：

| 量度 | 說明 |
| -------| ----------- |
| **[!UICONTROL 收到的記錄]** | 從資料湖接收的記錄數。 |
| **[!UICONTROL 記錄失敗]** | 因資料錯誤而未擷取至Platform的記錄數。 |
| **[!UICONTROL 略過的記錄]** | 已擷取但未擷取至 [!DNL Identity Service] 因為記錄列中只有一個標識符。 |
| **[!UICONTROL 擷取的記錄]** | 擷取到的記錄數 [!DNL Identity Service]. |
| **[!UICONTROL 已新增身分]** | 新增至的新識別碼淨數 [!DNL Identity Service]. |
| **[!UICONTROL 建立的圖表]** | 在中建立的淨新標識圖數 [!DNL Identity Service]. |
| **[!UICONTROL 圖形已更新]** | 已用新邊更新的現有標識圖形的數量。 |
| **[!UICONTROL 狀態]** | 定義資料流的總體狀態。 可能的狀態值為： <ul><li>`Success`:指示資料流處於活動狀態，並正在根據資料流提供的計畫來接收資料。</li><li>`Failed`:表示資料流的激活過程因錯誤而中斷。 </li><li>`Processing`:指示資料流尚未處於活動狀態。 建立新資料流後，通常會立即出現此狀態。</li></ul> |
| **[!UICONTROL 資料流運行開始]** | 資料流開始運行的日期和時間。 |
| **[!UICONTROL 上次更新時間]** | 上次更新資料流的日期和時間。 |
| **[!UICONTROL 錯誤摘要]** | 如果資料流運行失敗，則顯示錯誤代碼和資料流運行失敗原因的摘要。 |
| **[!UICONTROL 資料流運行ID]** | 資料流運行的ID。 |
| **[!UICONTROL IMS組織ID]** | 資料流運行所屬的組織ID。 |

此外，您可以選取切換來檢視失敗記錄或已略過記錄。 「錯誤」部分包括有關錯誤代碼的詳細資訊以及失敗或排除的記錄數。
