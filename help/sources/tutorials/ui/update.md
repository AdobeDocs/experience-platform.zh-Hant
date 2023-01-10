---
keywords: Experience Platform；首頁；熱門主題；更新帳戶
description: 在某些情況下，可能需要更新現有源帳戶的詳細資訊。 「來源」工作區可讓您新增、編輯和刪除現有批次或串流連線的詳細資訊，包括其名稱、說明和憑證。
solution: Experience Platform
title: 在UI中更新源連接帳戶詳細資訊
type: Tutorial
exl-id: de264bd4-fe3d-4622-9f24-f1612d8334c9
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 0%

---

# 更新UI中的帳戶詳細資訊

在某些情況下，可能需要更新現有源帳戶的詳細資訊。 此 [!UICONTROL 來源] 工作區可讓您新增、編輯和刪除現有批次或串流連線的詳細資訊，包括其名稱、說明和憑證。

本教學課程提供從 [!UICONTROL 來源] 工作區。

## 快速入門

本教學課程需要妥善了解下列Adobe Experience Platform元件：

- [來源](../../home.md):Experience Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。
- [沙箱](../../../sandboxes/home.md):Experience Platform提供可將單一Platform執行個體分割成個別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

## 更新帳戶

登入 [Experience PlatformUI](https://platform.adobe.com) 然後選取 **[!UICONTROL 來源]** 從左側導覽器存取 [!UICONTROL 來源] 工作區。 選擇 **[!UICONTROL 帳戶]** 從頂端標題檢視現有帳戶。

![目錄](../../images/tutorials/update/catalog.png)

此 **[!UICONTROL 帳戶]** 頁。 此頁上是可查看帳戶的清單，包括有關其源、用戶名、資料流數和建立日期的資訊。

選取篩選圖示 ![篩選](../../images/tutorials/update/filter.png) ，啟動排序面板。

![accounts-list](../../images/tutorials/update/accounts-list.png)

排序面板提供所有來源的清單。 您可以從清單中選擇多個源以訪問與不同源關聯的帳戶的篩選選擇。

選擇要使用的源，以查看其現有帳戶的清單。 識別您要更新的帳戶後，請選取點(`...`)。

![accounts-sort](../../images/tutorials/update/accounts-sort.png)

下拉式功能表隨即顯示，提供選項 **[!UICONTROL 新增資料]**, **[!UICONTROL 編輯詳細資訊]**，和 **[!UICONTROL 刪除]**. 選擇 **[!UICONTROL 編輯詳細資訊]** 從功能表更新您的帳戶。

![更新](../../images/tutorials/update/update.png)

此 **[!UICONTROL 編輯帳戶詳細資訊]** 對話框允許您更新帳戶的名稱、說明和驗證憑據。 更新所需資訊後，請選取 **[!UICONTROL 儲存]**.

![edit-account-details](../../images/tutorials/update/edit-account-details.png)

幾分鐘後，畫面底部會顯示確認方塊，以確認更新成功。

![更新確認](../../images/tutorials/update/update-confirmed.png)

## 後續步驟

依照本教學課程，您已成功使用 [!UICONTROL 來源] 工作區，以更新現有來源帳戶的資訊。

有關如何以程式設計方式使用 [!DNL Flow Service] API，請參閱 [使用流服務API更新連接資訊](../../tutorials/api/update.md).
