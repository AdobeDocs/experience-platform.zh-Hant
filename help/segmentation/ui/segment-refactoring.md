---
keywords: Experience Platform；首頁；熱門主題；分段；區段產生器；區段產生器
solution: Experience Platform
title: 重構分段時間限制UI指南
topic-legacy: ui guide
description: 區段產生器提供豐富的工作區，可讓您與設定檔資料元素互動。 工作區提供建立和編輯規則的直覺式控制項，例如用來表示資料屬性的拖放圖磚。
exl-id: 3a352d46-829f-4a58-b676-73c3147f792c
source-git-commit: 681418b4198c2b1303fda937c3ffc60dad21b672
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---

# 時間約束重分解

Adobe Experience Platform 2020年10月版本已對Adobe Experience Platform分段服務導入效能變更，新增OR和AND邏輯運算子的使用限制。 這些變更將影響使用區段產生器UI所建立或編輯的新區段。 本指南說明如何緩解這些變更。

2020年10月版本之前，所有規則層級、群組層級和事件層級時間限制都以重複方式參照相同的時間戳記。 為了釐清時間限制使用方式，已移除規則層級和群組層級時間限制。 為了適應此變更，所有時間限制都必須重寫為事件層級時間限制。

過去，個別事件可附加多個時間限制規則。

![先前的時間限制樣式會在區段產生器中強調顯示。](../images/ui/segment-refactoring/former-time-constraint.png)

如您所見，此區段在規則層級有兩個限制：一個代表「[!UICONTROL 今天]「 」和「 」[!UICONTROL 昨天]」。

上一個區段等同於下列區段 — 兩個事件層級時間限制皆已使用AND運算子連結。 第一個事件層級時間限制會參考名稱等於「Training」且今天發生的點按事件，而第二個事件層級時間限制會參考名稱等於「Pets」且昨天發生的點按事件。

![新的時間限制樣式會在區段產生器中強調顯示。](../images/ui/segment-refactoring/time-constraint-1.png) ![新的時間限制樣式會在區段產生器中強調顯示。](../images/ui/segment-refactoring/time-constraint-2.png)

時間約束的這種重構還會影響使用OR運算子連接的時間約束。
