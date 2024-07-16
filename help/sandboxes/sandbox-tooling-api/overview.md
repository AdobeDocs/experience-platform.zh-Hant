---
title: 沙箱工具API指南
description: Adobe Experience Platform中的沙箱工具可讓您匯出和匯入沙箱之間的沙箱設定快照。
exl-id: 4bcc095b-5db1-4824-8b7c-c2ea5a393b98
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 1%

---

# [!DNL Sandbox]工具API指南

[!DNL Sandbox]工具API提供數個端點，可讓您在組織內可用的沙箱之間匯出和匯入快照。 所有互動都會透過HTTP端點進行。 在匯出快照之前，會檢查來源沙箱是否有成品，這些成品是包含在封裝中的物件。 發出匯入要求時，會取得[!DNL Azure Blob]快照並做為範本使用，以便為目的地沙箱產生幾乎類似的成品。 如需支援的物件與限制的清單，請參閱[沙箱工具](../ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling)檔案。

這些端點概述如下。 如需詳細資訊，請瀏覽個別端點指南，並參閱[快速入門手冊](./getting-started.md)，以取得必要標頭、讀取範例API呼叫等重要資訊。

## 套件 {#packages}

沙箱工具套件端點可讓您管理套件。 沙箱工具套件是成品定義的集合，包括套件ID、名稱、說明、組織ID和建立者ID。 如需在API中使用套件的詳細資訊，請參閱[套件端點指南](./packages.md)。

## 工具 {#tools}

沙箱工具端點可讓您獨立擷取作業JSON資料。 如需在API中擷取工作JSON資料的詳細資訊，請參閱[工具端點指南](./tools.md)。

## 後續步驟 {#next-steps}

若要開始使用沙箱工具API進行呼叫，請閱讀[快速入門手冊](./getting-started.md)，然後選取其中一個端點指南，以瞭解如何使用特定端點。
