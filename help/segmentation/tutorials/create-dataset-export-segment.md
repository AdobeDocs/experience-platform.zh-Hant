---
solution: Experience Platform
title: 建立資料集以匯出對象
type: Tutorial
description: 瞭解如何使用Experience PlatformUI建立可用於匯出閱聽眾的資料集。
exl-id: 1cd16e43-b050-42ba-a894-d7ea477b65f3
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 1%

---

# 建立資料集以匯出對象

[!DNL Adobe Experience Platform]可讓您根據特定屬性，將客戶設定檔細分為受眾。 建立區段定義後，您可以將產生的受眾匯出至資料集，以供存取及據以採取行動。 為了成功匯出，資料集必須正確設定。

本教學課程將逐步解說建立資料集所需的步驟，該資料集可用來使用[!DNL Experience Platform] UI匯出對象。

此教學課程與[評估與存取區段結果](./evaluate-a-segment.md)的教學課程中概述的步驟直接相關。 區段定義評估教學課程提供使用[!DNL Catalog Service] API建立資料集的步驟，而本教學課程則概述使用[!DNL Experience Platform] UI建立資料集的步驟。

## 快速入門

為了匯出對象，資料集必須以[!DNL XDM Individual Profile Union Schema]為基礎。 聯合結構描述是系統產生的唯讀結構描述，可彙總共用相同類別的所有結構描述的欄位。 如需聯合結構描述的詳細資訊，請參閱[結構描述組合基本概念](../../xdm/schema/composition.md#union)的指南。

若要在UI中檢視聯合結構描述，請在左側導覽中選取&#x200B;**[!UICONTROL 設定檔]**，然後選取&#x200B;**[!UICONTROL 聯合結構描述]**，如下所示。

![聯合結構描述索引標籤已反白顯示。](../images/tutorials/segment-export-dataset/union.png)

## 資料集工作區

[!UICONTROL 資料集]工作區可讓您檢視及管理組織的所有資料集。

在左側導覽中選取&#x200B;**[!UICONTROL 資料集]**&#x200B;以存取工作區，然後選取&#x200B;**[!UICONTROL 瀏覽]**。 此索引標籤會顯示資料集及其詳細資訊的清單。 根據每欄的寬度，您可能需要向左或向右捲動才能檢視所有欄。

>[!NOTE]
>
>選取搜尋列旁的篩選圖示，即可使用篩選功能，僅檢視為[!DNL Real-Time Customer Profile]啟用的資料集。

![資料集工作區已顯示。](../images/tutorials/segment-export-dataset/browse.png)

## 建立資料集

若要建立資料集，請選取&#x200B;**[!UICONTROL 建立資料集]**。

![已醒目提示[建立資料集]按鈕。](../images/tutorials/segment-export-dataset/create-dataset.png)

在下一個畫面中，選取&#x200B;**[!UICONTROL 從結構描述建立資料集]**。

![從結構描述建立資料集選項已反白顯示。](../images/tutorials/segment-export-dataset/create-from-schema.png)

## 選取XDM個別設定檔聯合結構描述

若要選取要在您的資料集中使用的[!DNL XDM Individual Profile Union Schema]，請在&#x200B;**[!UICONTROL 選取結構描述]**&#x200B;畫面上尋找&quot;[!UICONTROL XDM個別設定檔]&quot;結構描述。 選取結構描述後，您可以在右側邊欄中確認它是否為&#x200B;**[!UICONTROL API使用情形]**&#x200B;下的聯合結構描述。 如果[!UICONTROL 結構描述]路徑結尾是`_union`，則為聯合結構描述。

>[!NOTE]
>
>雖然聯合結構依定義會參與即時客戶個人檔案，但由於未以與傳統結構相同的方式為個人檔案啟用，因此它們被列為「未啟用」。

選取&#x200B;**[!UICONTROL XDM個別設定檔]**&#x200B;旁的選項按鈕，然後選取&#x200B;**[!UICONTROL 下一步]**。

![已反白顯示XDM個別設定檔結構描述。](../images/tutorials/segment-export-dataset/select-schema.png)

## 設定資料集

在下一個畫面中，您必須為資料集命名。 您也可以新增說明（選擇性）。

**資料集名稱的附註：**

* 資料集名稱應簡短且具有描述性，以便日後在程式庫中輕鬆找到資料集。
* 資料集名稱必須是唯一的，這表示它們也應該是足夠具體的，以便將來不會重複使用。
* 您應使用說明欄位提供有關資料集的其他資訊，因為這樣可協助其他使用者日後區分資料集。

資料集有了名稱和描述後，請選取&#x200B;**[!UICONTROL 完成]**。

![顯示[設定資料集]頁面。 組態選項會反白顯示。](../images/tutorials/segment-export-dataset/configure-dataset.png)

## 資料集活動

建立資料集後，系統就會顯示該資料集的活動頁面。 您應該會在工作區的左上角看到資料集的名稱，並附上「未新增任何批次」的通知。 這是正常情況，因為您尚未新增任何批次至此資料集。

右邊欄包含與新資料集相關的資訊，例如資料集ID、名稱、說明、結構描述等。 請記下&#x200B;**[!UICONTROL 資料集識別碼]**，因為此值是完成對象匯出工作流程所必需的。

![會顯示資料集活動頁面。 資料集ID會反白顯示，因為未來步驟需要記下此值。](../images/tutorials/segment-export-dataset/activity.png)

## 後續步驟

現在您已根據[!DNL XDM Individual Profile Union Schema]建立資料集，您可以使用資料集ID來繼續[評估及存取區段定義結果](./evaluate-a-segment.md)教學課程。

此時，請返回評估區段定義結果教學課程，並從匯出對象工作流程的[產生對象成員的設定檔](./evaluate-a-segment.md#generate-profiles)步驟中選取。
