---
title: 透過延展的啟用來啟用Audience Manager對象
description: 瞭解如何透過Audience Manager展開啟用，將Audience Manager對象啟用至社交和廣告目的地。
exl-id: 4105f5c5-db69-414f-9ee4-8630b0a86da7
source-git-commit: 2222e9fbf75f3082d331868f820247e0c0ce3ba2
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%

---

# 透過Audience Manager展開啟用來啟用對象

此頁面說明您必須遵循的端對端工作流程，才能將對象從Audience Manager啟動至擴展啟動支援的目的地平台。

## 開始之前 {#before-you-begin}

本指南中說明的步驟假設您已閱讀[展開式啟用概觀頁面](overview.md)，並已確認您符合對象啟用的先決條件。

>[!IMPORTANT]
>
>若要透過[!DNL Expanded Activation]啟用對象，請確定您的Audience Manager對象是以&#x200B;**雜湊電子郵件地址**&#x200B;為基礎。 如需詳細資訊，請參閱[必要條件](overview.md#prerequisites)。

## 步驟1：設定Audience Manager來源連線 {#configure-source}

[Audience Manager來源聯結器](../sources/connectors/adobe-applications/audience-manager.md)會傳送在Adobe Audience Manager中收集的對象資料，以在「擴充啟用」支援的目的地平台中啟用。

按照如何[建立Audience Manager來源連線](../sources/tutorials/ui/create/adobe-applications/audience-manager.md)的指南來設定您的來源聯結器。

![顯示具有Audience Manager來源連線之[來源]索引標籤的Platform UI影像。](assets/sources-tab.png)

>[!TIP]
>
>Adobe Audience Manager來源聯結器是「展開啟用」中唯一可用的來源聯結器。
>
>如果您想要根據其他識別碼來擷取對象，您必須購買[Real-Time CDP](../rtcdp/overview.md)的版本。 如需詳細資訊，請聯絡您的Adobe代表。

### 檢視和監視擷取的對象 {#view-audiences}

您從Audience Manager帶入「展開啟用」的對象，可以在&#x200B;**[!UICONTROL 對象]**&#x200B;儀表板中檢視。

若要檢視您的對象，請移至&#x200B;**[!UICONTROL 客戶]** -> **[!UICONTROL 對象]** -> **[!UICONTROL 瀏覽]**。

![顯示[對象]頁面的Platform UI影像。](assets/audiences-browse.png)

>[!IMPORTANT]
>
>* 要完全填入展開啟用中的對象，最多可能需要48小時的時間。 此也適用於現有Audience Manager對象的更新。
>* 新建立的Audience Manager對象不會自動出現在展開啟用中。 若要在展開啟用中擷取新區段，您必須透過Audience Manager來源聯結器新增區段。

設定Audience Manager來源聯結器後，請移至[步驟2](#create-destination-connection)。

## 步驟2：建立新的目的地連線 {#create-destination-connection}

您必須先建立與目的地平台的連線，才能將Audience Manager對象傳送至您選擇的目的地平台。

在左側邊欄中，移至&#x200B;**[!UICONTROL 連線]** -> **[!UICONTROL 目的地]** -> **[!UICONTROL 目錄]**。

[!DNL Expanded Activation]可用的目的地類別為[廣告](../destinations/catalog/advertising/overview.md)和[社交](../destinations/catalog/social/overview.md)。

![平台UI影像顯示擴展啟用的目的地目錄。](assets/destination-catalog.png)

若要建立與目的地平台的新連線，請按照[上的指南來建立新的目的地連線](../destinations/ui/connect-destination.md)。 然後，移至[步驟3](#activate-audiences)。

## 步驟3：對您的目的地啟用對象 {#activate-audiences}

在您成功[內嵌Audience Manager對象](#configure-source)及[建立新的目的地連線](#create-destination-connection)後，您現在可以將對象啟用至您選擇的目的地平台。

![平台UI影像顯示擴展啟用的目的地目錄。](assets/activate-audiences.png)

若要針對您的目的地啟用對象，請依照[上的指南操作，瞭解如何針對串流目的地啟用對象](../destinations/ui/activate-segment-streaming-destinations.md)。

## 驗證受眾啟用 {#verify}

請檢視[目的地監視檔案](../dataflows/ui/monitor-destinations.md)，以取得有關如何監視流向目的地的資料流的詳細資訊。
