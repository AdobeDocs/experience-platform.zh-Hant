---
keywords: Experience Platform;insights; customer ai;popular topics
solution: Experience Platform
title: 建立具有預測分數的客戶細分
topic: Create a segment
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---


# 建立具有預測分數的客戶細分

當預測執行完成時，「設定檔」會自動使用預測傾向分數。 利用客戶人工智慧豐富個人檔案分數可建立客戶細分，以根據其傾向分數尋找受眾。 本節提供使用區段產生器建立區段的步驟。 如需建立區段的更強穩教學課程，請參閱「區段產 [生器」使用指南](../../../segmentation/tutorials/create-a-segment.md)。

>[!IMPORTANT]
>
>為了運用此方法，資料集需要啟用即時客戶設定檔。

在「平台UI」中，按一下左 **[!UICONTROL 側導覽中的]** 「區段」，然後按一下「 **[!UICONTROL 建立區段」]**。

![](../images/user-guide/segments.png)

此時會 *顯示「區段產生* 器」。 在左側的 *欄位* ，在「屬性」標籤下，按一下名為「 *XDM Individual Profile***** 」的檔案夾，然後按一下具有您組織名稱空間的檔案夾。 名為 **[!UICONTROL Customer AI]** 的資料夾包含預測執行的結果，並以分數所屬的例項命名。 按一下例項資料夾，以存取所需例項的結果。

![](../images/user-guide/results.png)

位於「區段產生器」的中心，將「分數」屬性拖放至 **[!UICONTROL 規則產生器畫布上，]** 以定義規則 ** 。

在右側的區段 *屬性欄* ，提供區段的名稱。

![](../images/user-guide/properties.png)

在左側的「欄 *位* 」欄上方，按一下 **gear** 圖示，然後從下拉式清單中選取 *「合併* 」原則。 Click **[!UICONTROL Save]** to create the segment.

![](../images/user-guide/merge_policy.png)

## 後續步驟

透過本教學課程，您已使用「區段產生器」，根據受眾的傾向分數成功找到受眾。 您現在可以透過將受眾啟動至目標來定位受眾。 如需詳細 [資訊，請參閱](https://docs.adobe.com/content/help/en/experience-platform/rtcdp/destinations/destinations-overview.html) 「目標概觀」。