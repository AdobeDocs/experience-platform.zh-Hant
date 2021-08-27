---
keywords: Experience Platform；首頁；熱門主題；分段；分段服務；API; API;
title: 區段服務API指南
topic-legacy: guide
description: 區段服務API可讓開發人員以程式設計方式管理Adobe Experience Platform中的區段作業。 請依照本指南，了解如何使用API執行重要作業。
exl-id: cebecaf3-9746-4b0b-9c50-11789fba66c3
source-git-commit: 5160bc8057a7f71e6b0f7f2d594ba414bae9d8f6
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 0%

---

# 區段服務API指南

[!DNL Adobe Experience Platform Segmentation Service] 可讓您建立區段，並從資料 [!DNL Adobe Experience Platform] 產生 [!DNL Real-time Customer Profile] 對象。

[!DNL Segmentation Service] API提供多個端點，可讓您以程式設計方式管理[!DNL Experience Platform]中的分段操作。 本概述檔案提供每個端點的高階簡介，以及相關端點指南的連結，以取得詳細資訊。 閱讀個別端點指南之前，請參閱[快速入門手冊](./getting-started.md)以取得必要標題、讀取範例API呼叫等的重要資訊。

若要檢視所有可用端點和CRUD操作，請參閱[分段服務API參考](https://www.adobe.io/experience-platform-apis/references/segmentation/)。

## 匯出工作

匯出工作是非同步程式，可用來將對象區段成員保留至資料集。 您可以使用`/export/jobs`端點來檢索所有導出作業、建立新導出作業、檢索特定導出作業的詳細資訊或取消特定導出作業。

有關使用此終結點的詳細資訊，請參閱[導出作業終結點指南](./export-jobs.md)。

## 預覽和估計

預覽提供區段定義之合格設定檔的編頁清單，讓您能比較結果與預期的結果。 您可以使用`/preview`端點建立新的預覽作業或查找特定預覽作業的結果。

預估值會提供區段定義的統計資訊，例如預測對象大小、信賴區間和錯誤標準差。 您可以使用`/estimate`端點來檢視區段定義的估計值。

有關使用這些端點的詳細資訊，請參閱[預覽和估計端點指南](./previews-and-estimates.md)。

## 排程器

排程是一種工具，可用來每天自動執行一次批次分段工作。 您可以使用`/config/schedules`端點來檢索調度清單、建立新調度、檢索特定調度的詳細資訊、更新特定調度或刪除特定調度。

有關使用此終結點的詳細資訊，請參閱[調度終結點指南](./schedules.md)。

## 區段定義

區段定義會定義哪些設定檔將成為哪些受眾區段的一部分。 您可以使用`/segment/definitions`端點來管理區段定義。

有關使用此端點的詳細資訊，請參閱[段定義端點指南](./segment-definitions.md)。

## 區段作業

區段工作會處理先前建立的區段定義，以產生對象區段。 您可以使用`/segment/jobs`端點管理區段作業。

有關使用此終結點的詳細資訊，請參閱[segment作業終結點指南](./segment-jobs.md)。

## 區段搜尋

區段搜尋可用來搜尋各種資料來源所包含的欄位，並近乎即時傳回。 若要開始使用區段搜尋，請參閱[search端點指南](segment-search.md)

## 後續步驟

若要開始使用[!DNL Segmentation Service] API，請檢閱不同端點指南，以取得如何呼叫服務的各種端點的詳細步驟。 若要進一步了解如何使用[!DNL Platform] UI的區段，請參閱[分段使用手冊](../ui/overview.md)。
