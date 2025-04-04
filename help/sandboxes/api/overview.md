---
keywords: Experience Platform；首頁；熱門主題；沙箱開發人員指南
solution: Experience Platform
title: Sandbox API指南
description: Adobe Experience Platform中的沙箱提供獨立的開發環境，可讓您測試功能、執行實驗及進行自訂設定，而不會影響您的生產環境。
role: Developer
exl-id: c77e96dc-d138-4126-bbb0-b67beb0a02d6
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 0%

---

# [!DNL Sandbox] API指南

[!DNL Sandbox] API提供數個端點，可讓您以程式設計方式管理組織內所有可供您使用的沙箱。 這些端點概述如下。 如需詳細資訊，請瀏覽個別端點指南，並參閱[快速入門手冊](./getting-started.md)，以取得必要標頭、讀取範例API呼叫等重要資訊。

若要檢視所有可用的端點和CRUD作業，請造訪[[!DNL Sandbox] API參考](https://www.adobe.io/experience-platform-apis/references/sandbox)。

## 可用的沙箱

可用沙箱端點可讓您檢視目前使用者可用的所有沙箱清單，包括有關每個沙箱的名稱、標題、狀態、型別和區域的資訊。 所有使用者都可以存取[!DNL Sandbox] API中可用的沙箱端點，包括沒有沙箱管理存取許可權的使用者。 請參閱[可用沙箱端點指南](./available.md)，瞭解如何在API中檢視可用沙箱。

## 沙箱管理

沙箱是單一Adobe Experience Platform執行個體中的虛擬分割區，可讓您與數位體驗應用程式的開發流程無縫整合。 您可以使用`/sandboxes`端點建立、檢視、編輯、重設和刪除生產及開發沙箱。 若要瞭解如何使用此端點，請參閱[沙箱端點指南](./sandboxes.md)。

## 沙箱型別

目前，Experience Platform上支援的沙箱型別為生產及開發沙箱。 預設Experience Platform授權共授予您5個沙箱，您可將其分類為生產或開發。 您可以額外授權10個沙箱，最多總共75個沙箱。 請參閱[沙箱型別端點指南](./types.md)，瞭解如何在API中檢視貴組織支援的沙箱型別。

## 後續步驟

若要開始使用[!DNL Sandbox] API進行呼叫，請閱讀[快速入門手冊](./getting-started.md)，然後選取其中一個端點指南，以瞭解如何使用特定端點。
