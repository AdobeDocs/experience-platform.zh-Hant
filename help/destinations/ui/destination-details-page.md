---
keywords: 目標；目標；目標詳細資訊頁；目標詳細資訊頁
title: 檢視目標詳細資訊
description: '個別目標的詳細資料頁面提供目標詳細資料的概述。 目標詳細資訊包括目標名稱、ID、對應至目標的區段，以及用於編輯啟動以及啟用和停用資料流的控制項。 '
seo-description: '個別目標的詳細資料頁面提供目標詳細資料的概述。 目標詳細資訊包括目標名稱、ID、對應至目標的區段，以及用於編輯啟動以及啟用和停用資料流的控制項。 '
translation-type: tm+mt
source-git-commit: 4f5e7dfee17b2dde371efb82cf52d91c08696f39
workflow-type: tm+mt
source-wordcount: '701'
ht-degree: 0%

---


# 檢視目標詳細資訊

## 概述 {#overview}

在Adobe Experience Platform用戶介面中，您可以查看和監視目標的屬性和活動。 這些詳細資訊包括目標的名稱和ID、啟用或停用目標的控制項，以及更多功能。 批次目的地的詳細資訊還包括已啟動描述檔記錄的度量和資料流執行的歷史記錄。

>[!NOTE]
>
>目標詳細資訊頁面是平台UI中[!UICONTROL Destinations]工作區的一部分。 如需詳細資訊，請參閱[[!UICONTROL Destinations]工作區概觀](./destinations-workspace.md)。

在平台UI的&#x200B;**[!UICONTROL Destinations]**&#x200B;工作區中，導覽至&#x200B;**[!UICONTROL Browse]**&#x200B;標籤，並選取您要檢視的目標名稱。

![](../assets/ui/details-page/select-destination.png)

此時會顯示目標的詳細資料頁面，顯示其可用控制項。 如果您正在查看批處理目標的詳細資訊，則還會顯示一個監視控制面板。

![](../assets/ui/details-page/details.png)

此外，在「瀏覽」頁籤上，您可以選擇![垃圾桶](../assets/ui/details-page/trash-icon.png)表徵圖來刪除選定的資料流。 在刪除資料流之前，任何激活到目標的段都將被取消映射。

![](../assets/ui/details-page/delete-flow.png)

## 右邊欄

右側邊欄會顯示目標的基本資訊。

![](../assets/ui/details-page/right-rail.png)

下表涵蓋右側導軌提供的控制項和詳細資訊：

| 右側欄項目 | 說明 |
| --- | --- |
| [!UICONTROL Activate] | 選取此控制項可編輯哪些區段已對應至目標。 如需詳細資訊，請參閱[啟用區段至目標](./activate-destinations.md)的指南。 |
| [!UICONTROL Delete] | 允許您刪除此資料流，並取消映射以前激活的段（如果有）。 |
| [!UICONTROL Destination name] | 可以編輯此欄位以更新目標的名稱。 |
| [!UICONTROL Description] | 您可以編輯此欄位，以更新或新增選擇性說明至目標。 |
| [!UICONTROL Destination] | 代表對象被傳送至的目標平台。 如需詳細資訊，請參閱[目標目錄](../catalog/overview.md)。 |
| [!UICONTROL Status] | 指示目標是啟用還是禁用。 |
| [!UICONTROL Marketing actions] | 指出針對資料治理用途適用於此目的地的行銷動作（使用案例）。 |
| [!UICONTROL Category] | 指示目標類型。 如需詳細資訊，請參閱[目標目錄](../catalog/overview.md)。 |
| [!UICONTROL Connection type] | 指出將觀眾傳送至目的地的表單。 可能的值包括&quot;[!UICONTROL Cookie]&quot;和&quot;[!UICONTROL Profile-based]&quot;。 |
| [!UICONTROL Frequency] | 指出觀眾被傳送至目的地的頻率。 可能的值包括&quot;[!UICONTROL Streaming]&quot;和&quot;[!UICONTROL Batch]&quot;。 |
| [!UICONTROL Identity] | 代表目標接受的識別名稱空間，例如`GAID`、`IDFA`或`email`。 有關接受的身份名稱空間的詳細資訊，請參閱[身份名稱空間概述](../../identity-service/namespaces.md)。 |
| [!UICONTROL Created by] | 表示建立此目標的用戶。 |
| [!UICONTROL Created] | 指示建立此目標時的UTC日期時間。 |

{style=&quot;table-layout:auto&quot;}

## [!UICONTROL Enabled]/[!UICONTROL Disabled] toggle

您可以使用&#x200B;**[!UICONTROL Enabled]/[!UICONTROL Disabled]**&#x200B;切換來啟動和暫停所有匯出至目的地的資料。

![](../assets/ui/details-page/enable-disable.png)

## [!UICONTROL Dataflow runs]

[!UICONTROL Dataflow runs]頁籤提供資料流運行到批處理目標的度量資料。 會顯示個別執行及其特定度量的清單，以及下列描述檔記錄總計：

* **[!UICONTROL Profile records activated]**:為啟動而建立或更新的描述檔記錄總計。
* **[!UICONTROL Profile records skipped]**:根據描述檔退出或遺失屬性，跳過以進行啟動的描述檔記錄總計。

![](../assets/ui/details-page/dataflow-runs.png)

>[!NOTE]
>
>根據目標資料流的調度頻率生成資料流運行。 會針對套用至區段的每個合併原則執行個別的資料流。

要查看特定資料流運行的詳細資訊，請從清單中選擇運行的開始時間。 資料流運行的詳細資訊頁包含其他資訊，如處理的資料大小和錯誤診斷詳細資訊中發生的所有錯誤的清單。

![](../assets/ui/details-page/dataflow.png)

## [!UICONTROL Activation data] {#activation-data}

[!UICONTROL Activation data]標籤會顯示已映射至目標的區段清單，包括其開始日期和結束日期（如果適用）。 若要檢視特定區段的詳細資訊，請從清單中選取其名稱。

![](../assets/ui/details-page/activation-data.png)

>[!NOTE]
>
>如需探索區段詳細資訊頁面的詳細資訊，請參閱[區段UI概觀](../../segmentation/ui/overview.md#segment-details)。

## 後續步驟

本檔案涵蓋目標詳細資訊頁面的功能。 有關在UI中管理目標的詳細資訊，請參閱[[!UICONTROL Destinations]工作區](./destinations-workspace.md)的概述。