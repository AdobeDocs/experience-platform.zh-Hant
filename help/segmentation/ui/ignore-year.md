---
solution: Experience Platform
title: 忽略年度時間限制更新
description: 瞭解如何解決忽略年份時間限制的問題。
source-git-commit: d0bd7990f0d77cd5f8d30da735b89c188e13c780
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---


# 忽略年度時間限制更新 {#ignore-year}

>[!CONTEXTUALHELP]
>id="platform_audiences_segmentBuilder_ignoreYear"
>title="忽略年度更新"
>abstract="已更新忽略年份時間限制。 請重新儲存您的對象。"

2024年2月發行的Adobe Experience Platform已對Adobe Experience Platform分段服務進行變更，以解決在對象建立和評估中「忽略年份」選項的問題。

「忽略年份」選項的設計目的，是在執行對象評估時，忽略日期中的年份部分。 在不同事件之間的暫時性關係很重要，但特定年份不重要的情況下（例如出生日期欄位），可以使用此選項。

然而，在閏年（例如2024），基礎系統無法正確處理此選項，導致不準確的對象評估。 因此，如果在閏年啟用「忽略年份」，對象評估將遺漏一天。

如果您在此修正發行之前建立了對象，則只需在區段產生器中重新儲存對象即可套用修正。 如果您不確定您的對象是否會受到此解決方案的影響，則現有對象是否會受到此問題影響，區段產生器會提示使用者。
