---
keywords: Experience Platform；深入分析；customer ai；熱門主題；customer ai區段
solution: Experience Platform, Real-Time Customer Data Platform
feature: Customer AI
title: 使用預測分數建立客戶區段
description: 預測執行完成時，個人檔案會自動使用預測傾向分數。 使用Customer AI分數擴充設定檔可建立客戶區段，以根據其傾向分數尋找對象。 本節提供使用「區段產生器」建立區段的步驟。
exl-id: ac81f798-f599-4a8d-af25-c00c92e74b4e
source-git-commit: 07a110f6d293abff38804b939014e28f308e3b30
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

---

# 使用預測分數建立客戶區段

預測執行完成時，個人檔案會自動使用預測傾向分數。 使用Customer AI分數擴充設定檔可建立客戶區段，以根據其傾向分數尋找對象。 本節提供使用「區段產生器」建立區段的步驟。 如需建立區段的更強大教學課程，請參閱 [區段產生器使用手冊](../../../segmentation/ui/segment-builder.md).

>[!IMPORTANT]
>
>若要使用此方法，需要為資料集啟用「即時客戶個人檔案」 。

在平台UI中，按一下 **[!UICONTROL 區段]** ，然後按一下 **[!UICONTROL 建立區段]**.

![](../images/user-guide/segments.png)

此 **區段產生器** 隨即顯示。 從左側 **[!UICONTROL 欄位]** 欄和底下 **[!UICONTROL 屬性]** 索引標籤，按一下名為的資料夾 **[!UICONTROL XDM個別設定檔]** 然後按一下包含您組織名稱空間的資料夾。 資料夾命名為 **[!UICONTROL Customer AI]** 包含預測執行的結果，並以分數所屬的執行個體命名。 按一下執行個體資料夾以存取其所需執行個體的結果。

![](../images/user-guide/results.png)

位於區段產生器的中心，拖放 **[!UICONTROL 分數]** 屬性至 *規則產生器畫布* 以定義規則。

在右手下 *區段屬性* 欄中，提供區段的名稱。

![](../images/user-guide/properties.png)

在左側上方 *欄位* 欄，按一下 **齒輪** 圖示並選取 *合併原則* 從下拉式清單。 按一下 **[!UICONTROL 儲存]** 以建立區段。

![](../images/user-guide/merge_policy.png)

## 後續步驟

依照本教學課程，您已成功使用區段產生器，根據其傾向分數找到對象。 您現在可以將對象啟用至目的地，藉此鎖定對象。 請參閱 [目的地概觀](../../../destinations/home.md) 以取得詳細資訊。
