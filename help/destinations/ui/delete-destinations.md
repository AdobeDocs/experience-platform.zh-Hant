---
keywords: 刪除目的地，如何刪除目的地，刪除目的地
title: 刪除目的地
type: Tutorial
description: 本教學課程列出刪除Adobe Experience Platform UI中現有目的地的步驟
exl-id: 7b672859-e61a-4b3c-9db9-62048258f0aa
source-git-commit: a97b235e2d8834f6be002923be9cdbca5f08495b
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---

# 刪除目的地 {#delete-destinations}

## 概覽 {#overview}

在Adobe Experience Platform使用者介面中，您可以刪除與目的地的現有連線。

刪除目標會刪除該目標的任何現有資料流。 在刪除資料流之前，激活到您刪除的目標的所有段都未映射。

有兩種方式可從[!DNL Platform] [!DNL UI]中刪除目標。 您可以：

* [從[!UICONTROL Browse]標籤中刪除目標](#delete-browse-tab)
* [從目的地詳細資訊頁面刪除目的地](#delete-destination-details-page)

>[!IMPORTANT]
>
>雖然如本文所述，您可以刪除目的地的現有&#x200B;*連線*，但Platform目前不允許您刪除現有的&#x200B;*[目的地帳戶](/help/destinations/ui/destinations-workspace.md#accounts)*。

## 從「瀏覽」索引標籤刪除目標{#delete-browse-tab}

請依照下列步驟從[!UICONTROL Browse]標籤中刪除目標。

1. 登入[Experience PlatformUI](https://platform.adobe.com/)並從左側導覽列選取&#x200B;**[!UICONTROL 目的地]**。 若要檢視您現有的目的地，請從頂端標題選取&#x200B;**[!UICONTROL Browse]**。

   ![瀏覽目的地](../assets/ui/delete-destinations/browse-destinations.png)

2. 選擇左上角的篩選表徵圖![Filter-icon](../assets/ui/delete-destinations/filter.png)以啟動排序面板。 排序面板會提供所有目的地的清單。 您可以從清單中選擇多個目標，以查看與所選目標關聯的資料流的篩選選擇。

   ![篩選目的地](../assets/ui/delete-destinations/filter-destinations.png)

3. 在「名稱」列中選擇![More按鈕](../assets/ui/delete-destinations/more-icon.png)按鈕，然後選擇![Delete按鈕](../assets/ui/delete-destinations/delete-icon.png) **[!UICONTROL Delete]**以刪除現有目標連接。
   ![刪除目的地](../assets/ui/delete-destinations/delete-destinations.png)

4. 選擇&#x200B;**[!UICONTROL Delete]**&#x200B;以確認目標連接的刪除。

   ![確認刪除目標](../assets/ui/delete-destinations/delete-destinations-confirm.png)


## 從目的地詳細資訊頁面刪除目的地{#delete-destination-details-page}

請依照下列步驟，從目的地詳細資訊頁面刪除目的地。

1. 登入[Experience PlatformUI](https://platform.adobe.com/)並從左側導覽列選取&#x200B;**[!UICONTROL 目的地]**。 若要檢視您現有的目的地，請從頂端標題選取&#x200B;**[!UICONTROL Browse]**。

   ![瀏覽目的地](../assets/ui/delete-destinations/browse-destinations.png)

2. 選擇左上角的篩選表徵圖![Filter-icon](../assets/ui/delete-destinations/filter.png)以啟動排序面板。 排序面板會提供所有目的地的清單。 您可以從清單中選擇多個目標，以查看與所選目標關聯的資料流的篩選選擇。

   ![篩選目的地](../assets/ui/delete-destinations/filter-destinations.png)

3. 選取您要刪除的目的地名稱。

   ![選擇目標](../assets/ui/delete-destinations/delete-destination-select.png)

   * 如果目標中有現有資料流，則會將您帶到[!UICONTROL 資料流運行]頁簽。

      ![資料流運行頁簽](../assets/ui/delete-destinations/destination-details-dataflows.png)

   * 如果目的地沒有現有資料流，則會將您帶至空白頁面，讓您開始啟用對象。

      ![目的地詳細資訊](../assets/ui/delete-destinations/destination-details-empty.png)


4. 在右側邊欄中選取&#x200B;**[!UICONTROL Delete]**。

   ![刪除目標](../assets/ui/delete-destinations/delete-destinations-button.png)

5. 在確認對話方塊中選取&#x200B;**[!UICONTROL Delete]**&#x200B;以移除目的地。

   ![刪除目標確認](..//assets/ui/delete-destinations/delete-destinations-delete.png)

   >[!NOTE]
   >
   >根據伺服器負載，[!DNL Platform]刪除目標可能需要幾分鐘的時間。
