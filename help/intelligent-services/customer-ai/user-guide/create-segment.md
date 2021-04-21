---
keywords: Experience Platform；見解；客戶智慧；熱門主題；客戶智慧細分
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
title: 使用預測分數建立客戶區段
topic-legacy: Create a segment
description: 當預測執行完成時，「設定檔」會自動使用預測傾向分數。 利用客戶人工智慧豐富個人檔案分數可建立客戶細分，以根據其傾向分數尋找受眾。 本節提供使用區段產生器建立區段的步驟。
exl-id: ac81f798-f599-4a8d-af25-c00c92e74b4e
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# 建立具有預測分數的客戶細分

當預測執行完成時，「設定檔」會自動使用預測傾向分數。 利用客戶人工智慧豐富個人檔案分數可建立客戶細分，以根據其傾向分數尋找受眾。 本節提供使用區段產生器建立區段的步驟。 如需建立區段的更強穩教學課程，請參閱[區段產生器使用指南](../../../segmentation/ui/segment-builder.md)。

>[!IMPORTANT]
>
>為了運用此方法，資料集需要啟用即時客戶設定檔。

在平台UI中，按一下左側導覽中的&#x200B;**[!UICONTROL Segments]**，然後按一下&#x200B;**[!UICONTROL Create segment]**。

![](../images/user-guide/segments.png)

出現&#x200B;**區段產生器**。 在左&#x200B;**[!UICONTROL Fields]**&#x200B;欄和&#x200B;**[!UICONTROL Attributes]**&#x200B;標籤下，按一下名為&#x200B;**[!UICONTROL XDM Individual Profile]**&#x200B;的資料夾，然後按一下具有您組織名稱空間的資料夾。 名為&#x200B;**[!UICONTROL Customer AI]**&#x200B;的資料夾包含預測執行的結果，並以分數所屬的例項命名。 按一下例項資料夾，以存取所需例項的結果。

![](../images/user-guide/results.png)

位於區段產生器中心，將&#x200B;**[!UICONTROL Score]**&#x200B;屬性拖放至&#x200B;*規則產生器畫布*&#x200B;以定義規則。

在右側的&#x200B;*區段屬性*&#x200B;欄下，提供區段的名稱。

![](../images/user-guide/properties.png)

在左側的&#x200B;*欄位*&#x200B;欄上，按一下&#x200B;**gear**&#x200B;圖示，然後從下拉式清單中選取&#x200B;*合併原則*。 按一下&#x200B;**[!UICONTROL Save]**&#x200B;以建立區段。

![](../images/user-guide/merge_policy.png)

## 後續步驟

透過本教學課程，您已使用「區段產生器」，根據受眾的傾向分數成功找到受眾。 您現在可以透過將受眾啟動至目標來定位受眾。 如需詳細資訊，請參閱[目標概觀](../../../destinations/home.md)。
