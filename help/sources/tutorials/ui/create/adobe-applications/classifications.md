---
keywords: Experience Platform；首頁；熱門主題；分析；分類
description: 瞭解如何在UI中建立Adobe Analytics來源聯結器，以將分類資料帶入Adobe Experience Platform。
solution: Experience Platform
title: 在UI中建立分類資料的Adobe Analytics Source連線
type: Tutorial
exl-id: d606720d-f1ca-47cc-919b-643a8fc61e07
source-git-commit: fcebef97ba9cc667f80afd55980c5460912a56fb
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 0%

---

# 在UI中建立分類資料的Adobe Analytics來源連線

本教學課程提供在UI中建立Adobe Analytics分類資料來源連線的步驟，以將分類資料帶入Adobe Experience Platform。

## 快速入門

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)：Experience Platform用來組織客戶體驗資料的標準化架構。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md)：Experience Platform提供可將單一Platform執行個體分割成個別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

Analytics Classifications Data Connector會要求您的資料先移轉至Adobe Analytics的新[!DNL Classifications]基礎結構才能使用。 若要確認資料的移轉狀態，請聯絡您的Adobe客戶團隊。

## 選取您的分類

登入[Adobe Experience Platform](https://platform.adobe.com)，然後從左側導覽列中選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取來源工作區。 **[!UICONTROL 目錄]**&#x200B;畫面會顯示可用來建立輸入連線的可用來源。 每個來源卡片都會顯示選項，讓您設定新帳戶或將資料新增至現有帳戶。

您可以從熒幕左側的目錄中選取適當的類別。 或者，您可以使用搜尋選項來尋找您要使用的特定來源。

在&#x200B;**[!UICONTROL Adobe應用程式]**&#x200B;類別下，選取&#x200B;**[!UICONTROL Adobe Analytics]**&#x200B;卡片，然後選取&#x200B;**[!UICONTROL 新增資料]**&#x200B;以開始使用Analytics分類資料。

![](../../../../images/tutorials/create/classifications/catalog.png)

**[!UICONTROL Analytics來源新增資料]**&#x200B;步驟隨即顯示。 從頂端標題選取「**[!UICONTROL 分類]**」，即可檢視[!DNL Classifications]個資料集的清單，包含其維度ID、報表套裝名稱和報表套裝ID的相關資訊。

每個頁面最多可顯示10個您可選擇的不同[!DNL Classifications]資料集。 選取頁面底部的&#x200B;**[!UICONTROL 下一步]**&#x200B;以瀏覽更多選項。 右側的面板會顯示您選取的[!DNL Classifications]個資料集總數及其名稱。 此面板也可讓您移除任何您可能不小心選取的[!DNL Classifications]資料集，或透過單一動作清除所有選取專案。

您最多可以選取30個不同的[!DNL Classifications]資料集以引入[!DNL Platform]。

選取[!DNL Classifications]資料集後，請在頁面右上角選取「**[!UICONTROL 下一步]**」。

![](../../../../images/tutorials/create/classifications/add-data.png)

## 檢閱您的分類

**[!UICONTROL 檢閱]**&#x200B;步驟隨即顯示，可讓您在建立所選的[!DNL Classifications]資料集之前先檢閱該資料集。 詳細資料會分組到以下類別中：

* **[!UICONTROL 連線]**：顯示來源平台和連線的狀態。
* **[!UICONTROL 資料型別]**：顯示選取的[!DNL Classifications]數目。
* **[!UICONTROL 排程]**：顯示[!DNL Classifications]資料的同步處理頻率。

檢閱您的資料流後，請按一下[完成] ****，並等待一些時間來建立資料流。

![](../../../../images/tutorials/create/classifications/review.png)

## 監視您的分類資料流

建立資料流後，您可以監視透過它擷取的資料。 在&#x200B;**[!UICONTROL 目錄]**&#x200B;畫面中，選取&#x200B;**[!UICONTROL 資料流程]**&#x200B;以檢視與您的[!DNL Classifications]帳戶關聯的已建立流程清單。

![](../../../../images/tutorials/create/classifications/dataflows.png)

**[!UICONTROL 資料流]**&#x200B;畫面會出現。 此頁面提供資料流清單，包含其名稱、來源資料和資料流執行狀態的資訊。 右側是&#x200B;**[!UICONTROL 屬性]**&#x200B;面板，其中包含您的[!DNL Classifications]資料流相關中繼資料。

選取您要存取的&#x200B;**[!UICONTROL 目標資料集]**。

![](../../../../images/tutorials/create/classifications/list-of-dataflows.png)

**[!UICONTROL 資料集活動]**&#x200B;頁面會顯示您所選取目標資料集的相關資訊，包括其批次狀態、資料集ID和結構描述的詳細資訊。

![](../../../../images/tutorials/create/classifications/dataset.png)

## 後續步驟

依照本教學課程中的指示，您已建立將[!DNL Classifications]資料帶入[!DNL Platform]的Analytics Classifications Data Connector。 有關[!DNL Analytics]和[!DNL Classifications]資料的詳細資訊，請參閱下列檔案：

* [Analytics資料聯結器總覽](../../../../connectors/adobe-applications/analytics.md)
* [在使用者介面中建立Analytics資料連線](./analytics.md)
* [關於分類](https://experienceleague.adobe.com/docs/analytics/components/classifications/c-classifications.html)
