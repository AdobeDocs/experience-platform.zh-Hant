---
keywords: Experience Platform；首頁；熱門主題；沙箱開發人員指南
solution: Experience Platform
title: 沙箱API指南
topic-legacy: developer guide
description: Adobe Experience Platform中的沙箱提供孤立的開發環境，可讓您測試功能、執行實驗及進行自訂設定，而不會影響您的生產環境。
source-git-commit: f00e6161d82f1fd7ba442be9f06283f3c866573f
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 0%

---

# [!DNL Sandbox] API指南

[!DNL Sandbox] API提供數個端點，可讓您以程式設計方式管理IMS組織內所有可用的沙箱。 這些端點概述如下。 如需詳細資訊，請造訪個別端點指南，並參閱[快速入門手冊](./getting-started.md)，以取得必要標題、讀取範例API呼叫等的重要資訊。

若要查看所有可用端點和CRUD操作，請造訪[[!DNL Sandbox]  API參考](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sandbox-api.yaml)。

## 可用的沙箱

可用的沙箱端點可讓您檢視目前使用者可用的所有沙箱清單，包括每個沙箱名稱、標題、狀態、類型和地區的相關資訊。 [!DNL Sandbox] API中可用的沙箱端點可供所有使用者存取，包括沒有沙箱管理存取權限的使用者。 請參閱[可用的沙箱端點指南](./available.md)，了解如何在API中檢視可用的沙箱。

## 沙箱管理

沙箱是Adobe Experience Platform單一例項中的虛擬分區，可與數位體驗應用程式的開發程式順暢整合。 您可以使用`/sandboxes`端點建立、檢視、編輯、重設和刪除生產與開發沙箱。 若要了解如何使用此端點，請參閱[沙箱端點指南](./sandboxes.md)。

## 沙箱類型

目前，支援的Experience Platform沙箱類型為生產沙箱和開發沙箱。 預設的Platform授權共授予您五個沙箱，您可將其分類為生產或開發。 您可以授權額外的10個沙箱套件，最多總共75個沙箱。 請參閱[沙箱類型端點指南](./types.md) ，了解如何在API中檢視支援的組織沙箱類型。

## 後續步驟

若要開始使用[!DNL Sandbox] API進行呼叫，請閱讀[快速入門手冊](./getting-started.md)，然後選取其中一個端點手冊，以了解如何使用特定端點。