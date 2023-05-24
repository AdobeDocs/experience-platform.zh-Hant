---
keywords: 刪除目標，如何刪除目標，刪除目標
title: 刪除目標
type: Tutorial
description: 本教程列出了刪除Adobe Experience PlatformUI中現有目標的步驟
exl-id: 7b672859-e61a-4b3c-9db9-62048258f0aa
source-git-commit: 1ef6430b6661a2b8b5aef196b75cfaf3f6220aab
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---

# 刪除目標 {#delete-destinations}

## 總覽 {#overview}

在Adobe Experience Platform用戶介面中，可以刪除到目標的現有連接。

刪除目標會將任何現有資料流刪除到該目標。 在刪除資料流之前，所有激活到您刪除的目標的段都將取消映射。

有兩種方法可從 [!DNL Platform] [!DNL UI]。 您可以：

* [從 [!UICONTROL 瀏覽] 頁籤](#delete-browse-tab)
* [從目標詳細資訊頁刪除目標](#delete-destination-details-page)

## 從「瀏覽」頁籤中刪除目標{#delete-browse-tab}

按照以下步驟從 [!UICONTROL 瀏覽] 頁籤。

1. 登錄到 [Experience PlatformUI](https://platform.adobe.com/) 選擇 **[!UICONTROL 目標]** 的下界。 要查看現有目標，請選擇 **[!UICONTROL 瀏覽]** 的下界。

   ![瀏覽目標](../assets/ui/delete-destinations/browse-destinations.png)

2. 選擇篩選器表徵圖 ![篩選器表徵圖](../assets/ui/delete-destinations/filter.png) 的子菜單。 排序面板提供所有目標的清單。 可以從清單中選擇多個目標，以查看與所選目標關聯的資料流的篩選選擇。

   ![篩選目標](../assets/ui/delete-destinations/filter-destinations.png)

3. 選擇 ![「更多」按鈕](../assets/ui/delete-destinations/more-icon.png) 按鈕，然後選擇 ![刪除按鈕](../assets/ui/delete-destinations/delete-icon.png) **[!UICONTROL 刪除]** 刪除現有目標連接。
   ![刪除目標](../assets/ui/delete-destinations/delete-destinations.png)

4. 選擇 **[!UICONTROL 刪除]** 確認刪除目標連接。

   ![確認刪除目標](../assets/ui/delete-destinations/delete-destinations-confirm.png)

## 從目標詳細資訊頁刪除目標{#delete-destination-details-page}

按照以下步驟從目標詳細資訊頁面中刪除目標。

1. 登錄到 [Experience PlatformUI](https://platform.adobe.com/) 選擇 **[!UICONTROL 目標]** 的下界。 要查看現有目標，請選擇 **[!UICONTROL 瀏覽]** 的下界。

   ![瀏覽目標](../assets/ui/delete-destinations/browse-destinations.png)

2. 選擇篩選器表徵圖 ![篩選器表徵圖](../assets/ui/delete-destinations/filter.png) 的子菜單。 排序面板提供所有目標的清單。 可以從清單中選擇多個目標，以查看與所選目標關聯的資料流的篩選選擇。

   ![篩選目標](../assets/ui/delete-destinations/filter-destinations.png)

3. 選擇要刪除的目標的名稱。

   ![選擇目標](../assets/ui/delete-destinations/delete-destination-select.png)

   * 如果目標具有現有資料流，則將轉到 [!UICONTROL 資料流運行] 頁籤。

      ![「資料流運行」頁籤](../assets/ui/delete-destinations/destination-details-dataflows.png)

   * 如果目標沒有現有資料流，則您將進入一個空頁，在該頁中可以開始激活受眾。

      ![目標詳細資訊](../assets/ui/delete-destinations/destination-details-empty.png)

4. 選擇 **[!UICONTROL 刪除]** 右欄。

   ![刪除目標](../assets/ui/delete-destinations/delete-destinations-button.png)

5. 選擇 **[!UICONTROL 刪除]** 的子菜單。

   ![刪除目標確認](..//assets/ui/delete-destinations/delete-destinations-delete.png)

   >[!NOTE]
   >
   >根據伺服器負載，可能需要幾分鐘 [!DNL Platform] 刪除目標。
