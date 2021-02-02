---
keywords: Experience Platform;home；熱門主題；api;API;XDM;XDM系統；體驗資料模型；ui;workspace;identity;field;
solution: Experience Platform
title: 在UI中定義識別欄位
description: 瞭解如何在Experience Platform使用者介面中定義識別欄位。
topic: user guide
translation-type: tm+mt
source-git-commit: f5f507c2e962e2ff9f81376bfe363a6f438056cd
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 0%

---


# 在UI中定義識別欄位

在Experience Data Model(XDM)中，身分欄位代表一個欄位，可用來識別與記錄或時間序列事件相關的個人。 本檔案涵蓋如何在Adobe Experience Platform UI中定義識別欄位。

## 必要條件

身分欄位是在Platform中建構客戶身分圖形的重要元件，這最終會影響即時客戶個人檔案如何合併不同的資料片段，以獲得客戶的完整檢視。 在您的架構中定義身份欄位之前，請參閱以下文檔以瞭解與身份欄位相關的關鍵服務和概念：

* [Adobe Experience Platform Identity Service](../../../identity-service/home.md):跨裝置和系統橋接身分識別，並根據資料集符合的XDM架構所定義的身分欄位，將資料集連結在一起。
   * [身分名稱空間](../../../identity-service/namespaces.md):身份名稱空間定義了與單個人員相關的不同類型的身份資訊，並且是每個身份欄位的必需元件。
* [即時客戶個人檔案](../../../profile/home.md):利用客戶身分圖表，根據來自多個來源的匯總資料提供統一的消費者個人檔案，這些資料幾乎即時更新。

## 定義身份欄位

當[在UI中定義新欄位](./overview.md#define)時，您可以選取右側導軌中的&#x200B;**[!UICONTROL Identity]**&#x200B;核取方塊，將其設為識別欄位。

![](../../images/ui/fields/special/identity.png)

選取核取方塊後，會顯示其他控制項。 如果希望此欄位是方案的主標識，請選中&#x200B;**[!UICONTROL 主標識]**&#x200B;複選框。

>[!NOTE]
>
>單一架構可能定義了多個身份欄位，但只能有一個主要身份。 所有身分欄位（主要或其他）都會為個別客戶的身分圖形貢獻，但即時客戶個人檔案在合併資料片段時，只會使用主要身分作為真相來源。 如果要啟用方案以便在配置式中使用，該方案必須定義主標識。

在&#x200B;**[!UICONTROL Identity namespace]**&#x200B;下，使用下拉菜單為身份欄位選擇適當的命名空間。 Adobe提供的標準名稱空間以及貴組織定義的任何自訂名稱空間都會列出。

完成後，選擇&#x200B;**[!UICONTROL Apply]**&#x200B;將更改應用到模式。

![](../../images/ui/fields/special/identity-config.png)

畫布會更新以反映變更，而選取的欄位會取得指紋符號(![](../../images/ui/fields/special/identity-symbol.png))以指定其為身分。 在左側導軌中，識別欄位現在會列在類別或混合名稱下，提供欄位給架構。

由於所有身分欄位都預設為必填，因此欄位現在會列在左側導軌的「必填欄位」下方。 ****&#x200B;如果標識欄位在架構結構內嵌，則所有父欄位也將按需要列出。

![](../../images/ui/fields/special/identity-applied.png)

如果定義了方案的主要標識，現在可以繼續[啟用方案以用於即時客戶概要檔案](../resources/schemas.md#profile)。

## 後續步驟

本指南涵蓋如何在UI中定義識別欄位。 當使用此架構擷取資料時，您的客戶識別圖表將會更新，以反映該架構的識別欄位。 請參閱[identity graph viewer](../../../identity-service/ui/identity-graph-viewer.md)上的指南，瞭解如何在UI中探索您組織的專用圖表。

請參閱[定義UI](./overview.md#special)中欄位的概觀，瞭解如何定義[!DNL Schema Editor]中的其他XDM欄位類型。