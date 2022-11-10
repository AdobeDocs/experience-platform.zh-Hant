---
keywords: Experience Platform；首頁；熱門主題；存取控制；基於屬性的存取控制；ABAC
title: 基於屬性的訪問控制建立策略
description: 本檔案提供有關透過Adobe Experience Cloud中的權限介面管理原則的資訊
exl-id: 66820711-2db0-4621-908d-01187771de14
source-git-commit: 1a755fa5480e036bde50617f01440cfabbaf64c2
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 0%

---

# 管理原則

政策是將屬性集合在一起，以制定允許和不允許的行動的聲明。 策略可以是本地策略或全局策略，也可以覆蓋其他策略。

## 建立新策略

要建立新策略，請選擇 **[!UICONTROL 原則]** 標籤，然後選取 **[!UICONTROL 建立原則]**.

![flac-new-policy](../../images/flac-ui/flac-new-policy.png)

此 **[!UICONTROL 建立新策略]** 對話框出現，提示您輸入名稱和可選說明。 完成後，請選取 **[!UICONTROL 確認]**.

![flac-create-new-policy](../../images/flac-ui/flac-create-new-policy.png)

使用下拉式箭頭，選取是否要 **允許存取** (![flac-permit-access-to](../../images/flac-ui/flac-permit-access-to.png))資源或 **拒絕訪問** (![flac-deny-access-to](../../images/flac-ui/flac-deny-access-to.png))資源。

接下來，使用下拉菜單和搜索訪問類型（讀或寫）選擇要包含在策略中的資源。

![flac-flac-policy-resource-down](../../images/flac-ui/flac-policy-resource-dropdown.png)

接下來，使用下拉箭頭選擇要應用於此策略的條件， **以下為true** (![flac-policy-true](../../images/flac-ui/flac-policy-true.png))或 **以下為false** (![flac-policy-false](../../images/flac-ui/flac-policy-false.png))。

選取加號圖示 **新增符合運算式** 或 **新增運算式群組** （針對資源）。

![flac-policy-expression](../../images/flac-ui/flac-policy-expression.png)

使用下拉式清單，選取 **資源**.

![flac-policy-resource-dolforming](../../images/flac-ui/flac-policy-resource-dropdown-1.png)

接下來，使用下拉式清單選取 **符合**.

![flac-policy-matches-down](../../images/flac-ui/flac-policy-matches-dropdown.png)

接下來，使用下拉式清單，選取標籤類型(**[!UICONTROL 核心標籤]** 或 **[!UICONTROL 自訂標籤]**)以符合指派給角色中使用者的標籤。

![flac-policy-user-dolforming](../../images/flac-ui/flac-policy-user-dropdown.png)

最後，選取 **沙箱** 使用下拉式功能表套用政策條件。

![flac-policy-sandbox-down](../../images/flac-ui/flac-policy-sandboxes-dropdown.png)

選擇 **新增資源** 以新增更多資源。 完成後，請選取 **[!UICONTROL 儲存並退出]**.

![flac-policy-save-and-exit](../../images/flac-ui/flac-policy-save-and-exit.png)

已成功建立新策略，並且會將您重定向到 **[!UICONTROL 原則]** 頁簽中，您將看到新建立的策略出現在清單中。

![flac-policy-saved](../../images/flac-ui/flac-policy-saved.png)

## 編輯策略

要編輯現有策略，請從 **[!UICONTROL 原則]** 標籤。 或者，使用篩選選項來篩選結果以查找要編輯的策略。

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

接下來，選取省略號(`…`)旁邊，下拉式清單會顯示編輯、停用、刪除或複製角色的控制項。 從下拉式清單中選取「編輯」 。

![flac-policy-edit](../../images/flac-ui/flac-policy-edit.png)

此時將顯示策略權限螢幕。 進行更新，然後選取 **[!UICONTROL 儲存並退出]**.

![flac-policy-save-and-exit](../../images/flac-ui/flac-policy-save-and-exit.png)

策略已成功更新，系統會將您重定向到 **[!UICONTROL 原則]** 標籤。

## 複製策略

要複製現有策略，請從 **[!UICONTROL 原則]** 標籤。 或者，使用篩選選項來篩選結果以查找要編輯的策略。

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

接下來，選取省略號(`…`)旁邊，下拉式清單會顯示編輯、停用、刪除或複製角色的控制項。 從下拉式清單中選取「複製」。

![flac-policy-duplicate](../../images/flac-ui/flac-policy-duplicate.png)

此 **[!UICONTROL 重複策略]** 對話框，提示您確認複製。

![flac-policy-duplicate-confirm](../../images/flac-ui/flac-duplicate-confirm.png)

新策略將作為原始策略的副本顯示在清單中， **[!UICONTROL 原則]** 標籤。

![flac-role-duplicate-saved](../../images/flac-ui/flac-role-duplicate-saved.png)

## 刪除策略

要刪除現有策略，請從 **[!UICONTROL 原則]** 標籤。 或者，使用篩選選項篩選結果，以查找要刪除的策略。

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

接下來，選取省略號(`…`)旁邊，下拉式清單會顯示編輯、停用、刪除或複製角色的控制項。 從下拉式清單中選取「刪除」 。

![flac-policy-delete](../../images/flac-ui/flac-policy-delete.png)

此 **[!UICONTROL 刪除用戶策略]** 對話框，提示您確認刪除。

![flac-policy-delete-confirm](../../images/flac-ui/flac-policy-delete-confirm.png)

您會回到 **[!UICONTROL 原則]** 標籤中，刪除確認彈出窗口隨即顯示。

![flac-policy-delete-confirmation](../../images/flac-ui/flac-policy-delete-confirmation.png)

## 啟用原則

要激活現有策略，請從 **[!UICONTROL 原則]** 標籤。 或者，使用篩選選項篩選結果，以查找要刪除的策略。

![flac-policy-select](../../images/flac-ui/flac-policy-select.png)

接下來，選取省略號(`…`)旁邊，下拉式清單會顯示編輯、啟用、刪除或複製角色的控制項。 從下拉式清單中選取「啟動」 。

![flac-policy-activate](../../images/flac-ui/flac-policy-delete.png)

此 **[!UICONTROL 激活用戶策略]** 對話框，提示您確認激活。

![flac-policy-activate-confirm](../../images/flac-ui/flac-policy-activate-confirm.png)

您會回到 **[!UICONTROL 原則]** 標籤上，並顯示確認啟動快顯視窗。 策略狀態顯示為活動狀態。

![flac策略激活](../../images/flac-ui/flac-policy-activated.png)

## 後續步驟

建立新策略後，您可以繼續執行 [管理角色的權限](permissions.md).
