---
keywords: Experience Platform;home；熱門主題；分段；分段；分段服務；API;api;
title: 區段服務API指南
topic-legacy: guide
description: Segmentation Service API可讓開發人員以程式設計方式管理Adobe Experience Platform的分段作業。 請依照本指南，瞭解如何使用API執行關鍵作業。
exl-id: cebecaf3-9746-4b0b-9c50-11789fba66c3
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---

# 區段服務API指南

[!DNL Adobe Experience Platform Segmentation Service] 可讓您建立區段，並從資料中 [!DNL Adobe Experience Platform] 產生 [!DNL Real-time Customer Profile] 觀眾。

[!DNL Segmentation Service] API提供多個端點，可讓您以程式設計方式管理[!DNL Experience Platform]中的分段作業。 本概述檔案提供這些端點的高階介紹，以及其相關端點指南的連結，以取得詳細資訊。 在閱讀個別端點指南之前，請參閱[快速入門手冊](./getting-started.md)，以取得必要標題、讀取範例API呼叫等重要資訊。

若要檢視所有可用的端點和CRUD作業，請參閱[分段服務API參考](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml)。

## 匯出工作

匯出工作是非同步程式，用來將讀者區段成員持續存留至資料集。 您可以使用`/export/jobs`端點來檢索所有導出作業、建立新的導出作業、檢索特定導出作業的詳細資訊或取消特定導出作業。

有關使用此端點的詳細資訊，請閱讀[導出作業端點指南](./export-jobs.md)。

## 預覽和估計

預覽提供區段定義的合格設定檔分頁清單，讓您比較結果與預期結果。 您可以使用`/preview`端點來建立新的預覽工作或查找特定預覽工作的結果。

估計值提供區段定義的統計資訊，例如預計讀者大小、信賴區間和錯誤標準差。 您可以使用`/estimate`端點來查看段定義的估計值。

有關使用這些端點的詳細資訊，請閱讀[預覽和估計端點指南](./previews-and-estimates.md)。

## 計畫

排程是一種工具，可用來每天自動執行一次批次分段工作。 您可以使用`/config/schedules`端點來檢索計劃清單、建立新計畫、檢索特定計畫的詳細資訊、更新特定計畫或刪除特定計畫。

有關使用此端點的詳細資訊，請閱讀[計畫端點指南](./schedules.md)。

## 區段定義

區段定義會定義哪些描述檔將屬於哪些讀者區段。 您可以使用`/segment/definitions`端點來管理區段定義。

有關使用此端點的詳細資訊，請閱讀[段定義端點指南](./segment-definitions.md)。

## 區段工作

區段工作會處理先前建立的區段定義，以產生觀眾區段。 您可以使用`/segment/jobs`端點來管理段作業。

有關使用此端點的詳細資訊，請閱讀[段作業端點指南](./segment-jobs.md)。

## 區段搜尋

區段搜尋可用來搜尋各資料來源所包含的欄位，並近乎即時地傳回這些欄位。 若要開始使用區段搜尋，請參閱[搜尋端點指南](segment-search.md)

## 後續步驟

若要開始使用[!DNL Segmentation Service] API，請檢視不同端點指南，以取得如何呼叫服務各端點的詳細步驟。 若要進一步瞭解如何使用[!DNL Platform] UI的區段，請參閱[區段使用指南](../ui/overview.md)。
