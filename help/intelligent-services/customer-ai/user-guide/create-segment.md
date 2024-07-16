---
keywords: Experience Platform；深入分析；customer ai；熱門主題；customer ai區段
solution: Experience Platform, Real-Time Customer Data Platform
feature: Customer AI
title: 使用預測分數建立客戶區段
description: 預測執行完成時，個人檔案會自動使用預測傾向分數。 使用Customer AI分數擴充設定檔可建立客戶區段，以根據其傾向分數尋找對象。 本節提供使用「區段產生器」建立區段的步驟。
exl-id: ac81f798-f599-4a8d-af25-c00c92e74b4e
source-git-commit: 68aa226395e8dcbf98a851134332f31303a8c710
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

---

# 使用預測分數建立客戶區段

預測執行完成時，個人檔案會自動使用預測傾向分數。 使用Customer AI分數擴充設定檔可建立客戶區段，以根據其傾向分數尋找對象。 本節提供使用「區段產生器」建立區段的步驟。 如需建立區段的更完善教學課程，請參閱[區段產生器使用手冊](../../../segmentation/ui/segment-builder.md)。

>[!IMPORTANT]
>
>若要使用此方法，需要為資料集啟用「即時客戶個人檔案」 。

在Platform UI中，按一下左側導覽中的&#x200B;**[!UICONTROL 區段]**，然後按一下&#x200B;**[!UICONTROL 建立區段]**。

![](../images/user-guide/segments_new.png)

**區段產生器**&#x200B;會出現。 從左側&#x200B;**[!UICONTROL 欄位]**&#x200B;欄位和&#x200B;**[!UICONTROL 屬性]**&#x200B;標籤下，按一下名為&#x200B;**[!UICONTROL XDM個人設定檔]**&#x200B;的資料夾，然後按一下具有您組織名稱空間的資料夾。 名為&#x200B;**[!UICONTROL Customer AI]**&#x200B;的資料夾包含預測執行的結果，並以分數所屬的執行個體命名。 按一下執行個體資料夾以存取其所需執行個體的結果。

![](../images/user-guide/results_new.png)

位於區段產生器的中心，將&#x200B;**[!UICONTROL 分數]**&#x200B;屬性拖放至&#x200B;*規則產生器畫布*&#x200B;以定義規則。

在右側&#x200B;*區段屬性*&#x200B;欄下，提供區段的名稱。

![](../images/user-guide/properties_new.png)

在左側&#x200B;*欄位*&#x200B;欄的上方，按一下&#x200B;**齒輪**&#x200B;圖示，並從下拉式清單中選取&#x200B;*合併原則*。 按一下&#x200B;**[!UICONTROL 儲存]**&#x200B;以建立區段。

![](../images/user-guide/merge_policy_new.png)

## 後續步驟

依照本教學課程，您已成功使用區段產生器，根據其傾向分數找到對象。 您現在可以將對象啟用至目的地，藉此鎖定對象。 如需詳細資訊，請參閱[目的地概觀](../../../destinations/home.md)。
