---
keywords: 編輯啟動、編輯目的地、編輯目的地
title: 編輯啟動資料流
type: Tutorial
description: 請依照本文的步驟，在Adobe Experience Platform中編輯現有的啟用資料流。
exl-id: 0d79fbff-bfde-4109-8353-c7530e9719fb
source-git-commit: ca33131c505803b74075f6d8331095b016a301a0
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 0%

---

# 編輯啟動資料流 {#edit-activation-flows}

在Adobe Experience Platform中，您可以將現有啟用資料流的各種元件設定到目的地，例如：

* [啟用或停用](#enable-disable-dataflows)啟動資料流；
* [新增其他對象和設定檔屬性](#add-audiences)至啟動資料流；
* [新增其他資料集](#add-datasets)至啟用工作流程；
* [編輯啟動資料流程的名稱和說明](#edit-names-descriptions)；

<!-- * [Apply access labels](#apply-access-labels) to exported data; -->

## 瀏覽啟動資料流 {#browse-activation-dataflows}

請依照下列步驟，瀏覽您現有的啟用資料流程，並識別您要編輯的資料流程。

1. 登入[Experience PlatformUI](https://platform.adobe.com/)，並從左側導覽列中選取&#x200B;**[!UICONTROL 目的地]**。 從頂端標題選取&#x200B;**[!UICONTROL 瀏覽]**&#x200B;以檢視您現有的目的地資料流。

   ![瀏覽目的地](../assets/ui/edit-activation/browse-destinations.png)

2. 選取左上方的篩選圖示![篩選圖示](../../images/icons/filter.png)以啟動排序面板。 排序面板會提供您所有目的地的清單。 您可以從清單中選取多個目的地，以檢視與所選目的地相關聯的資料流篩選選取專案。

   ![篩選目的地](../assets/ui/edit-activation/filter-destinations.png)

3. 選取您要編輯的目的地資料流名稱。

   ![選取目的地](../assets/ui/edit-activation/destination-select.png)

4. 目的地的&#x200B;**[!UICONTROL 資料流執行]**&#x200B;頁面隨即顯示，並顯示其可用的控制項。 您可以根據目的地型別執行各種資料流作業。 如需每個支援的資料流作業的相關資訊，請參閱下一節。

## 啟用或停用啟用資料流程 {#enable-disable-dataflows}

使用&#x200B;**[!UICONTROL 已啟用]/[!UICONTROL 已停用]**&#x200B;切換以開始或暫停所有資料匯出至目的地。

![Experience PlatformUI影像顯示已啟用/已停用的資料流執行切換。](../assets/ui/edit-activation/enable-toggle.png)

## 將對象新增至啟用資料流 {#add-audiences}

在右側邊欄中選取「**[!UICONTROL 啟用對象]**」，以變更要傳送至目的地的對象或設定檔屬性。 此動作會將您導向啟動工作流程，此工作流程會依目的地型別而有所不同。

![顯示[啟用對象資料流執行]選項的Experience PlatformUI影像。](../assets/ui/edit-activation/activate-audiences.png)

如需每種目的地型別之啟用工作流程的詳細資訊，請參閱下列指南：

* [啟用串流目的地的對象](./activate-segment-streaming-destinations.md) (例如Facebook或Twitter)；
* [啟用對象以批次設定檔匯出目的地](./activate-batch-profile-destinations.md) (例如，Amazon S3或Oracle Eloqua)；
* [啟用受眾以串流設定檔匯出目的地](./activate-streaming-profile-destinations.md) (例如HTTP API或Amazon Kinesis)。

## 將資料集新增至啟用資料流 {#add-datasets}

在右側邊欄中選取「**[!UICONTROL 匯出資料集]**」，以選取其他要匯出至目的地的資料集。 此選項會帶您前往[資料集匯出工作流程](export-datasets.md)。

>[!NOTE]
>
>此選項僅對支援資料集匯出](export-datasets.md#supported-destinations)的[目的地可見。

![顯示[匯出資料集]資料流執行選項的Experience PlatformUI影像。](../assets/ui/edit-activation/export-datasets.png)

<!-- ## Apply access labels {#apply-access-labels}

Select **[!UICONTROL Apply access labels]** to edit the data usage labels for the exported data. See the [data usage labels documentation](../../data-governance/labels/overview.md) to learn more.

![Experience Platform UI image showing the Export datasets dataflow run option.](../assets/ui/edit-activation/apply-access-labels.png) -->

## 編輯啟動資料流名稱和說明 {#edit-names-descriptions}

若要編輯啟動資料流名稱和描述，請使用&#x200B;**[!UICONTROL 目的地名稱]**&#x200B;和&#x200B;**[!UICONTROL 描述]**&#x200B;欄位。

![目的地詳細資料](../assets/ui/edit-activation/edit-destination-name-description.png)

## 後續步驟 {#next-steps}

依照本教學課程中的指示，您已成功使用&#x200B;**[!UICONTROL 目的地]**&#x200B;工作區來更新現有的目的地資料流。

如需有關目的地的詳細資訊，請參閱[目的地概觀](../catalog/overview.md)。
