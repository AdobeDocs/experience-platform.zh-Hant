---
keywords: Experience Platform; home；熱門主題；analytics；分類
description: 瞭解如何建立UI的Adobe Analytics來源連接器，將分類資料匯入Adobe Experience Platform。
solution: Experience Platform
title: 在UI中建立分類資料的Adobe Analytics來源連線
topic-legacy: overview
type: Tutorial
exl-id: d606720d-f1ca-47cc-919b-643a8fc61e07
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '631'
ht-degree: 0%

---

# 在UI中建立分類資料的Adobe Analytics來源連線

本教學課程提供在UI中建立「Adobe Analytics分類資料來源」連線以將分類資料匯入Adobe Experience Platform的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列部分有正確的理解：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化架構。
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md):Experience Platform提供虛擬沙盒，可將單一平台實例分割為獨立的虛擬環境，以協助開發和發展數位體驗應用程式。

Analytics分類資料連接器要求您的資料在使用前必須移轉至Adobe Analytics的新[!DNL Classifications]基礎架構。 若要確認資料的移轉狀態，請連絡您的Adobe客戶成功經理。

## 選取您的分類

登入[Adobe Experience Platform](https://platform.adobe.com)，然後從左側導覽列選擇&#x200B;**[!UICONTROL Sources]**&#x200B;以存取來源工作區。 **[!UICONTROL Catalog]**&#x200B;螢幕顯示可用源，以建立入站連接。 每個來源卡會顯示一個選項，可設定新帳戶或將資料新增至現有帳戶。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在&#x200B;**[!UICONTROL Adobe applications]**&#x200B;類別下，選取&#x200B;**[!UICONTROL Adobe Analytics]**&#x200B;卡片，然後選取&#x200B;**[!UICONTROL Add data]**&#x200B;以開始使用Analytics分類資料。

![](../../../../images/tutorials/create/classifications/catalog.png)

出現&#x200B;**[!UICONTROL Analytics source add data]**&#x200B;步驟。 從頂端標題中選取&#x200B;**[!UICONTROL Classifications]**，以檢視[!DNL Classifications]資料集清單，包括其維度ID、報表套裝名稱和報表套裝ID的相關資訊。

每個頁面最多會顯示十個不同的[!DNL Classifications]資料集。 選擇頁面底部的&#x200B;**[!UICONTROL Next]**&#x200B;以瀏覽更多選項。 右側的面板顯示所選[!DNL Classifications]資料集的總數及其名稱。 此面板還允許您刪除您可能誤選的[!DNL Classifications]資料集，或通過一個操作清除所有選擇。

您最多可以選擇30個不同的[!DNL Classifications]資料集，以導入[!DNL Platform]。

選擇[!DNL Classifications]資料集後，請選擇頁面右上方的&#x200B;**[!UICONTROL Next]**。

![](../../../../images/tutorials/create/classifications/add-data.png)

## 檢視您的分類

出現&#x200B;**[!UICONTROL Review]**&#x200B;步驟，允許您在建立[!DNL Classifications]資料集之前查看所選的資料集。 詳細資訊會分組在下列類別中：

* **[!UICONTROL Connection]**:顯示源平台和連接狀態。
* **[!UICONTROL Data type]**:顯示選定的數量 [!DNL Classifications]。
* **[!UICONTROL Scheduling]**:顯示資料的同步 [!DNL Classifications] 頻率。

複查資料流後，按一下&#x200B;**[!UICONTROL Finish]** ，並為建立資料流留出一些時間。

![](../../../../images/tutorials/create/classifications/review.png)

## 監控您的分類資料流

建立資料流後，您可以監視通過其獲取的資料。 在&#x200B;**[!UICONTROL Catalog]**&#x200B;螢幕中，選擇&#x200B;**[!UICONTROL Dataflows]**&#x200B;以查看與[!DNL Classifications]帳戶關聯的已建立流的清單。

![](../../../../images/tutorials/create/classifications/dataflows.png)

出現&#x200B;**[!UICONTROL Dataflows]**&#x200B;螢幕。 此頁上是資料流清單，包括有關其名稱、源資料和資料流運行狀態的資訊。 在右側是&#x200B;**[!UICONTROL Properties]**&#x200B;面板，其中包含有關[!DNL Classifications]資料流的元資料。

選擇要訪問的&#x200B;**[!UICONTROL Target dataset]**。

![](../../../../images/tutorials/create/classifications/list-of-dataflows.png)

**[!UICONTROL Dataset activity]**&#x200B;頁面會顯示您選取之目標資料集的相關資訊，包括其批次狀態、資料集ID和架構的詳細資訊。

>[!IMPORTANT]
>
>雖然刪除資料集對於其他來源連接器是可能的，但Analytics分類資料連接器目前不支援它。 如果您確實錯誤刪除資料集，請聯絡Adobe客戶服務。

![](../../../../images/tutorials/create/classifications/dataset.png)


## 後續步驟

在本教學課程中，您已建立Analytics分類資料連接器，可將[!DNL Classifications]資料匯入[!DNL Platform]。 有關[!DNL Analytics]和[!DNL Classifications]資料的詳細資訊，請參閱以下文檔：

* [Analytics資料連接器概觀](../../../../connectors/adobe-applications/analytics.md)
* [在UI中建立Analytics資料連線](./analytics.md)
* [關於分類](https://experienceleague.adobe.com/docs/analytics/components/classifications/c-classifications.html)
