---
keywords: 編輯激活，編輯目標，編輯目標
title: 編輯激活資料流
type: Tutorial
description: 按照本文中的步驟編輯Adobe Experience Platform的現有激活資料流。
exl-id: 0d79fbff-bfde-4109-8353-c7530e9719fb
source-git-commit: a6fe0f5a0c4f87ac265bf13cb8bba98252f147e0
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 0%

---

# 編輯激活資料流 {#edit-activation-flows}

在Adobe Experience Platform，您可以編輯現有激活資料流的各個元件到目標，如導出的段和配置檔案屬性、導出頻率、激活資料流是啟用還是禁用等。

## 編輯資料流 {#edit-dataflows}

按照以下步驟編輯現有激活資料流：

1. 登錄到 [Experience PlatformUI](https://platform.adobe.com/) 選擇 **[!UICONTROL 目標]** 的下界。 選擇 **[!UICONTROL 瀏覽]** 以查看現有目標資料流。

   ![瀏覽目標](../assets/ui/edit-activation/browse-destinations.png)

2. 選擇篩選器表徵圖 ![篩選器表徵圖](../assets/ui/edit-activation/filter.png) 的子菜單。 排序面板提供所有目標的清單。 可以從清單中選擇多個目標，以查看與所選目標關聯的資料流的篩選選擇。

   ![篩選目標](../assets/ui/edit-activation/filter-destinations.png)

3. 選擇要編輯的目標資料流的名稱。

   ![選擇目標](../assets/ui/edit-activation/destination-select.png)

4. 的 **[!UICONTROL 資料流運行]** 的子菜單。 此時，您可以編輯目標資料流的幾個元件：

   * 選擇 **[!UICONTROL 激活段]** 中，更改要發送到目標的段或配置檔案屬性。 此操作將引導您進入激活工作流，該工作流因目標類型而異。 有關詳細資訊，請參閱上的指南：
      * [激活觀眾資料，將流目標分段](./activate-segment-streaming-destinations.md) (例如Facebook或Twitter);
      * [將受眾資料激活到基於批配置檔案的目標](./activate-batch-profile-destinations.md) (例如，AmazonS3或OracleEloca);
      * [將觀眾資料激活到基於流配置檔案的目標](./activate-streaming-profile-destinations.md) (例如，HTTP API或AmazonKinesis)。
   * 此外，還可以編輯目標資料流名稱和說明。
   * 您可以使用 **[!UICONTROL 已啟用]/[!UICONTROL 已禁用]** 切換以啟動並暫停向目標的所有資料導出。

   ![目標詳細資訊](../assets/ui/edit-activation/destination-details.png)

## 後續步驟 {#next-steps}

按照本教程，您已成功使用 **[!UICONTROL 目的地]** 工作區以更新現有目標資料流。

有關目標的詳細資訊，請參閱 [目標概述](../catalog/overview.md)。
