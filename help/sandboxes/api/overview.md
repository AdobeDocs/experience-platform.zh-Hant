---
keywords: Experience Platform；首頁；熱門主題；沙箱開發人員指南
solution: Experience Platform
title: 沙箱API指南
description: Adobe Experience Platform中的沙箱提供孤立的開發環境，可讓您測試功能、執行實驗及進行自訂設定，而不會影響您的生產環境。
exl-id: c77e96dc-d138-4126-bbb0-b67beb0a02d6
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---

# [!DNL Sandbox] API指南

此 [!DNL Sandbox] API提供數個端點，可讓您以程式設計方式管理組織內可用的所有沙箱。 這些端點概述如下。 如需詳細資訊，請參閱個別端點指南，並參閱 [快速入門手冊](./getting-started.md) 如需必要標題、讀取範例API呼叫等的重要資訊。

若要查看所有可用端點和CRUD操作，請造訪 [[!DNL Sandbox] API參考](https://www.adobe.io/experience-platform-apis/references/sandbox).

## 可用的沙箱

可用的沙箱端點可讓您檢視目前使用者可用的所有沙箱清單，包括每個沙箱名稱、標題、狀態、類型和地區的相關資訊。 中可用的沙箱端點 [!DNL Sandbox] 所有使用者都可存取API，包括沒有沙箱管理存取權限的使用者。 請參閱 [可用的沙箱端點指南](./available.md) 了解如何在API中檢視可用的沙箱。

## 沙箱管理

沙箱是Adobe Experience Platform單一例項中的虛擬分區，可與數位體驗應用程式的開發程式順暢整合。 您可以使用 `/sandboxes` 端點。 若要了解如何使用此端點，請參閱 [沙箱端點指南](./sandboxes.md).

## 沙箱類型

目前，支援的Experience Platform沙箱類型為生產沙箱和開發沙箱。 預設的Platform授權共授予您五個沙箱，您可將其分類為生產或開發。 您可以授權額外的10個沙箱套件，最多總共75個沙箱。 請參閱 [沙箱類型端點指南](./types.md) 了解如何在API中檢視支援的組織沙箱類型。

## 後續步驟

若要開始使用進行呼叫 [!DNL Sandbox] API，請閱讀 [快速入門手冊](./getting-started.md) 然後，選取其中一個端點指南，以了解如何使用特定端點。
