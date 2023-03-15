---
keywords: 刪除目標帳戶、目標帳戶、如何刪除帳戶
title: 刪除目標帳戶
type: Tutorial
description: 本教學課程列出在Adobe Experience Platform UI中刪除目的地帳戶的步驟
exl-id: 9b39ba4b-19a4-48a8-a6f1-f860777cdb9e
source-git-commit: 2ea56957e122140fbc68c727e36666f8f9a71dd8
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# 刪除目標帳戶

## 總覽 {#overview}

此 **[!UICONTROL 帳戶]** 索引標籤會顯示您已與各種目的地建立之連線的詳細資訊。 請參閱 [帳戶概述](../ui/destinations-workspace.md#accounts) 取得每個目的地帳戶的所有資訊。

本教學課程涵蓋使用Experience PlatformUI刪除不再需要的目的地帳戶的步驟。

![帳戶索引標籤](../assets/ui/update-accounts/destination-accounts.png)

## 刪除帳戶 {#delete}

>[!TIP]
>
>在刪除目標帳戶之前，必須先刪除與目標帳戶關聯的任何現有資料流。 要刪除現有目標資料流，請參閱 [刪除UI中的目標資料流](./delete-destinations.md).

請依照下列步驟刪除現有的目的地帳戶。

1. 登入 [Experience PlatformUI](https://platform.adobe.com/) 選取 **[!UICONTROL 目的地]** 的下一頁。 選擇 **[!UICONTROL 帳戶]** 從頂端標題檢視現有帳戶。

   ![帳戶索引標籤](../assets/ui/delete-accounts/accounts-tab.png)

2. 選取篩選圖示 ![篩選器圖示](../assets/ui/update-accounts/filter.png) ，啟動排序面板。 排序面板會提供所有目的地的清單。 您可以從清單中選取多個目的地，以查看與所選目的地關聯之帳戶的篩選選取項目。

   ![篩選目的地](../assets/ui/delete-accounts/filter-accounts.png)

3. 選取點(`...`)，並在您要刪除的帳戶名稱旁邊。 此時將出現彈出式面板，提供以下選項 **[!UICONTROL 啟用區段]**, **[!UICONTROL 編輯詳細資訊]**，和 **[!UICONTROL 刪除]** 帳戶。 選取 ![刪除按鈕](../assets/ui/workspace/pencil-icon.png) **[!UICONTROL 刪除]** 按鈕以刪除所需帳戶。

   ![刪除目標帳戶](../assets/ui/delete-accounts/delete-accounts.png)

4. 最後確認對話框出現，請選擇 **[!UICONTROL 刪除]** 來完成此程式。

![確認帳戶刪除](../assets/ui/delete-accounts/confirm-account-deletion.png)

## 後續步驟

依照本教學課程，您已成功使用目的地工作區來刪除現有帳戶。

有關如何以程式設計方式使用 [!DNL Flow Service] API，請參閱 [使用流服務API刪除連接](../api/delete-destination-account.md)
