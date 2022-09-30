---
keywords: Experience Platform；首頁；熱門主題；存取控制；基於屬性的存取控制；ABAC
title: 基於屬性的訪問控制管理角色權限
description: 本檔案提供透過Adobe Experience Cloud中的權限介面來設定角色權限的相關資訊
exl-id: 8acd2bb6-eef8-4b23-8fd8-3566c7508fe7
source-git-commit: 9e44e647e4647a323fa9d1af55266d6f32b5ccb9
workflow-type: tm+mt
source-wordcount: '899'
ht-degree: 0%

---

# 管理角色的權限

>[!IMPORTANT]
>
>存取控制使用使用者ID（指派給使用者的內部唯一ID）來授予權限。 當組織從Adobe ID移轉至業務ID時，其使用者所設定的所有權限都會遺失，因為使用者ID變更且存取控制將使用新產生的使用者ID。 如果貴組織已移轉至Business ID，請連絡您的Adobe代表，將您的使用者ID從Adobe ID移轉至Business ID。

權限是管理員可在其中定義用戶角色和訪問策略，以管理產品應用程式中功能和對象的訪問權限的Experience Cloud區域。

您可以透過權限建立和管理角色，並為這些角色指派所需的資源權限。 權限也可讓您管理與特定角色相關聯的標籤、沙箱和使用者。

