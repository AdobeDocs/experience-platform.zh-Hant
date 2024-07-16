---
keywords: Experience Platform；首頁；熱門主題；更新帳戶
description: 在某些情況下，可能需要更新現有來源帳戶的詳細資料。 「來源」工作區可讓您新增、編輯和刪除現有批次或串流連線的詳細資料，包括其名稱、說明和認證。
solution: Experience Platform
title: 在UI中更新Source連線帳戶詳細資料
type: Tutorial
exl-id: de264bd4-fe3d-4622-9f24-f1612d8334c9
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 1%

---

# 在UI中更新帳戶詳細資料

在某些情況下，可能需要更新現有來源帳戶的詳細資料。 [!UICONTROL 來源]工作區可讓您新增、編輯和刪除現有批次或串流連線的詳細資料，包括其名稱、說明和認證。

本教學課程提供從[!UICONTROL 來源]工作區更新現有帳戶的詳細資訊和認證的步驟。

## 快速入門

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

- [來源](../../home.md)：Experience Platform允許從各種來源擷取資料，同時讓您能夠使用Platform服務來建構、加標籤以及增強傳入的資料。
- [沙箱](../../../sandboxes/home.md)：Experience Platform提供的虛擬沙箱可將單一Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

## 更新帳戶

登入[Experience PlatformUI](https://platform.adobe.com)，然後從左側導覽選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取[!UICONTROL 來源]工作區。 從頂端標題選取&#x200B;**[!UICONTROL 帳戶]**&#x200B;以檢視現有帳戶。

![目錄](../../images/tutorials/update/catalog.png)

**[!UICONTROL 帳戶]**&#x200B;頁面隨即顯示。 此頁面是可檢視帳戶的清單，包括有關其來源、使用者名稱、資料流數量和建立日期的資訊。

選取左上方的篩選圖示![篩選](../../images/tutorials/update/filter.png)以啟動排序面板。

![帳戶清單](../../images/tutorials/update/accounts-list.png)

排序面板提供所有來源的清單。 您可以從清單中選取多個來源，以存取與不同來源關聯的已篩選帳戶選項。

選取您要使用的來源，以檢視其現有帳戶的清單。 識別要更新的帳戶後，請選取帳戶名稱旁的省略符號(`...`)。

![帳戶排序](../../images/tutorials/update/accounts-sort.png)

出現下拉式功能表，提供您選項&#x200B;**[!UICONTROL 新增資料]**、**[!UICONTROL 編輯詳細資料]**&#x200B;和&#x200B;**[!UICONTROL 刪除]**。 從功能表選取「**[!UICONTROL 編輯詳細資料]**」以更新您的帳戶。

![更新](../../images/tutorials/update/update.png)

**[!UICONTROL 編輯帳戶詳細資料]**&#x200B;對話方塊可讓您更新帳戶的名稱、說明和驗證認證。 更新所需的資訊後，請選取&#x200B;**[!UICONTROL 儲存]**。

![edit-account-details](../../images/tutorials/update/edit-account-details.png)

幾分鐘後，畫面底部會顯示一個確認方塊，以確認更新成功。

![更新已確認](../../images/tutorials/update/update-confirmed.png)

## 後續步驟

依照本教學課程，您已成功使用[!UICONTROL 來源]工作區來更新現有來源帳戶的資訊。

如需有關如何使用[!DNL Flow Service] API以程式設計方式執行這些操作的步驟，請參閱有關[使用流程服務API更新連線資訊的教學課程](../../tutorials/api/update.md)。
