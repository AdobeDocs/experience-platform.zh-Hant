---
title: 帳戶設定檔儀表板
description: Adobe Experience Platform提供控制面板，讓您檢視有關組織B2B帳戶設定檔的重要資訊。
exl-id: c9a3d786-6240-4ba4-96c8-05f658e1150c
source-git-commit: 442fcee17cbe38a9e1608324581ebedee4ba7fe6
workflow-type: tm+mt
source-wordcount: '2362'
ht-degree: 4%

---

# 帳戶設定檔儀表板

Adobe Experience Platform使用者介面(UI)提供儀表板，您可透過儀表板檢視有關帳戶設定檔的重要資訊，如每日快照期間所擷取。 本指南概述如何在UI中存取及使用[!UICONTROL 帳戶設定檔]儀表板，並提供有關儀表板中顯示之視覺效果的詳細資訊。

本檔案概述[!UICONTROL 帳戶設定檔]儀表板中的功能，並詳細說明可用的標準深入分析。 請參閱[[!UICONTROL 帳戶設定檔] UI指南](../../rtcdp/accounts/account-profile-ui-guide.md)，以取得其可用功能的完整詳細資訊。

## 快速入門

您必須有[Adobe Real-time Customer Data Platform B2B edition](../../rtcdp/b2b-overview.md)的許可權，才能存取B2B [!UICONTROL 帳戶設定檔]儀表板。

## 帳戶設定檔資料 {#data}

[!UICONTROL 帳戶設定檔]儀表板會顯示您整合式帳戶資訊的快照。 此帳戶資訊來自於行銷管道的多個來源，以及貴組織目前用來儲存客戶帳戶資訊的各種系統。

快照中的設定檔資料顯示的資料與拍攝快照的特定時間點完全相同。 換句話說，快照集不是資料的近似或範例，且[!UICONTROL 帳戶設定檔]儀表板不會即時更新。

>[!NOTE]
>
>自拍攝快照以來對資料所做的任何變更或更新都不會反映在儀表板中，直到拍攝下一個快照為止。

## 探索[!UICONTROL 帳戶設定檔]儀表板 {#explore}

若要導覽至Platform UI中的[!UICONTROL 帳戶設定檔]儀表板，請在左側導覽面板的[!UICONTROL 帳戶]下選取&#x200B;**[!UICONTROL 設定檔]**。

![左側導覽中具有帳戶設定檔的Platform UI反白顯示，且總覽標籤顯示。](../images/account-profiles/account-profiles-dashboard.png)

