---
title: 帳戶設定檔儀表板指南
description: Adobe Experience Platform提供控制面板，讓您檢視有關組織B2B帳戶設定檔的重要資訊。
exl-id: c9a3d786-6240-4ba4-96c8-05f658e1150c
source-git-commit: 79966442f5333363216da17342092a71335a14f0
workflow-type: tm+mt
source-wordcount: '1052'
ht-degree: 0%

---

# [!UICONTROL 帳戶設定檔] 儀表板

Adobe Experience Platform使用者介面(UI)提供儀表板，您可透過儀表板檢視有關帳戶設定檔的重要資訊，如每日快照期間所擷取。 本指南概述如何存取及使用 [!UICONTROL 帳戶設定檔] UI中的控制面板，並提供控制面板中顯示之視覺效果的詳細資訊。

如需帳戶設定檔使用者介面中所有功能的概述，請造訪 [帳戶設定檔UI指南](../../rtcdp/accounts/account-profile-ui-guide.md).

## 快速入門

您必須有權使用 [Adobe Real-time Customer Data Platform B2B版本](../../rtcdp/b2b-overview.md) 以存取B2B [!UICONTROL 帳戶設定檔] 儀表板。

## 帳戶設定檔資料

此 [!UICONTROL 帳戶設定檔] 儀表板會顯示您的行銷管道的多個來源，以及貴組織目前用來儲存客戶帳戶資訊的各種系統的整合帳戶資訊快照。

快照中的設定檔資料顯示的資料與拍攝快照的特定時間點完全相同。 換言之，快照不是資料的近似或樣本，而且 [!UICONTROL 帳戶設定檔] 儀表板未即時更新。

>[!NOTE]
>
>自拍攝快照以來對資料所做的任何變更或更新都不會反映在儀表板中，直到拍攝下一個快照為止。

## 探索 [!UICONTROL 帳戶設定檔] 儀表板

若要導覽至 [!UICONTROL 帳戶設定檔] 在Platform UI中，選取 **[!UICONTROL 設定檔]** 在 [!UICONTROL 帳戶] ，位於左側導覽面板中。

![左側導覽中具有帳戶設定檔的Platform UI會醒目提示，並會顯示概觀標籤。](../images/account-profiles/account-profiles-dashboard.png)

