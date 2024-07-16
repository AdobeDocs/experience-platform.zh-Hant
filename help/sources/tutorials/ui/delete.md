---
keywords: Experience Platform；首頁；熱門主題；刪除資料流
description: 來源工作區可讓您刪除包含錯誤或已過時的現有批次和串流資料流。
solution: Experience Platform
title: 刪除UI中的資料流
type: Tutorial
exl-id: aa224467-7733-40de-aab7-0ff1c557abf2
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '367'
ht-degree: 1%

---

# 刪除UI中的資料流

[!UICONTROL 來源]工作區可讓您刪除包含錯誤或已作廢的現有批次和串流資料流。

本教學課程提供使用[!UICONTROL 來源]工作區刪除資料流的步驟。

## 快速入門

本教學課程需要您實際瞭解下列Adobe Experience Platform元件：

- [來源](../../home.md)： [!DNL Experience Platform]允許從各種來源擷取資料，同時讓您能夠使用[!DNL Platform]服務來建構、加標籤以及增強傳入的資料。
- [沙箱](../../../sandboxes/home.md)： [!DNL Experience Platform]提供可將單一[!DNL Platform]執行個體分割成個別虛擬環境的虛擬沙箱，以利開發及改進數位體驗應用程式。

## 刪除資料流

在[Experience PlatformUI](https://platform.adobe.com)中，從左側導覽選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取[!UICONTROL 來源]工作區，然後從頂端標題選取&#x200B;**[!UICONTROL 資料流]**。

![目錄](../../images/tutorials/delete/catalog.png)

**[!UICONTROL 資料流]**&#x200B;頁面隨即顯示。 此頁面是可檢視資料流的清單，包括有關其目標資料集、來源、帳戶名稱和建立日期的資訊。

選取左上方的篩選圖示（![篩選圖示](../../images/tutorials/delete/filter.png)）以啟動排序面板。

![資料流](../../images/tutorials/delete/dataflows.png)

排序面板提供所有來源的清單。 您可以從清單中選取多個來源，以存取與您所選取特定來源相關的資料流篩選選取專案。

選取您要使用的來源，以檢視其現有資料流的清單。 識別您要刪除的資料流後，請選取資料流名稱旁邊的省略符號(`...`)。

![資料流 — 篩選器](../../images/tutorials/delete/dataflows-filter.png)

下拉式功能表隨即顯示，提供您編輯資料流排程、停用資料流或將其完全刪除的選項。

選取&#x200B;**[!UICONTROL 刪除]**&#x200B;以刪除資料流。

![刪除](../../images/tutorials/delete/delete.png)

最後確認對話方塊隨即顯示。 選取&#x200B;**[!UICONTROL 刪除]**&#x200B;以完成程式。

![確認](../../images/tutorials/delete/confirm.png)

幾分鐘後，畫面底部會顯示一個確認方塊，以確認刪除成功。

![已確認](../../images/tutorials/delete/confirmed.png)

## 後續步驟

依照此教學課程，您已成功使用[!UICONTROL 來源]工作區來刪除現有的資料流。

請參閱有關[使用流程服務API刪除資料流](../../tutorials/api/delete-dataflows.md)的教學課程，以瞭解如何使用API呼叫以程式設計方式執行這些操作的步驟。
