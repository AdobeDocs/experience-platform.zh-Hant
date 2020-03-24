---
title: 目標工作區
seo-title: 目標工作區
description: 在Adobe即時客戶資料平台中，從左側導覽列選取「目標」以存取目標工作區。
seo-description: 在Adobe即時客戶資料平台中，從左側導覽列選取「目標」以存取目標工作區。
translation-type: tm+mt
source-git-commit: e87ddff936da88b1b2b3cf71c2d6c24ed28b39ab

---


# 目標工作區 {#destinations-workspace}

在Adobe即時客戶資料平台中，從左側導覽列選 **取** 「目標」以存取「目標」工作區。

「目標」工作區由四個部 **分組成**：目錄、瀏 **覽、帳**&#x200B;戶和系 ********&#x200B;統視圖，這些部分在下面的部分中介紹。

![目標——概觀](/help/rtcdp/destinations/assets/destinations-overview.png)

## 目錄 {#catalog}

此標 **[!UICONTROL Catalog]** 簽會顯示Adobe提供的所有目的地清單，您可將資料傳送至這些目的地。

使用頁面上的搜尋功能，以尋找特定目標或使用控制項來篩選 **[!UICONTROL Categories]** 目標。

在目錄中選擇目標以開啟右邊欄。 在這裡，您可以設定到目的地的連線(**Connect目的地**)、檢視現有的目的地連線(**Browse目的地**)，或檢視檔案(**View documentation**)，以進一步瞭解每個目的地的詳細資訊。

![目標目錄選項](/help/rtcdp/destinations/assets/destination-ui-catalog-options.png)

有關目標類別和每個目標資訊的詳細資訊，請參 [閱目標目錄](/help/rtcdp/destinations/destinations-catalog.md)。

## 瀏覽 {#browse}

該選 **[!UICONTROL Browse]** 項卡顯示您已建立連接的目標。 啟用切換 **功能的** 「目標」會將目標設為「活動」，反之亦然。 您也可以選取「區段>瀏覽」，並選取要檢查的區段， **以檢視您有資料流動的目的地** 。 有關「瀏覽」頁籤中為每個目標提供的所有資訊，請參見下表：

![瀏覽標籤](/help/rtcdp/destinations/assets/browse-tab.png)

| 元素 | 說明 |
---------|----------
| 名稱 | 您為啟動流程提供的名稱，會前往此目的地。 |
| 目的地 | 您為啟動流程選擇的目標平台。 |
| 連線類型 | 表示與儲存桶或目標的連接類型。 <ul><li>對於電子郵件行銷目標：可以是S3或FTP。</li><li>針對即時廣告目的地：伺服器對伺服器</li></ul> |
| 使用者名稱 | 您為目標流選擇的帳戶憑據。 |
| 區段 | 要啟動至此目標的區段數。 |
| 已建立 | 建立啟動流程至目的地的日期和UTC時間。 |
| 狀態 | `Active` 或 `Inactive`. 指出資料目前是否正在啟動至此目標。 若要編輯狀態，請參閱停 [用啟動](/help/rtcdp/destinations/activate-destinations.md#disable-activation)。 |

按一下目標列，以顯示右側導軌中有關目標的詳細資訊。

![按一下目標行](/help/rtcdp/destinations/assets/click-destination-row.png)

選取目標名稱，以查看啟動至此目標之區段的相關資訊。 按一 **[!UICONTROL Edit activation]** 下可修改或新增至傳送至此目的地的區段。

## 帳戶 {#accounts}

在該選 **[!UICONTROL Accounts]** 項卡中，您可以進一步瞭解您與各種目標建立的連接。 請參閱下表，以取得有關每個目標的所有資訊：

![「帳戶」頁籤](/help/rtcdp/destinations/assets/accounts-tab.png)

| 元素 | 說明 |
---------|----------
| 平台 | 您已設定連接的目標。 |
| 連線類型 | 表示與儲存桶或目標的連接類型。 <ul><li>對於電子郵件行銷目標：可以是S3或FTP。</li><li>針對即時廣告目的地：伺服器對伺服器</li><li>對於Amazon S3雲端儲存空間目標：存取金鑰 </li><li>對於SFTP雲端儲存空間目標：SFTP的基本驗證</li></ul> |
| 使用者名稱 | 在連接目標嚮導中選 [擇的用戶名](/help/rtcdp/destinations/email-marketing-destinations.md#connect-destination)。 |
| 資料流 | 表示與為目標建立的基本資訊連接的唯一成功目標流的數量。 |
| 已驗證 | 授權此目的地的連線的日期。 |
| 狀態 | `Active` 或 `Inactive`. 指出資料目前是否正在啟動至此目標。 若要編輯狀態，請參閱停 [用啟動](/help/rtcdp/destinations/activate-destinations.md#disable-activation)。 |

## 系統視圖 {#system-view}

此標 **[!UICONTROL System View]** 簽會顯示您在即時客戶資料平台中設定之啟動流程的圖形表示。

![Data-flows1](/help/rtcdp/destinations/assets/data-flows1.png)

選擇頁面上顯示的任意目標，然 **[!UICONTROL View flows]** 後按鍵查看您為每個目標設定的所有連接資訊。

![Data-flows2](/help/rtcdp/destinations/assets/data-flows2.png)