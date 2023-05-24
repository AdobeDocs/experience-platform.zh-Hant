---
keywords: Experience Platform；主題；熱門主題；訪問控制；基於屬性的訪問控制；ABAC
title: 基於屬性的訪問控制管理角色權限
description: 本文檔提供有關通過Adobe Experience Cloud的「權限」介面配置角色權限的資訊
exl-id: 8acd2bb6-eef8-4b23-8fd8-3566c7508fe7
source-git-commit: 9515527f5a2c250b0a9057aa37769431e3b6fa07
workflow-type: tm+mt
source-wordcount: '966'
ht-degree: 4%

---

# 管理角色的權限

>[!IMPORTANT]
>
>訪問控制使用用戶ID（分配給用戶的內部唯一ID）授予權限。 當組織從Adobe ID遷移到業務ID時，其用戶設定的所有權限都將丟失，因為用戶ID更改，訪問控制將使用新生成的用戶ID。 如果您的組織已遷移到業務ID，請與Adobe代表聯繫，將您的用戶ID從Adobe ID遷移到業務ID。

權限是Experience Cloud區域，管理員可以在該區域定義用戶角色和訪問策略，以管理產品應用程式中功能和對象的訪問權限。

透過 權限，您可以建立和管理角色，並為這些角色指派所需的資源權限。 權限也可讓您管理與特定角色相關聯的標籤、沙箱和使用者。

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

![flac-confirm-user-groups-delete](../../images/flac-ui/flac-confirm-user-groups-delete.png)

您將返回 **[!UICONTROL 用戶組]** 頁籤。

## 通過產品配置檔案向Experience Platform添加用戶

要將用戶添加到產品配置檔案，請登錄到Admin Console並選擇 **[!UICONTROL 添加用戶]**

![product-profile-add用戶](../../images/flac-ui/product-profile-add-users.png)

的 **[!UICONTROL 將用戶添加到團隊]** 對話框。 輸入用戶電子郵件地址、名（可選）和姓氏（可選）。

選擇鉛筆表徵圖以選擇產品和用戶組，選擇 **[!UICONTROL Adobe Experience Platform]**，然後選擇 **[!UICONTROL AEP — 預設 — 所有用戶]**，然後選擇  **[!UICONTROL 保存]**。

![產品概要](../../images/flac-ui/product-profile.png)

## 後續步驟

建立權限後，您可以繼續下一步， [管理用戶](users.md)。
