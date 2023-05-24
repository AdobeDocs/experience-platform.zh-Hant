---
keywords: Experience Platform；主題；熱門主題；訪問控制；基於屬性的訪問控制；ABAC
title: 基於屬性的訪問控制建立角色
description: 本文檔提供有關通過Adobe Experience Cloud的「權限」介面管理角色的資訊
exl-id: 85699716-339d-4992-8390-95563c7ea7fe
source-git-commit: 9e44e647e4647a323fa9d1af55266d6f32b5ccb9
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 7%

---

# 管理角色

角色定義管理員、專家或最終用戶對您組織中的資源的訪問權限。 在基於角色的訪問控制環境中，用戶訪問設定是通過共同的責任和需要進行分組的。 一個角色具有一組給定的權限，您的組織成員可以指派到一個或多個角色，依據他們需要的視圖範圍或寫入權限而定。

## 建立新角色

要建立新角色，請選擇 **[!UICONTROL 角色]** 頁籤，然後選擇 **[!UICONTROL 建立角色]**。

![新角色](../../images/flac-ui/flac-new-role.png)

的 **[!UICONTROL 建立新角色]** 對話框，提示您輸入名稱和可選說明。

完成後，選擇 **[!UICONTROL 確認]**。

![flac-create-new-role](../../images/flac-ui/flac-create-new-role.png)

接下來，使用下拉菜單選擇要包括在角色中的資源權限。

![flac-add-role-permission](../../images/flac-ui/flac-add-role-permission.png)

要添加其他資源，請選擇 **[!UICONTROL Adobe Experience Platform]** 的子菜單。 或者，在左側導航面板的搜索欄中輸入資源名稱。

![flac-add附加資源](../../images/flac-ui/flac-add-additional-resources.png)

按一下並拖動相關資源，然後放入主面板。

![flac-addition-resources-added](../../images/flac-ui/flac-additional-resources-added.png)

使用下拉菜單選擇要包括在角色中的資源權限。 對要包括該角色的所有資源重複此步驟。 完成後，選擇 **[!UICONTROL 保存並退出]**。

![flac節約資源](../../images/flac-ui/flac-save-resources.png)

新角色已成功建立，您將重定向到 **[!UICONTROL 角色]** 的子菜單。

![角色保存](../../images/flac-ui/flac-role-saved.png)

請參閱 [管理角色的權限](#manage-permissions-for-a-role) 有關建立角色權限後如何管理角色權限的詳細資訊。

## 複製角色

要複製現有角色，請從 **[!UICONTROL 角色]** 頁籤。 或者，使用篩選選項篩選結果以查找要複製的角色。

![flac重複角色](../../images/flac-ui/flac-duplicate-role.png)

下一步，選擇 **[!UICONTROL 重複]** 從螢幕右上角開始。

![偽碼](../../images/flac-ui/flac-duplicate.png)

的 **[!UICONTROL 重複角色]** 對話框，提示您確認複製。

![flac-duplice-confirm](../../images/flac-ui/flac-duplicate-confirm.png)

接下來，您將轉到角色的詳細資訊頁面，在該頁面中可以更改角色的名稱和權限。 「詳細資訊」(Details)、「標籤」(Labels)和「沙箱」(Sandboxes)與上一個角色重複。 需要通過用戶頁籤添加用戶。 您可以查看 [管理角色的權限](permissions.md) 文檔，以瞭解有關將詳細資訊、標籤、沙箱和用戶添加到角色的詳細資訊。

按一下左箭頭返回 **[!UICONTROL 角色]** 頁籤。

![flac返回角色](../../images/flac-ui/flac-return-to-roles.png)

新角色將出現在 **[!UICONTROL 角色]** 的子菜單。

![flac-role-duplicate-saved](../../images/flac-ui/flac-role-duplicate-saved.png)

## 刪除角色

選擇省略號(`…`)旁邊，下拉清單將顯示編輯、刪除或複製角色的控制項。 從下拉清單中選擇「刪除」。

![flac角色刪除](../../images/flac-ui/flac-role-delete.png)

的 **[!UICONTROL 刪除用戶角色]** 對話框，提示您確認刪除。

![flac-confirm-role-delete](../../images/flac-ui/flac-confirm-role-delete.png)

您將返回 **[!UICONTROL 角色]** 頁籤。

## 後續步驟

建立新角色後，您可以繼續執行下一步操作 [管理角色的權限](permissions.md)。
