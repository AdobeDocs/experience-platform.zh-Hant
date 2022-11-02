---
keywords: 平台；目的地；目的地工作區；工作區；ui；目的地ui；目錄；目的地目錄；
title: 目的地工作區
description: 「目的地」工作區包含5個區段：概述、目錄、瀏覽、帳戶和系統檢視。 以下各節將說明這些規則。
exl-id: 0f46f08d-0fe3-441d-933a-86bc146c0f19
source-git-commit: 69e1f065cb3b302c4b144f39c84179075379f648
workflow-type: tm+mt
source-wordcount: '1223'
ht-degree: 2%

---

# 目的地工作區 {#destinations-workspace}

在Adobe Experience Platform中，選取 **[!UICONTROL 目的地]** 從左側導覽列存取 [!UICONTROL 目的地] 工作區。

此 [!UICONTROL 目的地] 工作區包含五個區段， [!UICONTROL 概述], [!UICONTROL 目錄], [!UICONTROL 瀏覽], [!UICONTROL 帳戶]，和 [!UICONTROL 系統視圖]，於以下章節中說明。

![目標概述控制面板顯示三個小工具。](../assets/ui/workspace/destinations-overview.png)

## [!UICONTROL 概觀] {#overview}

此 **[!UICONTROL 概述]** 標籤顯示 [!UICONTROL 目的地] 控制面板，提供與貴組織目的地資料相關的關鍵量度。 若要進一步了解，請造訪 [[!UICONTROL 目的地] 儀表板指南](../../dashboards/guides/destinations.md).

