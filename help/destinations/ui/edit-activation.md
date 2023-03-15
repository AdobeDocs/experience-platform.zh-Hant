---
keywords: 編輯激活，編輯目標，編輯目標
title: 編輯激活資料流
type: Tutorial
description: 請依照本文中的步驟，編輯Adobe Experience Platform中現有的啟動資料流。
exl-id: 0d79fbff-bfde-4109-8353-c7530e9719fb
source-git-commit: a6fe0f5a0c4f87ac265bf13cb8bba98252f147e0
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 0%

---

# 編輯激活資料流 {#edit-activation-flows}

在Adobe Experience Platform中，您可以編輯現有激活資料流到目標的各種元件，如導出的段和配置檔案屬性、導出頻率、激活資料流是否已啟用或禁用等。

## 編輯資料流 {#edit-dataflows}

請按照以下步驟編輯現有激活資料流：

1. 登入 [Experience PlatformUI](https://platform.adobe.com/) 選取 **[!UICONTROL 目的地]** 的下一頁。 選擇 **[!UICONTROL 瀏覽]** 從頂部標題查看現有目標資料流。

   ![瀏覽目的地](../assets/ui/edit-activation/browse-destinations.png)

2. 選取篩選圖示 ![篩選器圖示](../assets/ui/edit-activation/filter.png) ，啟動排序面板。 排序面板會提供所有目的地的清單。 您可以從清單中選擇多個目標，以查看與所選目標關聯的資料流的篩選選擇。

   ![篩選目的地](../assets/ui/edit-activation/filter-destinations.png)

3. 選擇要編輯的目標資料流的名稱。

   ![選擇目標](../assets/ui/edit-activation/destination-select.png)

4. 此 **[!UICONTROL 資料流運行]** 頁面，顯示其可用的控制項。 此時，您可以編輯目標資料流的多個元件：

   * 選擇 **[!UICONTROL 啟用區段]** ，以變更要傳送至目的地的區段或設定檔屬性。 此動作會帶您進入啟動工作流程，其會依目的地類型而有所不同。 如需詳細資訊，請參閱下列指南：
      * [啟用對象資料以劃分串流目的地](./activate-segment-streaming-destinations.md) (例如Facebook或Twitter);
      * [啟用受眾資料以批次設定檔式目的地](./activate-batch-profile-destinations.md) (例如Amazon S3或OracleEloqua);
      * [啟用受眾資料至串流設定檔式目的地](./activate-streaming-profile-destinations.md) (例如HTTP API或Amazon Kinesis)。
   * 此外，您還可以編輯目標資料流名稱和說明。
   * 您可以使用 **[!UICONTROL 已啟用]/[!UICONTROL 已停用]** 切換以開始和暫停所有匯出至目的地的資料。

   ![目的地詳細資訊](../assets/ui/edit-activation/destination-details.png)

## 後續步驟 {#next-steps}

依照本教學課程，您已成功使用 **[!UICONTROL 目的地]** 工作區，以更新現有的目標資料流。

如需目的地的詳細資訊，請參閱 [目的地概述](../catalog/overview.md).
