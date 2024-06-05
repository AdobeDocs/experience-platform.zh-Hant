---
title: 在Experience Platform中存取AI助理
description: 瞭解如何在Experience CloudUI中存取AI助理。
source-git-commit: b51291e6c3663c6d6e6d416f0d2c37563c852155
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

* **存取應用程式：** 您可以在Adobe Experience Platform、Adobe Real-Time CDP、Adobe Journey Optimizer中存取AI助理 [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/ai-assistant).
<!-- * **Contractual access:** Your company must agree to certain [!DNL GenAI]-related legal terms before your organization can use AI Assistant. Contact your organization's administrator or your Adobe Account Team if you are not able to access AI Assistant.  -->
* **許可權：** 使用 [許可權UI](../access-control/abac/ui/permissions.md) 來授予或撤銷貴組織中AI Assistant的存取權。 為了使用AI助理，指定的使用者必須屬於以布建的角色 **啟用AI助理** 和 **檢視營運分析** 許可權。
   * 身為管理員，您可以新增 **啟用AI助理** 並新增使用者至該角色，讓他們可存取您組織中的AI助理。
   * 身為管理員，您可以新增 **檢視營運分析** 將使用者新增至指定角色，讓他們能夠使用AI助理的作業深入分析功能。 營運見解目前處於Beta版。

![許可權UI頁面具有給定角色中包含的啟用AI助理和檢視操作深入分析許可權。](./images/permissions.png)

使用許可權UI授予在Experience Platform和Journey Optimizer中使用AI助理的許可權。 如需如何在Customer Journey Analytics中存取AI助理的相關資訊。 請閱讀以下檔案： [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/ai-assistant).

一旦您擁有必要的許可權，您就可以存取AI助理員，方法是選取您正在使用的應用程式頂端標題上的AI助理員圖示。

![具有首次使用者體驗的AI助理。](./images/ai-assistant.png)

## 後續步驟

當您擁有AI助理的完整存取權後，您便可以在工作流程中繼續使用功能，請閱讀 [AI助理使用者介面指南](./ui-guide.md) 以取得詳細資訊。