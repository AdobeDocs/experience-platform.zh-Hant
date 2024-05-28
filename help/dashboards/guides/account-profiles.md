---
title: 帳戶設定檔儀表板
description: Adobe Experience Platform提供控制面板，讓您檢視有關組織B2B帳戶設定檔的重要資訊。
exl-id: c9a3d786-6240-4ba4-96c8-05f658e1150c
source-git-commit: 4f67df5d3667218c79504535534de57f871b0650
workflow-type: tm+mt
source-wordcount: '1675'
ht-degree: 1%

---

# [!UICONTROL 帳戶設定檔] 儀表板

Adobe Experience Platform使用者介面(UI)提供儀表板，您可透過儀表板檢視有關帳戶設定檔的重要資訊，如每日快照期間所擷取。 本指南概述如何存取及使用 [!UICONTROL 帳戶設定檔] UI中的控制面板，並提供控制面板中顯示之視覺效果的詳細資訊。

本檔案提供內的功能概觀 [!UICONTROL 帳戶設定檔] 儀表板和詳細說明可用的標準深入分析。 請參閱 [[!UICONTROL 帳戶設定檔] UI指南](../../rtcdp/accounts/account-profile-ui-guide.md) 以取得其可用功能的完整細節。

## 快速入門

您必須有權使用 [Adobe Real-time Customer Data Platform B2B版本](../../rtcdp/b2b-overview.md) 存取B2B [!UICONTROL 帳戶設定檔] 儀表板。

## 帳戶設定檔資料 {#data}

此 [!UICONTROL 帳戶設定檔] 儀表板會顯示整合帳戶資訊的快照。 此帳戶資訊來自於行銷管道的多個來源，以及貴組織目前用來儲存客戶帳戶資訊的各種系統。

快照中的設定檔資料顯示的資料與拍攝快照的特定時間點完全相同。 換言之，快照不是資料的近似或樣本，而且 [!UICONTROL 帳戶設定檔] 儀表板未即時更新。

>[!NOTE]
>
>自拍攝快照以來對資料所做的任何變更或更新都不會反映在儀表板中，直到拍攝下一個快照為止。

## 探索 [!UICONTROL 帳戶設定檔] 儀表板 {#explore}

若要導覽至 [!UICONTROL 帳戶設定檔] 在Platform UI中，選取 **[!UICONTROL 設定檔]** 在 [!UICONTROL 帳戶] ，位於左側導覽面板中。

![左側導覽中具有帳戶設定檔的Platform UI會醒目提示，並會顯示概觀標籤。](../images/account-profiles/account-profiles-dashboard.png)

