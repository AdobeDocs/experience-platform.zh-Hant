---
keywords: 編輯啟動、編輯目的地、編輯目的地
title: 編輯啟動資料流
type: Tutorial
description: 請依照本文的步驟，在Adobe Experience Platform中編輯現有的啟用資料流。
exl-id: 0d79fbff-bfde-4109-8353-c7530e9719fb
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 0%

---

# 編輯啟動資料流 {#edit-activation-flows}

在Adobe Experience Platform中，您可以編輯傳送到目的地的現有啟用資料流的各種元件，例如匯出的對象和設定檔屬性、匯出頻率、啟用資料流已啟用或停用等等。

## 編輯資料流 {#edit-dataflows}

請依照下列步驟編輯現有的啟用資料流程：

1. 登入[Experience PlatformUI](https://platform.adobe.com/)，並從左側導覽列中選取&#x200B;**[!UICONTROL 目的地]**。 從頂端標題選取&#x200B;**[!UICONTROL 瀏覽]**&#x200B;以檢視您現有的目的地資料流。

   ![瀏覽目的地](../assets/ui/edit-activation/browse-destinations.png)

2. 選取左上方的篩選圖示![篩選圖示](/help/images/icons/filter.png)以啟動排序面板。 排序面板會提供您所有目的地的清單。 您可以從清單中選取多個目的地，以檢視與所選目的地相關聯的資料流篩選選取專案。

   ![篩選目的地](../assets/ui/edit-activation/filter-destinations.png)

3. 選取您要編輯的目的地資料流名稱。

   ![選取目的地](../assets/ui/edit-activation/destination-select.png)

4. 目的地的&#x200B;**[!UICONTROL 資料流執行]**&#x200B;頁面隨即顯示，並顯示其可用的控制項。 此時，您可以編輯目的地資料流的數個元件：

   * 在右側邊欄中選取「**[!UICONTROL 啟用對象]**」，以變更要傳送至目的地的對象或設定檔屬性。 此動作會將您導向啟動工作流程，此工作流程會依目的地型別而有所不同。 如需詳細資訊，請參閱以下指南：
      * [啟用對象資料至對象串流目的地](./activate-segment-streaming-destinations.md) (例如Facebook或Twitter)；
      * [將對象資料啟用至批次設定檔型目的地](./activate-batch-profile-destinations.md) (例如Amazon S3或Oracle Eloqua)；
      * [啟用受眾資料至串流設定檔型目的地](./activate-streaming-profile-destinations.md) (例如HTTP API或Amazon Kinesis)。

   * 此外，您可以編輯目的地資料流名稱和說明。
   * 您可以使用&#x200B;**[!UICONTROL 已啟用]/[!UICONTROL 已停用]**&#x200B;切換來開始和暫停所有資料匯出至目的地。

   ![目的地詳細資料](../assets/ui/edit-activation/destination-details.png)

## 後續步驟 {#next-steps}

依照本教學課程中的指示，您已成功使用&#x200B;**[!UICONTROL 目的地]**&#x200B;工作區來更新現有的目的地資料流。

如需有關目的地的詳細資訊，請參閱[目的地概觀](../catalog/overview.md)。
