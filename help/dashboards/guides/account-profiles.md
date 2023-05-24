---
title: 帳戶配置檔案儀表板指南
description: Adobe Experience Platform提供了一個儀表板，您可以通過該儀表板查看有關組織B2B帳戶配置檔案的重要資訊。
exl-id: c9a3d786-6240-4ba4-96c8-05f658e1150c
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '1052'
ht-degree: 0%

---

# [!UICONTROL 帳戶配置檔案] 儀表板

Adobe Experience Platform用戶介面(UI)提供了一個儀表板，您可以通過該儀表板查看有關帳戶配置檔案的重要資訊，這些資訊在每日快照中捕獲。 本指南概括介紹了如何訪問和使用 [!UICONTROL 帳戶配置檔案] UI中的儀表板，並提供了有關儀表板中顯示的可視化效果的詳細資訊。

有關帳戶配置檔案用戶介面中所有功能的概述，請訪問 [帳戶配置檔案UI指南](../../rtcdp/accounts/account-profile-ui-guide.md)。

## 快速入門

你必須有權 [Adobe Real-time Customer Data PlatformB2B版](../../rtcdp/b2b-overview.md) 為了訪問B2B [!UICONTROL 帳戶配置檔案] 控制項欄。

## 帳戶配置檔案資料

的 [!UICONTROL 帳戶配置檔案] 控制面板顯示來自多個來源的統一帳戶資訊的快照，這些來源來自您的市場營銷渠道以及您的組織當前用於儲存客戶帳戶資訊的各種系統。

快照中的配置檔案資料與拍攝快照時在特定時間點顯示的資料完全相同。 換句話說，快照不是資料的近似或示例， [!UICONTROL 帳戶配置檔案] 儀表板不會即時更新。

>[!NOTE]
>
>自拍攝快照以來對資料所做的任何更改或更新不會反映在儀表板中，直到拍攝下一個快照。

## 瀏覽 [!UICONTROL 帳戶配置檔案] 儀表板

導航到 [!UICONTROL 帳戶配置檔案] 平台UI中的儀表板，選擇 **[!UICONTROL 配置檔案]** 在 [!UICONTROL 帳戶] 的子菜單。

![左側導航中的「Platform UI（平台UI）」和「Account Profiles（帳戶配置檔案）」突出顯示，並顯示「Overview（概述）」頁籤。](../images/account-profiles/account-profiles-dashboard.png)

