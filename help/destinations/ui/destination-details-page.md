---
keywords: 目的地；目的地；目的地詳細資料頁面；目的地詳細資料頁面
title: 查看目標詳細資訊
description: '個別目的地的詳細資訊頁面提供目的地詳細資訊的概觀。 目的地詳細資訊包括目的地名稱、ID、對應至目的地的區段，以及編輯啟用和啟用資料流的控制項。 '
seo-description: 個別目的地的詳細資訊頁面提供目的地詳細資訊的概觀。 目的地詳細資訊包括目的地名稱、ID、對應至目的地的區段，以及編輯啟用和啟用資料流的控制項。
exl-id: e44e2b2d-f477-4516-8a47-3e95c2d85223
source-git-commit: a619227de30513bb06a22ce7b4f2fc13847c1ab6
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 2%

---

# 查看目標詳細資訊

## 概覽 {#overview}

在Adobe Experience Platform使用者介面中，您可以檢視及監控目的地的屬性和活動。 這些詳細資訊包括目的地的名稱和ID、啟用或停用目的地的控制項等。 批次目的地的詳細資訊還包括已啟用設定檔記錄的量度，以及資料流執行的歷史記錄。

>[!NOTE]
>
>目的地詳細資訊頁面是[!DNL Platform] [!DNL UI]中[!UICONTROL 目的地]工作區的一部分。 如需詳細資訊，請參閱[[!UICONTROL Destinations]工作區概述](./destinations-workspace.md) 。

## 查看目標詳細資訊 {#view-details}

請依照下列步驟，檢視關於現有目的地的詳細資訊。

1. 登入[Experience PlatformUI](https://platform.adobe.com/)並從左側導覽列選取&#x200B;**[!UICONTROL 目的地]**。 從頂端標題選取&#x200B;**[!UICONTROL Browse]**&#x200B;以檢視您現有的目的地。

   ![瀏覽目的地](../assets/ui/details-page/browse-destinations.png)

1. 選擇左上角的篩選表徵圖![Filter-icon](../assets/ui/details-page/filter.png)以啟動排序面板。 排序面板會提供所有目的地的清單。 您可以從清單中選擇多個目標，以查看與所選目標關聯的資料流的篩選選擇。

   ![篩選目的地](../assets/ui/details-page/filter-destinations.png)

1. 選取您要檢視的目的地名稱。

   ![選擇目標](../assets/ui/details-page/destination-select.png)

1. 目的地的詳細資訊頁面隨即顯示，並顯示其可用的控制項。 如果您正在查看批處理目標的詳細資訊，則還會顯示監視控制面板。

   ![目的地詳細資訊](../assets/ui/details-page/destination-details.png)

## 右側邊欄

右側邊欄會顯示所選目的地的基本資訊。

![右側邊欄](../assets/ui/details-page/right-sidebar.png)

下表涵蓋右側邊欄提供的控制項和詳細資訊：

| 右側邊欄項目 | 說明 |
| --- | --- |
| [!UICONTROL 啟動] | 選取此控制項可編輯對應至目的地的區段。 如需詳細資訊，請參閱[啟用對象資料以劃分串流目的地](./activate-segment-streaming-destinations.md)、[啟用對象資料以批次設定檔目的地](./activate-batch-profile-destinations.md)和[啟用對象資料以串流設定檔目的地](./activate-streaming-profile-destinations.md)的相關指南。 |
| [!UICONTROL 刪除] | 允許您刪除此資料流，並取消映射先前激活的段（如果有的話）。 |
| [!UICONTROL 目的地名稱] | 可以編輯此欄位以更新目標的名稱。 |
| [!UICONTROL 說明] | 您可以編輯此欄位，以更新或新增選擇性說明至目的地。 |
| [!UICONTROL 目標] | 代表對象被傳送至的目的地平台。 如需詳細資訊，請參閱[目的地目錄](../catalog/overview.md) 。 |
| [!UICONTROL 狀態] | 指示目標是啟用還是禁用。 |
| [!UICONTROL 行銷動作] | 指出針對此目的地為資料控管目的而套用的行銷動作（使用案例）。 |
| [!UICONTROL 類別] | 指示目標類型。 如需詳細資訊，請參閱[目的地目錄](../catalog/overview.md) 。 |
| [!UICONTROL 連線類型] | 指出將對象傳送至目的地的表單。 可能的值包括[!UICONTROL Cookie]和[!UICONTROL Profile-based]。 |
| [!UICONTROL 頻率] | 指出對象傳送至目的地的頻率。 可能的值包括[!UICONTROL 流]和[!UICONTROL 批]。 |
| [!UICONTROL 身分] | 代表目的地接受的身分命名空間，例如`GAID`、`IDFA`或`email`。 如需接受的身分識別命名空間的詳細資訊，請參閱[身分識別命名空間概述](../../identity-service/namespaces.md)。 |
| [!UICONTROL 建立者] | 指示建立此目標的用戶。 |
| [!UICONTROL 已建立] | 指示建立此目標時的UTC日期時間。 |

{style=&quot;table-layout:auto&quot;}

## [!UICONTROL 啟用]/ 停用切換

您可以使用&#x200B;**[!UICONTROL Enabled]/[!UICONTROL Disabled]**&#x200B;切換開始和暫停所有匯出至目的地的資料。

![啟用禁用切換](../assets/ui/details-page/enable-disable.png)

## [!UICONTROL 資料流運行]

[!UICONTROL 資料流運行]頁簽提供資料流運行到批處理目標的度量資料。 有關詳細資訊，請參閱[監視資料流](monitor-dataflows.md)。

## [!UICONTROL 啟動資料] {#activation-data}

[!UICONTROL 啟動資料]標籤會顯示已對應至目的地的區段清單，包括其開始日期和結束日期（若適用）。 若要檢視特定區段的詳細資訊，請從清單中選取其名稱。

![啟動資料](../assets/ui/details-page/activation-data.png)

>[!NOTE]
>
>如需探索區段詳細資訊頁面的詳細資訊，請參閱[分段UI概述](../../segmentation/ui/overview.md#segment-details)。
