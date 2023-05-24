---
keywords: Experience Platform；首頁；熱門主題；沙盒開發人員指南
solution: Experience Platform
title: 沙盒API指南
description: Adobe Experience Platform的沙箱提供獨立的開發環境，使您能夠test功能、運行實驗和進行定制配置，而不會影響您的生產環境。
exl-id: c77e96dc-d138-4126-bbb0-b67beb0a02d6
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---

# [!DNL Sandbox] API指南

的 [!DNL Sandbox] API提供了多個端點，允許您以寫程式方式管理組織內可用的所有沙箱。 下面概述了這些端點。 請訪問各個端點指南以瞭解詳細資訊，並參閱 [入門指南](./getting-started.md) 有關所需標頭、讀取示例API調用等的重要資訊。

要查看所有可用端點和CRUD操作，請訪問 [[!DNL Sandbox] API引用](https://www.adobe.io/experience-platform-apis/references/sandbox)。

## 可用沙箱

可用沙箱端點允許您查看當前用戶可用的所有可用沙箱的清單，包括有關每個沙箱的名稱、標題、狀態、類型和區域的資訊。 中可用的沙箱端點 [!DNL Sandbox] 所有用戶都可以訪問API，包括那些沒有沙盒管理訪問權限的用戶。 查看 [可用的沙箱端點指南](./available.md) 瞭解如何在API中查看可用的沙箱。

## 沙盒管理

沙盒是Adobe Experience Platform單個實例中的虛擬分區，它允許與您的數字型驗應用程式的開發過程無縫整合。 可以使用 `/sandboxes` 端點。 要瞭解如何使用此終結點，請參閱 [沙箱端點指南](./sandboxes.md)。

## 沙盒類型

目前，Experience Platform上支援的沙盒類型是生產和開發沙盒。 預設的平台許可證授予您總共五個沙箱，您可以將其分類為生產或開發。 您最多可以許可10個沙箱的附加包，最多可以合計75個沙箱。 查看 [沙盒類型終結點指南](./types.md) 瞭解如何在API中查看組織支援的沙盒類型。

## 後續步驟

使用 [!DNL Sandbox] API，讀取 [入門指南](./getting-started.md) 然後選擇其中一個端點參考線，以瞭解如何使用特定端點。
