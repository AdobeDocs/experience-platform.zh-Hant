---
title: Privacy Service API指南
description: 瞭解如何使用Privacy Service API以程式設計方式管理受支援Adobe Experience Cloud應用程式的隱私權工作。
role: Developer
exl-id: 665466ac-2447-4a9d-a8cf-62092c09e431
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 2%

---

# [!DNL Privacy Service] API指南

Privacy Service API提供數個端點，可讓您以程式設計方式管理組織的隱私權工作。 這些端點概述如下。 如需詳細資訊，請參閱個別端點指南，並參閱 [快速入門手冊](./getting-started.md) 如需必要標題的重要資訊，請參閱範例API呼叫等。

>[!NOTE]
>
>本指南涵蓋如何使用 [!DNL Privacy Service] API。 如需如何使用UI的詳細資訊，請參閱 [Privacy Service UI總覽](../ui/overview.md).

若要檢視所有可用的端點和CRUD作業，請造訪 [Privacy Service API參考](https://www.adobe.io/experience-platform-apis/references/privacy-service/).

## 隱私權職位

當Privacy Service收到存取或刪除主體個人資料的請求時，系統會建立隱私權工作以滿足該請求。 每個隱私權工作包含與資料主體相關的身分資訊、工作套用的Adobe Experience Cloud產品中繼資料，以及工作的處理狀態。

此 `/jobs` 端點可讓您為組織建立和擷取隱私權工作。 若要瞭解如何使用此端點，請參閱 [隱私權工作端點指南](./privacy-jobs.md).

## 同意

特定法規要求客戶明確同意才能收集其個人資料。 此 `/consent` 端點可讓您處理客戶同意請求，並將其整合至您的隱私權工作流程。 請參閱 [同意端點指南](./consent.md) 以進一步瞭解。

## 後續步驟

若要開始使用Privacy Service API進行呼叫，請閱讀 [快速入門手冊](./getting-started.md) 然後選取其中一個端點指南以瞭解如何使用特定端點。