緊接在 [建立新角色](#create-a-new-role)，您會回到 **[!UICONTROL 角色]** 標籤。 如果您正在編輯現有角色的權限，請從 **[!UICONTROL 角色]** 標籤。 或者，使用篩選選項來篩選結果以尋找角色。

## 篩選角色

選取漏斗圖示(![篩選圖示](../../images/icon.png))以顯示篩選控制項清單，以縮小結果範圍。

![flac濾波器](../../images/flac-ui/flac-filters.png)

下列篩選器適用於UI中的角色：

| 篩選 | 說明 |
| --- | --- |
| [!UICONTROL 建立於] | 選取開始日期和/或結束日期，以定義要依據篩選結果的日期範圍。 |
| [!UICONTROL 建立者] | 從下拉式清單中選取使用者，依角色建立者篩選。 |
| [!UICONTROL 在] | 選取開始日期和/或結束日期，以定義要依據篩選結果的日期範圍。 |
| [!UICONTROL 修改者] | 從下拉式清單中選取使用者，依角色修飾詞篩選。 |

若要移除篩選器，請針對相關篩選器在藥丸圖示上選取「X」，或選取 **[!UICONTROL 全部清除]** 移除所有篩選器。

![flac-clear-filters](../../images/flac-ui/flac-clear-filters.png)

## 角色詳細資訊

從 **[!UICONTROL 角色]** 頁簽，該頁將開啟角色的詳細資訊頁。

![flac-details](../../images/flac-ui/flac-details.png)

詳細資訊索引標籤提供角色的概觀。 概覽顯示角色名稱、角色說明、建立和修改角色的用戶名、建立和修改角色時的用戶名以及附加到角色的權限。 如果需要，可以修改角色名稱和角色說明。

## 管理角色的標籤

選取 **[!UICONTROL 標籤]** 頁簽以開啟「角色標籤」頁，然後選擇 **[!UICONTROL 新增標籤]** 為角色分配標籤。

![flac標籤](../../images/flac-ui/flac-labels.png)

標籤列在此頁面上。 清單會顯示標籤名稱、好記名稱、類別及其說明。

從要添加到角色的清單中選擇標籤，然後選擇 **[!UICONTROL 儲存]**

![flac-add-labels](../../images/flac-ui/flac-add-labels.png)

新增的標籤會顯示在 **[!UICONTROL 標籤]** 標籤。

![flac添加的標籤](../../images/flac-ui/flac-added-labels.png)

要從角色中刪除標籤，請選擇 **X** 表徵圖。

![flac-delete-labels](../../images/flac-ui/flac-delete-labels.png)

## 管理角色的沙箱

選取 **[!UICONTROL 沙箱]** 頁簽以開啟「角色」沙箱頁面。 您可以在此處查看已新增至角色的沙箱清單。

![黃沙箱](../../images/flac-ui/flac-sandboxes.png)

若要新增更多沙箱至角色，請選取 **[!UICONTROL 編輯]**.

![flac-add-sandboxes](../../images/flac-ui/flac-add-sandboxes.png)

下一個畫面會提示您使用下拉式清單，選擇沙箱中要納入角色的資源權限。 完成後，請選取 **[!UICONTROL 儲存並退出]**.

![flac-add-role-permission](../../images/flac-ui/flac-add-role-permission.png)

## 管理角色的使用者

選取 **[!UICONTROL 使用者]** 頁簽以開啟「角色用戶」頁，然後選擇 **[!UICONTROL 新增使用者]** 為角色分配用戶。

![flac-users](../../images/flac-ui/flac-users.png)

從要添加到角色的清單中選擇用戶。 或者，使用搜索欄通過輸入用戶的姓名或電子郵件地址來搜索用戶，然後選擇 **[!UICONTROL 儲存]**

![flac-add-users](../../images/flac-ui/flac-add-users.png)

新增的使用者會顯示在 **[!UICONTROL 使用者]** 標籤。

![flac新增的使用者](../../images/flac-ui/flac-added-users.png)

若要從角色中移除使用者，請選取 **X** 圖示。

![flac-remove-users](../../images/flac-ui/flac-remove-users.png)

## 管理角色的API憑證

選取 **[!UICONTROL API憑證]** 頁簽以開啟「角色API憑據」頁，然後選擇 **[!UICONTROL 新增API憑證]** 將API憑證指派給角色。

![flac-api-credentials](../../images/flac-ui/flac-api-credentials.png)

從您要新增至角色的清單中選取API憑證，然後選取 **[!UICONTROL 儲存]**

![flac-add-api-credentials](../../images/flac-ui/flac-add-api-credentials.png)

新增的API憑證會顯示在 **[!UICONTROL API憑證]** 標籤。

![flac-added-api-credentials](../../images/flac-ui/flac-added-api-credentials.png)

若要從角色中移除API憑證，請選取 **X** 表徵圖。

![flac-remove-api-credentials](../../images/flac-ui/flac-remove-api-credentials.png)

此 **[!UICONTROL 移除API憑證]** 對話框，提示您確認刪除。

![flac-confirm-api-credentials-delete](../../images/flac-ui/flac-confirm-api-credentials-delete.png)

您將會返回 **[!UICONTROL API憑證]** 標籤。

## 管理角色的使用者群組

使用者群組是多個已分組且有權執行相同功能的使用者。

選取 **[!UICONTROL 使用者群組]** 頁簽以開啟「角色」用戶組頁，然後選擇 **[!UICONTROL 新增群組]** 將用戶組分配給角色。

![flac-user-groups](../../images/flac-ui/flac-user-groups.png)

從要添加到角色的清單中選擇用戶組。 或者，使用搜索欄通過輸入組名來搜索用戶組，然後選擇 **[!UICONTROL 儲存]**

![flac-add-user-groups](../../images/flac-ui/flac-add-user-groups.png)

新增的使用者群組會顯示在 **[!UICONTROL 使用者群組]** 標籤。

![flac-added-user-groups](../../images/flac-ui/flac-added-user-groups.png)

若要從角色中移除使用者群組，請選取 **X** 圖示。

![flac-remove-user-groups](../../images/flac-ui/flac-remove-user-groups.png)

此 **[!UICONTROL 移除使用者群組]** 對話框，提示您確認刪除。

![flac-confirm-user-groups -delete](../../images/flac-ui/flac-confirm-user-groups-delete.png)

您將會返回 **[!UICONTROL 使用者群組]** 標籤。

## 後續步驟

建立權限後，您可以繼續進行下一個步驟： [管理使用者](users.md).
