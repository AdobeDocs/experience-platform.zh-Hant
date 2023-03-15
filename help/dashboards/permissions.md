---
solution: Experience Platform
title: 如何取得和授與Experience Platform控制面板的存取權限
type: Documentation
description: 授予使用者使用Adobe Admin Console檢視、編輯和更新Experience Platform控制面板的能力。
exl-id: 2e50790f-b3ab-4851-a9a5-7cb98bf98ce3
source-git-commit: fa4fc154f57243250dec9bdf9557db13ef7768e8
workflow-type: tm+mt
source-wordcount: '642'
ht-degree: 6%

---

# 控制面板的存取權限

若要授與使用者檢視、編輯和更新控制面板的能力，您必須先啟用權限。 在Adobe Experience Platform中，存取控制是透過 [Adobe Admin Console](https://adminconsole.adobe.com/). 使用者可透過 [!DNL Admin Console].

本檔案提供控制面板可用權限的摘要，包括控制面板可存取的功能及其可啟用的使用者功能。 如需取得和指派存取權限的詳細資訊，請先閱讀 [存取控制概觀](../access-control/home.md).

## 先決條件

為了配置 [!DNL Experience Platform]，則您必須擁有具有 [!DNL Experience Platform] 產品整合。 請參閱Adobe Help Center上的文章： [管理角色](https://helpx.adobe.com/enterprise/using/admin-roles.html) 以取得更多資訊。

## 可用的控制面板權限 {#available-permissions}

此 [!DNL Dashboards] 服務提供三個權限，結合後可提供完整存取權 [!UICONTROL 設定檔], [!UICONTROL 區段], [!UICONTROL 目的地]，和 [!UICONTROL 授權使用] Adobe Experience Platform中的控制面板。 這些權限包括：

| 權限 | 說明 |
|---|---|
| **管理標準控制面板** | 此權限是 **全局讀寫權限**. 它可讓您 [建立自訂小工具](./customize/custom-widgets.md) 和 [編輯介面工具集結構](./customize/edit-schema.md) 通過 [!UICONTROL 介面工具集程式庫]. |
| **檢視標準控制面板** | 這提供 **只讀** 功能 [!UICONTROL 設定檔], [!UICONTROL 目的地]，和 [!UICONTROL 區段] 控制面板，並可透過Platform的左側導覽存取控制面板。 它還補充了 [!UICONTROL 控制面板] 左側導覽並存取 [!UICONTROL 控制面板] 詳細目錄和整合功能索引標籤。 |
| **查看許可證使用情況儀表板** | 此權限可讓使用者 **只讀** 存取 [許可證使用儀表板](./guides/license-usage.md) 在Experience PlatformUI中。 |

有五個權限未包含在 [!DNL Dashboard] 類別，視您的需求而定。 下表概述其類別在Admin Console中的位置：

>[!IMPORTANT]
>
>兩者 **[!DNL Manage Standard Dashboards]** 和 **[!DNL View Standard Dashboards]** 權限 **要求** 「檢視」或「管理」權限 [!DNL Profile Management] 或 [!DNL Destinations] 類別，以啟用Platform UI中的相關區段。

| 權限 | Admin Console類別位置 |
|---|---|
| [!DNL View Profiles] | [!DNL Profile Management] |
| [!DNL View Segments] | [!DNL Profile Management] |
| [!DNL View Destinations] | [!DNL Destinations] |
| [!DNL Manage Queries] | [!DNL Query Service] |
| [!DNL Manage Sandboxes] | [!DNL Sandbox Administration] |

## 存取控制矩陣

下列存取控制矩陣提供需要哪些權限的劃分，以及這些權限針對存取不同控制面板功能提供哪些功能。 權限會列在水準的上方，而Platform UI工作區會沿著左欄列出。

|  | [!UICONTROL 檢視標準控制面板] 或 [!UICONTROL 管理標準控制面板] | [!UICONTROL 檢視設定檔],<br/>[!UICONTROL 檢視區段],<br/> [!UICONTROL 檢視目的地] | [!UICONTROL 管理查詢] &amp; [!UICONTROL 管理沙箱] | [!UICONTROL 查看許可證使用情況儀表板] |
|---|---|---|---|---|
| [!DNL Profiles],<br/>[!DNL Segments],<br/>[!DNL Destinations] 的下一頁。 | 不適用 | **需要「檢視」或「管理」權限** 每個控制面板。 | 不適用 | 不適用 |
| [!DNL Dashboards] 的下一頁。 | 已啟用 | **至少需要一個**. | 不適用 | 不適用 |
| [!DNL Dashboards] [!DNL Inventory] <br/>（瀏覽頁簽） | 已啟用 | 不適用 | 不適用 | 不適用 |
| [!DNL Dashboards] [!DNL Integrations] 標籤 <br/>(用於安裝Power BI) | 已啟用 | **至少需要一個** | 不適用 | 不適用 |
| Power BI安裝按鈕和工作流程 | 已啟用 | 不適用 | **必要** | 不適用 |
| [!DNL Profiles],<br/>[!DNL Segments],<br/>[!DNL Destinations] 控制面板。<br/>編輯Widget結構並新增屬性以自訂Widget的功能 | **需要管理 — 標準 — 儀表板** | **必填（每個控制面板）** | 不適用 | 不適用 |
| [!DNL License Usage Dashboard] | 不適用 | 不適用 | 不適用 | 已啟用 |

{style="table-layout:auto"}

## 將權限新增至您的產品設定檔

使用上述提供的資訊，將適當的權限新增至您的產品設定檔。 如需的完整指示，請參閱本檔案。 [如何透過存取控制UI新增權限](../access-control/ui/permissions.md).

有關權限的說明，請參閱 [可用權限](#available-permissions) 一節。

>[!NOTE]
>
>您不必為所有使用者啟用所有權限。 根據您的組織結構，您可能想要為特定使用者建立個別的產品設定檔，並授予有限的存取權（例如唯讀）。 請參閱有關管理產品設定檔使用者的檔案以了解 [如何為特定使用者指派權限](../access-control/ui/users.md).

新增必要的存取權限後，組織內的使用者就可以開始在Experience PlatformUI中檢視控制面板，並根據您指派的權限執行其他動作。
