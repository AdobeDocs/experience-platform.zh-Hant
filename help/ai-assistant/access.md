---
title: 在Experience Platform中存取AI助理
description: 瞭解如何在Experience CloudUI中存取AI助理。
exl-id: c4cdff25-512c-4b4c-be91-ad9360067a0a
source-git-commit: 706a20e70aa20adb0f4a554d0ec35518811ea9a1
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 0%

---

# 在Experience Platform中存取AI助理

您可以在Adobe Experience Cloud中的數個應用程式中存取AI助理。

>[!IMPORTANT]
>
>如果您在許可權UI中收到快顯訊息，通知您組織必須首先同意其他法律條款才能存取AI Assistant，然後聯絡您的Adobe客戶團隊以取得這些條款的指引。

對AI助理的存取受下列引數控制：

* **存取應用程式：**&#x200B;您可以在Adobe Experience Platform、Adobe Real-Time CDP、Adobe Journey Optimizer和[Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/ai-assistant)中存取AI小幫手。
<!-- * **Contractual access:** Your company must agree to certain [!DNL GenAI]-related legal terms before your organization can use AI Assistant. Contact your organization's administrator or your Adobe Account Team if you are not able to access AI Assistant.  -->
* **許可權：**&#x200B;使用[許可權UI](../access-control/abac/ui/permissions.md)授與或撤銷您組織中AI助理的存取權。 若要使用AI助理，指定的使用者必須屬於已布建具有&#x200B;**啟用AI助理**&#x200B;和&#x200B;**檢視作業分析**&#x200B;許可權的角色。
   * 身為管理員，您可以將&#x200B;**啟用AI小幫手**&#x200B;新增至指定的角色，並將使用者新增至該角色，以允許他們存取您組織中的AI小幫手。
   * 作為管理員，您可以將&#x200B;**檢視作業分析**&#x200B;新增到指定的角色，並將使用者新增到該角色，以允許他們使用AI助理的作業分析功能。 營運見解目前處於Beta版。

![許可權UI頁面具有指定角色中包含的[啟用AI助理員]和[檢視操作深入分析]許可權。](./images/permissions.png)

使用許可權UI授予在Experience Platform和Journey Optimizer中使用AI助理的許可權。 如需如何在Customer Journey Analytics中存取AI助理的相關資訊。 以[Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/ai-assistant)閱讀檔案。

一旦您擁有必要的許可權，您就可以存取AI助理員，方法是選取您正在使用的應用程式頂端標題上的AI助理員圖示。

![具有首次使用者體驗的AI小幫手。](./images/ai-assistant.png)

## 後續步驟

一旦您擁有AI助理的完整存取權，您就可以在工作流程中繼續使用該功能，請閱讀[AI助理使用者介面指南](./ui-guide.md)以取得詳細資訊。
