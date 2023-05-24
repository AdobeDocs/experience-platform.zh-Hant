---
solution: Experience Platform
title: 如何獲取和授予Experience Platform儀表板的訪問權限
type: Documentation
description: 允許用戶使用Adobe Admin Console查看、編輯和更新Experience Platform儀表板。
exl-id: 2e50790f-b3ab-4851-a9a5-7cb98bf98ce3
source-git-commit: fa4fc154f57243250dec9bdf9557db13ef7768e8
workflow-type: tm+mt
source-wordcount: '642'
ht-degree: 6%

---

# 儀表板的訪問權限

要授予用戶查看、編輯和更新儀表板的能力，必須首先啟用權限。 在Adobe Experience Platform，通過 [Adobe Admin Console](https://adminconsole.adobe.com/)。 用戶通過產品配置檔案連結到 [!DNL Admin Console]。

此文檔提供儀表板可用權限的摘要，包括儀表板所授予的訪問權限和所啟用的用戶功能。 有關獲取和分配訪問權限的詳細資訊，請從閱讀 [訪問控制概述](../access-control/home.md)。

## 先決條件

為了配置訪問控制 [!DNL Experience Platform]，您必須具有具有 [!DNL Experience Platform] 產品整合。 參見Adobe Help Center上的 [管理角色](https://helpx.adobe.com/enterprise/using/admin-roles.html) 的子菜單。

## 可用儀表板權限 {#available-permissions}

的 [!DNL Dashboards] 服務提供三種權限，當組合時，提供對 [!UICONTROL 配置檔案]。 [!UICONTROL 段]。 [!UICONTROL 目標], [!UICONTROL 許可證使用] Adobe Experience Platform的儀錶盤。 這些權限是：

| 權限 | 說明 |
|---|---|
| **管理標準儀表板** | 此權限是 **全局讀寫權限**。 它允許你 [建立自定義小部件](./customize/custom-widgets.md) 和 [編輯構件架構](./customize/edit-schema.md) 通過 [!UICONTROL 小部件庫]。 |
| **查看標準儀表板** | 這提供了 **只讀** 功能 [!UICONTROL 配置檔案]。 [!UICONTROL 目標], [!UICONTROL 段] 並允許通過平台的左側導航訪問儀表板。 它還補充了 [!UICONTROL 儀表板] 的 [!UICONTROL 儀表板] 清單和整合頁籤。 |
| **查看許可證使用儀表板** | 此權限允許用戶 **只讀** 訪問 [許可證使用儀表板](./guides/license-usage.md) 在Experience PlatformUI中。 |

有五個權限未包含在 [!DNL Dashboard] 可能需要的類別。 下表概述了它們在Admin Console中的類別位置：

>[!IMPORTANT]
>
>都 **[!DNL Manage Standard Dashboards]** 和 **[!DNL View Standard Dashboards]** 權限 **要求** 「查看」或「管理」權限 [!DNL Profile Management] 或 [!DNL Destinations] Admin Console中的類別，以激活平台UI中的相關部分。

| 權限 | Admin Console類別位置 |
|---|---|
| [!DNL View Profiles] | [!DNL Profile Management] |
| [!DNL View Segments] | [!DNL Profile Management] |
| [!DNL View Destinations] | [!DNL Destinations] |
| [!DNL Manage Queries] | [!DNL Query Service] |
| [!DNL Manage Sandboxes] | [!DNL Sandbox Administration] |

## 訪問控制矩陣

下面的訪問控制清單提供了需要哪些權限以及它們在訪問不同儀表板功能方面提供哪些功能的細分。 權限列在上水準行中，平台UI工作區列在左列中。

|  | [!UICONTROL 查看標準儀表板] 或 [!UICONTROL 管理標準儀表板] | [!UICONTROL 查看配置檔案]。<br/>[!UICONTROL 查看段]。<br/> [!UICONTROL 查看目標] | [!UICONTROL 管理查詢] &amp; [!UICONTROL 管理沙箱] | [!UICONTROL 查看許可證使用儀表板] |
|---|---|---|---|---|
| [!DNL Profiles]。<br/>[!DNL Segments]。<br/>[!DNL Destinations] 的子菜單。 | 不適用 | **需要「查看」或「管理」權限** 每個控制板。 | 不適用 | 不適用 |
| [!DNL Dashboards] 的子菜單。 | 已啟用 | **至少需要一個**。 | 不適用 | 不適用 |
| [!DNL Dashboards] [!DNL Inventory] <br/>（瀏覽頁籤） | 已啟用 | 不適用 | 不適用 | 不適用 |
| [!DNL Dashboards] [!DNL Integrations] 頁籤 <br/>(用於安裝Power BI) | 已啟用 | **至少需要一個** | 不適用 | 不適用 |
| Power BI安裝按鈕和工作流 | 已啟用 | 不適用 | **必需** | 不適用 |
| [!DNL Profiles]。<br/>[!DNL Segments]。<br/>[!DNL Destinations] 儀表板。<br/>編輯小部件架構和添加新屬性以進行小部件自定義的功能 | **需要管理標準儀表板** | **必需（對於每個相應儀表板）** | 不適用 | 不適用 |
| [!DNL License Usage Dashboard] | 不適用 | 不適用 | 不適用 | 已啟用 |

{style="table-layout:auto"}

## 將權限添加到您的產品配置檔案

使用上面提供的資訊將相應的權限添加到產品配置檔案中。 請參閱文檔以瞭解有關 [如何通過訪問控制UI添加權限](../access-control/ui/permissions.md)。

有關權限的說明，請參閱 [可用權限](#available-permissions) 的子菜單。

>[!NOTE]
>
>您不必為所有用戶啟用所有權限。 根據您組織的結構，您可能希望為某些用戶建立單獨的產品配置檔案並授予有限訪問權限（如只讀）。 請參閱有關管理產品配置檔案用戶的文檔以瞭解 [如何為特定用戶分配權限](../access-control/ui/users.md)。

添加必要的訪問權限後，組織內的用戶可以開始查看Experience PlatformUI中的儀表板，並根據您分配的權限執行其他操作。
