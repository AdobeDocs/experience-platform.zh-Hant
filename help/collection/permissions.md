---
title: Experience Platform中資料收集的許可權管理
description: 有關如何在Adobe Experience Platform中管理許可權和控制資料收集功能存取的高級概觀。
exl-id: 8426d54b-ec1d-475a-a769-f45a8c924fe7
source-git-commit: 3d0f2823dcf63f25c3136230af453118c83cdc7e
workflow-type: tm+mt
source-wordcount: '1274'
ht-degree: 29%

---

# Experience Platform中資料收集的許可權管理

[Adobe Experience Platform中的資料彙集](./home.md) 由數種不同的技術組成，可共同合作收集及傳輸您的資料。 這些技術的存取權可透過Adobe Admin Console中精細的角色型許可權來控制。

本指南說明如何管理資料收集功能的許可權。

## 快速入門

若要設定資料收集的存取控制，您必須擁有與Adobe Experience Platform Data Collection產品整合之組織的管理員許可權。 若要能授予或撤回權限，至少要擁有&#x200B;**產品設定檔管理員**&#x200B;的角色。其他可管理權限的管理員角色為&#x200B;**產品管理員** (可管理產品內的所有設定檔) 和&#x200B;**系統管理員** (沒有任何限制)。如需詳細資訊，請參閱 Adobe 企業版管理指南中有關[管理角色](https://helpx.adobe.com/enterprise/using/admin-roles.html)的文章。