>[!NOTE]
>
>如果您的組織剛開始Experience Platform，且尚未有作用中的目的地，則 [!UICONTROL 目的地] 控制面板和 [!UICONTROL 概述] 標籤未顯示。 而是選取 [!UICONTROL 目的地] 從左側導覽顯示 [[!UICONTROL 目錄] 標籤](#catalog).

![「目的地」控制面板概述標籤。](../../dashboards/images/destinations/dashboard-overview.png)

## [!UICONTROL 目錄] {#catalog}

此 **[!UICONTROL 目錄]** 索引標籤會顯示 [!DNL Platform]，您可將資料傳送至。

此 [!DNL Platform] 使用者介面在目的地目錄頁面上提供數個搜尋和篩選選項：

* 使用頁面上的搜尋功能來尋找特定目的地。
* 使用 [!UICONTROL 類別] 控制。
* 切換 [!UICONTROL 所有目的地] 和 [!UICONTROL 我的目的地]. 選取 **[!UICONTROL 所有目的地]**，全部可用 [!DNL Platform] 目的地隨即顯示。 選取 **[!UICONTROL 我的目的地]**，您只能查看已建立連線的目的地。
* 選取以檢視 **[!UICONTROL 連線]** 和/或 **[!UICONTROL 擴充功能]** 類型。 若要了解這兩個類別之間的差異，請閱讀 [目的地類型和類別](../destination-types.md).

![目的地目錄會顯示一些廣告和雲端儲存空間目的地。](../assets/ui/workspace/catalog.png)

目標卡包含主控制項和次控制項選項。 主要控制項包括 [!UICONTROL 設定], [!UICONTROL 啟動], [!UICONTROL 啟用區段]，或 [!UICONTROL 匯出資料集]. 輔助控制項允許查看選項。 以下說明這些控制項：

| 控制 | 說明 |
|---------|----------|
| [!UICONTROL 設定] | 可讓您建立與目的地的連線。 |
| [!UICONTROL 啟動] | 建立與目的地的連線後，您就可以啟用區段或將資料集匯出至此目的地。 |
| [!UICONTROL 啟用區段] | 建立與目的地的連線後，您就可以啟動此目的地的區段。 |
| [!UICONTROL 匯出資料集] | 建立與目的地的連線後，您就可以將資料集匯出至此目的地。 |
| [!UICONTROL 查看帳戶] | 查看您為目標而連接的帳戶。 |
| [!UICONTROL 查看資料流] | 檢視目的地的資料啟動流程。 |
| [!UICONTROL 檢視檔案] | 開啟該特定目的地的檔案頁面連結，以取得詳細資訊並協助您進行設定。 |

{style=&quot;table-layout:auto&quot;}

![控制目的地卡](../assets/ui/workspace/destination-card-options.png)

在目錄中選取目的地卡片，以開啟右側邊欄。 您可以在此處查看目的地的說明。 右側邊欄提供上表所述的相同控制項，包括目的地說明以及目的地類別和類型的指示。

![目標目錄選項](../assets/ui/workspace/destination-right-rail.png)

如需目的地類別的詳細資訊和每個目的地的相關資訊，請參閱 [目標目錄](../catalog/overview.md) 和 [目的地類型和類別](../destination-types.md).

## [!UICONTROL 帳戶] {#accounts}

此 **[!UICONTROL 帳戶]** 索引標籤會顯示您已與各種目的地建立之連線的詳細資訊，並可讓您更新或刪除現有的帳戶詳細資訊。 請參閱下表，以取得每個目的地帳戶的所有資訊。

>[!TIP]
>
> * 選取省略號(`...`) [!UICONTROL 平台] 欄和使用 ![啟動控制](../assets/ui/workspace/add-data-symbol.png)**[!UICONTROL 啟動&#x200B;]**/**[!UICONTROL &#x200B;啟用區段&#x200B;]**/**[!UICONTROL &#x200B;匯出資料集&#x200B;]**控制項可將區段或資料集匯出至該目的地。
> * 選取省略號(`...`) [!UICONTROL 平台] 欄和使用 ![編輯詳細資訊控制項](../assets/ui/workspace/pencil-icon.png)**[!UICONTROL 編輯詳細資訊&#x200B;]**控制 [更新](update-accounts.md) 現有目標帳戶的詳細資訊。
> * 選取省略號(`...`) [!UICONTROL 平台] 欄和使用 ![刪除控制項](../assets/ui/workspace/delete-destination-symbol.png)**[!UICONTROL 刪除&#x200B;]**控制 [刪除](delete-destination-account.md) 現有目的地帳戶。


![帳戶索引標籤](../assets/ui/workspace/destination-account-options.png)

| 元素 | 說明 |
|---|---|
| [!UICONTROL 平台] | 您已設定連線的目的地。 |
| [!UICONTROL 連線類型] | 代表與儲存貯體或目的地的帳戶連線類型。 驗證選項依目的地而定： <ul><li>對於電子郵件行銷目的地：可以是S3、FTP或Azure Blob。</li><li>針對即時廣告目的地：伺服器對伺服器</li><li>針對Amazon S3雲端儲存空間目的地：訪問密鑰 </li><li>針對SFTP雲端儲存目標：SFTP的基本驗證</li><li>OAuth 1或OAuth 2驗證</li><li>承載令牌驗證</li></ul> |
| [!UICONTROL 使用者名稱] | 您在 [連接目標嚮導](../catalog/email-marketing/overview.md#connect-destination). |
| [!UICONTROL 目的地] | 表示與為目標建立的基本資訊連接的唯一成功目標資料流的數量。 |
| [!UICONTROL 已驗證] | 授權與此目的地的連線的日期。 |

{style=&quot;table-layout:auto&quot;}

## [!UICONTROL 瀏覽] {#browse}

此 **[!UICONTROL 瀏覽]** 索引標籤會顯示您已建立連線的目的地。 具有 **[!UICONTROL 啟用/停用]** 切換為開啟，分別將目標設定為使用中或非使用中。 您也可以透過選取 **[!UICONTROL 區段]** > **[!UICONTROL 瀏覽]** 並選取要檢查的區段。 請參閱下表，以了解 [!UICONTROL 瀏覽] 標籤：

>[!TIP]
>
> * 選取省略號(`...`) [!UICONTROL 名稱] 欄和使用 ![啟動區段控制](../assets/ui/workspace/add-data-symbol.png)**[!UICONTROL 啟動&#x200B;]**控制項可將區段或資料集匯出至該目的地。
> * 選取省略號(`...`) [!UICONTROL 名稱] 欄和使用 ![刪除控制項](../assets/ui/workspace/delete-destination-symbol.png)**[!UICONTROL 刪除&#x200B;]**控制 [移除](delete-destinations.md) 與目的地的現有連線。
> * 選取省略號(`...`) [!UICONTROL 名稱] 欄和使用 ![在監視控制中查看](../assets/ui/workspace/monitoring-icon.png)**[!UICONTROL 在監視中查看&#x200B;]**控制項，可在 [監視儀表板](/help/dataflows/ui/monitor-destinations.md#monitoring-destinations-dashboard).
> * 選取省略號(`...`) [!UICONTROL 名稱] 欄和使用 ![訂閱警報 ](../assets/ui/workspace/alerts-icon.png)**[!UICONTROL 訂閱警報&#x200B;]**對目標資料流警報的訂閱控制。 您可以訂閱警報，以接收有關流程執行狀態、成功或失敗的訊息。 請參閱 [訂閱內容內目的地警報](alerts.md) 有關目標資料流警報的詳細資訊……


![瀏覽頁簽](../assets/ui/workspace/browse-tab.png)

| 元素 | 說明 |
|---------|----------|
| 名稱 | 您為啟動流程提供的名稱，可用於此目的地。 同一欄包含兩個控制項： [!UICONTROL 啟動 ] 和 [!UICONTROL 刪除目標]. |
| [!UICONTROL 上次流運行狀態] | 上次資料流運行的狀態。 請參閱 [查看目標詳細資訊](destination-details-page.md) 有關資料流運行的詳細資訊。 |
| [!UICONTROL 上次流運行日期] | 上次資料流運行發生的時間和日期。 請參閱 [查看目標詳細資訊](destination-details-page.md) 有關資料流運行的詳細資訊。 |
| [!UICONTROL 目標] | 您為啟動流程選取的目的地平台。 |
| [!UICONTROL 連線類型] | 代表與儲存貯體或目的地的連線類型。 <ul><li>對於電子郵件行銷目的地：可以是S3、FTP或 [!DNL Azure Blob].</li><li>針對即時廣告目的地：伺服器對伺服器。</li><li>針對串流目的地：可以是 [!DNL Azure Event Hubs] 或 [!DNL Amazon Kinesis].</li></ul> |
| [!UICONTROL 使用者名稱] | 您為目的地流程選擇的帳戶憑據。 |
| [!UICONTROL 啟動資料] | 指出要啟動至此目的地的區段數。 選取此控制項，即可進一步了解已啟用的區段。 請參閱 [啟動資料](/help/destinations/ui/destination-details-page.md#activation-data) ，以取得已啟用區段的詳細資訊。 |
| [!UICONTROL 已建立] | 建立至目的地的啟動流程的日期和UTC時間。 選取向上/向下箭頭符號，依最新、最先或最舊先排序啟動流程。 |
| [!UICONTROL 狀態] | `Enabled` 或 `Disabled`. 指示是否正在將資料激活到此目標。 |

按一下目的地列，在右側邊欄中顯示有關目的地的詳細資訊。

![按一下目標列](../assets/ui/workspace/click-destination-row.png)

選取目標名稱，以查看已啟動至此目標之區段的相關資訊。 按一下 **[!UICONTROL 編輯啟用]** 修改或新增至要傳送至此目的地的區段。

## [!UICONTROL 系統視圖] {#system-view}

此 **[!UICONTROL 系統視圖]** 標籤會顯示您已在Adobe Experience Platform中設定的啟用流程的圖形表示。

![資料流1](../assets/ui/workspace/data-flows1.png)

選取頁面上顯示的任何目的地，然後按一下 **[!UICONTROL 查看資料流]** 查看已為每個目標設定的所有連接的資訊。

![資料流2](../assets/ui/workspace/data-flows2.png)
