---
solution: Experience Platform
title: 重構分段時間限制UI指南
description: 區段產生器提供豐富的工作區，可讓您與設定檔資料元素互動。 工作區提供用於建置和編輯規則的直覺式控制項，例如用來表示資料屬性的拖放圖磚。
exl-id: 3a352d46-829f-4a58-b676-73c3147f792c
source-git-commit: 665bbd1904e857336a4fb677230389d7977f6b60
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 9%

---

# 時間限制重構 {#refactorization}

>[!CONTEXTUALHELP]
>id="platform_audiences_segmentBuilder_constraints"
>title="時間限制重構"
>abstract="為了釐清時間限制的使用，我們已將規則層級和群組層級的時間限制。請將您的限制重新寫入為畫布層級或卡片層級的時間限制。"

2024年1月發行的Adobe Experience Platform已對Adobe Experience Platform分段服務進行變更，在可以定義時間限制的地方新增限制。 這些變更會影響使用區段產生器UI新建或編輯的區段。 本指南說明如何減少這些變更。

在2024年1月版本之前，所有規則層級、群組層級和畫布層級時間限制都重複參考相同的時間戳記。 為了釐清時間限制的使用方式，已移除規則層級和群組層級時間限制。 為了配合此變更，所有時間限制&#x200B;**必須**&#x200B;重寫為&#x200B;**畫布層級**&#x200B;或&#x200B;**卡片層級**&#x200B;時間限制。

過去，個別事件可以附加多個時間限制規則。 最近更新後，嘗試將時間限制新增至規則現在會導致&#x200B;**錯誤**。

![規則層級時間限制會反白顯示。 隨後發生的錯誤也會反白顯示。](../images/ui/segment-refactoring/rule-time-constraint.png)

時間限制現在只能在畫布層級或卡片層級套用。

在畫布層級套用時間限制時，您仍然可以選取所有可用的時間限制。

>[!NOTE]
>
>如果畫布上只有&#x200B;**一個**&#x200B;卡片，則套用時間限制到卡片是&#x200B;**等同於**&#x200B;套用時間限制到畫布層級。
>
>如果畫布上有&#x200B;**多**&#x200B;張卡片，套用時間限制到畫布層級將會將該時間限制套用到畫布上的&#x200B;**所有**&#x200B;張卡片。

![畫布層級時間限制已反白顯示。](../images/ui/segment-refactoring/canvas-time-constraint.png)

若要在卡片層級套用時間限制，請選取您要套用時間限制的特定卡片。 **[!UICONTROL 事件規則]**&#x200B;容器隨即顯示。 您現在可以選取要套用至卡片的時間限制。

![卡片層級時間限制已反白顯示。](../images/ui/segment-refactoring/card-time-constraint.png)
