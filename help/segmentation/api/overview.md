---
title: Segmentation Service API指南
description: 分段服務API可讓開發人員以程式設計方式管理Adobe Experience Platform中的分段作業。 請遵循本指南以了解如何使用 API 執行關鍵作業。
role: Developer
exl-id: cebecaf3-9746-4b0b-9c50-11789fba66c3
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 2%

---

# 分段服務API指南

Adobe Experience Platform [!DNL Segmentation Service] 可讓您透過Adobe Experience Platform中的區段定義或其他來源，從您的 [!DNL Real-Time Customer Profile] 資料。

此 [!DNL Segmentation Service] API提供多個端點，可讓您以程式設計方式管理您在中的分段操作 [!DNL Experience Platform]. 本概述檔案提供這些端點各自的高層級簡介，以及相關聯的端點指南連結，以取得詳細資訊。 在閱讀個別端點指南之前，請參閱 [快速入門手冊](./getting-started.md) 如需必要標題的重要資訊，請參閱範例API呼叫等。

若要檢視所有可用的端點和CRUD作業，請參閱 [Segmentation Service API參考](https://www.adobe.io/experience-platform-apis/references/segmentation/).

## 對象

對象是具有相同類似行為和/或特徵的人物集合。 這些可透過使用Platform或從外部來源產生。 您可以使用 `/audiences` 端點可擷取所有對象、建立新對象、擷取特定對象的詳細資料、更新特定對象或刪除特定對象。

如需使用此端點的詳細資訊，請參閱 [對象端點指南](./audiences.md).

## 匯出工作

匯出作業是用來將受眾區段成員保留至資料集的非同步程式。 您可以使用 `/export/jobs` 端點可擷取所有匯出作業、建立新的匯出作業、擷取特定匯出作業的詳細資訊，或取消特定匯出作業。

如需使用此端點的詳細資訊，請參閱 [匯出作業端點指南](./export-jobs.md).

## 預覽和預估

預覽會提供符合區段定義之合格設定檔的分頁清單，好讓您將結果與預期進行比較。 您可以使用 `/preview` 端點以建立新的預覽作業或查閱特定預覽作業的結果。

預估可提供區段定義的統計資訊，例如預計對象人數、信賴區間和錯誤標準差。 您可以使用 `/estimate` 端點以檢視區段定義的預估值。

如需使用這些端點的詳細資訊，請閱讀 [預覽和估計端點指南](./previews-and-estimates.md).

## 時程表

排程是一種工具，可用於每天自動執行一次批次分段工作。 您可以使用 `/config/schedules` 端點可擷取排程清單、建立新排程、擷取特定排程的詳細資料、更新特定排程或刪除特定排程。

如需使用此端點的詳細資訊，請參閱 [排程端點指南](./schedules.md).

## 區段定義

區段定義會定義哪些設定檔將成為哪些對象的一部分。 您可以使用 `/segment/definitions` 端點以管理區段定義。

如需使用此端點的詳細資訊，請參閱 [區段定義端點指南](./segment-definitions.md).

## 區段工作

區段作業會處理先前建立的區段定義以產生對象。 您可以使用 `/segment/jobs` 端點以管理區段作業。

如需使用此端點的詳細資訊，請參閱 [區段作業端點指南](./segment-jobs.md).

## 區段搜尋

區段搜尋是用來搜尋各種資料來源包含的欄位，並近乎即時地傳回欄位。 若要開始使用區段搜尋，請參閱 [搜尋端點指南](segment-search.md)

## 後續步驟

若要開始使用 [!DNL Segmentation Service] API，檢閱不同的端點指南，以取得如何呼叫服務各種端點的詳細步驟。 若要進一步瞭解如何使用 [!DNL Platform] UI，請參閱 [分段使用手冊](../ui/overview.md).
