---
title: 透過延展的啟用來啟用Audience Manager對象
description: 瞭解如何透過Audience Manager展開啟用，將Audience Manager對象啟用至社交和廣告目的地。
source-git-commit: 19fb369a7faa0c5ac27a34db7b848b0332cb8695
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%

---


# 透過Audience Manager展開啟用來啟用對象

此頁面說明您必須遵循的端對端工作流程，才能將對象從Audience Manager啟動至擴展啟動支援的目的地平台。

## 開始之前 {#before-you-begin}

本指南中所述的步驟假設您已閱讀 [展開的啟用概觀頁面](overview.md) 而且您已確認您符合對象啟用的先決條件。

>[!IMPORTANT]
>
>若要透過啟用對象 [!DNL Expanded Activation]，確定您的Audience Manager對象是根據 **雜湊電子郵件地址**. 請參閱 [必備條件](overview.md#prerequisites) 以取得更多詳細資料。

## 步驟1：設定Audience Manager來源連線 {#configure-source}

此 [Audience Manager來源聯結器](../sources/connectors/adobe-applications/audience-manager.md) 傳送在Adobe Audience Manager中收集以在「擴充啟用」支援的目的地平台中啟用的對象資料。

遵循指南操作 [建立Audience Manager來源連線](../sources/tutorials/ui/create/adobe-applications/audience-manager.md) 以設定來源聯結器。

![顯示具有Audience Manager來源連線之「來源」索引標籤的Platform UI影像。](assets/sources-tab.png)

>[!TIP]
>
>Adobe Audience Manager來源聯結器是「展開啟用」中唯一可用的來源聯結器。
>
>如果您想要根據其他識別碼擷取對象，則必須購買某個版本的 [Real-Time CDP](../rtcdp/overview.md). 如需詳細資訊，請聯絡您的Adobe代表。

### 檢視和監視擷取的對象 {#view-audiences}

您從Audience Manager帶入展開式啟用的對象，可讓您在 **[!UICONTROL 受眾]** 儀表板。

若要檢視您的對象，請前往 **[!UICONTROL 客戶]** -> **[!UICONTROL 受眾]** -> **[!UICONTROL 瀏覽]**.

![顯示「對象」頁面的平台UI影像。](assets/audiences-browse.png)

>[!IMPORTANT]
>
>* 要完全填入展開啟用中的對象，最多可能需要48小時的時間。 此也適用於現有Audience Manager對象的更新。
>* 新建立的Audience Manager對象不會自動出現在展開啟用中。 若要在展開啟用中擷取新區段，您必須透過Audience Manager來源聯結器新增區段。

設定Audience Manager來源聯結器後，請移至 [步驟2](#create-destination-connection).

## 步驟2：建立新的目的地連線 {#create-destination-connection}

您必須先建立與目的地平台的連線，才能將Audience Manager對象傳送至您選擇的目的地平台。

在左側邊欄中，前往 **[!UICONTROL 連線]** -> **[!UICONTROL 目的地]** -> **[!UICONTROL 目錄]**.

可用的目的地類別 [!DNL Expanded Activation] 為 [廣告](../destinations/catalog/advertising/overview.md) 和 [社交](../destinations/catalog/social/overview.md).

![顯示展開啟用的目的地目錄的Platform UI影像。](assets/destination-catalog.png)

若要建立與目的地平台的新連線，請遵循以下指南： [如何建立新的目的地連線](../destinations/ui/connect-destination.md). 然後，移至 [步驟3](#activate-audiences).

## 步驟3：對您的目的地啟用對象 {#activate-audiences}

在您成功之後 [擷取的Audience Manager對象](#configure-source) 和 [已建立新的目的地連線](#create-destination-connection)，您現在可以將對象啟用至您選擇的目的地平台。

![顯示展開啟用的目的地目錄的Platform UI影像。](assets/activate-audiences.png)

若要對您的目的地啟用對象，請遵循以下指南： [如何啟用串流目的地的對象](../destinations/ui/activate-segment-streaming-destinations.md).

## 驗證受眾啟用 {#verify}

檢查 [目的地監視檔案](../dataflows/ui/monitor-destinations.md) 有關如何監視流向目的地的資料流的詳細資訊。