從 [!UICONTROL 帳戶配置檔案] 儀表板 [瀏覽已導入您組織的帳戶配置檔案](#browse-account-profiles)或 [使用小部件一目瞭然地查看整個帳戶配置檔案資料](#standard-widgets) 可以直觀地顯示資料的各個方面。

## 瀏覽帳戶配置檔案 {#browse-account-profiles}

的 [!UICONTROL 瀏覽] 頁籤允許您使用連接的企業來源中的帳戶ID或直接輸入來源詳細資訊來搜索和查看導入您組織的只讀帳戶配置檔案。 從此處，您可以看到屬於帳戶配置檔案的重要資訊，包括其名稱、行業、收入和細分等。

選擇 [!UICONTROL 配置檔案ID] 顯示在 [!UICONTROL 瀏覽] 按鈕 [!UICONTROL 詳細資訊] 頁籤。

![「帳戶配置檔案」瀏覽頁籤顯示結果，並突出顯示「配置檔案ID」。](../images/account-profiles/account-profiles-browse-tab.png)

顯示在 [!UICONTROL 詳細資訊] 已從多個配置檔案片段合併到一起，以形成單個帳戶的單個視圖。 請參閱 [瀏覽帳戶配置檔案Adobe Real-time Customer Data Platform](../../rtcdp/accounts/account-profile-ui-guide.md#browse-account-profiles) 瞭解有關平台UI中帳戶配置檔案查看功能的詳細資訊。

## 的 [!UICONTROL 帳戶配置檔案] [!UICONTROL 概述] {#overview}

的 [!UICONTROL 概述] 頁籤由提供只讀度量以傳遞有關帳戶配置檔案的重要資訊的小部件組成。 選擇 **[!UICONTROL 修改儀表板]** 更改 [!UICONTROL 概述] 按鈕。

![突出顯示了「修改」面板的「帳戶概要檔案」概述頁籤。](../images/account-profiles/modify-dashboard.png)

請參閱上的文檔 [修改儀表板](../customize/modify.md) 和 [小部件庫概述](../customize/widget-library.md) 來瞭解更多資訊。

## 標準小部件 {#standard-widgets}

Adobe提供了標準小部件，您可以使用這些小部件來可視化與帳戶配置檔案相關的不同度量。

要瞭解有關每個可用標準小部件的詳細資訊，請從以下清單中選擇小部件的名稱：

* [按行業分列的總帳](#total-accounts-by-industry)
* [已添加帳戶配置檔案](#account-profiles-added)
* [預測計分分配](#predictive-scoring-distribution)
* [預測性評分最大影響因素](#predictive-scoring-top-influential-factors)

### 按行業分列的總帳 {#total-accounts-by-industry}

此小部件以單個度量顯示帳戶總數，並使用甜圈圖來說明構成總數的行業計數的比例大小。 該鍵為構成環形圖的不同行業提供顏色編碼資訊。

當游標懸停在圓圈圖的相應部分上時，不同行業的單個計數將顯示在對話框中。

![按行業小部件列出的帳戶總數。](../images/account-profiles/total-accounts-by-industry-widget.png)

### 已添加帳戶配置檔案 {#account-profiles-added}

此小部件使用彩色編碼條形圖來說明在給定時間段內添加到帳戶的配置檔案計數，以及構成這些添加的配置檔案的不同行業的比例。 這些行業是彩色編碼的，一個鍵為組成條形圖的不同行業提供顏色編碼資訊。 分析期間從構件下拉菜單中選擇。 條形圖可在30天、90天和12個月期間可視化。

>[!NOTE]
>
>由於配置檔案只被添加到帳戶且從未被刪除，因此在一段時間內添加的配置檔案的數量可能最低為零。

![帳戶配置檔案已添加小部件。](../images/account-profiles/accounts-profiles-added-widget.png)

### 預測計分分配 {#predictive-scoring-distribution}

的 [!UICONTROL 預測計分分配] 小部件顯示所有帳戶配置檔案的分數分佈，以幫助您一目瞭然地瞭解銷售渠道的運行狀況。 記分資料通過環形圖和柱形圖傳送。

甜甜圈圖說明了在購買時段的高、中和低傾向中，您的總帳戶配置檔案所佔的比例。 該關鍵字提供了有關顏色編碼部分的更多詳細資訊，包括評分時段範圍和該範圍內的帳戶配置檔案數。

該清單提供了更細粒度的評分細分。 每列顯示20個五點增量時段中每個時段中的帳戶配置檔案數。

構件中的下拉菜單允許您選擇帳戶計分模型。

![預測計分分發構件。](../images/account-profiles/predictive-scoring-distribution.png)

### 預測性評分最大影響因素 {#predictive-scoring-top-influential-factors}

的 [!UICONTROL 預測性評分最大影響因素] 小部件可幫助您瞭解推動每個傾向時段得分的最重要因素。

此小部件顯示了高、中和低傾向時段中每個時段的最主要影響因素。 每個影響因素的條表示該傾向時段中包含特定影響因素的帳戶配置檔案的百分比。

構件中的下拉菜單允許您選擇帳戶計分模型。

![預測性評分頂級影響因素小部件。](../images/account-profiles/predictive-scoring-top-influential-factors.png)

## 後續步驟

現在，您應該知道如何查找 [!UICONTROL 帳戶配置檔案] 控制項欄。 您還應瞭解可用小部件中顯示的度量。 要瞭解有關在Experience PlatformUI中將帳戶配置檔案作為B2B資料一部分的詳細資訊，請參閱 [帳戶概要資訊](../../rtcdp/accounts/account-profile-overview.md) Adobe Real-Time CDPB2B版。
