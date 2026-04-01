---
title: 存取Experience Platform中的AI助理（舊版）
description: 瞭解如何在Experience Cloud UI中存取AI助理。
exl-id: c4cdff25-512c-4b4c-be91-ad9360067a0a
source-git-commit: daaf3ff0218b73a9fd827ab2ef090d8046cef3bb
workflow-type: tm+mt
source-wordcount: '876'
ht-degree: 0%

---

# 存取Experience Platform中的AI助理（舊版）

>[!IMPORTANT]
>
>本檔案適用於AI助理（舊版）。 如需AI助理(Next-Gen)的相關資訊，請閱讀Experience Cloud[檔案中](https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-ai/experience-cloud-ai/ai-assistant/ai-assistant-ui)AI的[AI助理UI指南](https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-ai/experience-cloud-ai/home)。

請參閱下表以取得「AI助理（舊版）」和「AI助理（次世代）」的比較結果：

| 功能區域 | AI助理（舊版） | AI助理（新一代） |
| --- | --- | --- |
| 使用者體驗 | AI助理（舊版）僅在右邊欄面板中可用。 | AI Assistant (Next-Gen)提供右欄面板和沈浸式全熒幕體驗。 |
| 功能範圍 | 您可以使用AI助理（舊版）來取得產品知識和營運見解。 | 您可以使用AI Assistant （新一代）來瞭解產品知識、營運深入分析，以及進階代理技能和多步驟任務執行。 |
| 平台架構 | AI助理（舊版）並非建置在Agent Orchestrator棧疊上。 | AI Assistant (Next-Gen)由[Adobe Experience Platform Agent Orchestrator](https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator)提供技術支援，可擴充性以及各種功能的進階協調。 |
| 應用程式涵蓋範圍 | AI助理（舊版）是應用程式專用的實作。 | 您可以使用AI助理（新一代），在所有Adobe Experience Cloud應用程式中提供統一的AI助理體驗。 |
| 存取與許可權模型 | 應用程式範圍的存取模型會與個別產品邊界對齊。 | 所有使用者都能存取AI Assistant (Next-Gen)和相關聯的Experience Platform代理程式。 **附註**： <ul><li>**Adobe Experience Manager**：您的管理員必須授予您透過[Adobe Admin Console](https://helpx.adobe.com/tw/enterprise/using/admin-console.html)存取AI小幫手(Next-Gen)的許可權。</li><li>**Customer Journey Analytics**：您的管理員必須透過[Customer Journey Analytics存取控制](https://experienceleague.adobe.com/zh-hant/docs/analytics-platform/using/technotes/access-control?lang=en)授與您存取AI小幫手的許可權。 這可讓您詢問產品知識和資料見解問題。 |

您可以在Adobe Experience Cloud中的多個應用程式中存取AI助理（舊版）。

>[!NOTE]
>
>如果您在許可權UI中收到快顯訊息，通知您組織必須首先同意其他法律條款才能存取AI Assistant （舊版），則請聯絡您的Adobe客戶團隊以取得這些條款的指引。

## 開始使用 {#get-started}

您必須先完成兩個先決條件步驟，才能存取AI助理（舊版）。

1. 貴組織必須首先同意法律條款。 如需詳細資訊，請聯絡您的Adobe客戶團隊。
2. 您的管理員必須授予您足夠許可權才能存取AI助理（舊版）。

如果您未完成這兩個先決條件步驟中的一個，則當您在Experience Platform UI中選取AI助理（舊版）聊天圖示時，將會看到下列訊息。

>[!BEGINTABS]

>[!TAB 您的組織無法使用AI助理（舊版）]

如果您使用的組織在法律上不符合使用AI助理（舊版）的資格，您將看到以下訊息。 在此案例中，您必須聯絡Adobe帳戶團隊以解決存取問題。

![組織無法使用AI助理（舊版）時，Experience Platform UI上顯示的快顯訊息。](./images/access/modal-one.png)

>[!TAB 您沒有正確的許可權]

如果您的組織在法律上符合使用AI Assistant （舊版）的資格，但您仍然無法存取該功能，則您將在Experience Platform UI上看到以下訊息。 這種情況表示您沒有足夠的許可權可存取該功能，因此您必須聯絡管理員以解決許可權問題。

![如果您沒有AI小幫手（舊版）的必要許可權，Experience Platform UI上就會顯示快顯訊息。](./images/access/modal-two.png)

>[!ENDTABS]

## 取得AI助理的存取權（舊版） {#get-access-to-ai-assistant}

對AI助理（舊版）的存取受以下引數控制：

* **存取應用程式：**&#x200B;您可以在Adobe Experience Platform、Adobe Real-Time CDP、Adobe Journey Optimizer和[Customer Journey Analytics](https://experienceleague.adobe.com/zh-hant/docs/analytics-platform/using/ai-assistant)中存取AI助理（舊版）。
<!-- * **Contractual access:** Your company must agree to certain [!DNL GenAI]-related legal terms before your organization can use AI Assistant (Legacy). Contact your organization's administrator or your Adobe Account Team if you are not able to access AI Assistant (Legacy).  -->
* **許可權：**&#x200B;使用[許可權UI](../access-control/abac/ui/permissions.md)來授與或撤銷貴組織中AI小幫手（舊版）的存取權。 若要使用AI助理（舊版），指定的使用者必須屬於已布建具有&#x200B;**啟用AI助理**&#x200B;和&#x200B;**檢視作業分析**&#x200B;許可權的角色。
   * 作為管理員，您可以將&#x200B;**啟用AI小幫手**&#x200B;新增到指定的角色，並將使用者新增到該角色，以允許他們存取您組織中的AI小幫手（舊版）。 **注意**：此許可權可讓上述使用者存取AI小幫手（舊版），但不會授與他們任何管理能力，而讓其他人存取AI小幫手（舊版）。
   * 身為管理員，您可以將&#x200B;**檢視營運分析**&#x200B;新增至指定角色，並將使用者新增至該角色，以允許他們使用AI助理（舊版）的營運分析功能。

使用[許可權UI](../access-control/abac/ui/roles.md)來授與Experience Platform和Journey Optimizer中使用AI助理（舊版）的許可權。 如需如何在Customer Journey Analytics中存取AI助理（舊版）的相關資訊。 閱讀[Customer Journey Analytics](https://experienceleague.adobe.com/zh-hant/docs/analytics-platform/using/ai-assistant)的檔案。

![許可權UI頁面具有指定角色中包含的「啟用AI小幫手（舊版）」和「檢視操作深入分析」許可權。](./images/access/access-permissions.png)

一旦您擁有必要的許可權，您就可以存取AI小幫手（舊版），方法是選取您正在使用的應用程式頂端標題上的![AI小幫手（舊版）](/help/images/icons/ai-assistant.png)圖示。

![具有首次使用者體驗的AI小幫手（舊版）。](./images/access/access-home.png)

觀看以下影片，瞭解如何為組織和使用者設定AI Assistant （舊版）的存取權。

>[!VIDEO](https://video.tv.adobe.com/v/3475930/?captions=chi_hant&learn=on)

## 後續步驟

一旦您擁有AI助理（舊版）的完整存取權，您就可以在工作流程期間繼續使用該功能，請閱讀[AI助理（舊版） UI指南](./ui-guide.md)以取得詳細資訊。
