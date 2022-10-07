---
title: 帳戶設定檔控制面板指南
description: Adobe Experience Platform提供控制面板，讓您透過該控制面板檢視貴組織B2B帳戶設定檔的重要資訊。
exl-id: c9a3d786-6240-4ba4-96c8-05f658e1150c
source-git-commit: 19d6d3c03e6b3b0f9f82ceeee30816fa054261a3
workflow-type: tm+mt
source-wordcount: '1050'
ht-degree: 0%

---

# [!UICONTROL 帳戶設定檔] 儀表板

Adobe Experience Platform使用者介面(UI)提供控制面板，您可以透過控制面板檢視帳戶設定檔的重要資訊，如每日快照中所擷取。 本指南概述如何存取及使用 [!UICONTROL 帳戶設定檔] 控制面板，並提供控制面板中所顯示視覺效果的詳細資訊。

如需帳戶設定檔使用者介面中所有功能的概觀，請造訪 [帳戶設定檔UI指南](../../rtcdp/accounts/account-profile-ui-guide.md).

## 快速入門

您必須有權 [Real-time Customer Data Platform B2B版](../../rtcdp/b2b-overview.md) 以存取B2B [!UICONTROL 帳戶設定檔] 控制面板。

## 帳戶設定檔資料

此 [!UICONTROL 帳戶設定檔] 控制面板會顯示來自您的行銷管道的多個來源，以及您的組織目前用來儲存客戶帳戶資訊的不同系統的統一帳戶資訊快照。

快照中的配置檔案資料顯示的資料與拍攝快照時在特定時間點顯示的資料完全相同。 換句話說，快照不是資料的近似值或樣本，而且 [!UICONTROL 帳戶設定檔] 控制面板不會即時更新。

>[!NOTE]
>
>自拍攝快照以來對資料所做的任何更改或更新都不會反映在儀表板中，直到拍攝下一個快照。

## 探索 [!UICONTROL 帳戶設定檔] 儀表板

導覽至 [!UICONTROL 帳戶設定檔] 平台UI中的控制面板，請選取 **[!UICONTROL 設定檔]** 在 [!UICONTROL 帳戶] ，即可取得Advertising Cloud的說明。

![左側導覽中顯示「帳戶設定檔」的Platform UI，並顯示「概觀」標籤。](../images/account-profiles/account-profiles-dashboard.png)