從[!UICONTROL 帳戶設定檔]儀表板，您可以[瀏覽擷取到您組織的帳戶設定檔](#browse-account-profiles)，或[使用Widget](#standard-widgets)檢視您完整的帳戶設定檔資料。

### 日期篩選器 {#date-filter}

[!UICONTROL 總覽]標籤是由提供唯讀量度的Widget所組成，可傳達有關您帳戶設定檔的重要資訊。 選取行事曆圖示或日期，以變更Widget的全域日期篩選。

>[!IMPORTANT]
>
>您在下拉式行事曆中選取的日期範圍會影響所有深入分析，但兩個預測性評分Widget除外（[分佈](#predictive-scoring-distribution)和[主要影響因素](#predictive-scoring-top-influential-factors)）。

![帳號設定檔總覽索引標籤，日期選擇器和篩選器圖示會醒目提示。](../images/account-profiles/date-filter.png)

### 設定銷售機會至帳戶比對服務 {#lead-to-account-matching-service}

選取&#x200B;**[!UICONTROL 設定]**&#x200B;以從[!UICONTROL 帳戶設定]對話方塊設定銷售機會與帳戶比對服務。 如需有關如何設定銷售機會與帳戶比對的完整詳細資訊，請參閱[UI指南](../../rtcdp/accounts/account-profile-ui-guide.md#configure-lead-to-account-matching)。 若要進一步瞭解銷售機會與帳戶的比對，請參閱Real-Time CDP B2B檔案](../../rtcdp/b2b-ai-ml-services/lead-to-account-matching.md)中的[銷售機會與帳戶的比對。

![設定反白的帳戶設定檔儀表板。](../images/account-profiles/settings.png)

## 瀏覽帳戶設定檔 {#browse-account-profiles}

從[!UICONTROL 瀏覽]索引標籤，您可以搜尋並檢視擷取至您組織的唯讀帳戶設定檔。 使用連線企業來源的帳戶ID或直接輸入來源詳細資料。 在此工作區中，您可以檢視屬於帳戶個人資料的重要資訊，包括其名稱、產業、收入和對象等。

從[!UICONTROL 瀏覽]標籤上顯示的結果中選取[!UICONTROL 設定檔識別碼]，以開啟帳戶設定檔的[!UICONTROL 詳細資料]標籤。

![「帳戶設定檔」瀏覽標籤，顯示結果並反白顯示設定檔ID。](../images/account-profiles/account-profiles-browse-tab.png)

[!UICONTROL 詳細資料]標籤上顯示的帳戶設定檔資訊已從多個設定檔片段合併在一起，以形成個別帳戶的單一檢視。 請參閱有關[在Adobe Real-time Customer Data Platform](../../rtcdp/accounts/account-profile-ui-guide.md#browse-account-profiles)中瀏覽帳戶設定檔的檔案，以進一步瞭解Platform UI中的帳戶設定檔檢視功能。

## 標準 Widget {#standard-widgets}

>[!CONTEXTUALHELP]
>id="platform_dashboards_accountprofiles_customersperaccountoverview"
>title="每個帳戶的客戶概觀"
>abstract="此鑽研 Widget 能夠讓您深入分析 B2B 資料的結構。其能幫助您確定有多少帳戶設定檔沒有連結客戶設定檔，或者與一個或多個客戶設定檔相關聯。<ul><li>直接客戶：透過 `personComponents` 路徑直接連結至帳戶的客戶設定檔。</li><li>間接客戶：透過 `Account-Person` 路徑連結至帳戶的客戶設定檔。</li></ul>"

Adobe提供標準的Widget，您可用來視覺化與帳戶設定檔相關的不同量度。

>[!IMPORTANT]
>
>如果您未提供日期篩選器，前瞻分析的預設行為會分析從前一年到今天新增的資料。

若要進一步瞭解每個可用的標準Widget，請從下列清單中選取Widget的名稱：

* [已新增的帳戶輪廓](#account-profiles-added)
* [每個帳戶的客戶概觀](#customers-per-account-overview)
   * [每個客戶的機會概覽](#opportunities-per-account-overview)
   * [每個客戶的商機詳細資料](#opportunities-per-account-detail)
   * [每個帳戶的客戶詳細資料](#customers-per-account-detail)
* [依產業的新帳戶](#accounts-by-industry)
* [新帳戶（依型別）](#accounts-by-type)
* [依個人角色的新機會](#opportunities-by-person-role)
* [按收入顯示的新商機](#opportunities-by-revenue)
* [按狀態和階段的新機會](#opportunities-by-status-&-stage)
* [贏得新商機](#opportunities-won)
* [已新增的機會](#opportunities-added)
* [預測性評分分佈](#predictive-scoring-distribution)
* [預測性評分主要影響因素](#predictive-scoring-top-influential-factors)

### 已新增的帳戶輪廓 {#account-profiles-added}

[!UICONTROL 新增的帳戶設定檔] Widget會使用線圖來顯示一段時間內每天新增的帳戶設定檔數目。 使用位於儀表板頂端的全域日期篩選器來決定分析時段。 如果未提供日期篩選器，預設行為會列出今天之前一年新增的帳戶設定檔。 結果可用於推斷新增的帳戶設定檔數量趨勢。

![帳戶設定檔已新增Widget。](../images/account-profiles/account-profiles-added.png)

### 每個帳戶的客戶概觀 {#customers-per-account-overview}

[!UICONTROL 每個帳戶的客戶總覽]圖表會根據其客戶型別提供帳戶的摘要。 它會顯示一個四清單格，將帳戶分類為擁有直接或間接客戶，或沒有直接或間接客戶的帳戶。 它提供每個類別的帳戶總數。 圖表可協助識別具有直接與間接客戶的科目分配。

直接客戶是透過`personComponents`路徑直接連結至帳戶的客戶設定檔。 這種關係更為直接，並涉及客戶與帳戶之間的直接、明確連線。

間接客戶是透過`Account-Person`路由連結至帳戶的客戶設定檔。 這種關係較不直接，且涉及中間實體或客戶與帳戶之間更複雜的連線，通常透過其他帳戶或關係進行。

![每個帳戶的客戶總覽Widget。](../images/account-profiles/customers-per-account-overview-widget.png)

若要存取更詳細的深入分析，請在[!UICONTROL 每個帳戶的客戶總覽]圖表上選取橢圓(**...**)，然後從下拉式選單中選擇&#x200B;**[!UICONTROL 鑽研]**。

![每個帳戶的客戶總覽Widget，其橢圓下拉式功能表和Drill through反白顯示。](../images/account-profiles/customers-per-account-overview-dropdown.png)

鑽研檢視隨即顯示。 接下來，探索可用的鑽研圖表，以更深入地瞭解B2B資料的結構。 您可以使用這些鑽研圖表來識別有多少帳戶設定檔未連結客戶設定檔，或有一或多個客戶設定檔與其相關聯。 您也可以使用它們來識別有多少直接或間接客戶與您的帳戶相關聯。

* [[!UICONTROL 每個帳戶的客戶詳細資料]](#customers-per-account-detail)
* [[!UICONTROL 每個機會的帳戶總覽]](#accounts-per-opportunity-overview)
* [每個帳戶詳細資料的[!UICONTROL 商機]](#accounts-per-opportunity-detail)

### [!UICONTROL 在儀表板檢視之間導覽] {#dashboard-view-navigation}

若要在鑽研與「帳戶設定檔」儀表板之間切換，請選取資料夾圖示(![資料夾圖示。](../images/account-profiles/folder-icon.png))，接著在下拉式功能表中顯示正確的檢視。

![帳戶設定檔儀表板中的鑽研檢視中，導覽下拉式功能表反白顯示。](../images/account-profiles/navigation-dropdown.png)

若要進一步瞭解Platform UI中的鑽研，請參閱[鑽研指南](../sql-insights-query-pro-mode/drill-through.md)。

#### [!UICONTROL 每個帳戶的客戶詳細資料] {#customers-per-account-detail}

[!UICONTROL 每個帳戶的客戶詳細資料]圖表提供更細微的詳細資料，說明與不同客戶型別相關聯的帳戶數目。 它會顯示一個三欄表格，詳列按客戶型別（直接或間接）區分的帳戶數目，以及與帳戶相關聯的客戶範圍。 此圖表可協助您瞭解客戶在不同客戶類別中的分配方式，以及與每個類別相關聯的帳戶總數。

![每個帳戶的客戶詳細資料Widget。](../images/account-profiles/customers-per-account-detail.png)

#### [!UICONTROL 每個帳戶的機會] {#opportunities-per-account-overview}

每個帳戶的[!UICONTROL 商機概觀]圖表會顯示有或沒有商機的帳戶摘要。 此雙資料清單格有助於快速判斷與商機相關聯的帳戶數量，提供跨帳戶商機參與情形的快照。

![每個帳戶的機會概觀Widget。](../images/account-profiles/opportunities-per-account-overview.png)

#### 每個帳戶詳細資料的[!UICONTROL 商機] {#opportunities-per-account-detail}

每個帳戶的[!UICONTROL 商機詳細資料]圖表會根據客戶的商機數量，提供更詳細的帳戶劃分。 此表格顯示依商機計數範圍分組的科目數目，例如1-10個商機或100+個商機。 此圖表可協助您識別科目如何依其管理的商機數量分配。

![每個帳戶的機會Widget.](../images/account-profiles/opportunities-per-account-detail.png)

### 依產業的新帳戶 {#accounts-by-industry}

依產業分類的[!UICONTROL 新帳戶] Widget會在環形圖內顯示單一量度中的帳戶總數。 環圈圖說明了組成此總計的不同產業的相對組成。 以色彩編碼的索引鍵提供所有包含的產業劃分。 當游標暫留在環圈圖的個別區段上時，會在對話方塊中顯示每個產業的個人計數。

![依產業Widget的新帳戶。](../images/account-profiles/new-accounts-by-industry.png)

### 新帳戶（依型別） {#accounts-by-type}

依型別]的[!UICONTROL 新帳戶Widget會在環形圖內顯示單一量度中的帳戶總數。 環形圖說明構成此總計的不同帳戶型別的相對組成。 以色彩編碼的金鑰提供所有包含的帳戶型別的劃分。 當游標暫留在環圈圖的個別區段上時，每種型別的帳戶個別計數都會顯示在對話方塊中。

![依型別Widget的新帳戶。](../images/account-profiles/new-accounts-by-type.png)

### 依個人角色的新機會 {#opportunities-by-person-role}

[!UICONTROL 依人員角色的新商機] Widget會在環形圖內的單一量度中顯示商機總數。 環圈圖說明構成此機會總數的角色相對組成。 以色彩編碼的金鑰提供所有包含角色的劃分。 當游標暫留在環圈圖的個別區段上時，每個角色的個別計數都會顯示在對話方塊中。

>[!NOTE]
>
>結構描述中未使用&#39;Opportunity-Person&#39; bridge-table時，造成[!UICONTROL 找不到資料]或[!UICONTROL 無法載入]錯誤。 如果您的分析顯示其中一個錯誤，請檢查您的聯合結構描述，並確定「機會 — 人員」欄位群組正在擷取資料。

![依人員角色的新機會Widget。](../images/account-profiles/new-opportunities-by-person-role.png)

### 按收入顯示的新商機 {#opportunities-by-revenue}

按收入]列出的[!UICONTROL 新商機Widget使用長條圖來說明商機所產生的預估收入總額。 Widget最多可支援六個機會。

若要檢視包含商機之特定收入總計的對話方塊，請使用游標暫留在個別長條上。

![依據收入Widget的新商機。](../images/account-profiles/new-opportunities-by-revenue.png)

### 按狀態與階段{#opportunities-by-status-&-stage}的新商機

此Widget使用長條圖來說明在行銷/銷售漏斗的所有階段中開啟或關閉的機會數量。 Widget會使用顏色來區分機會的階段。 以色彩編碼的索引鍵表示商機的可用階段。

![依據狀態和階段Widget的新商機。](../images/account-profiles/new-opportunities-by-status-&-stage.png)

### 贏得新商機 {#opportunities-won}

[!UICONTROL 新機會贏得了]個Widget會在環形圖中顯示已在單一量度中成功完成的機會總數。 環圈圖可說明成功或失敗機會的相對組成。 以色彩編碼的金鑰會區分成功與未成功的商機。 當游標暫留在環圈圖的個別區段上時，每個角色的個別計數都會顯示在對話方塊中。

![新機會贏得Widget。](../images/account-profiles/new-opportunities-won.png)

### 已新增的機會 {#opportunities-added}

新增的[!UICONTROL 商機] Widget會使用折線圖來顯示一段時間內每天新增商機的數量。 使用位於儀表板頂端的全域日期篩選器來決定分析時段。 如果未提供日期篩選，預設行為會列出今天之前一年新增的機會。 這些結果可用來推斷新增商機數量的趨勢。

<!-- Link to date filter documentation from Annamalai -->

![機會已新增Widget。](../images/account-profiles/opportunities-added.png)

### 預測性評分分佈 {#predictive-scoring-distribution}

[!UICONTROL 預測性評分分佈] Widget會顯示所有帳戶設定檔的分數分佈，以幫助您一眼就瞭解銷售管道的狀況。 評分資料會透過環形圖和直條圖傳送。

環形圖可說明您的帳戶設定檔總數在高、中及低購買值區傾向中的比例。 索引鍵提供色碼區段的詳細資訊，包括評分貯體範圍及該範圍內的帳戶設定檔數量。

柱狀圖提供更細微的評分劃分。 每欄顯示20個五點增量貯體中每個的帳戶設定檔數。

Widget中的下拉式功能表可讓您選取帳戶評分模式。

>[!NOTE]
>
>全域日期範圍篩選器不適用於預測性評分深入分析。 預測性評分Widget會根據下拉式清單中選取的帳戶評分模型分析資料。

![預測性評分分佈Widget。](../images/account-profiles/predictive-scoring-distribution.png)

### 預測性評分主要影響因素 {#predictive-scoring-top-influential-factors}

[!UICONTROL 預測性評分主要影響因素] Widget可協助您瞭解驅動每個傾向性貯體評分的最重要因素。

此Widget會顯示每個高、中及低傾向值區的主要影響因素。 每個影響因子的橫條會指出該傾向性貯體中包含特定影響因子的帳戶設定檔百分比。

Widget中的下拉式功能表可讓您選取帳戶評分模式。

>[!NOTE]
>
>全域日期範圍篩選器不適用於預測性評分深入分析。 預測性評分Widget會根據下拉式清單中選取的帳戶評分模型分析資料。

![預測性評分主要影響因素Widget。](../images/account-profiles/predictive-scoring-top-influential-factors.png)

## 無法載入資料錯誤 {#errors}

如果介面工具顯示&#x200B;*[!UICONTROL 無法載入。 請再試一次。]*&#x200B;這是因為沒有可用於B2B實體的資料。 例如，在[!UICONTROL 依人員角色的新商機]下方顯示的Widget，會顯示訊息「[!UICONTROL 無法載入」。 請再試一次。]」，因為此沙箱沒有可用的機會資料。

![無法載入分析錯誤。](../images/account-profiles/unable-to-load.png)

若要解決此問題，您必須將B2B實體資料（例如&#x200B;*機會人員*&#x200B;資料）擷取到沙箱。 48小時後，資料會反映在Widget中。

## 後續步驟

閱讀本檔案後，您現在應該知道如何找到[!UICONTROL 帳戶設定檔]儀表板，同時也瞭解可用介面工具中顯示的量度。 若要進一步瞭解如何在Experience Platform UI中使用帳戶設定檔作為B2B資料的一部分，請參閱Adobe Real-Time CDP、B2B edition的[帳戶設定檔總覽](../../rtcdp/accounts/account-profile-overview.md)。
