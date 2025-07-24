---
title: 監視串流設定檔擷取
description: 瞭解如何使用監控儀表板來監控串流設定檔擷取
hide: true
hidefromtoc: true
source-git-commit: 2f78b70761ef676fe4ab61b89b6cbb261c99e9ca
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 3%

---

# 監視串流設定檔擷取

您可以使用Adobe Experience Platform UI中的監控儀表板，即時監控組織中的串流設定檔擷取率。 使用此功能可針對串流資料提供更佳的輸送量、延遲和資料品品質度透明度。 此外，您可以使用此功能來主動警報和擷取可操作的深入分析，以識別潛在的容量違規和資料擷取問題。

請閱讀以下指南，瞭解如何使用監視儀表板來監視組織中串流設定檔擷取工作的速率和量度。

## 瞭解串流設定檔擷取控制面板

您可以在監控儀表板中使用三種不同的量度類別來串流設定檔擷取： [!UICONTROL 輸送量]、[!UICONTROL 擷取]和[!UICONTROL 延遲]。

* **輸送量**：選取&#x200B;**[!UICONTROL 輸送量]**&#x200B;以檢視Experience Platform在設定的期間內處理的資料量相關資訊。 請參考此量度以評估系統的效率和容量。
   * **容量**：您的沙箱在定義的條件下可以處理的最大資料量。
   * **要求輸送量**：擷取系統接收事件的速率（以每秒事件數測量）。
   * **處理輸送量**：系統成功擷取及處理傳入事件裝載的速率（以每秒事件數測量）。
* **內嵌**：選取[!UICONTROL 內嵌]以檢視沙箱中內嵌工作的相關資訊。 這些內嵌工作會以三種不同的量度來測量：
   * **已建立的記錄**：在指定期間內建立的記錄總數。 此量度代表沙箱中的成功資料擷取流程。
   * **失敗的記錄**：因錯誤而未擷取的記錄總數。
   * **捨棄的記錄**：因為違反容量限制而被捨棄的記錄總數。
* **延遲**：選取[!UICONTROL 延遲]以檢視Experience Platform在指定期間內回應要求或完成作業所花費的時間的相關資訊。

## 監控串流設定檔擷取的量度 {#streaming-profile-metrics}

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile"
>title="監視串流設定檔擷取"
>abstract="串流設定檔的監控儀表板會顯示輸送量、擷取速率和延遲的相關資訊。 使用此儀表板可檢視、瞭解和分析資料處理量度。 將您的串流設定檔匯入Experience Platform。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_request_throughput"
>title="請求輸送量"
>abstract="此量度代表每秒進入擷取系統的事件數。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_processing_throughput"
>title="處理輸送量"
>abstract="此量度代表系統每秒成功擷取的事件數。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_p95_ingestion_latency"
>title="P95擷取延遲"
>abstract="此量度會測量第95個百分位數的延遲，從事件到Experience Platform的當下，一直到成功擷取到設定檔存放區時。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_max_throughput"
>title="最大輸送量"
>abstract="此量度代表每秒進入串流設定檔擷取的傳入要求數上限。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_records_ingested"
>title="已擷取的記錄"
>abstract="此量度代表在設定的時間範圍內，擷取到設定檔存放區的記錄總數。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_records_failed"
>title="失敗的記錄"
>abstract="此量度代表在設定的時間範圍內，由於錯誤而無法擷取到設定檔存放區的記錄總數。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_records_skipped"
>title="略過的記錄"
>abstract="此量度代表在設定的時間範圍內，由於設定或容量違規而捨棄的記錄總數。"
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_monitoring_streaming_profile_error_details"
>title="錯誤詳細資料"
>abstract="此量度代表因錯誤而失敗的事件數。"
>text="Learn more in documentation"

| 量度 | 說明 | 維度 | 測量頻率 |
| --- | --- | --- | --- |
| 請求輸送量 | 此量度代表每秒進入擷取系統的事件數。 | 沙箱/資料流 | 每60秒重新整理資料即可即時監控。 |
| 處理輸送量 | 此量度代表系統每秒成功擷取的事件數。 | 沙箱/資料流 | 每60秒重新整理資料即可即時監控。 |
| P95擷取延遲 | 此量度會測量第95個百分位數的延遲，從事件到Experience Platform的當下，一直到成功擷取到設定檔存放區時。 | 沙箱/資料流 | 每60秒重新整理資料即可即時監控。 |
| 最大輸送量 |
| 已擷取的記錄 | 此量度代表在設定的時間範圍內，擷取到設定檔存放區的記錄總數。 | <ul><li>沙箱/資料流</li><li>資料流執行</li></ul> | <ul><li>沙箱/資料流：即時監視，每60秒重新整理一次資料。</li><li>資料流執行：在15分鐘內分組。</li></ul> |
| 失敗的記錄 | 此量度代表在設定的時間範圍內，由於錯誤而無法擷取到設定檔存放區的記錄總數。 | <ul><li>沙箱/資料流</li><li>資料流執行</li></ul> | <ul><li>沙箱/資料流：即時監視，每60秒重新整理一次資料。</li><li>資料流執行：在15分鐘內分組。</li></ul> |
| 略過的記錄 | 此量度代表在設定的時間範圍內，由於設定或容量違規而捨棄的記錄總數。 | <ul><li>沙箱/資料流</li><li>資料流執行</li></ul> | <ul><li>沙箱/資料流：即時監視，每60秒重新整理一次資料。</li><li>資料流執行：在15分鐘內分組。</li></ul> |
| 錯誤詳細資料 | 此量度代表因錯誤而失敗的事件數。 | 資料流執行 | 以每小時為時段分組。 |

{style="table-layout:auto"}