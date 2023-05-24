---
keywords: Experience Platform；主題；熱門主題；訪問控制；基於屬性的訪問控制；ABAC
title: 基於屬性的訪問控制瀏覽
description: 本文檔提供有關在Adobe Experience Cloud使用「權限」介面的資訊
exl-id: 39634bde-8858-44a6-b39a-776846654fc1
source-git-commit: 38447348bc96b2f3f330ca363369eb423efea1c8
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 4%

---

# 權限指南

[!UICONTROL 權限] 是Adobe Experience Cloud的區域，在該區域，管理員可以定義用戶角色和訪問策略，以管理產品應用程式中功能和對象的訪問權限。

與 [!UICONTROL 權限]，您可以配置：

* [訪問策略](./policies.md)
* [標記](./labels.md)
* [權限](./permissions.md)
* [角色](./roles.md)
* [沙箱](./sandboxes.md)
* [使用者](./users.md)

為了訪問基於屬性的訪問控制權限 [!DNL Experience Cloud]，您必須是您的組織的管理員，該組織具有對 [!DNL Experience Cloud]。 雖然Adobe支援組織的靈活管理員層次結構，但您必須是Adobe Experience Platform的產品管理員才能配置權限。 參見Adobe Help Center上的 [管理角色](https://helpx.adobe.com/enterprise/using/admin-roles.html) 的子菜單。

如果您沒有管理員權限，請與系統管理員聯繫以獲得訪問權限。

一旦您具有管理員權限，請轉到 [Adobe Experience Cloud](https://experience.adobe.com/) 並使用您的Adobe憑據登錄。 登錄後， **[!UICONTROL 概述]** 頁面。 此頁顯示您的組織訂閱的產品以及將用戶和管理員添加到整個組織的其他控制項。 選擇 **[!UICONTROL 權限]** 開啟基於屬性的訪問控制工作區，以用於平台整合。

![flac-select產品](../../images/flac-ui/flac-select-product.png)

此時將顯示Adobe Experience Cloud的基於屬性的訪問控制工作區，開啟 **[!UICONTROL 角色]** 的子菜單。 此頁允許您查看所有角色並管理本文檔中概述的各種設定。

>[!IMPORTANT]
>
>在您的組織啟用基於屬性的訪問控制後，您可以開始在Adobe Experience Cloud使用權限，而不是在Adobe Admin Console使用產品配置檔案，以管理組織中用戶、功能、標籤和其他資源的權限。

![flac選擇角色](../../images/flac-ui/flac-select-roles.png)

本使用手冊重點介紹如何使用 [!DNL Experience Cloud] 為平台分配訪問權限。 有關如何導航的更一般資訊 [!DNL Admin Console]，請參見 [Admin Console使用手冊](https://helpx.adobe.com/tw/enterprise/using/admin-console.html)。

## 後續步驟

在導航了權限工作區後，繼續下一步到 [建立新角色](roles.md)。
