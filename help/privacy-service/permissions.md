---
title: 管理Privacy Service
description: 了解如何使用Adobe Admin Console管理Adobe Experience Platform Privacy Service的使用者權限。
exl-id: 6aa81850-48d7-4fff-95d1-53b769090649
source-git-commit: 37a67b19fa0cb38e9e34066c869dd9dc49edefd6
workflow-type: tm+mt
source-wordcount: '1064'
ht-degree: 1%

---

# 管理Privacy Service權限

>[!IMPORTANT]
>
>Adobe Experience Platform Privacy Service的權限已經過改良，以提升其精細度。 這些變更可讓組織管理員授予更多使用者所需角色和權限層級的存取權。 技術帳戶使用者必須更新其Privacy Service權限，因為此即將進行的更新對他們而言構成重大變更。 此權限變更的實施將在 **2023年3月28日**.
>
>技術帳戶可供企業客戶使用，並透過Adobe開發人員控制台建立。 技術帳戶持有人的Adobe ID終止於 `@techacct.adobe.com`. 如果您不確定自己是否是技術帳戶持有者，請聯絡您的組織管理員。

存取 [Adobe Experience Platform Privacy Service](./home.md) 是透過Adobe Admin Console中精細的角色型權限控制。 透過建立將權限指派給使用者群組的產品設定檔，您可以決定誰有權存取Privacy Service中的哪些功能 [UI](./ui/overview.md) 和 [API](./api/overview.md).

>[!NOTE]
>
>為Privacy ServiceAPI建立整合時，您必須選取現有的產品設定檔，才能判斷該整合具有權限的功能或動作。 請參閱 [開始使用Privacy ServiceAPI](./api/getting-started.md) 以取得更多資訊。

本指南會說明如何管理Privacy Service的權限。

## 快速入門

