---
keywords: 平台；目標；目標工作區；工作區；ui；目標ui；目錄；目標目錄；
title: 目標工作區概觀
description: 「目標」工作區包含4個部分：目錄、瀏覽、帳戶和系統視圖，這些部分在以下各節中介紹。
seo-description: 在Adobe Experience Platform，從左側導覽列選擇「目標」以存取目標工作區。
translation-type: tm+mt
source-git-commit: 95ff15b212e0d6f454f0319ac1ec5bbee9c07dac
workflow-type: tm+mt
source-wordcount: '1017'
ht-degree: 2%

---


# 目標工作區概述{#destinations-workspace}

在Adobe Experience Platform，從左側導航欄選擇&#x200B;**[!UICONTROL 目標]**&#x200B;以訪問[!UICONTROL 目標]工作區。

[!UICONTROL 目標]工作區由以下各節介紹的四個部分組成：[!UICONTROL 目錄]、[!UICONTROL 瀏覽]、[!UICONTROL 帳戶]和[!UICONTROL 系統視圖]。

![目標——概觀](../assets/ui/workspace/destinations-overview.png)

## [!UICONTROL 目錄] {#catalog}

**[!UICONTROL Catalog]**&#x200B;標籤顯示平台中所有可傳送資料的目標的清單。

「平台」使用者介面在目標目錄頁面上提供許多搜尋和篩選選項：

* 使用頁面上的搜尋功能來尋找特定目標。
* 使用[!UICONTROL Categories]控制項篩選目標。
* 在[!UICONTROL 所有目標]和[!UICONTROL 我的目標]之間切換。 選擇&#x200B;**[!UICONTROL 所有目標]**&#x200B;時，將顯示所有可用的平台目標。 選擇&#x200B;**[!UICONTROL 我的目標]**&#x200B;時，您只能看到已建立連接的目標。
* 選擇查看&#x200B;**[!UICONTROL 連接]**&#x200B;和／或&#x200B;**[!UICONTROL 擴展]**。 要瞭解兩個類別之間的差異，請參閱[目標類型和類別](../destination-types.md)。

![目標篩選和搜尋示範](../assets/ui/workspace/destinations-search-and-filter.gif)

目標卡包含&#x200B;**[!UICONTROL Configure]**&#x200B;或&#x200B;**[!UICONTROL Activate]**&#x200B;控制項，以及帶有更多選項的輔助控制項。 以下說明這些內容：

| 控制 | 說明 |
---------|----------
| [!UICONTROL 設定] | 允許您建立到目標的連接。 |
| [!UICONTROL 啟動] | 一旦建立與目標的連線後，您就可以啟動區段。 |
| [!UICONTROL 檢視帳戶] | 查看您已為目標連接的帳戶。 |
| [!UICONTROL 查看資料流] | 檢視目的地的資料啟動流程。 |
| [!UICONTROL 檢視檔案] | 開啟該特定目的地的檔案頁面連結，以取得詳細資訊並協助您設定。 |

![目標卡的控制項](../assets/ui/workspace/destination-card-options.png)

在目錄中選取目標卡片，以開啟右側導軌。  在這裡，您可以看到目的地的說明。 右側導軌提供與上表所述相同的控制項，以及目的地的描述，以及目的地類別和類型的指示。

![目標目錄選項](../assets/ui/workspace/destination-right-rail.png)

有關目標類別和每個目標資訊的詳細資訊，請參閱[目標目錄](../catalog/overview.md)和[目標類型和類別](../destination-types.md)。

## [!UICONTROL 帳戶] {#accounts}

在&#x200B;**[!UICONTROL Accounts]**&#x200B;標籤中，您可以進一步瞭解您與各種目標建立的連線。 請參閱下表，以取得有關每個目標的所有資訊：

>[!TIP]
>
>使用&#x200B;**[!UICONTROL Platform]**&#x200B;欄中的![Add data button](../assets/ui/workspace/add-data-symbol.png)按鈕，為該帳戶建立新的目標連線。

![「帳戶」頁籤](../assets/ui/workspace/edit-account-destinations.png)

