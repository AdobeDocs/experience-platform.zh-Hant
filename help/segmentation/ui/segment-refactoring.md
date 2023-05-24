---
keywords: Experience Platform；首頁；熱門主題；分段；段生成器；段生成器
solution: Experience Platform
title: 重構分段時間約束UI指南
description: 段生成器提供了一個豐富的工作區，允許您與「配置檔案」資料元素交互。 工作區為生成和編輯規則提供了直觀的控制項，如用於表示資料屬性的拖放拼貼。
exl-id: 3a352d46-829f-4a58-b676-73c3147f792c
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---

# 時間約束重分解

Adobe Experience Platform2020年10月發佈的《Adobe Experience Platform細分服務》對效能進行了更改，為使用或和邏輯運算子增加了新的限制。 這些更改將影響使用段生成器用戶介面新建或編輯的段。 本指南說明如何緩解這些更改。

在2020年10月發佈之前，所有規則級、組級和事件級時間約束都重複引用了相同的時間戳。 為了澄清時間約束的使用，已刪除規則級和組級時間約束。 要適應此更改，必須將所有時間約束重寫為事件級時間約束。

以前，單個事件可能附加了多個時間約束規則。

![在「段生成器」中加亮了以前的時間約束樣式。](../images/ui/segment-refactoring/former-time-constraint.png)

如您所見，此段在規則層有兩個約束：「」的一個[!UICONTROL 今天]&quot;和&quot;[!UICONTROL 昨天]。

上一個段相當於以下段 — 兩個事件級時間約束都已使用AND運算子連接。 第一個事件級時間約束引用名稱等於「Training」且正在發生的按一下事件，而第二個事件級時間約束引用名稱等於「Pets」且昨天發生的按一下事件。

![新的時間約束樣式在段生成器中加亮顯示。](../images/ui/segment-refactoring/time-constraint-1.png) ![新的時間約束樣式在段生成器中加亮顯示。](../images/ui/segment-refactoring/time-constraint-2.png)

時間約束的這種重構還影響使用OR運算子連接的時間約束。
