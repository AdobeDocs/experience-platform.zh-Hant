---
title: Privacy ServiceAPI指南
description: 瞭解如何使用Privacy ServiceAPI以寫程式方式管理受支援的Adobe Experience Cloud應用程式的隱私作業。
exl-id: 665466ac-2447-4a9d-a8cf-62092c09e431
source-git-commit: bda8d0ee1db4b58b4b856a23a8790cd7f76c0656
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 1%

---

# [!DNL Privacy Service] API指南

Privacy ServiceAPI提供了多個端點，允許您以寫程式方式管理組織的隱私作業。 下面概述了這些端點。 請訪問各個端點指南以瞭解詳細資訊，並參閱 [入門指南](./getting-started.md) 有關所需標頭、讀取示例API調用等的重要資訊。

>[!NOTE]
>
>本指南介紹如何使用 [!DNL Privacy Service] API。 有關如何使用UI的詳細資訊，請參閱 [Privacy ServiceUI概述](../ui/overview.md)。

要查看所有可用端點和CRUD操作，請訪問 [Privacy ServiceAPI參考](https://www.adobe.io/experience-platform-apis/references/privacy-service/)。

## 隱私作業

當Privacy Service接收到訪問或刪除主題的個人資料的請求時，系統建立隱私作業以滿足該請求。 每個隱私作業都包含與資料主題相關的身份資訊、關於作業應用的Adobe Experience Cloud產品的元資料以及作業的處理狀態。

的 `/jobs` 終結點允許您為組織建立和檢索隱私作業。 要瞭解如何使用此終結點，請參閱 [隱私作業終結點指南](./privacy-jobs.md)。

## 同意

某些法規要求客戶明確同意才能收集其個人資料。 的 `/consent` 端點允許您處理客戶同意請求並將其整合到您的隱私工作流中。 查看 [同意端點指南](./consent.md) 來瞭解更多資訊。

## 後續步驟

要開始使用Privacy ServiceAPI進行調用，請閱讀 [入門指南](./getting-started.md) 然後選擇其中一個端點參考線，以瞭解如何使用特定端點。
