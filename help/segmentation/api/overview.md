---
keywords: Experience Platform；首頁；熱門主題；分段；分段；分段服務；API;api;
title: 分段服務API指南
topic-legacy: guide
description: 分段服務API允許開發人員以寫程式方式管理Adobe Experience Platform的分段操作。 請遵循本指南以了解如何使用 API 執行關鍵作業。
exl-id: cebecaf3-9746-4b0b-9c50-11789fba66c3
source-git-commit: b48ead4255d50585cd315436ccb9727d86142d4c
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 2%

---

# 分段服務API指南

[!DNL Adobe Experience Platform Segmentation Service] 允許您在 [!DNL Adobe Experience Platform] 從 [!DNL Real-time Customer Profile] 資料。

的 [!DNL Segmentation Service] API提供多個端點，允許您以寫程式方式管理中的分段操作 [!DNL Experience Platform]。 本概述文檔提供了對這些端點中每個端點的高級介紹，並連結到它們關聯的端點指南以瞭解詳細資訊。 在閱讀各個端點指南之前，請參閱 [入門指南](./getting-started.md) 有關所需標頭、讀取示例API調用等的重要資訊。

要查看所有可用端點和CRUD操作，請參閱 [分段服務API參考](https://www.adobe.io/experience-platform-apis/references/segmentation/)。

## 對象

受眾是具有相似行為和/或特徵的人的集合。 這些可以通過使用平台或從外部源生成。 您可以使用 `/audiences` 終結點：檢索所有受眾、建立新受眾、檢索特定受眾的詳細資訊、更新特定受眾或刪除特定受眾。

有關使用此終結點的詳細資訊，請閱讀 [觀眾終結點指南](./audiences.md)。

## 導出作業

導出作業是用於將受眾段成員保留到資料集的非同步進程。 您可以使用 `/export/jobs` 終結點以檢索所有導出作業、建立新導出作業、檢索特定導出作業的詳細資訊或取消特定導出作業。

有關使用此終結點的詳細資訊，請閱讀 [導出作業終結點指南](./export-jobs.md)。

## 預覽和估計

預覽提供段定義的限定配置檔案的分頁清單，允許您將結果與預期結果進行比較。 您可以使用 `/preview` 終結點，以建立新預覽作業或查找特定預覽作業的結果。

估計提供段定義的統計資訊，如預計受眾規模、置信區間和誤差標準偏差。 您可以使用 `/estimate` 端點，以查看段定義的估計值。

有關使用這些終結點的詳細資訊，請閱讀 [預覽和估計端點指南](./previews-and-estimates.md)。

## 計畫

計畫是一種工具，可用於每天自動運行一次批分段作業。 您可以使用 `/config/schedules` 終結點：檢索計劃清單、建立新計畫、檢索特定計畫的詳細資訊、更新特定計畫或刪除特定計畫。

有關使用此終結點的詳細資訊，請閱讀 [計畫終結點指南](./schedules.md)。

## 段定義

段定義定義哪些配置檔案將成為哪些受眾段的一部分。 您可以使用 `/segment/definitions` 要管理段定義的端點。

有關使用此終結點的詳細資訊，請閱讀 [段定義端點指南](./segment-definitions.md)。

## 分段作業

段作業處理先前建立的段定義以生成受眾段。 您可以使用 `/segment/jobs` 端點以管理段作業。

有關使用此終結點的詳細資訊，請閱讀 [段作業終結點指南](./segment-jobs.md)。

## 段搜索

段搜索用於搜索包含在各種資料源中的欄位並以接近即時的方式返回它們。 要開始使用段搜索，請參閱 [搜索終結點指南](segment-search.md)

## 後續步驟

開始使用 [!DNL Segmentation Service] API，查看不同端點指南，瞭解有關如何調用服務各個端點的詳細步驟。 瞭解有關使用 [!DNL Platform] UI，請參見 [分段使用手冊](../ui/overview.md)。
