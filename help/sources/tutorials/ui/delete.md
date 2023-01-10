---
keywords: Experience Platform；首頁；熱門主題；刪除資料流
description: 源工作區允許您刪除包含錯誤或已過時的現有批處理和流資料流。
solution: Experience Platform
title: 刪除UI中的資料流
type: Tutorial
exl-id: aa224467-7733-40de-aab7-0ff1c557abf2
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 1%

---

# 刪除UI中的資料流

此 [!UICONTROL 來源] 工作區可讓您刪除包含錯誤或已淘汰的現有批次和串流資料流。

本教學課程提供使用 [!UICONTROL 來源] 工作區。

## 快速入門

本教學課程需要妥善了解下列Adobe Experience Platform元件：

- [來源](../../home.md): [!DNL Experience Platform] 可讓您從各種來源擷取資料，同時使用來建構、加標籤及增強傳入資料 [!DNL Platform] 服務。
- [沙箱](../../../sandboxes/home.md): [!DNL Experience Platform] 提供可分割單一沙箱的虛擬沙箱 [!DNL Platform] 例項放入個別的虛擬環境，以協助開發及改進數位體驗應用程式。

## 刪除資料流

在 [Experience PlatformUI](https://platform.adobe.com)，選取 **[!UICONTROL 來源]** 從左側導覽器存取 [!UICONTROL 來源] 工作區，然後選取 **[!UICONTROL 資料流]** 從頂端標題。

![目錄](../../images/tutorials/delete/catalog.png)

此 **[!UICONTROL 資料流]** 頁。 此頁面是可查看資料流的清單，包括有關其目標資料集、源、帳戶名和建立日期的資訊。

選取篩選圖示(![篩選圖示](../../images/tutorials/delete/filter.png))以啟動「排序」面板。

![資料流](../../images/tutorials/delete/dataflows.png)

排序面板提供所有來源的清單。 您可以從清單中選擇多個源以訪問與所選特定源關聯的資料流的篩選選擇。

選擇要使用的源，以查看其現有資料流的清單。 確定要刪除的資料流後，請選取點(`...`)。

![dataflows-filter](../../images/tutorials/delete/dataflows-filter.png)

此時將顯示一個下拉菜單，為您提供編輯資料流調度、禁用資料流或完全刪除資料流的選項。

選擇 **[!UICONTROL 刪除]** 刪除資料流。

![刪除](../../images/tutorials/delete/delete.png)

最後確認對話框隨即出現。 選擇 **[!UICONTROL 刪除]** 來完成此程式。

![confirm](../../images/tutorials/delete/confirm.png)

幾分鐘後，畫面底部會顯示確認方塊，以確認刪除是否成功。

![確認](../../images/tutorials/delete/confirmed.png)

## 後續步驟

依照本教學課程，您已成功使用 [!UICONTROL 來源] 工作區，刪除現有資料流。

請參閱 [使用流服務API刪除資料流](../../tutorials/api/delete-dataflows.md) 以取得如何以程式設計方式使用API呼叫執行這些作業的步驟。
