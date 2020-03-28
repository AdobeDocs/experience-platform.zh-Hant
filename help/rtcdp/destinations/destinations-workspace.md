---
title: 目標工作區
seo-title: 目標工作區
description: 在Adobe即時客戶資料平台中，從左側導覽列選取「目標」以存取目標工作區。
seo-description: 在Adobe即時客戶資料平台中，從左側導覽列選取「目標」以存取目標工作區。
translation-type: tm+mt
source-git-commit: 336aa90cf1e059a92a36dd0ef3222ef6a6f5123b

---


# 目標工作區 {#destinations-workspace}

在Adobe即時客戶資料平台中，從左側導 **[!UICONTROL Destinations]** 覽列選擇以存取工作 [!UICONTROL Destinations] 區。

工 [!UICONTROL Destinations] 作區由四個區 **[!UICONTROL Catalog]**&#x200B;域、 **[!UICONTROL Browse]**、 **[!UICONTROL Accounts]**&#x200B;和 **[!UICONTROL System View]**，在以下各節中說明。

![目標——概觀](/help/rtcdp/destinations/assets/destinations-overview.png)

## [!UICONTROL Catalog] {#catalog}

此標 **[!UICONTROL Catalog]** 簽會顯示Adobe提供的所有目的地清單，您可將資料傳送至這些目的地。

使用頁面上的搜尋功能，以尋找特定目標或使用控制項來篩選 **[!UICONTROL Categories]** 目標。

在目錄中選擇目標以開啟右邊欄。 在這裡，您可以設定目標(**[!UICONTROL Connect destination]**)的連線、檢視現有的目標連線(**[!UICONTROL Browse destinations]**)，或檢視檔案(**[!UICONTROL View documentation]**)，以進一步瞭解每個目標的詳細資訊。

![目標目錄選項](/help/rtcdp/destinations/assets/destination-ui-catalog-options.png)

有關目標類別和每個目標資訊的詳細資訊，請參 [閱目標目錄](/help/rtcdp/destinations/destinations-catalog.md)。

## [!UICONTROL Browse] {#browse}

該選 **[!UICONTROL Browse]** 項卡顯示您已建立連接的目標。 開啟切換 **[!UICONTROL enabled]** 的目標會將目標設定為作用中，反之亦然。 您也可以選取並選取要檢查的區段，以檢 **[!UICONTROL Segments > Browse]** 視資料流動的目標。 有關「瀏覽」頁籤中為每個目標提供的所有資訊，請參見下表：

![瀏覽標籤](/help/rtcdp/destinations/assets/browse-tab.png)

| 元素 | 說明 |
---------|----------
| 名稱 | 您為啟動流程提供的名稱，會前往此目的地。 |
| [!UICONTROL Destination] | 您為啟動流程選擇的目標平台。 |
| [!UICONTROL Connection Type] | 表示與儲存桶或目標的連接類型。 <ul><li>對於電子郵件行銷目標：可以是S3或FTP。</li><li>針對即時廣告目的地：伺服器對伺服器</li></ul> |
| [!UICONTROL Username] | 您為目標流選擇的帳戶憑據。 |
| [!UICONTROL Segments] | 要啟動至此目標的區段數。 |
| [!UICONTROL Created] | 建立啟動流程至目的地的日期和UTC時間。 |
| [!UICONTROL Status] | `Active` 或 `Inactive`. 指出資料目前是否正在啟動至此目標。 若要編輯狀態，請參閱停 [用啟動](/help/rtcdp/destinations/activate-destinations.md#disable-activation)。 |

按一下目標列，以顯示右側導軌中有關目標的詳細資訊。

![按一下目標行](/help/rtcdp/destinations/assets/click-destination-row.png)

選取目標名稱，以查看啟動至此目標之區段的相關資訊。 按一 **[!UICONTROL Edit activation]** 下可修改或新增至傳送至此目的地的區段。

## [!UICONTROL Accounts] {#accounts}

在該選 **[!UICONTROL Accounts]** 項卡中，您可以進一步瞭解您與各種目標建立的連接。 請參閱下表，以取得有關每個目標的所有資訊：

![「帳戶」頁籤](/help/rtcdp/destinations/assets/accounts-tab.png)

| 元素 | 說明 |
---------|----------
| [!UICONTROL Platform] | 您已設定連接的目標。 |
| [!UICONTROL Connection Type] | 表示與儲存桶或目標的連接類型。 <ul><li>對於電子郵件行銷目標：可以是S3或FTP。</li><li>針對即時廣告目的地：伺服器對伺服器</li><li>對於Amazon S3雲端儲存空間目標：存取金鑰 </li><li>對於SFTP雲端儲存空間目標：SFTP的基本驗證</li></ul> |
| [!UICONTROL Username] | 在連接目標嚮導中選 [擇的用戶名](/help/rtcdp/destinations/email-marketing-destinations.md#connect-destination)。 |
| [!UICONTROL Data Flows] | 表示與為目標建立的基本資訊連接的唯一成功目標流的數量。 |
| [!UICONTROL Authorized] | 授權此目的地的連線的日期。 |
| [!UICONTROL Status] | `Active` 或 `Inactive`. 指出資料目前是否正在啟動至此目標。 若要編輯狀態，請參閱停 [用啟動](/help/rtcdp/destinations/activate-destinations.md#disable-activation)。 |

## [!UICONTROL System View] {#system-view}

此標 **[!UICONTROL System View]** 簽會顯示您在即時客戶資料平台中設定之啟動流程的圖形表示。

![Data-flows1](/help/rtcdp/destinations/assets/data-flows1.png)

選擇頁面上顯示的任意目標，然 **[!UICONTROL View flows]** 後按鍵查看您為每個目標設定的所有連接資訊。

![Data-flows2](/help/rtcdp/destinations/assets/data-flows2.png)