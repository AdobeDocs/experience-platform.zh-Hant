---
keywords: Experience Platform；首頁；熱門主題；存取控制；屬性型存取控制；ABAC
title: 以屬性為基礎的存取控制管理角色許可權
description: 本檔案提供透過Adobe Experience Cloud中的許可權介面設定角色許可權的相關資訊
exl-id: 8acd2bb6-eef8-4b23-8fd8-3566c7508fe7
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '984'
ht-degree: 2%

---

# 管理角色的許可權

>[!IMPORTANT]
>
>存取控制使用使用者ID （指派給使用者的內部唯一ID）來授予許可權。 當組織從Adobe ID移轉至Business ID時，為其使用者設定的所有許可權都將遺失，因為使用者ID變更和存取控制將使用新產生的使用者ID。 如果您的組織移轉至Business ID，請聯絡您的Adobe代表，將您的使用者ID從Adobe ID移轉至Business ID。

許可權是Experience Cloud的區域，管理員可以在其中定義使用者角色和存取原則，以管理產品應用程式內功能和物件的存取許可權。

透過「許可權」，您可以建立和管理角色，並為這些角色指派所需的資源許可權。 權限也可讓您管理與特定角色相關聯的標籤、沙箱和使用者。

在[建立新角色](#create-a-new-role)之後，您立即返回&#x200B;**[!UICONTROL 角色]**&#x200B;標籤。 如果您正在編輯現有角色的許可權，請從「**[!UICONTROL 角色]**」標籤中選取該角色。 或者，使用篩選選項來篩選結果以尋找角色。

## 篩選角色

選取漏斗圖示（![篩選圖示](/help/images/icons/filter.png)）以顯示篩選控制項清單，以協助縮小結果範圍。

![flac-filters](../../images/flac-ui/flac-filters.png)

UI中的角色可使用下列篩選器：

| 篩選器 | 說明 |
| --- | --- |
| [!UICONTROL 建立時間介於]之間 | 選取開始日期和/或結束日期，以定義篩選結果的日期範圍。 |
| [!UICONTROL 建立者：] | 從下拉式清單中選取使用者，依角色建立者篩選。 |
| [!UICONTROL 修改時間介於]之間 | 選取開始日期和/或結束日期，以定義篩選結果的日期範圍。 |
| [!UICONTROL 修改者] | 從下拉式清單中選取使用者，依角色修飾元篩選。 |

若要移除濾鏡，請針對有問題的濾鏡選取藥丸圖示上的「X」，或選取&#x200B;**[!UICONTROL 全部清除]**&#x200B;以移除所有濾鏡。

![flac-clear-filters](../../images/flac-ui/flac-clear-filters.png)

## 角色詳細資料

從&#x200B;**[!UICONTROL 角色]**&#x200B;標籤中選取角色，這會開啟角色的詳細資訊頁面。

![flac-details](../../images/flac-ui/flac-details.png)

詳細資訊標籤提供角色的概觀。 此概觀會顯示角色名稱、角色說明、建立和修改角色的使用者名稱、建立和修改角色的時間，以及附加至角色的許可權。 如果需要，可以修改角色名稱和角色說明。

## 管理角色的標籤

選取&#x200B;**[!UICONTROL 標籤]**&#x200B;標籤以開啟角色標籤頁面，然後選取&#x200B;**[!UICONTROL 新增標籤]**&#x200B;以指派標籤給角色。

![flac-labels](../../images/flac-ui/flac-labels.png)

標籤會列在此頁面上。 清單會顯示標簽名稱、易記名稱、類別及其說明。

從清單中選取您要新增至角色的標籤，然後選取&#x200B;**[!UICONTROL 儲存]**

![flac-add-labels](../../images/flac-ui/flac-add-labels.png)

新增的標籤會顯示在&#x200B;**[!UICONTROL 標籤]**&#x200B;標籤下。

![flac新增的標籤](../../images/flac-ui/flac-added-labels.png)

若要從角色中移除標籤，請選取標簽名稱旁的&#x200B;**X**&#x200B;圖示。

![flac-delete-labels](../../images/flac-ui/flac-delete-labels.png)

## 管理角色的沙箱

選取「**[!UICONTROL 沙箱]**」標籤以開啟「角色」沙箱頁面。 在這裡，您可以看到新增至角色的沙箱清單。

![flac-sandboxes](../../images/flac-ui/flac-sandboxes.png)

若要新增更多沙箱至角色，請選取&#x200B;**[!UICONTROL 編輯]**。

![flac-add-sandboxes](../../images/flac-ui/flac-add-sandboxes.png)

下一個畫面會提示您使用下拉式清單，選擇沙箱中要包含在角色中的資源許可權。 完成時，選取&#x200B;**[!UICONTROL 儲存並結束]**。

![flac-add-role-permission](../../images/flac-ui/flac-add-role-permission.png)

## 管理角色的使用者

選取「**[!UICONTROL 使用者]**」標籤以開啟「角色使用者」頁面，然後選取「**[!UICONTROL 新增使用者]**」以將使用者指派給角色。

![flac-users](../../images/flac-ui/flac-users.png)

從清單中選取您想要新增至角色的使用者。 或者，使用搜尋列輸入使用者的名稱或電子郵件地址來搜尋使用者，然後選取&#x200B;**[!UICONTROL 儲存]**

![flac-add-users](../../images/flac-ui/flac-add-users.png)

新增的使用者會出現在&#x200B;**[!UICONTROL 使用者]**&#x200B;標籤下。

![flac-added-users](../../images/flac-ui/flac-added-users.png)

若要從角色中移除使用者，請選取使用者名稱旁的&#x200B;**X**&#x200B;圖示。

![flac-remove-users](../../images/flac-ui/flac-remove-users.png)

以下影片旨在協助您瞭解如何建立新角色及管理該角色的使用者。

>[!VIDEO](https://video.tv.adobe.com/v/336081/?learn=on)

## 管理角色的API認證 {#manage-api-credentials-for-role}

選取&#x200B;**[!UICONTROL API認證]**&#x200B;標籤以開啟角色API認證頁面，然後選取&#x200B;**[!UICONTROL 新增API認證]**&#x200B;以指派API認證給角色。

![flac-api-credentials](../../images/flac-ui/flac-api-credentials.png)

從清單中選取您想要新增至角色的API認證，然後選取&#x200B;**[!UICONTROL 儲存]**

![flac-add-api-credentials](../../images/flac-ui/flac-add-api-credentials.png)

新增的API認證會出現在&#x200B;**[!UICONTROL API認證]**&#x200B;標籤下。

![flac-added-api-credentials](../../images/flac-ui/flac-added-api-credentials.png)

若要從角色中移除API認證，請選取API認證名稱旁的&#x200B;**X**&#x200B;圖示。

![flac-remove-api-credentials](../../images/flac-ui/flac-remove-api-credentials.png)

**[!UICONTROL 移除API認證]**&#x200B;對話方塊會出現，提示您確認刪除。

![flac-confirm-api-credentials-delete](../../images/flac-ui/flac-confirm-api-credentials-delete.png)

您將會返回&#x200B;**[!UICONTROL API認證]**&#x200B;標籤。

## 管理角色的使用者群組

使用者群組是多個使用者，這些使用者已分組在一起，並且有權執行相同的功能。

選取&#x200B;**[!UICONTROL 使用者群組]**&#x200B;標籤以開啟角色使用者群組頁面，然後選取&#x200B;**[!UICONTROL 新增群組]**&#x200B;以將使用者群組指派給角色。

![flac-user-groups](../../images/flac-ui/flac-user-groups.png)

從清單中選取您想要新增至角色的使用者群組。 或者，使用搜尋列來搜尋使用者群組，方法是輸入群組名稱，然後選取&#x200B;**[!UICONTROL 儲存]**

![flac-add-user-groups](../../images/flac-ui/flac-add-user-groups.png)

新增的使用者群組會出現在&#x200B;**[!UICONTROL 使用者群組]**&#x200B;標籤下。

![flac-added-user-groups](../../images/flac-ui/flac-added-user-groups.png)

若要從角色中移除使用者群組，請選取使用者群組名稱旁的&#x200B;**X**&#x200B;圖示。

![flac-remove-user-groups](../../images/flac-ui/flac-remove-user-groups.png)

**[!UICONTROL 移除使用者群組]**&#x200B;對話方塊隨即顯示，提示您確認刪除。

![flac-confirm-user-groups-delete](../../images/flac-ui/flac-confirm-user-groups-delete.png)

您將會返回&#x200B;**[!UICONTROL 使用者群組]**&#x200B;標籤。

## 透過角色新增使用者至Experience Platform

若要新增使用者到角色，請登入Admin Console並選取&#x200B;**[!UICONTROL 新增使用者]**

![product-profile-add-users](../../images/flac-ui/product-profile-add-users.png)

**[!UICONTROL 新增使用者至您的團隊]**&#x200B;對話方塊就會顯示。 輸入使用者的電子郵件地址、名字（選用）和姓氏（選用）。

選取鉛筆圖示以選取產品和使用者群組，選取&#x200B;**[!UICONTROL Adobe Experience Platform]**，然後選取&#x200B;**[!UICONTROL AEP-Default-All-Users]**，然後選取&#x200B;**[!UICONTROL 儲存]**。

![產品設定檔](../../images/flac-ui/product-profile.png)

## 後續步驟

建立許可權後，您可以繼續下一步以[管理使用者](users.md)。