從 [!UICONTROL 帳戶設定檔] 控制面板，您可以 [瀏覽擷取到您組織中的帳戶設定檔](#browse-account-profiles)，或 [使用Widget快速檢視您帳戶設定檔資料的完整內容](#standard-widgets) 以視覺效果呈現資料的各方面。

## 瀏覽帳戶設定檔 {#browse-account-profiles}

此 [!UICONTROL 瀏覽] 索引標籤可讓您使用連線企業來源的帳戶ID或直接輸入來源詳細資訊，來搜尋及檢視擷取到您組織的唯讀帳戶設定檔。 從這裡，您可以看到屬於帳戶個人資料的重要資訊，包括其名稱、產業、收入和對象等。

選取 [!UICONTROL 設定檔ID] 結果顯示在 [!UICONTROL 瀏覽] 標籤以開啟 [!UICONTROL 詳細資料] 帳戶設定檔的標籤。

![「帳戶設定檔」瀏覽標籤會顯示結果，且設定檔ID會反白顯示。](../images/account-profiles/account-profiles-browse-tab.png)

顯示在上的帳戶設定檔資訊 [!UICONTROL 詳細資料] 索引標籤已從多個設定檔片段合併在一起，以形成個別帳戶的單一檢視。 請參閱以下檔案： [在Adobe Real-time Customer Data Platform中瀏覽帳戶設定檔](../../rtcdp/accounts/account-profile-ui-guide.md#browse-account-profiles) 以進一步瞭解Platform UI中的帳戶設定檔檢視功能。

## 此 [!UICONTROL 帳戶設定檔] [!UICONTROL 概觀] {#overview}

此 [!UICONTROL 概觀] tab由小工具組成，提供唯讀量度，傳達有關您帳戶設定檔的重要資訊。 選取 **[!UICONTROL 修改儀表板]** 變更 [!UICONTROL 概觀] 移動Widget並調整其大小以定位。

![帳號設定檔概述索引標籤中反白顯示修改儀表板。](../images/account-profiles/modify-dashboard.png)

請參考以下檔案： [修改儀表板](../customize/modify.md) 和 [Widget程式庫概觀](../customize/widget-library.md) 以進一步瞭解。

## 標準Widget {#standard-widgets}

Adobe提供標準的Widget，您可用來視覺化與帳戶設定檔相關的不同量度。

若要進一步瞭解每個可用的標準Widget，請從下列清單中選取Widget的名稱：

* [依產業區分的帳戶總數](#total-accounts-by-industry)
* [帳戶設定檔已新增](#account-profiles-added)
* [預測性評分分佈](#predictive-scoring-distribution)
* [預測性評分主要影響因素](#predictive-scoring-top-influential-factors)

### 依產業區分的帳戶總數 {#total-accounts-by-industry}

此Widget會顯示單一量度中的帳戶總數，並使用環形圖來說明構成整體數字的產業中計數比例大小。 索引鍵提供組成環圈圖之不同產業的色彩編碼資訊。

當游標暫留在環圈圖的個別區段上時，不同產業的個人計數會顯示在對話方塊中。

![依產業Widget區分的帳戶總數。](../images/account-profiles/total-accounts-by-industry-widget.png)

### 帳戶設定檔已新增 {#account-profiles-added}

此Widget會使用色彩編碼的長條圖，說明在指定期間內新增至帳戶的設定檔計數，以及構成這些新增設定檔的不同行業比例。 各產業皆以不同色彩編碼，按鍵會針對組成長條圖的不同產業提供色彩編碼資訊。 分析期間是從Widget下拉式選單中選取。 長條圖可在30天、90天和12個月期間進行視覺化。

>[!NOTE]
>
>由於設定檔只會新增至帳戶，永遠不會移除，因此一段時間內新增的設定檔最低數量為零。

![帳戶設定檔已新增Widget。](../images/account-profiles/accounts-profiles-added-widget.png)

### 預測性評分分佈 {#predictive-scoring-distribution}

此 [!UICONTROL 預測性評分分佈] widget會顯示所有帳戶設定檔的分數分佈，協助您一眼瞭解銷售管道的狀況。 評分資料會透過環形圖和直條圖傳送。

環形圖可說明您的帳戶設定檔總數在高、中及低購買值區傾向中的比例。 索引鍵提供色碼區段的詳細資訊，包括評分貯體範圍及該範圍內的帳戶設定檔數量。

柱狀圖提供更細微的評分劃分。 每欄顯示20個五點增量貯體中每個的帳戶設定檔數。

Widget中的下拉式功能表可讓您選取帳戶評分模式。

![預測性評分分佈Widget。](../images/account-profiles/predictive-scoring-distribution.png)

### 預測性評分主要影響因素 {#predictive-scoring-top-influential-factors}

此 [!UICONTROL 預測性評分主要影響因素] widget可協助您瞭解驅動每個傾向性貯體分數的最重要因素。

此Widget會顯示每個高、中及低傾向值區的主要影響因素。 每個影響因子的橫條會指出該傾向性貯體中包含特定影響因子的帳戶設定檔百分比。

Widget中的下拉式功能表可讓您選取帳戶評分模式。

![預測性評分主要影響因素Widget。](../images/account-profiles/predictive-scoring-top-influential-factors.png)

## 後續步驟

依照本檔案操作，您現在應該知道如何找到 [!UICONTROL 帳戶設定檔] 儀表板。 您也應該瞭解可用介面工具列中顯示的量度。 若要進一步瞭解如何在Experience Platform UI中使用帳戶設定檔做為B2B資料的一部分，請參閱 [帳戶設定檔概述](../../rtcdp/accounts/account-profile-overview.md) 適用於Adobe Real-Time CDP， B2B Edition。
