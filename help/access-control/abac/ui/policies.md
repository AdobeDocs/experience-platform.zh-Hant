---
keywords: Experience Platform；主題；熱門主題；訪問控制；基於屬性的訪問控制；ABAC
title: 基於屬性的訪問控制建立策略
description: 本文檔提供有關通過Adobe Experience Cloud的「權限」介面管理策略的資訊
exl-id: 66820711-2db0-4621-908d-01187771de14
source-git-commit: 97b4b98a2f14e36e8e8c71bd2ab9631782bc333f
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 0%

---

# 管理策略

>[!IMPORTANT]
>
>基於屬性的訪問控制目前在面向美國醫療保健客戶的有限版本中提供。 這一功能一旦完全發佈，將可供所有Real-time Customer Data Platform客戶使用。

策略是將屬性集合在一起以建立允許和不允許的操作的語句。 策略可以是本地策略或全局策略，並且可以覆蓋其他策略。

## 建立新策略

要建立新策略，請選擇 **[!UICONTROL 策略]** 頁籤，然後選擇 **[!UICONTROL 建立策略]**。

![flac-newpolicy（新政策）](../../images/flac-ui/flac-new-policy.png)

的 **[!UICONTROL 建立新策略]** 對話框，提示您輸入名稱和可選說明。 完成後，選擇 **[!UICONTROL 確認]**。

![flac-create-new-policy(flac-create-new-policy)](../../images/flac-ui/flac-create-new-policy.png)

使用下拉箭頭選擇是否 **允許訪問** (![flac允許訪問](../../images/flac-ui/flac-permit-access-to.png))資源或 **拒絕訪問** (![flac-deny-access-to](../../images/flac-ui/flac-deny-access-to.png))資源。

接下來，使用下拉菜單和搜索訪問類型（讀或寫）選擇要包括在策略中的資源。

![flac-flac-policy-resource-dropdown](../../images/flac-ui/flac-policy-resource-dropdown.png)

接下來，使用下拉箭頭選擇要應用於此策略的條件， **以下為真** (![flac策略真](../../images/flac-ui/flac-policy-true.png))或 **以下為false** (![flac策略錯誤](../../images/flac-ui/flac-policy-false.png))。

選擇加號表徵圖 **添加匹配表達式** 或 **添加表達式組** 的子菜單。

![flac策略表達](../../images/flac-ui/flac-policy-expression.png)

使用下拉清單，選擇 **資源**。

![flac-policy-resource-dropf](../../images/flac-ui/flac-policy-resource-dropdown-1.png)

接下來，使用下拉清單選擇 **匹配項**。

![flac-policy-matches-dropdown](../../images/flac-ui/flac-policy-matches-dropdown.png)

接下來，使用下拉清單選擇 **用戶**。

![flac-policy-user-dropf](../../images/flac-ui/flac-policy-user-dropdown.png)

最後，選擇 **沙盒** 使用下拉菜單來應用策略條件。

![flac-policy-sandbox-dropdown](../../images/flac-ui/flac-policy-sandboxes-dropdown.png)

選擇 **添加資源** 添加更多資源。 完成後，選擇 **[!UICONTROL 保存並退出]**。

![flac策略保存和退出](../../images/flac-ui/flac-policy-save-and-exit.png)

已成功建立新策略，並將您重定向到 **[!UICONTROL 策略]** 頁籤，您將看到新建立的策略出現在清單中。

![flac策略保存](../../images/flac-ui/flac-policy-saved.png)

## 編輯策略

要編輯現有策略，請從 **[!UICONTROL 策略]** 頁籤。 或者，使用篩選選項篩選結果以查找要編輯的策略。

![flac策略選擇](../../images/flac-ui/flac-policy-select.png)

接下來，選擇省略號(`…`)旁邊，下拉清單將顯示編輯、停用、刪除或複製角色的控制項。 從下拉清單中選擇「編輯」。

![flac策略編輯](../../images/flac-ui/flac-policy-edit.png)

出現策略權限螢幕。 進行更新，然後選擇 **[!UICONTROL 保存並退出]**。

![flac策略保存和退出](../../images/flac-ui/flac-policy-save-and-exit.png)

策略已成功更新，您將重定向到 **[!UICONTROL 策略]** 頁籤。

## 複製策略

要複製現有策略，請從 **[!UICONTROL 策略]** 頁籤。 或者，使用篩選選項篩選結果以查找要編輯的策略。

![flac策略選擇](../../images/flac-ui/flac-policy-select.png)

接下來，選擇省略號(`…`)旁邊，下拉清單將顯示編輯、停用、刪除或複製角色的控制項。 從下拉清單中選擇「重複」。

![flac策略複製](../../images/flac-ui/flac-policy-duplicate.png)

的 **[!UICONTROL 重複策略]** 對話框，提示您確認複製。

![flac-policy-duplicate-confirm](../../images/flac-ui/flac-duplicate-confirm.png)

新策略將作為源策略的副本顯示在 **[!UICONTROL 策略]** 頁籤。

![flac-role-duplicate-saved](../../images/flac-ui/flac-role-duplicate-saved.png)

## 刪除策略

要刪除現有策略，請從 **[!UICONTROL 策略]** 頁籤。 或者，使用篩選選項篩選結果以查找要刪除的策略。

![flac策略選擇](../../images/flac-ui/flac-policy-select.png)

接下來，選擇省略號(`…`)旁邊，下拉清單將顯示編輯、停用、刪除或複製角色的控制項。 從下拉清單中選擇「刪除」。

![flac策略刪除](../../images/flac-ui/flac-policy-delete.png)

的 **[!UICONTROL 刪除用戶策略]** 對話框，提示您確認刪除。

![flac-policy-delete-confirm](../../images/flac-ui/flac-policy-delete-confirm.png)

您返回 **[!UICONTROL 策略]** 的子菜單。

![flac-policy-delete-confirmation（flac-policy — 刪除確認）](../../images/flac-ui/flac-policy-delete-confirmation.png)

## 激活策略

要激活現有策略，請從 **[!UICONTROL 策略]** 頁籤。 或者，使用篩選選項篩選結果以查找要刪除的策略。

![flac策略選擇](../../images/flac-ui/flac-policy-select.png)

接下來，選擇省略號(`…`)旁邊，下拉清單顯示用於編輯、激活、刪除或複製角色的控制項。 從下拉清單中選擇「激活」。

![flac策略激活](../../images/flac-ui/flac-policy-delete.png)

的 **[!UICONTROL 激活用戶策略]** 對話框，提示您確認激活。

![flac策略激活 — 確認](../../images/flac-ui/flac-policy-activate-confirm.png)

您返回 **[!UICONTROL 策略]** 的子菜單。 策略狀態顯示為活動狀態。

![flac策略激活](../../images/flac-ui/flac-policy-activated.png)

## 後續步驟

建立新策略後，您可以繼續執行下一步 [管理角色的權限](permissions.md)。
