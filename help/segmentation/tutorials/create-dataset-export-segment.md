---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 建立資料集以匯出觀眾區隔
topic: tutorial
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '766'
ht-degree: 0%

---


# 建立資料集以匯出觀眾區隔

Adobe Experience Platform可讓您根據特定屬性，輕鬆將客戶個人檔案細分為受眾。 建立區段後，您可以將該對象匯出至資料集，以便存取並執行操作。 要成功導出，必須正確配置資料集。

本教學課程將逐步說明建立資料集所需的步驟，以便使用Experience Platform UI匯出觀眾區隔。

本教學課程直接與教學課程中概述的評估和存 [取區段結果的步驟相關](./evaluate-a-segment.md)。 評估區段教學課程提供使用目錄API建立資料集的步驟，而本教學課程則說明使用Experience Platform UI建立資料集的步驟。

## 快速入門

若要匯出區段，資料集必須以XDM個別描述檔結合架構為基礎。 聯合模式是系統生成的只讀模式，它聚合了共用相同類的所有模式的欄位（在本例中為XDM Individual Profile類）。 有關聯合視圖方案的詳細資訊，請參閱 [方案註冊開發人員指南的「即時客戶概要檔案」部分](../../xdm/schema/composition.md#union)。

要在UI中查看聯合架構，請按一下左側導 **航中的** Profiles，然後按一下 ** Union架構頁籤，如下所示。

![Experience Platform UI中的「結合架構」索引標籤](../images/tutorials/segment-export-dataset/union-schema-ui.png)


## 資料集工作區

Experience Platform UI中的資料集工作區可讓您檢視和管理IMS組織建立的所有資料集，並建立新的資料集。

若要檢視資料集工作區，請按一 **下左側導覽中的「資料集** 」，然後按一下「 *瀏覽* 」標籤。 資料集工作區包含資料集清單，包括 *Name*、Created *（日期和時間）、* Source *（日期和時間）、* Source Schema、 ****** Batch Last Status、Woll as the date ad time the dataset was Last Updated Jocraded 視每欄的寬度而定，您可能需要向左或向右捲動，才能查看所有欄。

>[!NOTE]
>
>按一下搜尋列旁的篩選圖示，使用篩選功能，只檢視為「即時客戶描述檔」啟用的資料集。

![查看所有資料集](../images/tutorials/segment-export-dataset/datasets-workspace.png)

## 建立資料集

若要建立資料集，請按一 **下「資料集** 」工作區右上角的「建立資料集」。

![按一下「建立資料集」](../images/tutorials/segment-export-dataset/dataset-click-create.png)

在「建 *立資料集* 」畫面上，按一 **下「從架構建立資料集** 」以繼續。

![選擇資料來源](../images/tutorials/segment-export-dataset/create-dataset.png)

## 選擇XDM單個配置式聯合模式

要選擇要在資料集中使用的XDM單個配置檔案聯合模式，請在「選擇模式」螢幕上查找具有類型為「聯合」的「XDM單個配置檔案」 *模式* 。

已選取「 **XDM Individual Profile**」( **XDM個人設定檔)旁的選項按鈕** ，然後按一下右上角的「Next」（下一步）。

![選擇方案](../images/tutorials/segment-export-dataset/select-schema.png)

## 設定資料集

在「設 **定資料集** 」畫面上，您必須為資料集指定名稱 *，並且可能也會提供資料集* 的說明 ** 。

**資料集名稱的附註：**
- 資料集名稱應簡短且具說明性，以便稍後在資料庫中輕鬆找到資料集。
- 資料集名稱必須是唯一的，這表示資料集名稱也應足夠具體，以免日後重複使用。
- 最好使用說明欄位來提供資料集的其他相關資訊，因為這可協助其他使用者在未來區隔資料集。

資料集有名稱和說明後，按一下「完 **成**」。

![設定資料集](../images/tutorials/segment-export-dataset/configure-dataset.png)

## 資料集活動

現在已建立空的資料集，您已返回「資料集」工作區 *的「資料集活動* 」標籤。 您應該會在工作區的左上角看到資料集名稱，以及「未新增任何批次」通知。 由於您尚未將任何批次新增至此資料集，因此預期會出現此情況。

在Datasets的右側，您會看到與新資料集相關的 **Info***Tab，例如* Info *ID、AdSignDesignDesignDesignDesignDesignDatases,*********** DDDSigSiDSinasig。 「資訊」標籤也包含資料集何時建立及其「上 *次修改* 」日 *期的相關資訊* 。

請記下資料集 **ID**，因為此值是完成觀眾區段匯出工作流程的必要值。

![資料集活動](../images/tutorials/segment-export-dataset/dataset-activity.png)

## 後續步驟

現在您已根據XDM個別描述檔結合架構建立資料集，您可以使用資料集 **ID** ，繼續 [評估和存取區段結果教學課程](./evaluate-a-segment.md) 。

目前，請返回評估區段結果教學課程，並從匯出區段工作流程的「產生 [XDM個人設定檔](./evaluate-a-segment.md#generate-profiles-for-audience-members) 」步驟 [中選取](./evaluate-a-segment.md#export-a-segment) 。
