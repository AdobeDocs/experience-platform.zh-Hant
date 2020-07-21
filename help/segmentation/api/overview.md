---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Adobe Experience Platform細分服務開發人員指南
topic: guide
translation-type: tm+mt
source-git-commit: 995fadef9abacf22d0561e0590dfbe172adf0a43
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---


# Adobe Experience Platform [!DNL Segmentation Service] API開發人員指南

[!DNL Adobe Experience Platform Segmentation Service] 可讓您建立區段，並從資料中產 [!DNL Adobe Experience Platform] 生受 [!DNL Real-time Customer Profile] 眾。

API提 [!DNL Segmentation Service] 供多個端點，可讓您以程式設計方式在中管理區段作業 [!DNL Experience Platform]。 本概述檔案提供這些端點的高階介紹，以及其相關端點指南的連結，以取得詳細資訊。 在閱讀個別端點指南之前，請參閱快速入 [門指南](./getting-started.md) ，以取得必要標題、讀取範例API呼叫等重要資訊。

若要檢視所有可用的端點和CRUD作業，請參閱區 [段服務API參考](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml)。

## 匯出工作

匯出工作是非同步程式，用來將讀者區段成員持續存留至資料集。 您可以使用端 `/export/jobs` 點來檢索所有導出作業、建立新的導出作業、檢索特定導出作業的詳細資訊或取消特定導出作業。

有關使用此端點的詳細資訊，請閱讀導 [出作業端點指南](./export-jobs.md)。

## 預覽和估計

預覽提供區段定義的合格設定檔分頁清單，讓您比較結果與預期結果。 您可以使用端 `/preview` 點來建立新的預覽工作或尋找特定預覽工作的結果。

估計值提供區段定義的統計資訊，例如預計讀者大小、信賴區間和錯誤標準差。 可使用端 `/estimate` 點來查看段定義的估計值。

如需使用這些端點的詳細資訊，請閱讀預覽和 [估計端點指南](./previews-and-estimates.md)。

## 計畫

排程是一種工具，可用來每天自動執行一次批次分段工作。 您可以使用端 `/config/schedules` 點來檢索計劃清單、建立新計畫、檢索特定計畫的詳細資訊、更新特定計畫或刪除特定計畫。

有關使用此端點的詳細資訊，請閱讀計畫端 [點指南](./schedules.md)。

## 區段定義

區段定義會定義哪些描述檔將屬於哪些讀者區段。 您可以使用端 `/segment/definitions` 點來管理區段定義。

有關使用此端點的詳細資訊，請閱讀段定 [義端點指南](./segment-definitions.md)。

## 區段工作

區段工作會處理先前建立的區段定義，以產生觀眾區段。 您可以使用端 `/segment/jobs` 點來管理區段工作。

有關使用此端點的詳細資訊，請閱讀段作 [業端點指南](./segment-jobs.md)。

## 區段搜尋

區段搜尋可用來搜尋各資料來源所包含的欄位，並近乎即時地傳回這些欄位。 若要開始使用區段搜尋，請參閱搜 [尋端點指南](segment-search.md)

## 後續步驟

若要開始使用 [!DNL Segmentation Service] API，請檢視不同端點指南，以取得如何呼叫服務各端點的詳細步驟。 若要進一步瞭解如何使用 [!DNL Platform] UI的區段，請參閱區 [段使用指南](../ui/overview.md)。