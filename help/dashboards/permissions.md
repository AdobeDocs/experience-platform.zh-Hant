---
solution: Experience Platform
title: 如何取得並授予Experience Platform儀表板的存取許可權
type: Documentation
description: 授予使用者使用Adobe Admin Console檢視、編輯和更新Experience Platform控制面板的能力。
exl-id: 2e50790f-b3ab-4851-a9a5-7cb98bf98ce3
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 6%

---

# 儀表板的存取許可權

若要授與使用者檢視、編輯和更新控制面板的能力，您必須先啟用許可權。 在Adobe Experience Platform中，存取控制是透過[Adobe Admin Console](https://adminconsole.adobe.com/)提供。 透過[!DNL Admin Console]中的產品設定檔將使用者與許可權和沙箱連結。

本檔案提供控制面板可用許可權的摘要，包括控制面板授予存取權的功能及其啟用的使用者功能。 如需取得及指派存取許可權的詳細資訊，請先閱讀[存取控制總覽](../access-control/home.md)。

## 先決條件

若要設定[!DNL Experience Platform]的存取控制，您必須擁有擁有[!DNL Experience Platform]產品整合之組織的管理員許可權。 如需詳細資訊，請參閱[管理角色](https://helpx.adobe.com/tw/enterprise/using/admin-roles.html)上的Adobe說明中心文章。

## 可用的儀表板許可權 {#available-permissions}

[!DNL Dashboards]服務提供三個許可權，合併後可提供對Adobe Experience Platform中[!UICONTROL 設定檔]、[!UICONTROL 區段]、[!UICONTROL 目的地]和[!UICONTROL 授權使用情況]儀表板的完整存取權。 這些許可權包括：

| 權限 | 說明 |
|---|---|
| **管理標準儀表板** | 此許可權是&#x200B;**全域讀取和寫入許可權**。 它可讓您[建立自訂Widget](./customize/custom-widgets.md)，並[透過[!UICONTROL Widget資料庫]編輯該Widget結構描述](./customize/edit-schema.md)。 |
| **檢視標準儀表板** | 這為[!UICONTROL 設定檔]、[!UICONTROL 目的地]和[!UICONTROL 區段]儀表板提供&#x200B;**唯讀**&#x200B;功能，並可透過Experience Platform的左側導覽存取這些儀表板。 它也會將[!UICONTROL 儀表板]新增至左側導覽並存取[!UICONTROL 儀表板]詳細目錄和整合標籤。 |
| **檢視授權使用量儀表板** | 此許可權可讓使用者&#x200B;**唯讀**&#x200B;存取Experience Platform UI中的[授權使用儀表板](./guides/license-usage.md)。 |

根據您的需求，[!DNL Dashboard]類別中可能未包含五個許可權。 下表概述其在Admin Console中的類別位置：

>[!IMPORTANT]
>
>**[!DNL Manage Standard Dashboards]**&#x200B;和&#x200B;**[!DNL View Standard Dashboards]**&#x200B;許可權&#x200B;**都需要**&#x200B;來自Admin Console中[!DNL Profile Management]或[!DNL Destinations]類別的「檢視」或「管理」許可權，才能啟用Experience Platform UI中的相關區段。

| 權限 | Admin Console類別位置 |
|---|---|
| [!DNL View Profiles] | [!DNL Profile Management] |
| [!DNL View Segments] | [!DNL Profile Management] |
| [!DNL View Destinations] | [!DNL Destinations] |
| [!DNL Manage Queries] | [!DNL Query Service] |
| [!DNL Manage Sandboxes] | [!DNL Sandbox Administration] |

## 存取控制矩陣

下列存取控制矩陣提供哪些許可權為必填，以及這些許可權提供哪些功能供您存取不同的儀表板功能。 許可權會橫跨頂端水準列列出，而Experience Platform UI工作區會沿著左欄列出。

|   | [!UICONTROL 檢視標準儀表板]或[!UICONTROL 管理標準儀表板] | [!UICONTROL 檢視設定檔]，<br/>[!UICONTROL 檢視區段]，<br/> [!UICONTROL 檢視目的地] | [!UICONTROL 管理查詢]和[!UICONTROL 管理沙箱] | [!UICONTROL 檢視授權使用量儀表板] |
|---|---|---|---|---|
| 左側導覽中的[!DNL Profiles]，<br/>[!DNL Segments]，<br/>[!DNL Destinations]。 | 不適用 | **每個儀表板都需要**&#x200B;一個「檢視」或「管理」許可權。 | 不適用 | 不適用 |
| 左側導覽中的[!DNL Dashboards]。 | 已啟用 | **至少需要一個**。 | 不適用 | 不適用 |
| [!DNL Dashboards] [!DNL Inventory] <br/> （瀏覽標籤） | 已啟用 | 不適用 | 不適用 | 不適用 |
| [!DNL Dashboards] [!DNL Integrations]索引標籤<br/>(用於安裝Power BI) | 已啟用 | **至少需要一個** | 不適用 | 不適用 |
| Power BI安裝按鈕和工作流程 | 已啟用 | 不適用 | **必要** | 不適用 |
| [!DNL Profiles]，<br/>[!DNL Segments]，<br/>[!DNL Destinations]儀表板。<br/>編輯Widget結構描述及新增自訂屬性的能力 | **需要Manage-standard-dashboard** | **必要（每個個別儀表板）** | 不適用 | 不適用 |
| [!DNL License Usage Dashboard] | 不適用 | 不適用 | 不適用 | 已啟用 |

{style="table-layout:auto"}

## 將許可權新增至您的產品設定檔

使用上方提供的資訊，將適當的許可權新增至您的產品設定檔。 請參閱檔案以取得[如何透過存取控制UI](../access-control/ui/permissions.md)新增許可權的完整指示。

如需許可權的描述，請參閱本檔案先前的[可用許可權](#available-permissions)區段。

>[!NOTE]
>
>您不需要為所有使用者啟用所有許可權。 根據您組織的結構，您可能想要為特定使用者建立個別的產品設定檔，並授與有限存取權（例如唯讀）。 請參閱產品設定檔的管理使用者檔案，以瞭解[如何為特定使用者指派許可權](../access-control/ui/users.md)。

新增必要的存取許可權後，組織內的使用者可以開始在Experience Platform UI中檢視儀表板，並根據您指派的許可權執行其他動作。
