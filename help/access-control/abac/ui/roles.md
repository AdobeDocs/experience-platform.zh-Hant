---
keywords: Experience Platform；首頁；熱門主題；存取控制；基於屬性的存取控制；ABAC
title: 基於屬性的訪問控制建立角色
description: 本檔案提供有關透過Adobe Experience Cloud中的權限介面管理角色的資訊
exl-id: 85699716-339d-4992-8390-95563c7ea7fe
source-git-commit: 9e44e647e4647a323fa9d1af55266d6f32b5ccb9
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 0%

---

# 管理角色

角色定義管理員、專家或一般使用者對您組織中資源的存取權。 在基於角色的訪問控制環境中，用戶訪問配置是通過共同的責任和需求進行分組的。 角色具有一組指定的權限，而您組織的成員可以根據其所需的檢視或寫入存取範圍，指派給一或多個角色。

## 建立新角色

若要建立新角色，請選取 **[!UICONTROL 角色]** 標籤，然後選取 **[!UICONTROL 建立角色]**.

![flac-new-role](../../images/flac-ui/flac-new-role.png)

此 **[!UICONTROL 建立新角色]** 對話框出現，提示您輸入名稱和可選說明。

完成後，請選取 **[!UICONTROL 確認]**.

![flac-create-new role](../../images/flac-ui/flac-create-new-role.png)

接下來，使用下拉式功能表，選取您要納入角色的資源權限。

![flac-add-role-permission](../../images/flac-ui/flac-add-role-permission.png)

若要新增其他資源，請選取 **[!UICONTROL Adobe Experience Platform]** 從左側導覽面板，其中顯示資源清單。 或者，在左側導覽面板的搜尋列中輸入資源名稱。

![flac-add-additional-resources](../../images/flac-ui/flac-add-additional-resources.png)

按一下並拖曳相關資源，並拖曳至主面板。

![flac-additional-resources-added](../../images/flac-ui/flac-additional-resources-added.png)

使用下拉式功能表，選取您要納入角色的資源權限。 對您要包含該角色的所有資源重複執行此操作。 完成後，請選取 **[!UICONTROL 儲存並退出]**.

![flac-save-resources](../../images/flac-ui/flac-save-resources.png)

新角色已成功建立，系統會將您重新導向至 **[!UICONTROL 角色]** 頁面中，新建立的角色將出現在清單中。

![flac-role-saved](../../images/flac-ui/flac-role-saved.png)

請參閱 [管理角色的權限](#manage-permissions-for-a-role) 有關建立角色權限後如何管理這些權限的詳細資訊。

## 複製角色

若要複製現有角色，請從 **[!UICONTROL 角色]** 標籤。 或者，使用篩選選項來篩選結果，以尋找您要複製的角色。

![flac-duplicate-role](../../images/flac-ui/flac-duplicate-role.png)

下一步，選擇 **[!UICONTROL 複製]** 從畫面右上角。

![flac-duplicate](../../images/flac-ui/flac-duplicate.png)

此 **[!UICONTROL 重複角色]** 對話框，提示您確認複製。

![flac-duplicate-confirm](../../images/flac-ui/flac-duplicate-confirm.png)

接下來，您將進入角色的詳細資訊頁面，您可在此變更角色的名稱和權限。 詳細資料、標籤和沙箱會與先前角色重複。 需要透過「使用者」索引標籤來新增使用者。 您可以檢視 [管理角色的權限](permissions.md) 檔案，以進一步了解如何將詳細資料、標籤、沙箱和使用者新增至角色。

按一下左箭頭以返回 **[!UICONTROL 角色]** 標籤。

![flac-return-to-roles](../../images/flac-ui/flac-return-to-roles.png)

新角色會出現在 **[!UICONTROL 角色]** 頁面。

![flac-role-duplicate-saved](../../images/flac-ui/flac-role-duplicate-saved.png)

## 刪除角色

選取省略號(`…`)旁邊，下拉式清單會顯示編輯、刪除或複製角色的控制項。 從下拉式清單中選取「刪除」 。

![flac-role-delete](../../images/flac-ui/flac-role-delete.png)

此 **[!UICONTROL 刪除用戶角色]** 對話框，提示您確認刪除。

![flac-confirm-role-delete](../../images/flac-ui/flac-confirm-role-delete.png)

您將會返回 **[!UICONTROL 角色]** 標籤。

## 後續步驟

建立新角色後，您可以繼續進行下一個步驟： [管理角色的權限](permissions.md).