從 [!UICONTROL 帳戶設定檔] 控制面板，您可以 [瀏覽擷取到您組織中的帳戶設定檔](#browse-account-profiles)，或 [使用Widget快速檢視您帳戶設定檔資料的完整內容](#standard-widgets).

### 日期篩選器 {#date-filter}

此 [!UICONTROL 概觀] tab由小工具組成，提供唯讀量度，傳達有關您帳戶設定檔的重要資訊。 選取行事曆圖示或日期，以變更Widget的全域日期篩選。

>[!IMPORTANT]
>
>您在下拉式行事曆中選取的日期範圍會影響所有深入分析，但兩個預測性評分Widget除外([分佈](#predictive-scoring-distribution) 和 [主要影響因素](#predictive-scoring-top-influential-factors))。

![帳戶設定檔概述索引標籤，其中醒目顯示日期選擇器和篩選器圖示。](../images/account-profiles/date-filter.png)

### 設定銷售機會至帳戶比對服務 {#lead-to-account-matching-service}

選取 **[!UICONTROL 設定]** 若要設定銷售線索與帳戶的比對服務，請從 [!UICONTROL 帳戶設定] 對話方塊。 如需有關如何設定銷售線索與帳戶比對的完整詳細資訊，請參閱 [UI指南](../../rtcdp/accounts/account-profile-ui-guide.md#configure-lead-to-account-matching). 若要進一步瞭解銷售線索與帳戶的比對，請參閱 [在Real-Time CDP B2B檔案中導致帳戶相符](../../rtcdp/b2b-ai-ml-services/lead-to-account-matching.md).

![反白顯示設定的「帳戶設定檔」控制面板。](../images/account-profiles/settings.png)

## 瀏覽帳戶設定檔 {#browse-account-profiles}

從 [!UICONTROL 瀏覽] 索引標籤上，您可以搜尋並檢視擷取到您組織中的唯讀帳戶設定檔。 使用連線企業來源的帳戶ID或直接輸入來源詳細資料。 在此工作區中，您可以檢視屬於帳戶個人資料的重要資訊，包括其名稱、產業、收入和對象等。

選取 [!UICONTROL 設定檔ID] 結果顯示在 [!UICONTROL 瀏覽] 標籤以開啟 [!UICONTROL 詳細資料] 帳戶設定檔的標籤。

![「帳戶設定檔」瀏覽標籤會顯示結果，且設定檔ID會反白顯示。](../images/account-profiles/account-profiles-browse-tab.png)

顯示在上的帳戶設定檔資訊 [!UICONTROL 詳細資料] 索引標籤已從多個設定檔片段合併在一起，以形成個別帳戶的單一檢視。 請參閱以下檔案： [在Adobe Real-time Customer Data Platform中瀏覽帳戶設定檔](../../rtcdp/accounts/account-profile-ui-guide.md#browse-account-profiles) 以進一步瞭解Platform UI中的帳戶設定檔檢視功能。

## 標準Widget {#standard-widgets}

Adobe提供標準的Widget，您可用來視覺化與帳戶設定檔相關的不同量度。

>[!IMPORTANT]
>
>如果您未提供日期篩選器，前瞻分析的預設行為會分析從前一年到今天新增的資料。

若要進一步瞭解每個可用的標準Widget，請從下列清單中選取Widget的名稱：

* [已新增的帳戶設定檔](#account-profiles-added)
* [依產業的新帳戶](#accounts-by-industry)
* [新帳戶（依型別）](#accounts-by-type)
* [依個人角色的新機會](#opportunities-by-person-role)
* [按收入顯示的新商機](#opportunities-by-revenue)
* [按狀態和階段的新機會](#opportunities-by-status-&-stage)
* [贏得新商機](#opportunities-won)
* [已新增的機會](#opportunities-added)
* [預測性評分分佈](#predictive-scoring-distribution)
* [預測性評分主要影響因素](#predictive-scoring-top-influential-factors)

### 已新增的帳戶設定檔 {#account-profiles-added}

此 [!UICONTROL 帳戶設定檔已新增] Widget使用線圖來顯示一段時間內每天新增的帳戶設定檔數。 使用位於儀表板頂端的全域日期篩選器來決定分析時段。 如果未提供日期篩選器，預設行為會列出今天之前一年新增的帳戶設定檔。 結果可用於推斷新增的帳戶設定檔數量趨勢。

![帳戶設定檔已新增Widget。](../images/account-profiles/account-profiles-added.png)

### 依產業的新帳戶 {#accounts-by-industry}

此 [!UICONTROL 依產業的新帳戶] widget會顯示環形圖內單一量度的帳戶總數。 環圈圖說明了組成此總計的不同產業的相對組成。 以色彩編碼的索引鍵提供所有包含的產業劃分。 當游標暫留在環圈圖的個別區段上時，會在對話方塊中顯示每個產業的個人計數。

![依產業Widget的新帳戶。](../images/account-profiles/new-accounts-by-industry.png)

### 新帳戶（依型別） {#accounts-by-type}

此 [!UICONTROL 新帳戶（依型別）] widget會顯示環形圖內單一量度的帳戶總數。 環形圖說明構成此總計的不同帳戶型別的相對組成。 以色彩編碼的金鑰提供所有包含的帳戶型別的劃分。 當游標暫留在環圈圖的個別區段上時，每種型別的帳戶個別計數都會顯示在對話方塊中。

![新帳戶（依型別Widget）。](../images/account-profiles/new-accounts-by-type.png)

### 依個人角色的新機會 {#opportunities-by-person-role}

此 [!UICONTROL 依個人角色的新機會] widget會在環形圖內的單一量度中顯示您的機會總數。 環圈圖說明構成此機會總數的角色相對組成。 以色彩編碼的金鑰提供所有包含角色的劃分。 當游標暫留在環圈圖的個別區段上時，每個角色的個別計數都會顯示在對話方塊中。

>[!NOTE]
>
>此 [!UICONTROL 找不到資料] 或 [!UICONTROL 無法載入] 未在結構描述中使用「Opportunity-Person」橋接表格時，會導致錯誤。 如果您的分析顯示其中一個錯誤，請檢查您的聯合結構描述，並確定「機會 — 人員」欄位群組正在擷取資料。

![依人員角色的新機會Widget。](../images/account-profiles/new-opportunities-by-person-role.png)

### 按收入顯示的新商機 {#opportunities-by-revenue}

此 [!UICONTROL 按收入顯示的新商機] widget使用長條圖來說明您的商機所產生的預估收入總額。 Widget最多可支援六個機會。

若要檢視包含商機之特定收入總計的對話方塊，請使用游標暫留在個別長條上。

![依收入分類的新商機Widget。](../images/account-profiles/new-opportunities-by-revenue.png)

### 按狀態和階段的新機會 {#opportunities-by-status-&-stage}

此Widget使用長條圖來說明在行銷/銷售漏斗的所有階段中開啟或關閉的機會數量。 Widget會使用顏色來區分機會的階段。 以色彩編碼的索引鍵表示商機的可用階段。

![按狀態和階段Widget顯示的新商機。](../images/account-profiles/new-opportunities-by-status-&-stage.png)

### 贏得新商機 {#opportunities-won}

此 [!UICONTROL 贏得新商機] widget會在環形圖中顯示已在單一量度中成功完成的業務機會總數。 環圈圖可說明成功或失敗機會的相對組成。 以色彩編碼的金鑰會區分成功與未成功的商機。 當游標暫留在環圈圖的個別區段上時，每個角色的個別計數都會顯示在對話方塊中。

![新機會贏得了Widget。](../images/account-profiles/new-opportunities-won.png)

### 已新增的機會 {#opportunities-added}

此 [!UICONTROL 機會已新增] Widget使用線圖來顯示一段時間中每天新增的機會數量。 使用位於儀表板頂端的全域日期篩選器來決定分析時段。 如果未提供日期篩選，預設行為會列出今天之前一年新增的機會。 這些結果可用來推斷新增商機數量的趨勢。

<!-- Link to date filter documentation from Annamalai -->

![機會已新增Widget。](../images/account-profiles/opportunities-added.png)

### 預測性評分分佈 {#predictive-scoring-distribution}

此 [!UICONTROL 預測性評分分佈] widget會顯示所有帳戶設定檔的分數分佈，協助您一眼瞭解銷售管道的狀況。 評分資料會透過環形圖和直條圖傳送。

環形圖可說明您的帳戶設定檔總數在高、中及低購買值區傾向中的比例。 索引鍵提供色碼區段的詳細資訊，包括評分貯體範圍及該範圍內的帳戶設定檔數量。

柱狀圖提供更細微的評分劃分。 每欄顯示20個五點增量貯體中每個的帳戶設定檔數。

Widget中的下拉式功能表可讓您選取帳戶評分模式。

>[!NOTE]
>
>全域日期範圍篩選器不適用於預測性評分深入分析。 預測性評分Widget會根據下拉式清單中選取的帳戶評分模型分析資料。

![預測性評分分佈Widget。](../images/account-profiles/predictive-scoring-distribution.png)

### 預測性評分主要影響因素 {#predictive-scoring-top-influential-factors}

此 [!UICONTROL 預測性評分主要影響因素] widget可協助您瞭解驅動每個傾向性貯體分數的最重要因素。

此Widget會顯示每個高、中及低傾向值區的主要影響因素。 每個影響因子的橫條會指出該傾向性貯體中包含特定影響因子的帳戶設定檔百分比。

Widget中的下拉式功能表可讓您選取帳戶評分模式。

>[!NOTE]
>
>全域日期範圍篩選器不適用於預測性評分深入分析。 預測性評分Widget會根據下拉式清單中選取的帳戶評分模型分析資料。

![預測性評分主要影響因素Widget。](../images/account-profiles/predictive-scoring-top-influential-factors.png)

## 後續步驟

依照本檔案操作，您現在應該知道如何找到 [!UICONTROL 帳戶設定檔] 儀表板，也瞭解可用介面工具列中顯示的量度。 若要進一步瞭解如何在Experience Platform UI中使用帳戶設定檔做為B2B資料的一部分，請參閱 [帳戶設定檔概述](../../rtcdp/accounts/account-profile-overview.md) 適用於Adobe Real-Time CDP， B2B Edition。
