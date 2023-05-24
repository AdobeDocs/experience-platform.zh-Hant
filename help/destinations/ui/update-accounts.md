---
keywords: 更新目標帳戶、目標帳戶、如何更新帳戶、更新目標帳戶
title: 更新目標帳戶
type: Tutorial
description: 本教程列出了在Adobe Experience PlatformUI中更新目標帳戶的步驟
exl-id: afb41878-4205-4c64-af4d-e2740f852785
source-git-commit: f31b54622c63f96fb8fa727f80dda295a926e2c7
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 0%

---

# 更新目標帳戶

## 總覽 {#overview}

的 **[!UICONTROL 帳戶]** 頁籤顯示您已與各種目標建立的連接的詳細資訊。 請參閱 [帳戶概述](../ui/destinations-workspace.md#accounts) 獲取每個目標帳戶上可獲取的所有資訊。

本教程介紹了使用Experience PlatformUI更新目標帳戶詳細資訊的步驟。

您可以更新目標帳戶詳細資訊，以刷新和重新驗證當前使用的目標的當前帳戶或過期帳戶的憑據。 通常，OAuth和承載令牌的生存期有限，具體取決於目標平台。 當這些令牌過期時，可以在下面所述的工作流中刷新它們。 此工作流將指導您完成OAuth工作流或重新插入令牌。 同樣，如果下游平台中的密碼或用戶訪問已更改，則可以刷新憑據。

對於批處理目標，您可以更新訪問密鑰或密鑰（如果其中任何密鑰已更改）。 另外，如果要對正在前進的檔案進行加密，則可以插入RSA公鑰，並且導出的檔案將在進行加密。

![「帳戶」頁籤](../assets/ui/update-accounts/destination-accounts.png)

## 更新帳戶 {#update}

按照以下步驟將連接詳細資訊更新到現有目標。

1. 登錄到 [Experience PlatformUI](https://platform.adobe.com/) 選擇 **[!UICONTROL 目標]** 的下界。 選擇 **[!UICONTROL 帳戶]** 查看現有帳戶。

   ![「帳戶」頁籤](../assets/ui/update-accounts/accounts-tab.png)

2. 選擇篩選器表徵圖 ![篩選器表徵圖](../assets/ui/update-accounts/filter.png) 的子菜單。 排序面板提供所有目標的清單。 您可以從清單中選擇多個目標，以查看與所選目標關聯的帳戶的篩選選擇。

   ![篩選目標帳戶](../assets/ui/update-accounts/filter-accounts.png)

3. 選取橢圓(`...`)。 出現一個彈出面板，提供選項 **[!UICONTROL 激活段]**。 **[!UICONTROL 編輯詳細資訊]**, **[!UICONTROL 刪除]** 賬戶。 選擇 ![「編輯詳細資訊」按鈕](../assets/ui/workspace/pencil-icon.png) **[!UICONTROL 編輯詳細資訊]** 按鈕，將選定控制項在Tab鍵次序中下移一個位置。

   ![編輯帳戶](../assets/ui/update-accounts/accounts-edit.png)

4. 輸入更新的帳戶憑據。

   * 對於使用 `OAuth1` 或 `OAuth2` 連接類型，選擇 **[!UICONTROL 重新連接OAuth]** 續訂帳戶憑據。 您還可以更新帳戶的名稱和說明。

   ![編輯詳細資訊OAuth](../assets/ui/update-accounts/edit-details-oauth.png)

   * 對於使用 `Access Key` 或 `ConnectionString` 連接類型，您可以編輯帳戶驗證資訊，包括訪問ID、密鑰或連接字串等資訊。 您還可以更新帳戶的名稱和說明。

   ![編輯詳細資訊訪問密鑰](../assets/ui/update-accounts/edit-details-key.png)

   * 對於使用 `Bearer token` 連接類型，如果需要，可以輸入新的承載令牌。 您還可以更新帳戶的名稱和說明。

   ![編輯詳細資訊持有者令牌](../assets/ui/update-accounts/edit-details-bearer.png)

   * 對於使用 `Server to server` 連接類型，您可以更新帳戶的名稱和說明。

   ![編輯詳細資訊伺服器到伺服器](../assets/ui/update-accounts/edit-details-s2s.png)

5. 選擇 **[!UICONTROL 保存]** 完成帳戶詳細資訊更新。

## 後續步驟

按照本教程，您已成功使用 **[!UICONTROL 目的地]** 工作區以更新現有帳戶。

有關目標的詳細資訊，請參閱 [目標概述](../catalog/overview.md)。