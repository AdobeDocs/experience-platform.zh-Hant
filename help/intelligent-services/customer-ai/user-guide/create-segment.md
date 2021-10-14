---
keywords: Experience Platform；深入分析；customer ai；熱門主題；customer ai區段
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
feature: Customer AI
title: 使用預測分數建立客戶區段
topic-legacy: Create a segment
description: 當預測執行完成時，設定檔會自動使用預測的傾向分數。 使用Customer AI分數豐富設定檔，可建立客戶區段，根據其傾向分數尋找對象。 本節提供使用「區段產生器」建立區段的步驟。
exl-id: ac81f798-f599-4a8d-af25-c00c92e74b4e
source-git-commit: c3320f040383980448135371ad9fae583cfca344
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

---

# 使用預測分數建立客戶區段

當預測執行完成時，設定檔會自動使用預測的傾向分數。 使用Customer AI分數豐富設定檔，可建立客戶區段，根據其傾向分數尋找對象。 本節提供使用「區段產生器」建立區段的步驟。 如需建立區段的更完善教學課程，請參閱[區段產生器使用指南](../../../segmentation/ui/segment-builder.md)。

>[!IMPORTANT]
>
>若要使用此方法，必須為資料集啟用即時客戶設定檔。

在Platform UI中，按一下左側導覽中的&#x200B;**[!UICONTROL 區段]**，然後按一下&#x200B;**[!UICONTROL 建立區段]**。

![](../images/user-guide/segments.png)

此時會出現&#x200B;**區段產生器**。 從左側的&#x200B;**[!UICONTROL 欄位]**&#x200B;欄和&#x200B;**[!UICONTROL 屬性]**&#x200B;標籤下，按一下名為&#x200B;**[!UICONTROL XDM個別設定檔]**&#x200B;的資料夾，然後按一下具有您組織的命名空間的資料夾。 名為&#x200B;**[!UICONTROL Customer AI]**&#x200B;的資料夾包含預測運行的結果，並以分數所屬的實例命名。 按一下執行個體資料夾以存取其所需執行個體的結果。

![](../images/user-guide/results.png)

位於區段產生器的中央，將&#x200B;**[!UICONTROL Score]**&#x200B;屬性拖放至&#x200B;*規則產生器畫布*&#x200B;以定義規則。

在右側的&#x200B;*區段屬性*&#x200B;欄下，提供區段的名稱。

![](../images/user-guide/properties.png)

在左側的&#x200B;*欄位*&#x200B;欄上，按一下&#x200B;**gear**&#x200B;圖示，然後從下拉式清單中選取&#x200B;*合併原則*。 按一下「**[!UICONTROL 儲存]**」以建立區段。

![](../images/user-guide/merge_policy.png)

## 後續步驟

依照本教學課程，您已使用「區段產生器」，根據其傾向分數成功找到對象。 您現在可以透過在目的地啟用對象來鎖定對象。 如需詳細資訊，請參閱[目的地概述](../../../destinations/home.md) 。
