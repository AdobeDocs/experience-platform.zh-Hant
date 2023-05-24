---
keywords: Experience Platform；首頁；熱門主題；更新帳戶
description: 在某些情況下，可能需要更新現有來源帳戶的詳細資訊。 「源」工作區允許您添加、編輯和刪除現有批處理或流連接的詳細資訊，包括其名稱、說明和憑據。
solution: Experience Platform
title: 在UI中更新源連接帳戶詳細資訊
type: Tutorial
exl-id: de264bd4-fe3d-4622-9f24-f1612d8334c9
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 1%

---

# 更新UI中的帳戶詳細資訊

在某些情況下，可能需要更新現有來源帳戶的詳細資訊。 的 [!UICONTROL 源] workspace使您能夠添加、編輯和刪除現有批處理或流連接的詳細資訊，包括其名稱、說明和憑據。

本教程提供了一些步驟，用於從 [!UICONTROL 源] 工作區。

## 快速入門

本教程需要對Adobe Experience Platform的以下部分進行有效的理解：

- [源](../../home.md):Experience Platform允許從各種源接收資料，同時讓您能夠使用平台服務構建、標籤和增強傳入資料。
- [沙箱](../../../sandboxes/home.md):Experience Platform提供虛擬沙箱，將單個平台實例分區為獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

## 更新帳戶

登錄到 [Experience PlatformUI](https://platform.adobe.com) ，然後選擇 **[!UICONTROL 源]** 從左側導航 [!UICONTROL 源] 工作區。 選擇 **[!UICONTROL 帳戶]** 查看現有帳戶。

![目錄](../../images/tutorials/update/catalog.png)

的 **[!UICONTROL 帳戶]** 的子菜單。 此頁上是可查看帳戶的清單，包括有關其源、用戶名、資料流數和建立日期的資訊。

選擇篩選器表徵圖 ![濾波器](../../images/tutorials/update/filter.png) 的子菜單。

![帳戶清單](../../images/tutorials/update/accounts-list.png)

排序面板提供所有源的清單。 您可以從清單中選擇多個源，以訪問與不同源關聯的帳戶的篩選選擇。

選擇要使用的源，以查看其現有帳戶的清單。 確定要更新的帳戶後，選擇省略號(`...`)。

![帳戶排序](../../images/tutorials/update/accounts-sort.png)

將出現下拉菜單，提供選項 **[!UICONTROL 添加資料]**。 **[!UICONTROL 編輯詳細資訊]**, **[!UICONTROL 刪除]**。 選擇 **[!UICONTROL 編輯詳細資訊]** 的子菜單。

![update](../../images/tutorials/update/update.png)

的 **[!UICONTROL 編輯帳戶詳細資訊]** 對話框允許您更新帳戶的名稱、說明和身份驗證憑據。 更新所需資訊後，選擇 **[!UICONTROL 保存]**。

![編輯帳戶詳細資訊](../../images/tutorials/update/edit-account-details.png)

幾分鐘後，螢幕底部將出現一個確認框，以確認成功更新。

![已確認更新](../../images/tutorials/update/update-confirmed.png)

## 後續步驟

按照本教程，您已成功使用 [!UICONTROL 源] 工作區以更新現有源帳戶的資訊。

有關如何使用 [!DNL Flow Service] API，請參閱有關 [使用流服務API更新連接資訊](../../tutorials/api/update.md)。