本指南假設您熟悉基本的 Admin Console 概念，例如產品設定檔以及它們如何授予個別使用者和群組產品權限。如需詳細資訊，請參閱 [Admin Console 使用手冊](https://helpx.adobe.com/tw/enterprise/using/admin-console.html)。

## 可用權限

透過Admin Console中的兩個產品指定來提供資料收集的相關許可權： **Adobe Experience Platform** 和 **Adobe Experience Platform資料彙集**. 以下各節概述每個產品下提供的許可權，以及這些許可權授予存取權的特定功能的說明。

### Adobe Experience Platform許可權

Adobe Experience Platform下的許可權包括存取資料串流、身分、結構描述和沙箱。 如需設定Adobe Experience Platform許可權的相關步驟，請參閱 [存取控制使用手冊](../access-control/ui/overview.md).

| 類別 | 權限 | 說明 |
| --- | --- | --- |
| 沙箱 | (不適用) | 根據 [沙箱](../sandboxes/home.md) 如果您已在組織下建立，則可以透過Admin Console中的此許可權類別控制對每一個的存取。 |
| 資料模型製作 | 管理結構描述 | 授予檢視、建立和編輯的能力 [體驗資料模型(XDM)結構描述](../xdm/home.md). |
| 資料模型製作 | 檢視結構描述 | 授予結構描述的唯讀存取權。 |
| Identity Management | 管理身分識別命名空間 | 授予檢視、建立和編輯的能力 [身分名稱空間](../identity-service/namespaces.md). |
| Identity Management | 檢視身分命名空間 | 授予識別名稱空間的唯讀存取權。 |
| 資料集合 | 管理資料串流 | 授予檢視、建立和編輯的能力 [資料串流](../datastreams/overview.md). |
| 資料集合 | 檢視資料串流 | 授予資料串流的唯讀存取權。 |

{style="table-layout:auto"}

### Adobe Experience Platform資料收集許可權

Adobe Experience Platform資料收集下的許可權可控制對標籤和事件轉送功能（包括屬性、擴充功能和環境）的存取。 如需設定Adobe Experience Platform資料收集許可權的相關步驟，請參閱 [以下區段](#manage).

| 類別 | 權限 | 說明 |
| --- | --- | --- |
| 平台 | Web | 授予存取權 [Web屬性](../tags/ui/administration/companies-and-properties.md) 與其他屬性權利結合時。 |
| 平台 | 行動 | 授予存取權 [行動屬性](../tags/ui/administration/companies-and-properties.md) 與其他屬性權利結合時。 |
| 平台 | Edge | 授予存取權 [事件轉送邊緣屬性](../tags/ui/event-forwarding/getting-started.md) 與其他屬性權利結合時。 |
| 屬性 | (不適用) | 根據已在您的組織下建立的屬性，您可以透過Admin Console中的此許可權類別控制對每一個屬性的存取。<br><br>使用者的指派屬性許可權僅適用於他們透過此許可權類別被授予存取權的屬性。 |
| 屬性權利 | 核准 | 授予核准程式庫組建的能力，使其成為 [發佈流程](../tags/ui/publishing/publishing-flow.md). |
| 屬性權利 | 開發 | 授予開發程式庫組建作為一部分的能力 [發佈流程](../tags/ui/publishing/publishing-flow.md). |
| 屬性權利 | 編輯屬性 | 授予編輯使用者有權存取之屬性的基本設定的能力。 |
| 屬性權利 | 管理環境 | 授予管理 [環境](../tags/ui/publishing/environments.md) 使用者有權存取的屬性。 |
| 屬性權利 | 管理擴充功能 | 授予管理 [擴充功能](../tags/ui/managing-resources/extensions/overview.md) 使用者有權存取的屬性。 |
| 屬性權利 | 發佈 | 授予將程式庫組建發佈為 [發佈流程](../tags/ui/publishing/publishing-flow.md). |
| 公司權利 | 開發擴充功能 | 授予建立及修改組織擁有的擴充功能套件的能力，包括私人發行和公開發行請求。 |
| 公司權利 | 管理擴充功能 | 此許可權僅適用於您擁有Adobe Journey Optimizer或其他解決方案的授權，可授予行動應用程式內及推送訊息存取權時。 這可讓您管理Adobe Experience Cloud知道的應用程式，以及與Firebase Cloud Messaging服務和Apple推播通知服務通訊所需的推播認證。 |

{style="table-layout:auto"}

>[!NOTE]
>
>如需這些許可權如何影響標籤中功能的詳細資訊，包括常見情境的管理策略，請參閱標籤檔案： [使用者許可權](../tags/ui/administration/user-permissions.md).

## 管理權限 {#manage}

資料收集的許可權透過兩個產品名稱管理： **Adobe Experience Platform** 和 **Adobe Experience Platform資料彙集**.

如需如何管理Admin Console中每個產品下相關許可權的步驟，請參閱以下小節：

* [Adobe Experience Platform許可權](#manage-platform)
* [Adobe Experience Platform資料收集許可權](#manage-collection)

### 在Adobe Experience Platform下管理許可權 {#manage-platform}

從 **[!UICONTROL 許可權]** Adobe Experience Platform區域，選取您要編輯的角色。

若要存取資料收集功能，您必須啟用 **[!UICONTROL 沙箱]**， **[!UICONTROL 資料模型]**， **[!UICONTROL Identity Management]**、和 **[!UICONTROL 資料彙集]** 類別。

![以Admin Console顯示資料收集產品卡的影像](./images/permissions/platform-permission-card.png)

請參閱 [存取控制UI指南](../access-control/ui/overview.md) 以取得管理Platform許可權的詳細說明。

>[!NOTE]
>
>根據您的組織有權存取的產品SKU，您可能沒有每個可用的平台許可權。

### 在Adobe Experience Platform資料收集下管理許可權 {#manage-collection}

若要管理這些許可權，請登入「Admin Console」並選取 **[!UICONTROL 產品]** 在頂端導覽列中，然後選取 **[!UICONTROL Adobe Experience Platform資料彙集]**.

![以Admin Console顯示資料收集產品卡的影像](./images/permissions/data-collection-card.png)

#### 選取或建立產品設定檔

下一個畫面顯示貴組織下資料收集的可用產品設定檔清單，預設設定檔為 **[!DNL Default Data Collection All Access]**. 您可以視需要選擇編輯預設的產品設定檔，也可以選擇 **[!UICONTROL 新設定檔]** 以建立一個。 如果您在貴組織中有多個角色或使用者群組，而這些需要不同層級的存取權限，則應為每個角色或使用者建立單獨的產品設定檔。

![顯示Admin Console中資料收集的產品設定檔的影像](./images/permissions/new-profile.png)

選取或建立產品設定檔後，您可以使用 **[!UICONTROL 編輯]** 要開始的圖示 [編輯許可權](#edit-permissions) ，或選取 **[!UICONTROL 使用者]** 索引標籤以開始 [指派使用者](#assign-users) 至設定檔。

![顯示產品設定檔 Admin Console 的權限索引標籤的影像](./images/permissions/edit-permission-categories.png)

#### 編輯產品設定檔的許可權 {#edit-permissions}

編輯設定檔的權限時，可用權限會顯示在左欄的清單中，而設定檔中包含的權限則會顯示在右欄的清單中。選取清單中的權限在任一欄之間移動。

![此影像顯示新增至包含欄下的許可權](./images/permissions/added-permissions.png)

將權限歸類到不同類別。若要在類別之間切換，請從左側導覽中選取所需的類別。

![此影像顯示許可權底下的公司許可權區段](./images/permissions/switch-category.png)

完成設定權限後，即可選取「**[!UICONTROL 儲存]**」。

![顯示已儲存的產品設定檔權限設定的影像](./images/permissions/save-permissions.png)

產品設定檔檢視會重新顯示，並新增所反映的權限。

![顯示產品設定檔新增權限的影像](./images/permissions/permissions-added.png)

#### 將使用者指派至產品設定檔 {#assign-users}

若要將使用者指派至產品設定檔 (並授予他們設定檔的設定權限)，請選取「**[!UICONTROL 使用者]**」索引標籤，接著選取「**[!UICONTROL 新增使用者]**」。

![顯示 Admin Console 中產品設定檔的使用者索引標籤的影像](./images/permissions/manage-users.png)

如需有關如何管理產品設定檔的使用者的詳細資訊，請參閱 [Admin Console 文件](https://helpx.adobe.com/tw/enterprise/using/manage-product-profiles.html)。

## 後續步驟

本指南說明資料收集的可用許可權，以及如何透過Admin Console管理這些許可權。 如需有關如何管理其他 Adob&#x200B;&#x200B;e Experience Platform 功能的權限的詳細資訊，請參閱[存取控制文件](../access-control/home.md)。