| 元素 | 說明 |
---------|----------
| [!UICONTROL 平台] | 您已設定連接的目標。 |
| [!UICONTROL 連線類型] | 表示與儲存桶或目標的連接類型。 <ul><li>對於電子郵件行銷目標：可以是S3或FTP。</li><li>針對即時廣告目的地：伺服器對伺服器</li><li>針對AmazonS3雲端儲存空間目標：存取金鑰 </li><li>對於SFTP雲端儲存空間目標：SFTP的基本驗證</li></ul> |
| [!UICONTROL 使用者名稱] | 在[連接目標嚮導](../catalog/email-marketing/overview.md#connect-destination)中選擇的用戶名。 |
| [!UICONTROL 目的地] | 表示與為目標建立的基本資訊連接的唯一成功目標流的數量。 |
| [!UICONTROL 已驗證] | 授權此目的地的連線的日期。 |

此外，您也可以編輯或更新帳戶資訊。 在&#x200B;**[!UICONTROL Platform]**&#x200B;欄中選擇![編輯帳戶按鈕](../assets/ui/workspace/pencil-icon.png)以編輯帳戶的資訊。

對於使用`OAuth2`連線類型的帳戶，您可以選取&#x200B;**[!UICONTROL 重新連線OAuth]**&#x200B;以續約您的帳戶憑證。

![Oauth影像](../assets/ui/workspace/reconnect-oauth.png)

對於使用`Access Key`或`ConnectionString`連線類型的帳戶，您可以編輯帳戶驗證資訊，包括存取ID、機密金鑰或連線字串等資訊。

![帳戶資訊影像](../assets/ui/workspace/edit-account-details.png)

編輯完帳戶詳細資訊後，選擇&#x200B;**[!UICONTROL 保存]**&#x200B;以完成更新。

## [!UICONTROL 瀏覽] {#browse}

**[!UICONTROL Browse]**&#x200B;標籤顯示您已建立連線的目標。 啟用&#x200B;****&#x200B;的目標開啟，將目標設為活動，反之亦然。 您也可以選擇&#x200B;**[!UICONTROL 區段]** > **[!UICONTROL 瀏覽]**&#x200B;並選取要檢查的區段，以檢視資料流動的目標。 有關「瀏覽」頁籤中為每個目標提供的所有資訊，請參見下表：

>[!TIP]
>
> * 使用&#x200B;**[!UICONTROL Name]**&#x200B;欄中的![新增區段按鈕](../assets/ui/workspace/add-data-symbol.png)按鈕，將其他區段啟用至該目標。
> * 使用&#x200B;**[!UICONTROL Name]**&#x200B;欄中的![刪除目標按鈕](../assets/ui/workspace/delete-destination-symbol.png)按鈕刪除目標的現有連接。


![瀏覽標籤](../assets/ui/workspace/browse-tab.png)

| 元素 | 說明 |
---------|----------
| 名稱 | 您為啟動流程提供的名稱，會前往此目的地。 同一欄包含兩個控制項：[!UICONTROL 啟動]和[!UICONTROL 刪除目標]。 |
| 上次流運行狀態 | 上次資料流運行的狀態。 有關資料流運行的詳細資訊，請參見[查看目標詳細資訊](destination-details-page.md)。 |
| 上次流程運行日期 | 上次資料流運行發生的時間和日期。 有關資料流運行的詳細資訊，請參見[查看目標詳細資訊](destination-details-page.md)。 |
| [!UICONTROL 目標] | 您為啟動流程選擇的目標平台。 |
| [!UICONTROL 連線類型] | 表示與儲存桶或目標的連接類型。 <ul><li>對於電子郵件行銷目標：可以是S3、FTP或[!DNL Azure Blob]。</li><li>針對即時廣告目的地：伺服器對伺服器。</li><li>對於串流目的地：可以是[!DNL Azure Event Hubs]或[!DNL Amazon Kinesis]。</li></ul> |
| [!UICONTROL 使用者名稱] | 您為目標流選擇的帳戶憑據。 |
| [!UICONTROL 啟動資料] | 指出要啟動至此目標的區段數。 選取此控制項，以進一步瞭解已啟動的區段。 如需已啟動區段的詳細資訊，請參閱目標詳細資訊頁面中的[啟動資料](/help/destinations/ui/destination-details-page.md#activation-data)。 |
| [!UICONTROL 已建立] | 建立啟動流程至目的地的日期和UTC時間。 |
| [!UICONTROL 狀態] | `Active` 或 `Inactive`. 指出資料目前是否正在啟動至此目標。 若要編輯狀態，請參閱[停用啟動](./activate-destinations.md#disable-activation)。 |

按一下目標列，以顯示右側導軌中有關目標的詳細資訊。

![按一下目標行](../assets/ui/workspace/click-destination-row.png)

選取目標名稱，以查看啟動至此目標之區段的相關資訊。 按一下「編輯啟動&#x200B;**[!UICONTROL 」，修改或新增至傳送至此目的地的區段。]**

## [!UICONTROL 系統視圖] {#system-view}

**[!UICONTROL 系統視圖]**&#x200B;頁籤顯示您在Adobe Experience Platform設定的激活流的圖形表示。

![資料流1](../assets/ui/workspace/data-flows1.png)

選擇頁面上顯示的任何目標，然後按&#x200B;**[!UICONTROL 查看流]**&#x200B;以查看您為每個目標設定的所有連接的資訊。

![資料流2](../assets/ui/workspace/data-flows2.png)