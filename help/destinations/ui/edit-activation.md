---
keywords: 編輯啟動、編輯目的地、編輯目的地
title: 編輯啟動資料流
type: Tutorial
description: 請依照本文的步驟，在Adobe Experience Platform中編輯現有的啟用資料流。
exl-id: 0d79fbff-bfde-4109-8353-c7530e9719fb
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '917'
ht-degree: 0%

---

# 編輯啟動資料流 {#edit-activation-flows}

在Adobe Experience Platform中，您可以將現有啟用資料流的各種元件設定到目的地，例如：

* [啟用或停用](#enable-disable-dataflows)啟用資料流
* [新增其他對象](#add-audiences)至啟用資料流
* [編輯對應的屬性和身分](#edit-mapped-attributes)
* [編輯啟用排程和匯出頻率](#edit-schedule-frequency)
* [新增其他資料集](#add-datasets)至啟用工作流程
* [編輯您啟動資料流程的行銷動作](#edit-marketing-actions)
* [套用存取標籤](#apply-access-labels)至匯出的資料
* [編輯啟動資料流程的名稱和說明](#edit-names-descriptions)

## 瀏覽啟動資料流 {#browse-activation-dataflows}

請依照下列步驟，瀏覽您現有的啟用資料流程，並識別您要編輯的資料流程。

1. 登入[Experience Platform UI](https://platform.adobe.com/)，並從左側導覽列中選取&#x200B;**[!UICONTROL Destinations]**。 從頂端標題選取&#x200B;**[!UICONTROL Browse]**&#x200B;以檢視您現有的目的地資料流。

   ![瀏覽目的地](../assets/ui/edit-activation/browse-destinations.png)

2. 選取左上方的篩選圖示![篩選圖示](../../images/icons/filter.png)以啟動排序面板。 排序面板會提供您所有目的地的清單。 您可以從清單中選取多個目的地，以檢視與所選目的地相關聯的資料流篩選選取專案。

   ![篩選目的地](../assets/ui/edit-activation/filter-destinations.png)

3. 選取您要編輯的目的地資料流名稱。

   ![選取目的地](../assets/ui/edit-activation/destination-select.png)

4. 目的地的&#x200B;**[!UICONTROL Dataflow runs]**&#x200B;頁面隨即顯示，並顯示其可用的控制項。 您可以根據目的地型別執行各種資料流作業。 如需每個支援的資料流作業的相關資訊，請參閱下一節。

## 啟用或停用啟用資料流程 {#enable-disable-dataflows}

使用&#x200B;**[!UICONTROL Enabled]/[!UICONTROL Disabled]**&#x200B;切換以開始或暫停所有匯出至目的地的資料。

![Experience Platform UI影像顯示「啟用/停用」資料流執行切換。](../assets/ui/edit-activation/enable-toggle.png)

## 將對象新增至啟用資料流 {#add-audiences}

在右側邊欄中選取&#x200B;**[!UICONTROL Activate audiences]**&#x200B;以變更要傳送至目的地的對象。 此動作會帶您進入啟動工作流程。

![Experience Platform UI影像顯示「啟用對象資料流執行」選項。](../assets/ui/edit-activation/activate-audiences.png)

在啟動工作流程的&#x200B;**[!UICONTROL Select audiences]**&#x200B;步驟中，您可以移除現有的對象，或將新對象新增至啟動工作流程。

啟用工作流程會依目的地型別而略有不同。 如需每種目的地型別之啟用工作流程的詳細資訊，請閱讀下列指南：

* [啟用串流目的地的對象](./activate-segment-streaming-destinations.md) （例如Facebook或Twitter）；
* [啟用對象以批次設定檔匯出目的地](./activate-batch-profile-destinations.md) (例如，Amazon S3或Oracle Eloqua)；
* [啟用受眾以串流設定檔匯出目的地](./activate-streaming-profile-destinations.md) (例如HTTP API或Amazon Kinesis)。

## 編輯啟用排程和匯出頻率 {#edit-schedule-frequency}

在右側邊欄中選取&#x200B;**[!UICONTROL Activate audiences]**。 此動作會帶您進入啟動工作流程。

![Experience Platform UI影像顯示「啟用對象資料流執行」選項。](../assets/ui/edit-activation/activate-audiences.png)

選取啟動工作流程中的&#x200B;**[!UICONTROL Scheduling]**&#x200B;步驟，以編輯資料流程的啟動排程和匯出頻率。 此步驟可讓您設定將資料匯出至目的地的頻率。

在啟動工作流程的&#x200B;**[!UICONTROL Scheduling]**&#x200B;步驟中，您可以：

* 調整匯出頻率。
* 設定或修改啟動資料流的開始和結束日期等。

您可以執行的排程作業會因目的地型別而稍有不同。 如需每種目的地型別之啟用工作流程的詳細資訊，請閱讀下列指南：

* [啟用串流目的地的對象](./activate-segment-streaming-destinations.md) （例如Facebook或Twitter）；
* [啟用對象以批次設定檔匯出目的地](./activate-batch-profile-destinations.md) (例如，Amazon S3或Oracle Eloqua)；
* [啟用受眾以串流設定檔匯出目的地](./activate-streaming-profile-destinations.md) (例如HTTP API或Amazon Kinesis)。

## 編輯對應的屬性和身分 {#edit-mapped-attributes}

在右側邊欄中選取&#x200B;**[!UICONTROL Activate audiences]**。 此動作會帶您進入啟動工作流程。

![Experience Platform UI影像顯示「啟用對象資料流執行」選項。](../assets/ui/edit-activation/activate-audiences.png)

選取啟動工作流程中的&#x200B;**[!UICONTROL Mapping]**&#x200B;步驟，以編輯啟動資料流程的對應屬性和身分。 這可讓您調整應將哪些設定檔屬性和身分匯出至目的地。

在啟動工作流程的&#x200B;**[!UICONTROL Mapping]**&#x200B;步驟中，您可以：

* 將新屬性或身分新增到對應。
* 從對應移除現有的屬性或身分。
* 調整對應順序，以定義匯出檔案中的欄順序。

啟用工作流程會依目的地型別而略有不同。 如需每種目的地型別之啟用工作流程的詳細資訊，請閱讀下列指南：

* [啟用串流目的地的對象](./activate-segment-streaming-destinations.md) （例如Facebook或Twitter）；
* [啟用對象以批次設定檔匯出目的地](./activate-batch-profile-destinations.md) (例如，Amazon S3或Oracle Eloqua)；
* [啟用受眾以串流設定檔匯出目的地](./activate-streaming-profile-destinations.md) (例如HTTP API或Amazon Kinesis)。

## 將資料集新增至啟用資料流 {#add-datasets}

在右側邊欄中選取「**[!UICONTROL Export datasets]**」，以選取要匯出至您目的地的其他資料集。 此選項會帶您前往[資料集匯出工作流程](export-datasets.md)。

>[!NOTE]
>
>此選項僅對支援資料集匯出[的](export-datasets.md#supported-destinations)目的地可見。

![Experience Platform UI影像顯示「匯出資料集」資料流執行選項。](../assets/ui/edit-activation/export-datasets.png)

## [!BADGE Beta]{type=Informative}編輯行銷動作 {#edit-marketing-actions}

>[!NOTE]
>
>此功能目前在&#x200B;**beta**&#x200B;中。 若要要求存取權，請聯絡您的Adobe代表。

您可以新增或移除最初連線至目的地時設定的行銷動作。

在右側邊欄中選取&#x200B;**[!UICONTROL Edit marketing actions]**&#x200B;以開啟行銷動作選取畫面。

![Experience Platform UI影像顯示[編輯行銷動作]選項。](../assets/ui/edit-activation/edit-marketing-actions.png)

選取適用的行銷動作，然後選取&#x200B;**[!UICONTROL Save]**&#x200B;以套用變更。

![Experience Platform UI影像顯示編輯行銷動作畫面。](../assets/ui/edit-activation/edit-marketing-actions-screen.png)


## 套用存取標籤 {#apply-access-labels}

選取&#x200B;**[!UICONTROL Apply access labels]**&#x200B;以編輯已匯出資料的資料使用標籤。 請參閱[資料使用標籤檔案](../../data-governance/labels/overview.md)以瞭解更多資訊。

![Experience Platform UI影像顯示「匯出資料集」資料流執行選項。](../assets/ui/edit-activation/apply-access-labels.png)

## 編輯啟動資料流名稱和說明 {#edit-names-descriptions}

若要編輯啟動資料流名稱和說明，請使用&#x200B;**[!UICONTROL Destination name]**&#x200B;和&#x200B;**[!UICONTROL Description]**&#x200B;欄位。

![目的地詳細資料](../assets/ui/edit-activation/edit-destination-name-description.png)

## 後續步驟 {#next-steps}

依照本教學課程中的指示，您已成功使用&#x200B;**[!UICONTROL destinations]**&#x200B;工作區來更新現有的目的地資料流。

如需有關目的地的詳細資訊，請參閱[目的地概觀](../catalog/overview.md)。
