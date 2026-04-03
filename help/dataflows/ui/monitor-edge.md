---
title: 監視邊緣分段
description: 瞭解如何使用監視儀表板來觀察邊緣分段輸送量。
exl-id: 7abba7e8-1f2d-4a21-a93f-8bda7aa4d849
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 3%

---

# 監視邊緣分段

您可以使用Adobe Experience Platform UI中的監控儀表板，對組織內的邊緣細分進行即時監控。 使用此功能來存取邊緣資料輸送量的更高透明度。

## 快速入門

本指南需要您深入瞭解下列Experience Platform元件：

* [資料串流](../../datastreams/overview.md)：資料串流可讓您將Experience Platform Edge Network連線至您的資料集。
* [容量](../../landing/license-usage-and-guardrails/capacity.md)：在Experience Platform中，容量可讓您知道您的組織是否超過您的護欄，並提供如何修正這些問題的資訊。
* [Edge分段](../../segmentation/methods/edge-segmentation.md)： Edge分段可在[邊緣，即時評估Adobe Experience Platform中的區段定義，啟用相同頁面和下一頁個人化使用案例。](../../landing/edge-and-hub-comparison.md)

## 存取權 {#access}

若要存取邊緣區段輸送量的監視儀表板，請在&#x200B;**[!UICONTROL Monitoring]**&#x200B;區段中選取&#x200B;**[!UICONTROL Data management]**，接著選取&#x200B;**[!UICONTROL Edge]**。

![存取監視器邊緣區段儀表板的方法已反白顯示。](/help/dataflows/assets/ui/monitor-edge/access.png)

監視控制面板隨即顯示。 這會顯示邊緣串流輸送量的監控量度、顯示邊緣串流輸送量的速率的圖表，以及資料流檢視。 這些量度可依服務、邊緣和日期篩選。

![監視儀表板中的篩選選項會反白顯示。](/help/dataflows/assets/ui/monitor-edge/filtering.png)

>[!NOTE]
>
>如果您選取&#x200B;**，則只能看到資料流檢視**[!UICONTROL Edge segmentation throughput]。

如果您依服務篩選，則可以選擇要檢視其輸送量資訊的服務。 其中包括Edge細分、資料收集、Target、Adobe Journey Optimizer、Offer Decisioning、自訂個人化目的地、事件轉送、Adobe Analytics和Adobe Audience Manager等服務。

如果依邊緣篩選，則可以選擇要檢視相關資訊的邊緣。 支援的邊緣包括美國東岸、美國西岸、歐洲、印度、新加坡、澳洲、日本和瑞士。 您可以一次選取多個邊進行檢視。

如果您依日期篩選，可以選擇要篩選事件的時幅。 此時間刻度最多可設定30天。 或者，您可以使用下列其中一個預先設定的時間範圍： [!UICONTROL Last 6 hours]、[!UICONTROL Last 12 hours]、[!UICONTROL Last 24 hours]、[!UICONTROL Last 7 days]以及[!UICONTROL Last 30 days]。

## 監控邊緣輸送量的量度

測量結果表格提供所選服務邊緣輸送量的特定資訊。 如需各欄的詳細資訊，請參閱下表。

| 量度 | 說明 |
| ------ | ----------- |
| 收到的請求 | 時間範圍內所選邊緣收到的要求數。 |
| 尖峰輸送量 | 時間範圍內所選邊緣接收請求的最高速率。 |

{style="table-layout:auto"}

## 監控邊緣分段輸送量的圖表

監控圖表顯示在分配的時間範圍內，與允許的最大容量相比，選取的邊緣每秒接收的記錄數。

![顯示邊緣區段輸送量圖表。](/help/dataflows/assets/ui/monitor-edge/edge-segmentation-throughput.png)

## 資料流檢視

>[!NOTE]
>
>如果您正在篩選Edge分段輸送量，資料流檢視僅&#x200B;**有**&#x200B;可用。

「資料流檢視」段落會顯示通過沙箱邊緣的最新資料流清單。

![會顯示資料串流檢視，顯示列出之資料串流的相關資訊。](/help/dataflows/assets/ui/monitor-edge/datastream-view.png)

| 欄位 | 說明 |
| ----- | ----------- |
| 資料流名稱 | 資料流的名稱。 |
| 資料集 | 資料流所屬的資料集名稱。 |
| 啟用的服務 | 啟用資料流的服務名稱。 |
| 請求 | 通過資料流的要求數。 |
| 尖峰輸送量 | 通過資料流的最高要求速率。 |
