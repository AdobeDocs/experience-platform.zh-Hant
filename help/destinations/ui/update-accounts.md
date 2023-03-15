---
keywords: 更新目標帳戶，目標帳戶，如何更新帳戶，更新目標
title: 更新目標帳戶
type: Tutorial
description: 本教學課程列出在Adobe Experience Platform UI中更新目標帳戶的步驟
exl-id: afb41878-4205-4c64-af4d-e2740f852785
source-git-commit: f31b54622c63f96fb8fa727f80dda295a926e2c7
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 0%

---

# 更新目標帳戶

## 總覽 {#overview}

此 **[!UICONTROL 帳戶]** 索引標籤會顯示您已與各種目的地建立之連線的詳細資訊。 請參閱 [帳戶概述](../ui/destinations-workspace.md#accounts) 取得每個目的地帳戶的所有資訊。

本教學課程涵蓋使用Experience PlatformUI更新目標帳戶詳細資訊的步驟。

您可以更新目標帳戶詳細資訊，以針對您目前使用的目標，重新整理目前帳戶或過期帳戶的認證並重新驗證認證。 一般而言，OAuth和持牌代號的存留期有限，視目的地平台而定。 當這些代號過期時，您可以在以下所述的工作流程中重新整理它們。 此工作流程會引導您完成OAuth工作流程或重新插入代號。 同樣地，如果下游平台中的密碼或使用者存取權限已變更，您可以重新整理憑證。

對於批次目的地，您可以更新存取權或機密金鑰（如果其中有任何變更）。 此外，如果要加密以後的檔案，可以插入RSA公鑰，您導出的檔案將隨後被加密。

![帳戶索引標籤](../assets/ui/update-accounts/destination-accounts.png)

## 更新帳戶 {#update}

請依照下列步驟，將連線詳細資料更新至現有目的地。

1. 登入 [Experience PlatformUI](https://platform.adobe.com/) 選取 **[!UICONTROL 目的地]** 的下一頁。 選擇 **[!UICONTROL 帳戶]** 從頂端標題檢視現有帳戶。

   ![帳戶索引標籤](../assets/ui/update-accounts/accounts-tab.png)

2. 選取篩選圖示 ![篩選器圖示](../assets/ui/update-accounts/filter.png) ，啟動排序面板。 排序面板會提供所有目的地的清單。 您可以從清單中選取多個目的地，以查看與所選目的地關聯之帳戶的篩選選取項目。

   ![篩選目標帳戶](../assets/ui/update-accounts/filter-accounts.png)

3. 選取點(`...`)，位於您要更新的帳戶名稱旁。 此時將出現彈出式面板，提供以下選項 **[!UICONTROL 啟用區段]**, **[!UICONTROL 編輯詳細資訊]**，和 **[!UICONTROL 刪除]** 帳戶。 選取 ![編輯詳細資訊按鈕](../assets/ui/workspace/pencil-icon.png) **[!UICONTROL 編輯詳細資訊]** 按鈕來編輯帳戶資訊。

   ![編輯帳戶](../assets/ui/update-accounts/accounts-edit.png)

4. 輸入您更新的帳戶憑證。

   * 對於使用 `OAuth1` 或 `OAuth2` 連接類型，選擇 **[!UICONTROL 重新連接OAuth]** 續訂帳戶憑證。 您也可以更新帳戶的名稱和說明。

   ![編輯詳細資訊OAuth](../assets/ui/update-accounts/edit-details-oauth.png)

   * 對於使用 `Access Key` 或 `ConnectionString` 連線類型，您可以編輯帳戶驗證資訊，包括存取ID、機密金鑰或連線字串等資訊。 您也可以更新帳戶的名稱和說明。

   ![編輯詳細資訊訪問密鑰](../assets/ui/update-accounts/edit-details-key.png)

   * 對於使用 `Bearer token` 連線類型，您可以視需要輸入新的承載權杖。 您也可以更新帳戶的名稱和說明。

   ![編輯詳細資訊承載令牌](../assets/ui/update-accounts/edit-details-bearer.png)

   * 對於使用 `Server to server` 連線類型，您可以更新帳戶的名稱和說明。

   ![編輯詳細資訊伺服器對伺服器](../assets/ui/update-accounts/edit-details-s2s.png)

5. 選擇 **[!UICONTROL 儲存]** 完成帳戶詳細資訊更新。

## 後續步驟

依照本教學課程，您已成功使用 **[!UICONTROL 目的地]** 工作區以更新現有帳戶。

如需目的地的詳細資訊，請參閱 [目的地概述](../catalog/overview.md).