---
keywords: Experience Platform；主題；熱門主題；訪問控制；基於屬性的訪問控制；ABAC
title: 基於屬性的訪問控制管理角色權限
description: 本檔案提供關於Adobe Experience Platform基於屬性的訪問控制的資訊
hide: true
hidefromtoc: true
exl-id: 8acd2bb6-eef8-4b23-8fd8-3566c7508fe7
source-git-commit: 19f1e8df8cd8b55ed6b03f80e42810aefd211474
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# 管理角色的權限

>[!IMPORTANT]
>
>基於屬性的訪問控制目前在面向美國醫療保健客戶的有限版本中提供。 這一功能一旦完全發佈，將可供所有Real-time Customer Data Platform客戶使用。

緊接著 [建立新角色](#create-a-new-role)，則返回 **[!UICONTROL 角色]** 頁籤。 如果正在編輯現有角色的權限，請從 **[!UICONTROL 角色]** 頁籤。 或者，使用篩選器選項篩選結果以查找角色。

## 篩選角色

選擇漏斗表徵圖(![「篩選器」表徵圖](../../images/icon.png))以顯示篩選器控制項清單，以幫助縮小結果範圍。

![flac濾波器](../../images/flac-ui/flac-filters.png)

以下篩選器可用於UI中的角色：

| 篩選 | 說明 |
| --- | --- |
| [!UICONTROL 建立時間] | 選擇起始日期和/或終止日期以定義日期範圍以篩選結果。 |
| [!UICONTROL 建立者] | 通過從下拉清單中選擇用戶按角色建立者篩選。 |
| [!UICONTROL 修改時間] | 選擇起始日期和/或終止日期以定義日期範圍以篩選結果。 |
| [!UICONTROL 修改者] | 通過從下拉清單中選擇用戶按角色修改量篩選。 |

要刪除濾鏡，請為有關的濾鏡選擇「X」，或選擇 **[!UICONTROL 全部清除]** 按鈕，將選定控制項在Tab鍵次序中下移一個位置。

![flac清除濾波器](../../images/flac-ui/flac-clear-filters.png)

## 角色詳細資訊

從 **[!UICONTROL 角色]** 的子菜單。

![flac細節](../../images/flac-ui/flac-details.png)

「詳細資訊」(Details)頁籤提供角色的概述。 概覽顯示角色名稱、角色說明、建立和修改角色的用戶名、建立和修改角色的時間以及附加到角色的權限。 如果需要，可以修改角色名稱和角色說明。

## 管理角色的標籤

選擇 **[!UICONTROL 標籤]** 頁籤，然後選擇 **[!UICONTROL 添加標籤]** 為角色分配標籤。

![flac標籤](../../images/flac-ui/flac-labels.png)

標籤列在此頁上。 該清單顯示標籤名稱、友好名稱、類別及其說明。

從要添加到角色的清單中選擇標籤，然後選擇 **[!UICONTROL 保存]**

![flac-add-labels](../../images/flac-ui/flac-add-labels.png)

添加的標籤顯示在 **[!UICONTROL 標籤]** 頁籤。

![添加了flac標籤](../../images/flac-ui/flac-added-labels.png)

要從角色中刪除標籤，請選擇 **X** 表徵圖。

![flac-delete-labels](../../images/flac-ui/flac-delete-labels.png)

## 管理角色的沙箱

選擇 **[!UICONTROL 沙箱]** 頁籤。 在這裡，您可以看到添加到角色的沙箱清單。

![黃沙箱](../../images/flac-ui/flac-sandboxes.png)

要向角色添加更多沙箱，請選擇 **[!UICONTROL 編輯]**。

![加層沙箱](../../images/flac-ui/flac-add-sandboxes.png)

下一個螢幕將提示您選擇沙箱中存在的資源權限，以便使用下拉清單在角色中包括。 完成後，選擇 **[!UICONTROL 保存並退出]**。

![flac-add-role-permission](../../images/flac-ui/flac-add-role-permission.png)

## 管理角色的用戶

選擇 **[!UICONTROL 用戶]** 頁籤開啟「角色用戶」頁，然後選擇 **[!UICONTROL 添加用戶]** 為角色分配用戶。

![flac用戶](../../images/flac-ui/flac-users.png)

從要添加到角色的清單中選擇用戶。 或者，使用搜索欄通過輸入用戶姓名或電子郵件地址來搜索用戶，然後選擇 **[!UICONTROL 保存]**

![flac-add用戶](../../images/flac-ui/flac-add-users.png)

添加的用戶顯示在 **[!UICONTROL 用戶]** 頁籤。

![增層用戶](../../images/flac-ui/flac-added-users.png)

要從角色中刪除用戶，請選擇 **X** 表徵圖。

![flac刪除用戶](../../images/flac-ui/flac-remove-users.png)

## 管理角色的API憑據

選擇 **[!UICONTROL API憑據]** 頁籤開啟「角色API憑據」頁，然後選擇 **[!UICONTROL 添加API憑據]** 為角色分配API憑據。

![flac-api憑據](../../images/flac-ui/flac-api-credentials.png)

從要添加到角色的清單中選擇API憑據，然後選擇 **[!UICONTROL 保存]**

![flac-add-api-credentials](../../images/flac-ui/flac-add-api-credentials.png)

添加的API憑據顯示在 **[!UICONTROL API憑據]** 頁籤。

![flac添加的api — 憑據](../../images/flac-ui/flac-added-api-credentials.png)

要從角色中刪除API憑據，請選擇 **X** 表徵圖。

![flac-remove-api-credentials](../../images/flac-ui/flac-remove-api-credentials.png)

的 **[!UICONTROL 刪除API憑據]** 對話框，提示您確認刪除。

![flac-confirm-api-credentials-delete](../../images/flac-ui/flac-confirm-api-credentials-delete.png)

您將返回 **[!UICONTROL API憑據]** 頁籤。

## 管理角色的用戶組

用戶組是多個已分組在一起並有權執行相同功能的用戶。

選擇 **[!UICONTROL 用戶組]** 頁籤開啟「角色」用戶組頁，然後選擇 **[!UICONTROL 添加組]** 將用戶組分配給角色。

![flac用戶組](../../images/flac-ui/flac-user-groups.png)

從要添加到角色的清單中選擇用戶組。 或者，使用搜索欄通過輸入組名稱搜索用戶組，然後選擇 **[!UICONTROL 保存]**

![flac-add-user-groups](../../images/flac-ui/flac-add-user-groups.png)

添加的用戶組顯示在 **[!UICONTROL 用戶組]** 頁籤。

![flac添加的用戶組](../../images/flac-ui/flac-added-user-groups.png)

要從角色中刪除用戶組，請選擇 **X** 表徵圖。

![flac-remove-user-groups](../../images/flac-ui/flac-remove-user-groups.png)

的 **[!UICONTROL 刪除用戶組]** 對話框，提示您確認刪除。

![flac-confirm用戶組 — delete](../../images/flac-ui/flac-confirm-user-groups-delete.png)

您將返回 **[!UICONTROL 用戶組]** 頁籤。

## 後續步驟

建立權限後，您可以繼續下一步， [管理用戶](users.md)。
