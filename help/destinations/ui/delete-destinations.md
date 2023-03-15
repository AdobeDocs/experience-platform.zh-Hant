---
keywords: 刪除目的地，如何刪除目的地，刪除目的地
title: 刪除目的地
type: Tutorial
description: 本教學課程列出刪除Adobe Experience Platform UI中現有目的地的步驟
exl-id: 7b672859-e61a-4b3c-9db9-62048258f0aa
source-git-commit: 1ef6430b6661a2b8b5aef196b75cfaf3f6220aab
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---

# 刪除目的地 {#delete-destinations}

## 總覽 {#overview}

在Adobe Experience Platform使用者介面中，您可以刪除與目的地的現有連線。

刪除目標會刪除該目標的任何現有資料流。 在刪除資料流之前，激活到您刪除的目標的所有段都未映射。

有兩種方式可從 [!DNL Platform] [!DNL UI]. 您可以：

* [從中刪除目的地 [!UICONTROL 瀏覽] 標籤](#delete-browse-tab)
* [從目的地詳細資訊頁面刪除目的地](#delete-destination-details-page)

## 從「瀏覽」索引標籤刪除目標{#delete-browse-tab}

請依照下列步驟，從 [!UICONTROL 瀏覽] 標籤。

1. 登入 [Experience PlatformUI](https://platform.adobe.com/) 選取 **[!UICONTROL 目的地]** 的下一頁。 若要檢視您現有的目的地，請選取 **[!UICONTROL 瀏覽]** 從頂端標題。

   ![瀏覽目的地](../assets/ui/delete-destinations/browse-destinations.png)

2. 選取篩選圖示 ![篩選器圖示](../assets/ui/delete-destinations/filter.png) ，啟動排序面板。 排序面板會提供所有目的地的清單。 您可以從清單中選擇多個目標，以查看與所選目標關聯的資料流的篩選選擇。

   ![篩選目的地](../assets/ui/delete-destinations/filter-destinations.png)

3. 選取 ![更多按鈕](../assets/ui/delete-destinations/more-icon.png) 按鈕，然後選取 ![刪除按鈕](../assets/ui/delete-destinations/delete-icon.png) **[!UICONTROL 刪除]** 刪除現有目標連接。
   ![刪除目的地](../assets/ui/delete-destinations/delete-destinations.png)

4. 選擇 **[!UICONTROL 刪除]** 確認刪除目標連接。

   ![確認刪除目標](../assets/ui/delete-destinations/delete-destinations-confirm.png)

## 從目的地詳細資訊頁面刪除目的地{#delete-destination-details-page}

請依照下列步驟，從目的地詳細資訊頁面刪除目的地。

1. 登入 [Experience PlatformUI](https://platform.adobe.com/) 選取 **[!UICONTROL 目的地]** 的下一頁。 若要檢視您現有的目的地，請選取 **[!UICONTROL 瀏覽]** 從頂端標題。

   ![瀏覽目的地](../assets/ui/delete-destinations/browse-destinations.png)

2. 選取篩選圖示 ![篩選器圖示](../assets/ui/delete-destinations/filter.png) ，啟動排序面板。 排序面板會提供所有目的地的清單。 您可以從清單中選擇多個目標，以查看與所選目標關聯的資料流的篩選選擇。

   ![篩選目的地](../assets/ui/delete-destinations/filter-destinations.png)

3. 選取您要刪除的目的地名稱。

   ![選擇目標](../assets/ui/delete-destinations/delete-destination-select.png)

   * 如果目標中有現有資料流，則會將您帶到 [!UICONTROL 資料流運行] 標籤。

      ![資料流運行頁簽](../assets/ui/delete-destinations/destination-details-dataflows.png)

   * 如果目的地沒有現有資料流，則會將您帶至空白頁面，讓您開始啟用對象。

      ![目的地詳細資訊](../assets/ui/delete-destinations/destination-details-empty.png)

4. 選擇 **[!UICONTROL 刪除]** 在右側邊欄。

   ![刪除目標](../assets/ui/delete-destinations/delete-destinations-button.png)

5. 選擇 **[!UICONTROL 刪除]** 在確認對話方塊中，移除目的地。

   ![刪除目標確認](..//assets/ui/delete-destinations/delete-destinations-delete.png)

   >[!NOTE]
   >
   >視伺服器負載而定，可能需要幾分鐘的時間才能 [!DNL Platform] 刪除目標。
