---
title: 監視串流對象
description: 瞭解如何使用監視儀表板來監視使用串流細分評估的對象
hide: true
hidefromtoc: true
source-git-commit: 6fe0a36a8f2ac2cb954935ee8fe64432442b6e84
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 6%

---


# 監視串流對象

簡介簡介

## 快速入門

本指南需要您深入瞭解下列Experience Platform元件：

* [資料流](../home.md)：資料流代表跨Experience Platform傳輸資訊的資料工作。 它們可在各種服務中進行設定，以促進資料從來源聯結器移動至目標資料集以及身分服務、即時客戶設定檔和目的地。
* [分段服務](../../segmentation/home.md)：
* [容量](../../landing/license-usage-and-guardrails/capacity.md)：在Experience Platform中，容量可讓您知道您的組織是否超過您的護欄，並提供如何修正這些問題的資訊。

## 監控串流對象的量度 {#streaming-audience-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_audience_evaluation_rate"
>title="評估率"
>abstract="此量度代表每秒評估的記錄數。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_audience_p95_latency"
>title="P95 攝取延遲"
>abstract="此量度會測量到達Adobe Experience Platform之事件的第95個百分位數延遲，以成功評估對象。"
>text="Learn more in documentation"

下表提供有關用於串流受眾的量度的詳細資訊。

| 量度 | 說明 | 維度 |
| ------ | ----------- | ---------- |
| 評估率 | 每秒處理的對象評估數目。 | 沙箱，資料集 |
| P95 攝取延遲 | 成功事件到達對象的第95個百分位延遲。 | 沙箱，資料集 |
| 已收到的記錄 | 在所選時間範圍內從串流區段的串流擷取接收的記錄總數。 | 資料集 |
| 已評估的記錄 | 在選取的時段內使用串流細分成功評估&#x200B;**的**&#x200B;記錄總數。 | 資料集 |
| 攝取失敗的記錄 | 在串流區段中由於所選時間範圍內的錯誤而進行&#x200B;**失敗**&#x200B;評估的記錄總數。 | 資料集，流量執行 |
| 略過的記錄 | 在串流區段中，由於所選時間範圍內的錯誤而略過&#x200B;**評估**&#x200B;的記錄總數。 | 資料集，流量執行 |
| 合格的設定檔 | 在所選時間範圍內符合對象資格的設定檔數。 | 沙箱，受眾 |
| 設定檔不合格 | 在選取的時間範圍內從對象中取消資格的設定檔數。 | 沙箱，受眾 |

{style="table-layout:auto"}

## 使用串流受眾的監控儀表板 {#monitoring-dashboard}

若要存取串流對象的監視儀表板，請移至Experience Platform UI，從左側導覽選取&#x200B;**[!UICONTROL 監視]**，然後選取&#x200B;**[!UICONTROL 串流端對端]**。

影像

控制面板頂端是&#x200B;**[!UICONTROL 對象]**&#x200B;量度卡片。 這會顯示有關對象的&#x200B;**評估率**&#x200B;的資訊。