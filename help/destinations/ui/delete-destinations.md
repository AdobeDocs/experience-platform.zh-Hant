---
keywords: 刪除目標；如何刪除目標
title: 刪除目標
type: 教學課程
description: 本教學課程列出刪除Adobe Experience PlatformUI中現有目標的步驟
exl-id: 7b672859-e61a-4b3c-9db9-62048258f0aa
translation-type: tm+mt
source-git-commit: e436d7147c613dad5b2ff596a412759fd60d228c
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 1%

---

# 刪除目標{#delete-destinations}

## 概述 {#overview}

在Adobe Experience Platform用戶介面中，您可以刪除與目標的現有連接。

刪除目標將刪除該目標的任何現有資料流。 在刪除資料流之前，所有激活到您刪除的目標的段都將被取消映射。

有兩種方法可以從[!DNL Platform] [!DNL UI]中刪除目標。 您可以：

* [從頁籤中刪除目 [!UICONTROL Browse] 標](#delete-browse-tab)
* [從目標詳細資訊頁刪除目標](#delete-destination-details-page)

## 從「瀏覽」頁籤{#delete-browse-tab}刪除目標

請遵循下列步驟，從[!UICONTROL Browse]標籤中刪除目標。

1. 登入[Experience PlatformUI](https://platform.adobe.com/)並從左導覽列選擇&#x200B;**[!UICONTROL Destinations]**。 要查看現有目標，請從頂部標題中選擇&#x200B;**[!UICONTROL Browse]**。

   ![瀏覽目標](../assets/ui/delete-destinations/browse-destinations.png)

2. 選擇左上角的篩選器表徵圖![Filter-icon](../assets/ui/delete-destinations/filter.png)以啟動排序面板。 排序面板提供您所有目的地的清單。 您可以從清單中選擇多個目標，以查看與所選目標相關聯的資料流的篩選選擇。

   ![篩選目標](../assets/ui/delete-destinations/filter-destinations.png)

3. 在&#x200B;**[!UICONTROL Platform]**&#x200B;欄中選擇![刪除按鈕](../assets/ui/delete-destinations/delete-icon.png) **[!UICONTROL Delete]**按鈕以刪除現有目標。
   ![刪除目標](../assets/ui/delete-destinations/delete-destinations.png)

4. 選擇&#x200B;**[!UICONTROL Delete]**&#x200B;以確認目標的刪除。

   ![確認刪除目標](../assets/ui/delete-destinations/delete-destinations-confirm.png)


## 從目標詳細資訊頁面刪除目標{#delete-destination-details-page}

請遵循下列步驟，從目標詳細資料頁面刪除目標。

1. 登入[Experience PlatformUI](https://platform.adobe.com/)並從左導覽列選擇&#x200B;**[!UICONTROL Destinations]**。 要查看現有目標，請從頂部標題中選擇&#x200B;**[!UICONTROL Browse]**。

   ![瀏覽目標](../assets/ui/delete-destinations/browse-destinations.png)

2. 選擇左上角的篩選器表徵圖![Filter-icon](../assets/ui/delete-destinations/filter.png)以啟動排序面板。 排序面板提供您所有目的地的清單。 您可以從清單中選擇多個目標，以查看與所選目標相關聯的資料流的篩選選擇。

   ![篩選目標](../assets/ui/delete-destinations/filter-destinations.png)

3. 選擇要刪除的目標名稱。

   ![選擇目標](../assets/ui/delete-destinations/delete-destination-select.png)

   * 如果目標有現有資料流，則將轉至[!UICONTROL Dataflow runs]頁籤。

      ![「資料流運行」頁籤](../assets/ui/delete-destinations/destination-details-dataflows.png)

   * 如果目標沒有現有的資料流，則會將您帶到一個空頁面，您可以在其中開始激活對象。

      ![目標詳細資訊](../assets/ui/delete-destinations/destination-details-empty.png)


4. 在右邊欄中選擇&#x200B;**[!UICONTROL Delete]**。

   ![刪除目標](../assets/ui/delete-destinations/delete-destinations-button.png)

5. 在確認對話框中選擇&#x200B;**[!UICONTROL Delete]**&#x200B;以刪除目標。

   ![刪除目標確認](..//assets/ui/delete-destinations/delete-destinations-delete.png)

   >[!NOTE]
   >
   >視伺服器負載而定，[!DNL Platform]刪除目標可能需要幾分鐘的時間。
