---
keywords: Experience Platform；首頁；熱門主題；分段；分段；分段生成器；分段生成器
solution: Experience Platform
title: 重構分段時間限制UI指南
topic-legacy: ui guide
description: 「區段產生器」提供豐富的工作區，可讓您與描述檔資料元素互動。 工作區提供建立和編輯規則的直覺式控制項，例如用來表示資料屬性的拖放圖格。
exl-id: 3a352d46-829f-4a58-b676-73c3147f792c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---

# 時間約束重分解

2020年10月的Adobe Experience Platform版本已對Adobe Experience Platform區段服務引入效能變更，為OR和AND邏輯運算子的使用增加新的限制。 這些變更將影響使用「區段產生器」UI所建立或編輯的新區段。 本指南說明如何緩解這些變更。

在2020年10月發行之前，所有規則層級、群組層級和事件層級時間限制都會重複參照相同的時間戳記。 為了釐清時間限制的使用，已移除規則層級和群組層級的時間限制。 為了適應此變更，所有時間限制都必須重寫為事件級時間限制。

以前，個別事件可能附加多個時間限制規則。

![](../images/ui/segment-refactoring/former-time-constraint.png)

如您所見，此區段在規則層級有兩個限制：一個代表&quot;[!UICONTROL Today]&quot;，另一個代表&quot;[!UICONTROL Yesterday]&quot;。

上一個區段等同於下列區段— 兩個事件層級時間限制都已使用AND運算子連接。 第一個事件層級時間限制會參照名稱等於「Training」且目前發生的點按事件，而第二個事件層級時間限制會參照名稱等於「Pets」且昨天發生的點按事件。

![](../images/ui/segment-refactoring/time-constraint-1.png) ![](../images/ui/segment-refactoring/time-constraint-2.png)

這種時間約束的重構還會影響使用OR運算子連接的時間約束。
