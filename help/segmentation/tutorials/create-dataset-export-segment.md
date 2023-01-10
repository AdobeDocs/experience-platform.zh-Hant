---
keywords: Experience Platform；首頁；熱門主題；分段服務；分段；建立資料集；匯出受眾區段；匯出區段；
solution: Experience Platform
title: 建立資料集以匯出受眾區段
type: Tutorial
description: 本教學課程逐步說明建立資料集所需的步驟，這些資料集可用來使用Experience PlatformUI匯出對象區段。
exl-id: 1cd16e43-b050-42ba-a894-d7ea477b65f3
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '757'
ht-degree: 0%

---

# 建立資料集以匯出受眾區段

[!DNL Adobe Experience Platform] 可讓您根據特定屬性，將客戶設定檔細分為受眾。 建立區段後，您可以將該對象匯出至資料集，供其存取並採取行動。 為了匯出成功，必須正確設定資料集。

本教學課程逐步說明建立資料集（可用來匯出受眾區段）的必要步驟，使用 [!DNL Experience Platform] UI。

本教學課程直接與 [評估和存取區段結果](./evaluate-a-segment.md). 區段評估教學課程提供使用 [!DNL Catalog Service] API，但本教學課程概述使用 [!DNL Experience Platform] UI。

## 快速入門

若要匯出區段，資料集必須以 [!DNL XDM Individual Profile Union Schema]. 聯合架構是系統產生的唯讀架構，可匯總共用相同類別之所有架構的欄位。 如需聯合結構的詳細資訊，請參閱 [架構組成的基本知識](../../xdm/schema/composition.md#union).

若要在UI中檢視聯合結構，請選取 **[!UICONTROL 設定檔]** 在左側導覽中，然後選取 **[!UICONTROL 聯合架構]** 如下所示。

![聯合架構頁簽將突出顯示。](../images/tutorials/segment-export-dataset/union.png)

## 資料集工作區

此 [!UICONTROL 資料集] 工作區可讓您檢視及管理組織的所有資料集。

選擇 **[!UICONTROL 資料集]** 在左側導覽器中存取工作區，然後選取 **[!UICONTROL 瀏覽]**. 此索引標籤會顯示資料集及其詳細資訊清單。 視每欄的寬度而定，您可能需要向左或向右捲動才能查看所有欄。

>[!NOTE]
>
>選取搜尋列旁的篩選圖示，即可使用篩選功能僅檢視已啟用的資料集 [!DNL Real-Time Customer Profile].

![資料集工作區隨即顯示。](../images/tutorials/segment-export-dataset/browse.png)

## 建立資料集

若要建立資料集，請選取 **[!UICONTROL 建立資料集]**.

![「建立資料集」按鈕會反白顯示。](../images/tutorials/segment-export-dataset/create-dataset.png)

在下一個畫面中，選取 **[!UICONTROL 從結構建立資料集]**.

![「從結構建立資料集」選項會反白顯示。](../images/tutorials/segment-export-dataset/create-from-schema.png)

## 選取XDM個別設定檔聯合結構

若要選取 [!DNL XDM Individual Profile Union Schema] 在資料集中使用，請尋找「[!UICONTROL XDM個別設定檔]&quot;架構 **[!UICONTROL 選擇架構]** 螢幕。 選取結構後，您可以確認是否為 **[!UICONTROL API使用狀況]** 在右側邊欄。 若 [!UICONTROL 結構] 路徑結尾為 `_union`，這是聯合模式。

>[!NOTE]
>
>雖然聯合結構依定義參與即時客戶設定檔，但由於未以與傳統結構相同的方式啟用設定檔，因此這些設定檔會列為「未啟用」。

選取旁邊的選項按鈕 **[!UICONTROL XDM個別設定檔]**，然後選取 **[!UICONTROL 下一個]**.

![系統會強調顯示XDM個別設定檔結構。](../images/tutorials/segment-export-dataset/select-schema.png)

## 設定資料集

在下一個畫面中，您必須為資料集命名。 您也可以新增選用的說明。

**資料集名稱附註：**

* 資料集名稱應簡短且具描述性，以便稍後在資料庫中輕鬆找到資料集。
* 資料集名稱必須是唯一的，亦即這些名稱的特定性也應足夠，以免日後重複使用。
* 最佳實務是使用說明欄位提供資料集的其他相關資訊，這可能有助於其他使用者日後區分資料集。

資料集有名稱和說明後，請選取 **[!UICONTROL 完成]**.

![此時會顯示「設定資料集」頁面。 會反白顯示設定選項。](../images/tutorials/segment-export-dataset/configure-dataset.png)

## 資料集活動

建立資料集後，系統會為您帶來該資料集的活動頁面。 您應該會在工作區的左上角看到資料集名稱，並看到「尚未新增任何批次」通知。 這是預期的情況，因為您尚未將任何批次新增至此資料集。

右側邊欄包含與新資料集相關的資訊，例如資料集ID、名稱、說明、結構等。 請注意 **[!UICONTROL 資料集ID]**，因為此值是完成對象區段匯出工作流程的必要值。

![會顯示資料集活動頁面。 資料集ID會反白顯示，因為此值需注意以後的步驟。](../images/tutorials/segment-export-dataset/activity.png)

## 後續步驟

現在，您已根據 [!DNL XDM Individual Profile Union Schema]，您可以使用資料集ID繼續 [評估和存取區段結果](./evaluate-a-segment.md) 教學課程。

此時，請返回評估區段結果教學課程，並從 [為對象成員產生設定檔](./evaluate-a-segment.md#generate-profiles) 匯出區段工作流程的步驟。
