---
title: 對Experience Platform中資料收集的權限管理
description: 概略說明如何管理Adobe Experience Platform中的權限及控制資料收集功能的存取權。
exl-id: 8426d54b-ec1d-475a-a769-f45a8c924fe7
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '1303'
ht-degree: 5%

---

# 對Experience Platform中資料收集的權限管理

[Adobe Experience Platform中的資料收集](./home.md) 由數種不同的技術組成，這些技術可共同收集和傳輸您的資料。 這些技術的存取權限是透過Adobe Admin Console中精細的角色型權限控制。

本指南會說明如何管理資料收集功能的權限。

## 快速入門

若要設定資料收集的存取控制，您必須擁有與Adobe Experience Platform Data Collection產品整合之組織的管理員權限。 可授予或撤回權限的最低角色為 **產品設定檔管理員**. 可管理權限的其他管理員角色包括 **產品管理員** （可管理產品中的所有設定檔）和 **系統管理員** （無限制）。 請參閱 [管理角色](https://helpx.adobe.com/enterprise/using/admin-roles.html) (位於「Adobe企業管理指南」中)以取得詳細資訊。

本指南假設您熟悉產品設定檔等基本Admin Console概念，以及這些概念如何將產品權限授予個別使用者和群組。 如需詳細資訊，請參閱 [Admin Console使用手冊](https://helpx.adobe.com/tw/enterprise/using/admin-console.html).

## 可用權限

資料收集的相關權限是透過Admin Console中的兩種產品名稱提供： **Adobe Experience Platform** 和 **Adobe Experience Platform資料收集**. 以下各節將概述每項產品下提供的權限，以及其所授予存取權的特定功能說明。

### Adobe Experience Platform權限

Adobe Experience Platform底下的權限包括資料流、身分、結構描述和沙箱的存取權。 如需設定Adobe Experience Platform權限的步驟，請參閱 [存取控制使用手冊](../access-control/ui/overview.md).

| 類別 | 權限 | 說明 |
| --- | --- | --- |
| 沙箱 | (不適用) | 視 [沙箱](../sandboxes/home.md) 已在您的組織下建立，您可以透過Admin Console中的此權限類別控制對每個使用者的存取。 |
| 資料模型製作 | 管理結構描述 | 授予檢視、建立和編輯的能力 [Experience Data Model(XDM)結構](../xdm/home.md). |
| 資料模型製作 | 檢視結構描述 | 授予結構的唯讀存取權。 |
| Identity Management | 管理身分識別命名空間 | 授予檢視、建立和編輯的能力 [身分識別命名空間](../identity-service/namespaces.md). |
| Identity Management | 檢視身分命名空間 | 授予身分識別命名空間的唯讀存取權。 |
| 資料彙集 | 管理資料流 | 授予檢視、建立和編輯的能力 [資料流](../edge/datastreams/overview.md). |
| 資料彙集 | 檢視資料流 | 授予資料流的唯讀存取權。 |

{style="table-layout:auto"}

<!-- (Feature not yet available?)
| Dashboards | Manage Custom Dashboards | |
| Dashboards | View Custom Dashboards | |
-->

### Adobe Experience Platform資料收集權限

Adobe Experience Platform資料收集底下的權限可控制對標籤和事件轉送功能（包括屬性、擴充功能和環境）的存取。 如需設定Adobe Experience Platform資料收集權限的步驟，請參閱 [下文](#manage).

| 類別 | 權限 | 說明 |
| --- | --- | --- |
| 平台 | Web | 授予 [網站屬性](../tags/ui/administration/companies-and-properties.md) 與其他屬性權利結合時。 |
| 平台 | 行動 | 授予 [行動屬性](../tags/ui/administration/companies-and-properties.md) 與其他屬性權利結合時。 |
| 屬性 | (不適用) | 您可以透過Admin Console中的此權限類別，控制對每個屬性的存取，具體取決於您組織下建立的屬性。<br><br>用戶的已分配屬性權限僅適用於通過此權限類別授予其訪問權限的屬性。 |
| 屬性權利 | 核准 | 授予核准程式庫組建的能力，作為 [發佈流程](../tags/ui/publishing/publishing-flow.md). |
| 屬性權利 | 開發 | 授予開發程式庫組建的能力，作為 [發佈流程](../tags/ui/publishing/publishing-flow.md). |
| 屬性權利 | 編輯屬性 | 授予編輯使用者有權存取之屬性之基本設定的能力。 |
| 屬性權利 | 管理環境 | 授予管理 [環境](../tags/ui/publishing/environments.md) 針對使用者有權存取的屬性。 |
| 屬性權利 | 管理擴充功能 | 授予管理 [擴充功能](../tags/ui/managing-resources/extensions/overview.md) 針對使用者有權存取的屬性。 |
| 屬性權利 | 發佈 | 授予發佈程式庫組建的能力，作為 [發佈流程](../tags/ui/publishing/publishing-flow.md). |
| 公司權利 | 開發擴充功能 | 授予建立和修改您組織擁有的擴充功能套件的能力，包括私人發行和公開發行請求。 |
| 公司權利 | 管理擴充功能 | 只有在您擁有Adobe Journey Optimizer的授權，或其他授予行動應用程式內及推送訊息存取權的解決方案，才適用此權限。 這可讓您管理Adobe Experience Cloud所知的應用程式，以及與Firebase雲端訊息服務和Apple推播通知服務通訊所需的必要推播憑證。 |

{style="table-layout:auto"}

>[!NOTE]
>
>如需這些權限如何影響標籤中功能的詳細資訊，包括常見案例的管理策略，請參閱上的標籤檔案 [使用者權限](../tags/ui/administration/user-permissions.md).

## 管理權限 {#manage}

如前一節所述，資料收集的權限是透過Admin Console中的兩個產品名稱管理： **Adobe Experience Platform** 和 **Adobe Experience Platform資料收集**.

若要管理這些權限，請登入 [Admin Console](https://adminconsole.adobe.com/) 選取 **[!UICONTROL 產品]** ，即可取得Advertising Cloud的說明。 從此處，選取您要設定之權限的產品卡片。 如需如何管理Admin Console中每個產品下的相關權限的步驟，請參閱以下子區段：

* [Adobe Experience Platform權限](#manage-platform)
* [Adobe Experience Platform資料收集權限](#manage-collection)

### 在Adobe Experience Platform下管理權限 {#manage-platform}

從 **[!UICONTROL 產品]** 在Admin Console中查看，選擇 **[!UICONTROL Adobe Experience Platform資料收集]**. 選取您要編輯的產品設定檔，然後導覽至 **[!UICONTROL 權限]** 標籤。

若要存取資料收集功能，您必須在 **[!UICONTROL 沙箱]**, **[!UICONTROL 資料模型]**, **[!UICONTROL Identity Management]**，和 **[!UICONTROL 資料收集]** 類別。

![顯示資料收集產品卡的影像，Admin Console](./images/permissions/platform-permission-card.png)

請參閱 [存取控制UI指南](../access-control/ui/overview.md) 以取得管理平台權限的詳細指示。

>[!NOTE]
>
>視貴組織可存取的產品SKU而定，您可能沒有所有可用的平台權限。

### 在Adobe Experience Platform資料收集下管理權限 {#manage-collection}

從 **[!UICONTROL 產品]** 在Admin Console中查看，選擇 **[!UICONTROL Adobe Experience Platform資料收集]**.

![顯示資料收集產品卡的影像，Admin Console](./images/permissions/data-collection-card.png)

#### 選取或建立產品設定檔

下一個畫面顯示貴組織下資料收集的可用產品設定檔清單，預設設定檔為 **[!DNL Default Data Collection All Access]**. 您可以視需要選擇編輯預設的產品設定檔，或選取 **[!UICONTROL 新設定檔]** 來建立。 如果貴組織中有多個角色或使用者群組，需要不同的存取層級，您應分別為每個角色或使用者群組建立產品設定檔。

![影像顯示資料收集中的產品設定檔Admin Console](./images/permissions/new-profile.png)

選取或建立產品設定檔後，您可以使用 **[!UICONTROL 編輯]** 表徵圖開始 [編輯權限](#edit-permissions) ，或選取 **[!UICONTROL 使用者]** 標籤開始 [指派使用者](#assign-users) 至設定檔。

![顯示產品設定檔Admin Console的權限標籤的影像](./images/permissions/edit-permission-categories.png)

#### 編輯產品設定檔的權限 {#edit-permissions}

編輯設定檔的權限時，可用權限會列在左欄中，而包含在設定檔中的權限則會列在右欄中。 選取列出的權限，以在任一欄之間移動。

![影像顯示在包含的欄下方新增的權限](./images/permissions/added-permissions.png)

權限可分為幾類。 若要在類別之間切換，請從左側導覽中選取所需的類別。

![在權限下顯示公司權限區段的影像](./images/permissions/switch-category.png)

選擇 **[!UICONTROL 儲存]** 權限設定完成後。

![顯示為產品設定檔儲存之權限設定的影像](./images/permissions/save-permissions.png)

產品設定檔檢視會重新顯示，並反映新增的權限。

![顯示產品設定檔新增權限的影像](./images/permissions/permissions-added.png)

#### 將使用者指派至產品設定檔 {#assign-users}

若要將使用者指派至產品設定檔（並授與設定檔的設定權限），請選取 **[!UICONTROL 使用者]** 標籤，後面 **[!UICONTROL 新增使用者]**.

![影像顯示Admin Console中產品設定檔的使用者索引標籤](./images/permissions/manage-users.png)

如需管理產品設定檔使用者的詳細資訊，請參閱 [Admin Console檔案](https://helpx.adobe.com/tw/enterprise/using/manage-product-profiles.html).

## 後續步驟

本指南說明資料收集的可用權限，以及如何透過Admin Console管理這些權限。 如需管理其他Adobe Experience Platform功能權限的詳細資訊，請參閱 [存取控制檔案](../access-control/home.md).
