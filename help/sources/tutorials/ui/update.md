---
keywords: Experience Platform；首頁；熱門主題；更新帳戶
description: 在某些情況下，可能需要更新現有來源帳戶的詳細資訊。 「來源」工作區可讓您新增、編輯和刪除現有批次或串流連線的詳細資訊，包括其名稱、說明和認證。
solution: Experience Platform
title: 在UI中更新來源連線帳戶詳細資訊
topic: overview
type: Tutorial
translation-type: tm+mt
source-git-commit: 4a7405e2c8c97442d2781295dd827c6940aa33eb
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 1%

---


# 在UI中更新帳戶詳細資訊

在某些情況下，可能需要更新現有來源帳戶的詳細資訊。 [!UICONTROL Sources]工作區可讓您新增、編輯和刪除現有批次或串流連線的詳細資訊，包括其名稱、說明和認證。

本教學課程提供從[!UICONTROL Sources]工作區更新現有帳戶的詳細資訊和認證的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列部分有正確的理解：

- [來源](../../home.md):Experience Platform可讓您從各種來源擷取資料，同時讓您能夠使用平台服務來建構、標示並增強傳入資料。
- [沙盒](../../../sandboxes/home.md):Experience Platform提供虛擬沙盒，可將單一平台實例分割為獨立的虛擬環境，以協助開發和發展數位體驗應用程式。

## 更新帳戶

登入[Experience PlatformUI](https://platform.adobe.com)，然後從左側導覽器選擇&#x200B;**[!UICONTROL Sources]**&#x200B;以存取[!UICONTROL Sources]工作區。 從頂部標題中選擇&#x200B;**[!UICONTROL Accounts]**&#x200B;以查看現有帳戶。

![目錄](../../images/tutorials/update/catalog.png)

此時將顯示&#x200B;**[!UICONTROL Accounts]**&#x200B;頁。 此頁面是可查看帳戶的清單，包括有關其源、用戶名、資料流數和建立日期的資訊。

選擇左上角的篩選器表徵圖![filter](../../images/tutorials/update/filter.png)以啟動排序面板。

![accounts-list](../../images/tutorials/update/accounts-list.png)

排序面板提供所有來源的清單。 您可以從清單中選擇多個源，以訪問與不同源關聯的帳戶的篩選選擇。

選擇要使用的源，以查看其現有帳戶的清單。 在確定要更新的帳戶後，請選擇帳戶名稱旁的省略號(`...`)。

![accounts-sort](../../images/tutorials/update/accounts-sort.png)

此時會出現下拉式功能表，提供您&#x200B;**[!UICONTROL Add data]**、**[!UICONTROL Edit details]**&#x200B;和&#x200B;**[!UICONTROL Delete]**&#x200B;的選項。 從菜單中選擇&#x200B;**[!UICONTROL Edit details]**&#x200B;以更新您的帳戶。

![更新](../../images/tutorials/update/update.png)

使用&#x200B;**[!UICONTROL Edit account details]**&#x200B;對話框可以更新帳戶的名稱、說明和驗證憑據。 更新所需資訊後，請選擇&#x200B;**[!UICONTROL Save]**。

![edit-account-details](../../images/tutorials/update/edit-account-details.png)

片刻後，畫面底部會出現確認方塊，確認更新是否成功。

![更新——確認](../../images/tutorials/update/update-confirmed.png)

## 後續步驟

在本教學課程之後，您已成功使用[!UICONTROL Sources]工作區來更新現有來源帳戶的資訊。

有關如何使用[!DNL Flow Service] API以程式設計方式執行這些操作的步驟，請參閱有關使用流服務API](../../tutorials/api/update.md)更新連接資訊的教程。[