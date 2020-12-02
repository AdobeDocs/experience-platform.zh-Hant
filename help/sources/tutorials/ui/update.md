---
keywords: Experience Platform;home;popular topics;update accounts;
description: null
solution: Experience Platform
title: 在UI中更新帳戶詳細資訊
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: 413687a0d9e790ea3f61a858002e9510216d7c34
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 0%

---


# 在UI中更新帳戶詳細資訊

在某些情況下，可能需要更新現有來源帳戶的詳細資訊。 「 [!UICONTROL 來源] 」工作區可讓您編輯、新增和刪除帳戶的詳細資訊，包括帳戶名稱、說明和驗證憑證的值。

本教學課程提供從 [!UICONTROL Sources工作區更新現有帳戶的詳細資訊和認證的] 步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列元件有正確的認識：

- [[!DNL Experience Data Model (XDM)] 系統](../../../xdm/home.md):組織客戶體驗資料 [!DNL Experience Platform] 的標準化架構。
   - [架構構成基礎](../../../xdm/schema/composition.md):瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   - [架構編輯器教程](../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自訂架構。
- [[!DNL Real-time Customer Profile]](../../../profile/home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

## 更新帳戶

登入「登入 [Experience Platform UI](https://platform.adobe.com) 」，然後從左側導覽器中選取「來源 **[!UICONTROL 」以存取「來源]** 」工作區。 從頂 **[!UICONTROL 端標題]** ，選擇「帳戶」以檢視現有帳戶。

![目錄](../../images/tutorials/update/catalog.png)

此時將 **[!UICONTROL 顯示]** 「帳戶」頁。 此頁面是可查看帳戶的清單，包括有關其源、用戶名、資料流數和建立日期的資訊。

選取左上角 ![的篩選器](../../images/tutorials/update/filter.png) 圖示篩選器，以啟動排序面板。

![accounts-list](../../images/tutorials/update/accounts-list.png)

排序面板提供所有來源的清單。 您可以從清單中選擇多個源，以訪問與不同源關聯的帳戶的篩選選擇。

選擇要使用的源，以查看其現有帳戶的清單。 在確定要更新的帳戶後，選擇帳戶名稱旁邊的省略號(`...`)。

![accounts-sort](../../images/tutorials/update/accounts-sort.png)

此時會出現下拉式功能表，提供您新增資 **[!UICONTROL 料]**、編 **[!UICONTROL 輯詳細資訊]**&#x200B;和 **[!UICONTROL 刪除]**。 從功 **[!UICONTROL 能表選擇]** 「編輯詳細資料」以更新您的帳戶。

![更新](../../images/tutorials/update/update.png)

「編 **[!UICONTROL 輯帳戶詳細資料]** 」對話方塊可讓您更新帳戶的名稱、說明和驗證憑證。 更新所需資訊後，請選取「儲 **[!UICONTROL 存」]**。

![edit-account-details](../../images/tutorials/update/edit-account-details.png)

片刻後，畫面底部會出現綠色的確認方塊，以確認更新是否成功。

![更新——確認](../../images/tutorials/update/update-confirmed.png)

## 後續步驟

在本教學課程中，您已成功使用 [!UICONTROL Sources] 工作區來更新帳戶資訊。

有關如何使用 [!DNL Flow Service] API以程式設計方式執行這些作業的步驟，請參閱使用Flow Service API [更新連線資訊的教學課程](../../tutorials/api/update.md)。