從 [!UICONTROL 帳戶設定檔] 控制面板，您可以 [瀏覽匯入您組織的帳戶設定檔](#browse-account-profiles)，或 [使用widget快速檢視帳戶設定檔資料的完整](#standard-widgets) 視覺化資料的各個方面。

## 瀏覽帳戶設定檔 {#browse-account-profiles}

此 [!UICONTROL 瀏覽] 索引標籤可讓您使用來自連線企業來源的帳戶ID或直接輸入來源詳細資訊，來搜尋及檢視內嵌至您組織的唯讀帳戶設定檔。 從這裡，您可以看到屬於帳戶設定檔的重要資訊，包括名稱、產業、收入和區段等。

選取 [!UICONTROL 設定檔ID] 從 [!UICONTROL 瀏覽] 標籤來開啟 [!UICONTROL 詳細資料] 標籤。

![顯示結果的「帳戶配置檔案」瀏覽頁簽，突出顯示配置檔案ID。](../images/account-profiles/account-profiles-browse-tab.png)

顯示在 [!UICONTROL 詳細資料] 索引標籤已從多個設定檔片段合併在一起，以形成個別帳戶的單一檢視。 請參閱 [瀏覽Real-time Customer Data Platform的帳戶設定檔](../../rtcdp/accounts/account-profile-ui-guide.md#browse-account-profiles) 若要進一步了解Platform UI中的帳戶設定檔檢視功能。

## 此 [!UICONTROL 帳戶設定檔] [!UICONTROL 概述] {#overview}

此 [!UICONTROL 概述] 索引標籤由小工具組成，小工具可提供唯讀量度，以傳達關於帳戶設定檔的重要資訊。 選擇 **[!UICONTROL 修改控制面板]** 更改 [!UICONTROL 概述] 頁簽。

![「帳戶設定檔概述」標籤，並反白顯示「修改」控制面板。](../images/account-profiles/modify-dashboard.png)

請參閱 [修改控制面板](../customize/modify.md) 和 [介面工具集程式庫概觀](../customize/widget-library.md) 了解更多。

## 標準介面工具集 {#standard-widgets}

Adobe提供標準Widget，您可使用這些Widget來視覺化與帳戶設定檔相關的不同量度。

若要進一步了解每個可用的標準介面工具集，請從下列清單中選取介面工具集的名稱：

* [按行業分列的總帳](#total-accounts-by-industry)
* [新增帳戶設定檔](#account-profiles-added)
* [預測性計分分佈](#predictive-scoring-distribution)
* [預測性計分最具影響力的因素](#predictive-scoring-top-influential-factors)

### 按行業分列的總帳 {#total-accounts-by-industry}

此Widget會以單一量度顯示帳戶總數，並使用環圈圖來說明構成整體數量之產業的計數比例大小。 鍵為構成環圈圖的不同行業提供顏色編碼資訊。

當游標停留在環圈圖的相應部分上時，不同行業的單個計數將顯示在對話框中。

![按行業介面工具集列出的總帳。](../images/account-profiles/total-accounts-by-industry-widget.png)

### 新增帳戶設定檔 {#account-profiles-added}

此介面工具集使用色彩編碼的長條圖，來說明指定時段內新增至帳戶的設定檔數，以及構成這些新增設定檔的不同產業的比例。 這些行業都用顏色編碼，鍵為構成長條圖的不同行業提供顏色編碼資訊。 分析期間從介面工具集下拉式選單中選取。 長條圖可在30天、90天和12個月期間內視覺化。

>[!NOTE]
>
>由於設定檔只會新增至帳戶且從未移除，因此一段時間內新增的設定檔數量可能最低，為零。

![帳戶設定檔新增了介面工具集。](../images/account-profiles/accounts-profiles-added-widget.png)

### 預測性計分分佈 {#predictive-scoring-distribution}

此 [!UICONTROL 預測性計分分佈] 介面工具集顯示所有帳戶設定檔的分數分佈，幫助您了解銷售管道的狀況，一覽無遺。 計分資料通過環圈圖和列圖傳送。

環圈圖說明在高、中、低購買貯體的傾向中，帳戶設定檔總數的比例。 索引鍵提供色彩編碼的區段的詳細資訊，包括計分貯體範圍及該範圍中的帳戶設定檔數目。

欄圖表提供更精細的計分劃分。 每欄會顯示20個五點增量貯體中每個貯體的帳戶設定檔數量。

介面工具集內的下拉式功能表可讓您選取帳戶計分模型。

![預測性計分分分佈介面工具集。](../images/account-profiles/predictive-scoring-distribution.png)

### 預測性計分最具影響力的因素 {#predictive-scoring-top-influential-factors}

此 [!UICONTROL 預測性計分最具影響力的因素] 介面工具集可協助您了解促成每個傾向貯體之分數的最重要因素。

此Widget會顯示高、中、低傾向貯體中每個的最高影響因素。 每個影響因素的長條代表該傾向貯體中包含特定影響因素的帳戶設定檔百分比。

介面工具集內的下拉式功能表可讓您選取帳戶計分模型。

![預測性計分最具影響力的因素Widget。](../images/account-profiles/predictive-scoring-top-influential-factors.png)

## 後續步驟

依照本檔案操作，您現在應了解如何找到 [!UICONTROL 帳戶設定檔] 控制面板。 您也應了解可用介面工具集中顯示的量度。 若要進一步了解如何在Experience PlatformUI中使用帳戶設定檔作為B2B資料的一部分，請參閱 [帳戶設定檔概觀](../../rtcdp/accounts/account-profile-overview.md) Adobe Real-Time CDP的B2B版。
