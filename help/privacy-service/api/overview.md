---
title: Privacy ServiceAPI指南
description: 了解如何使用Privacy ServiceAPI以程式設計方式管理支援Adobe Experience Cloud應用程式的隱私權工作。
source-git-commit: 196147e7691010707953561c110a3934fec8ba1b
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---

# [!DNL Privacy Service] API guide

Privacy ServiceAPI提供數個端點，可讓您以程式設計方式管理貴組織的隱私權工作。 These endpoints are outlined below. 如需詳細資訊，請參閱個別端點指南，並參閱 [快速入門手冊](./getting-started.md) 如需必要標題、讀取範例API呼叫等的重要資訊。

>[!NOTE]
>
>本指南說明如何使用 [!DNL Privacy Service] API。 For details on how to use the UI, see the [Privacy Service UI overview](../ui/overview.md).

若要檢視所有可用端點和CRUD作業，請造訪 [Privacy ServiceAPI參考](https://www.adobe.io/experience-platform-apis/references/privacy-service/).

## Privacy jobs

當Privacy Service收到存取或刪除主體個人資料的請求時，系統會建立隱私權工作以滿足該請求。 Each privacy job contains identity information related to the data subject, metadata about the Adobe Experience Cloud product that the job applies to, and the job&#39;s processing status.

此 `/jobs` 端點可讓您為組織建立和擷取隱私權工作。 若要了解如何使用此端點，請參閱 [隱私權工作端點指南](./privacy-jobs.md).

## Consent

某些法規需要客戶明確同意，才能收集其個人資料。 此 `/consent` 端點可讓您處理客戶同意請求，並將它們整合至您的隱私權工作流程中。 請參閱 [同意端點指南](./consent.md) 了解更多。

## 後續步驟

To begin making calls using the Privacy Service API, read the [getting started guide](./getting-started.md) then select one of the endpoint guides to learn how to use specific endpoints.
