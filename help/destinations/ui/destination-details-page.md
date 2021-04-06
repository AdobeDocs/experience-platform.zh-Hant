---
keywords: 目標；目標；目標詳細資訊頁；目標詳細資訊頁
title: 檢視目標詳細資訊
description: '個別目標的詳細資料頁面提供目標詳細資料的概述。 目標詳細資訊包括目標名稱、ID、對應至目標的區段，以及用於編輯啟動以及啟用和停用資料流的控制項。 '
seo-description: 個別目標的詳細資料頁面提供目標詳細資料的概述。 目標詳細資訊包括目標名稱、ID、對應至目標的區段，以及用於編輯啟動以及啟用和停用資料流的控制項。
exl-id: e44e2b2d-f477-4516-8a47-3e95c2d85223
translation-type: tm+mt
source-git-commit: cc432f7c07f0f82deec653864154016638ec8138
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 0%

---

# 檢視目標詳細資訊

## 概述 {#overview}

在Adobe Experience Platform用戶介面中，您可以查看和監視目標的屬性和活動。 這些詳細資訊包括目標的名稱和ID、啟用或停用目標的控制項，以及更多功能。 批次目的地的詳細資訊還包括已啟動描述檔記錄的度量和資料流執行的歷史記錄。

>[!NOTE]
>
>目標詳細資訊頁面是[!DNL Platform] [!DNL UI]中[!UICONTROL Destinations]工作區的一部分。 如需詳細資訊，請參閱[[!UICONTROL Destinations]工作區概觀](./destinations-workspace.md)。

## 查看目標詳細資訊{#view-details}

請依照下列步驟，檢視有關現有目標的詳細資訊。

1. 登入[Experience PlatformUI](https://platform.adobe.com/)並從左導覽列選擇&#x200B;**[!UICONTROL Destinations]**。 從頂部標題中選擇&#x200B;**[!UICONTROL Browse]**&#x200B;以查看現有目標。

   ![瀏覽目標](../assets/ui/details-page/browse-destinations.png)

1. 選擇左上角的篩選器表徵圖![Filter-icon](../assets/ui/details-page/filter.png)以啟動排序面板。 排序面板提供您所有目的地的清單。 您可以從清單中選擇多個目標，以查看與所選目標相關聯的資料流的篩選選擇。

   ![篩選目標](../assets/ui/details-page/filter-destinations.png)

1. 選擇要查看的目標名稱。

   ![選擇目標](../assets/ui/details-page/destination-select.png)

1. 此時會顯示目標的詳細資料頁面，顯示其可用控制項。 如果您正在查看批處理目標的詳細資訊，則還會顯示一個監視控制面板。

   ![目標詳細資訊](../assets/ui/details-page/destination-details.png)

## 右邊欄

右側邊欄顯示有關所選目標的基本資訊。

![右滑軌](../assets/ui/details-page/right-sidebar.png)

下表涵蓋右側導軌提供的控制項和詳細資訊：

| 右邊欄項目 | 說明 |
| --- | --- |
| [!UICONTROL Activate] | 選取此控制項可編輯哪些區段已對應至目標。 如需詳細資訊，請參閱[啟用區段至目標](./activate-destinations.md)的指南。 |
| [!UICONTROL Delete] | 允許您刪除此資料流，並取消映射以前激活的段（如果有）。 |
| [!UICONTROL Destination name] | 可以編輯此欄位以更新目標的名稱。 |
| [!UICONTROL Description] | 您可以編輯此欄位，以更新或新增選擇性說明至目標。 |
| [!UICONTROL Destination] | 代表對象被傳送至的目標平台。 如需詳細資訊，請參閱[目標目錄](../catalog/overview.md)。 |
| [!UICONTROL Status] | 指示目標是啟用還是禁用。 |
| [!UICONTROL Marketing actions] | 指出針對資料治理用途適用於此目的地的行銷動作（使用案例）。 |
| [!UICONTROL Category] | 指示目標類型。 如需詳細資訊，請參閱[目標目錄](../catalog/overview.md)。 |
| [!UICONTROL Connection type] | 指出將觀眾傳送至目的地的表單。 可能的值包括[!UICONTROL Cookie]和[!UICONTROL Profile-based]。 |
| [!UICONTROL Frequency] | 指出觀眾被傳送至目的地的頻率。 可能的值包括[!UICONTROL Streaming]和[!UICONTROL Batch]。 |
| [!UICONTROL Identity] | 代表目標接受的識別名稱空間，例如`GAID`、`IDFA`或`email`。 有關接受的身份名稱空間的詳細資訊，請參閱[身份名稱空間概述](../../identity-service/namespaces.md)。 |
| [!UICONTROL Created by] | 表示建立此目標的用戶。 |
| [!UICONTROL Created] | 指示建立此目標時的UTC日期時間。 |

{style=&quot;table-layout:auto&quot;}

## [!UICONTROL Enabled]/[!UICONTROL Disabled] toggle

您可以使用&#x200B;**[!UICONTROL Enabled]/[!UICONTROL Disabled]**&#x200B;切換來啟動和暫停所有匯出至目的地的資料。

![啟用停用切換](../assets/ui/details-page/enable-disable.png)

## [!UICONTROL Dataflow runs]

[!UICONTROL Dataflow runs]頁籤提供資料流運行到批處理目標的度量資料。 有關詳細資訊，請參閱[監控資料流](monitor-dataflows.md)。

## [!UICONTROL Activation data] {#activation-data}

[!UICONTROL Activation data]標籤會顯示已映射至目標的區段清單，包括其開始日期和結束日期（如果適用）。 若要檢視特定區段的詳細資訊，請從清單中選取其名稱。

![啟動資料](../assets/ui/details-page/activation-data.png)

>[!NOTE]
>
>如需探索區段詳細資訊頁面的詳細資訊，請參閱[區段UI概觀](../../segmentation/ui/overview.md#segment-details)。
