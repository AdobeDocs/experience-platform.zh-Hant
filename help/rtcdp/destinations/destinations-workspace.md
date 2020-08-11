---
title: 目標工作區
seo-title: 目標工作區
description: 在Adobe即時客戶資料平台中，從左側導覽列選取「目標」以存取目標工作區。
seo-description: 在Adobe即時客戶資料平台中，從左側導覽列選取「目標」以存取目標工作區。
translation-type: tm+mt
source-git-commit: f3e489416a9bc80cfb0502d3973a86748123a687
workflow-type: tm+mt
source-wordcount: '807'
ht-degree: 2%

---


# 目標工作區 {#destinations-workspace}

在Adobe即時客戶資料平台中，從左側導覽列選 **[!UICONTROL 取]** 「目標」以存取「 [!UICONTROL 目標] 」工作區。

工 [!UICONTROL 作區] 由四個目標部分組成：目錄 **[!UICONTROL 、瀏]**&#x200B;覽 **[!UICONTROL 、]** BrowseAccounts、 ******** ContralSystem View，這些部分在下面幾節中介紹。

![目標——概觀](/help/rtcdp/destinations/assets/destinations-overview.png)

## [!UICONTROL 目錄] {#catalog}

「目 **[!UICONTROL 錄]** 」標籤會顯示Adobe即時CDP中所有可傳送資料的目標清單。

Adobe即時CDP使用者介面在目標目錄頁面上提供許多搜尋和篩選選項：

* 使用頁面上的搜尋功能來尋找特定目標。
* 使用「類別」控制項 **[!UICONTROL 篩選目]** 標。
* 在「所有目 **[!UICONTROL 標」和「我]** 」目 **[!UICONTROL 標之間切換]**。 選取 **[!UICONTROL 所有目標]** ，會顯示所有可用的Adobe即時CDP目標。 選 **[!UICONTROL 取「我的目標]** 」時，您只能看到您已建立連線的目標。
* 選擇以查看 **[!UICONTROL 連接]** 和／或擴 **[!UICONTROL 展]**。 要瞭解兩個類別之間的差異，請參閱目 [標類型和類別](/help/rtcdp/destinations/destination-types.md)。

![目標篩選和搜尋示範](/help/rtcdp/destinations/assets/destinations-search-and-filter.gif)

目標卡包含「設 **[!UICONTROL 定]** 」或「啟 **** 動」控制項，以及可顯示更多選項的次要控制項。 以下說明這些內容：

| 控制 | 說明 |
---------|----------
| [!UICONTROL 設定] | 允許您建立到目標的連接。 |
| [!UICONTROL 啟動] | 一旦建立與目標的連線後，您就可以啟動區段。 |
| [!UICONTROL 檢視帳戶] | 查看您已為目標連接的帳戶。 |
| [!UICONTROL 查看資料流] | 檢視目的地的資料啟動流程 |
| [!UICONTROL 檢視檔案] | 開啟該特定目的地的檔案頁面連結，以取得詳細資訊並協助您設定。 |

![目標卡的控制項](/help/rtcdp/destinations/assets/destination-card-options.png)

在目錄中選取目標卡片，以開啟右側導軌。  在這裡，您可以看到目的地的說明。 右側導軌提供與上表所述相同的控制項，以及目的地的描述，以及目的地類別和類型的指示。

![目標目錄選項](/help/rtcdp/destinations/assets/destination-right-rail.png)

有關目標類別和每個目標資訊的詳細資訊，請參 [閱目標目錄](/help/rtcdp/destinations/destinations-catalog.md)[和目標類型和類別](/help/rtcdp/destinations/destination-types.md)。

## [!UICONTROL 瀏覽] {#browse}

「瀏 **[!UICONTROL 覽]** 」頁籤顯示已建立連接的目標。 啟用切換 **[!UICONTROL 功能的]** 「目標」會將目標設為「活動」，反之亦然。 您也可以選取「區段」>「瀏覽」，並選取要檢 **[!UICONTROL 查的區段，以檢]****** 視資料流動的目的地。 有關「瀏覽」頁籤中為每個目標提供的所有資訊，請參見下表：

![瀏覽標籤](/help/rtcdp/destinations/assets/browse-tab.png)

| 元素 | 說明 |
---------|----------
| 名稱 | 您為啟動流程提供的名稱，會前往此目的地。 |
| [!UICONTROL 目標] | 您為啟動流程選擇的目標平台。 |
| [!UICONTROL 連線類型] | 表示與儲存桶或目標的連接類型。 <ul><li>對於電子郵件行銷目標：可以是S3或FTP。</li><li>針對即時廣告目的地：伺服器對伺服器</li></ul> |
| [!UICONTROL 使用者名稱] | 您為目標流選擇的帳戶憑據。 |
| [!UICONTROL 區段] | 要啟動至此目標的區段數。 |
| [!UICONTROL 已建立] | 建立啟動流程至目的地的日期和UTC時間。 |
| [!UICONTROL 狀態] | `Active` 或 `Inactive`. 指出資料目前是否正在啟動至此目標。 若要編輯狀態，請參閱停 [用啟動](/help/rtcdp/destinations/activate-destinations.md#disable-activation)。 |

按一下目標列，以顯示右側導軌中有關目標的詳細資訊。

![按一下目標行](/help/rtcdp/destinations/assets/click-destination-row.png)

選取目標名稱，以查看啟動至此目標之區段的相關資訊。 按一 **[!UICONTROL 下「編輯啟動]** 」，修改或新增至傳送至此目的地的區段。

## [!UICONTROL 帳戶] {#accounts}

在「帳 **[!UICONTROL 戶]** 」標籤中，您可以進一步瞭解您與各種目的地建立的連線。 請參閱下表，以取得有關每個目標的所有資訊：

![「帳戶」頁籤](/help/rtcdp/destinations/assets/accounts-tab.png)

| 元素 | 說明 |
---------|----------
| [!UICONTROL 平台] | 您已設定連接的目標。 |
| [!UICONTROL 連線類型] | 表示與儲存桶或目標的連接類型。 <ul><li>對於電子郵件行銷目標：可以是S3或FTP。</li><li>針對即時廣告目的地：伺服器對伺服器</li><li>對於Amazon S3雲端儲存空間目標：存取金鑰 </li><li>對於SFTP雲端儲存空間目標：SFTP的基本驗證</li></ul> |
| [!UICONTROL 使用者名稱] | 在連接目標嚮導中選 [擇的用戶名](/help/rtcdp/destinations/email-marketing-destinations.md#connect-destination)。 |
| [!UICONTROL 資料流] | 表示與為目標建立的基本資訊連接的唯一成功目標流的數量。 |
| [!UICONTROL 已驗證] | 授權此目的地的連線的日期。 |
| [!UICONTROL 狀態] | `Active` 或 `Inactive`. 指出資料目前是否正在啟動至此目標。 若要編輯狀態，請參閱停 [用啟動](/help/rtcdp/destinations/activate-destinations.md#disable-activation)。 |

## [!UICONTROL 系統視圖] {#system-view}

「系 **[!UICONTROL 統檢視]** 」標籤會顯示您在即時客戶資料平台中設定之啟動流程的圖形表示。

![Data-flows1](/help/rtcdp/destinations/assets/data-flows1.png)

選擇頁面上顯示的任何目標，然後按「 **[!UICONTROL View flows]** 」（查看流）查看您為每個目標設定的所有連接的資訊。

![Data-flows2](/help/rtcdp/destinations/assets/data-flows2.png)