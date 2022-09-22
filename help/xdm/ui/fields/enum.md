---
keywords: Experience Platform；首頁；熱門主題；API; API; XDM; XDM系統；體驗資料模型；資料模型；ui；工作區；列舉；欄位；
solution: Experience Platform
title: 在UI中定義列舉欄位
description: 了解如何在Experience Platform使用者介面中定義列舉欄位。
topic-legacy: user guide
exl-id: 67ec5382-31de-4f8d-9618-e8919bb5a472
source-git-commit: 878d99d9eb45f40ff76e5e90116abf032be1c93f
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 2%

---

# 在UI中定義列舉欄位 {#enum}

>[!CONTEXTUALHELP]
>id="platform_xdm_enum_suggestedvalue"
>title="列舉和建議值"
>abstract="列舉會限制字串欄位，以僅允許擷取符合一組預先定義值的資料。 或者，您可以為欄位定義一組建議的值，這些值不限制擷取，而是定義您可在細分中選擇的屬性。 如需詳細資訊，請參閱文件。"

在Experience Data Model(XDM)中，列舉欄位代表欄位，此欄位受限於預先定義的可接受值清單。

當 [定義新欄位](./overview.md#define) 在Adobe Experience Platform使用者介面中，您可以選取 **[!UICONTROL 列舉]** 核取方塊。

![](../../images/ui/fields/special/enum.png)

選取核取方塊後會顯示其他控制項，讓您指定列舉的值限制。 在 **[!UICONTROL 值]** 欄，您必須提供要將欄位限制為的確切值。 此值必須符合 [!UICONTROL 類型] 您已為枚舉欄位選擇。 您可以選擇提供人性化 **[!UICONTROL 標籤]** 也是限制。

若要將其他限制新增至列舉，請選取 **[!UICONTROL 新增列]**.

![](../../images/ui/fields/special/enum-add-row.png)

繼續將所需的限制和選用標籤新增至列舉。 完成後，請選取 **[!UICONTROL 套用]** 將更改應用到架構。

![](../../images/ui/fields/special/enum-configured.png)

畫布會更新以反映變更。 日後探索此架構時，您可以在右側邊欄中檢視及編輯列舉欄位的限制。

![](../../images/ui/fields/special/enum-applied.png)

## 後續步驟

本指南說明如何在UI中定義列舉欄位。 請參閱 [定義UI中的欄位](./overview.md#special) 若要了解如何定義 [!DNL Schema Editor].
