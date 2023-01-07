---
keywords: Experience Platform；深入分析；customer ai；熱門主題；customer ai區段
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: 使用預測分數建立客戶區段
description: 當預測執行完成時，設定檔會自動使用預測的傾向分數。 使用Customer AI分數豐富設定檔，可建立客戶區段，根據其傾向分數尋找對象。 本節提供使用「區段產生器」建立區段的步驟。
exl-id: ac81f798-f599-4a8d-af25-c00c92e74b4e
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

---

# 使用預測分數建立客戶區段

當預測執行完成時，設定檔會自動使用預測的傾向分數。 使用Customer AI分數豐富設定檔，可建立客戶區段，根據其傾向分數尋找對象。 本節提供使用「區段產生器」建立區段的步驟。 如需建立區段的更完善教學課程，請參閱 [區段產生器使用手冊](../../../segmentation/ui/segment-builder.md).

>[!IMPORTANT]
>
>若要使用此方法，必須為資料集啟用即時客戶設定檔。

在Platform UI中，按一下 **[!UICONTROL 區段]** 在左側導覽器中，然後按一下 **[!UICONTROL 建立區段]**.

![](../images/user-guide/segments.png)

此 **區段產生器** 框。 從左邊 **[!UICONTROL 欄位]** 欄和下方 **[!UICONTROL 屬性]** 頁簽，按一下名為 **[!UICONTROL XDM個別設定檔]** 然後按一下含有您組織命名空間的資料夾。 名為 **[!UICONTROL Customer AI]** 包含預測執行的結果，並以分數所屬的例項命名。 按一下執行個體資料夾以存取其所需執行個體的結果。

![](../images/user-guide/results.png)

位於區段產生器的中央，拖放 **[!UICONTROL 分數]** 屬性上 *規則產生器畫布* 來定義規則。

在右下 *區段屬性* 欄，提供區段的名稱。

![](../images/user-guide/properties.png)

在左側 *欄位* 欄，按一下 **齒輪** 圖示並選取 *合併策略* 從下拉式清單中。 按一下 **[!UICONTROL 儲存]** 來建立區段。

![](../images/user-guide/merge_policy.png)

## 後續步驟

依照本教學課程，您已使用「區段產生器」，根據其傾向分數成功找到對象。 您現在可以透過在目的地啟用對象來鎖定對象。 請參閱 [目的地概述](../../../destinations/home.md) 以取得更多資訊。