若要設定Privacy Service的存取控制，您必須擁有與Adobe Experience Platform Privacy Service產品整合之組織的管理員權限。 可授予或撤回權限的最低角色為 **產品設定檔管理員**. 可管理權限的其他管理員角色包括 **產品管理員** （可管理產品中的所有設定檔）和 **系統管理員** （無限制）。 請參閱 [管理角色](https://helpx.adobe.com/enterprise/using/admin-roles.html) (位於「Adobe企業管理指南」中)以取得詳細資訊。

本指南假設您熟悉產品設定檔等基本Admin Console概念，以及這些概念如何將產品權限授予個別使用者和群組。 如需詳細資訊，請參閱 [Admin Console使用手冊](https://helpx.adobe.com/tw/enterprise/using/admin-console.html).

## 可用權限

下表概述Privacy Service的可用權限，並說明其所授予存取權的特定功能：

| 類別 | 權限 | 說明 |
| --- | --- | --- |
| [!UICONTROL Privacy Service權限] | [!UICONTROL 隱私權讀取權限] | 判斷使用者是否可檢視現有的存取和刪除請求，以及其詳細資訊。 |
| [!UICONTROL Privacy Service權限] | [!UICONTROL 隱私權寫入權限] | 判斷使用者是否可以建立新的存取和刪除請求。 |
| [!UICONTROL Privacy Service權限] | [!UICONTROL 讀取（存取）內容傳送權限] | 當Privacy Service處理存取請求時，會傳送包含客戶資料的ZIP檔案給該客戶。 查詢存取請求的詳細資訊時，此權限會決定使用者是否可存取請求ZIP檔案的下載連結。 |
| [!UICONTROL 選擇退出銷售權限] | [!UICONTROL 閱讀權限 — 選擇退出銷售] | 判斷使用者是否可檢視現有的選擇退出銷售請求及其詳細資訊。 |
| [!UICONTROL 選擇退出銷售權限] | [!UICONTROL 寫入權限 — 選擇退出銷售] | 判斷使用者是否可以建立新的選擇退出銷售請求。 |

{style="table-layout:auto"}

## 管理權限 {#manage}

若要管理Privacy Service權限，請登入 [Admin Console](https://adminconsole.adobe.com/) 選取 **[!UICONTROL 產品]** ，即可取得Advertising Cloud的說明。 從此處，選擇 **[!UICONTROL Adobe Experience Platform Privacy Service]**.

![顯示Privacy Service產品卡的影像Admin Console](./images/permissions/privacy-service-card.png)

### 選取或建立產品設定檔

下一個畫面會顯示貴組織下可供Privacy Service的可用產品設定檔清單。 如果沒有產品設定檔，請選取 **[!UICONTROL 新設定檔]** 來建立。 如果貴組織中有多個角色或使用者群組，需要不同的存取層級，您應分別為每個角色或使用者群組建立產品設定檔。

![影像顯示Privacy Service中的產品設定檔](./images/permissions/select-or-create-profile.png)

選取產品設定檔後，您可以使用 **[!UICONTROL 權限]** 標籤開始 [編輯權限](#edit-permissions) ，或選取 **[!UICONTROL 使用者]** 標籤開始 [指派使用者](#assign-users) 至設定檔。

![顯示產品設定檔Admin Console的權限標籤的影像](./images/permissions/users-permissions-tabs.png)

### 編輯設定檔的權限 {#edit-permissions}

在 **[!UICONTROL 權限]** 頁簽，選擇任何顯示的權限類別以訪問權限編輯視圖。

編輯設定檔的權限時，可用權限會列在左欄中，而包含在設定檔中的權限則會列在右欄中。 選取列出的權限，以在任一欄之間移動。

![顯示可用和已包含權限欄的影像](./images/permissions/edit-permissions.png)

權限可分為幾類。 若要在類別之間切換，請從左側導覽中選取所需的類別。

![顯示 [!UICONTROL 選擇退出銷售] 「權限」一節](./images/permissions/switch-category.png)

選擇 **[!UICONTROL 儲存]** 權限設定完成後。

![顯示為產品設定檔儲存之權限設定的影像](./images/permissions/save-permissions.png)

產品設定檔檢視會重新顯示，並反映新增的權限。

![顯示產品設定檔新增權限的影像](./images/permissions/permissions-added.png)

### 將使用者指派至設定檔 {#assign-users}

若要將使用者指派至產品設定檔（並授與設定檔的設定權限），請選取 **[!UICONTROL 使用者]** 標籤，後面 **[!UICONTROL 新增使用者]**.

![影像顯示Admin Console中產品設定檔的使用者索引標籤](./images/permissions/manage-users.png)

如需管理產品設定檔使用者的詳細資訊，請參閱 [Admin Console檔案](https://helpx.adobe.com/tw/enterprise/using/manage-product-profiles.html).

### 將舊版API憑證移轉至設定檔 {#migrate-tech-accounts}

>[!NOTE]
>
>本節內容僅適用於在將Privacy Service權限整合至Adobe Admin Console之前建立的現有API憑證。 若為新憑證，會透過指派產品設定檔（及其權限） [Adobe Developer Console專案](https://developer.adobe.com/developer-console/docs/guides/projects/) 。<br><br>請參閱 [將產品設定檔指派給專案](./api/getting-started.md#product-profiles) (位於「Privacy ServiceAPI快速入門手冊」中)，以取得詳細資訊。

若要將舊版API憑證移轉至產品設定檔，請選取 **[!UICONTROL API憑證]**，後跟 **[!UICONTROL 新增API憑證]**.

![[!UICONTROL 新增API憑證] 在Admin Console中選取，位於 [!UICONTROL API憑證] 標籤](./images/permissions/api-credentials.png)

從清單中選擇所需的開發人員控制台專案，然後選取 **[!UICONTROL 儲存]** 將其新增至產品設定檔。 所有使用這些專案憑證的API呼叫都將繼承產品設定檔所授予的詳細權限。

## 後續步驟

本指南說明Privacy Service的可用權限，以及如何透過Admin Console管理這些權限。

如需設定產品設定檔後如何建立新API整合的步驟，請參閱 [Privacy ServiceAPI快速入門手冊](./api/getting-started.md). 如需管理其他Adobe Experience Platform功能權限的詳細資訊，請參閱 [存取控制檔案](../access-control/home.md).
