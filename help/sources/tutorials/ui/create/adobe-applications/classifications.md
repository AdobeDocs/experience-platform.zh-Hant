---
keywords: Experience Platform；首頁；熱門主題；analytics；分類
description: 了解如何在UI中建立Adobe Analytics來源連接器，將分類資料匯入Adobe Experience Platform。
solution: Experience Platform
title: 在UI中為分類資料建立Adobe Analytics來源連線
type: Tutorial
exl-id: d606720d-f1ca-47cc-919b-643a8fc61e07
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 6%

---

# 在UI中為分類資料建立Adobe Analytics來源連線

本教學課程提供在UI中建立Adobe Analytics分類資料來源連線，將分類資料匯入Adobe Experience Platform的步驟。

## 快速入門

本教學課程需要妥善了解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化架構。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md):Experience Platform提供可將單一Platform執行個體分割成個別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

Analytics分類Data Connector會要求您的資料已移轉至新的 [!DNL Classifications] Adobe Analytics基礎設施。 若要確認資料的移轉狀態，請連絡您的Adobe客戶成功經理。

## 選取您的分類

登入 [Adobe Experience Platform](https://platform.adobe.com) 然後選取 **[!UICONTROL 來源]** 從左側導覽列存取來源工作區。 此 **[!UICONTROL 目錄]** 螢幕顯示可用來建立入站連線的來源。 每個來源卡會顯示設定新帳戶或新增資料至現有帳戶的選項。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在 **[!UICONTROL Adobe應用程式]** 類別，請選取 **[!UICONTROL Adobe Analytics]** 卡片，然後選取 **[!UICONTROL 新增資料]** 以開始使用Analytics分類資料。

![](../../../../images/tutorials/create/classifications/catalog.png)

此 **[!UICONTROL Analytics來源新增資料]** 步驟。 選擇 **[!UICONTROL 分類]** 從頂端標題查看 [!DNL Classifications] 資料集，包括其維度ID、報表套裝名稱和報表套裝ID的相關資訊。

每個頁面最多顯示10個不同 [!DNL Classifications] 可選擇的資料集。 選擇 **[!UICONTROL 下一個]** ，以瀏覽更多選項。 右側的面板顯示 [!DNL Classifications] 您選取的資料集及其名稱。 此面板也可讓您移除 [!DNL Classifications] 您可能錯誤選取了資料集，或使用一個動作清除所有選取項目。

您最多可以選取30個不同的 [!DNL Classifications] 將資料集帶入 [!DNL Platform].

選取您的 [!DNL Classifications] 資料集，選取 **[!UICONTROL 下一個]** 在頁面的右上角。

![](../../../../images/tutorials/create/classifications/add-data.png)

## 檢閱分類

此 **[!UICONTROL 檢閱]** 步驟，讓您檢閱您選取的 [!DNL Classifications] 資料集之前建立。 詳細資料會分組為下列類別：

* **[!UICONTROL 連線]**:顯示源平台和連接狀態。
* **[!UICONTROL 資料類型]**:顯示所選的數量 [!DNL Classifications].
* **[!UICONTROL 排程]**:顯示的同步頻率 [!DNL Classifications] 資料。

審核資料流後，按一下 **[!UICONTROL 完成]** 並允許建立資料流的時間。

![](../../../../images/tutorials/create/classifications/review.png)

## 監視分類資料流

建立資料流後，您就可以監視正在通過它進行內嵌的資料。 從 **[!UICONTROL 目錄]** 螢幕，選擇 **[!UICONTROL 資料流]** 查看與 [!DNL Classifications] 帳戶。

![](../../../../images/tutorials/create/classifications/dataflows.png)

此 **[!UICONTROL 資料流]** 畫面。 此頁上是資料流清單，包括有關其名稱、源資料和資料流運行狀態的資訊。 在右邊， **[!UICONTROL 屬性]** 包含與您的 [!DNL Classifications] 資料流。

選取 **[!UICONTROL 目標資料集]** 您想要存取。

![](../../../../images/tutorials/create/classifications/list-of-dataflows.png)

此 **[!UICONTROL 資料集活動]** 「 」頁面顯示您所選目標資料集的相關資訊，包括批次狀態、資料集ID和結構的詳細資訊。

>[!IMPORTANT]
>
>雖然對其他來源連接器而言，刪除資料集是可行的，但是目前 Analytics Classifications 資料連接器不支援此作業。 如果您誤刪了資料集，請聯絡 Adobe 客戶服務。

![](../../../../images/tutorials/create/classifications/dataset.png)


## 後續步驟

依照本教學課程，您已建立Analytics分類資料連接器，其 [!DNL Classifications] 資料 [!DNL Platform]. 如需詳細資訊，請參閱下列檔案 [!DNL Analytics] 和 [!DNL Classifications] 資料：

* [Analytics Data Connector概觀](../../../../connectors/adobe-applications/analytics.md)
* [在UI中建立Analytics資料連線](./analytics.md)
* [關於分類](https://experienceleague.adobe.com/docs/analytics/components/classifications/c-classifications.html)
