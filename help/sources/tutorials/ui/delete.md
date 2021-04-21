---
keywords: Experience Platform; home；熱門主題；刪除資料流
description: 來源工作區可讓您刪除包含錯誤或已過時的現有批處理和流資料流。
solution: Experience Platform
title: 刪除UI中的資料流
topic-legacy: overview
type: Tutorial
exl-id: aa224467-7733-40de-aab7-0ff1c557abf2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 1%

---

# 刪除UI中的資料流

[!UICONTROL Sources]工作區允許您刪除包含錯誤或已過時的現有批處理和流資料流。

本教程提供使用[!UICONTROL Sources]工作區刪除資料流的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列部分有正確的理解：

- [來源](../../home.md): [!DNL Experience Platform] 允許從各種來源接收資料，同時提供使用服務構建、標籤和增強傳入資料的 [!DNL Platform] 能力。
- [沙盒](../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙盒，可將單一執行個體分 [!DNL Platform] 割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

## 刪除資料流

在[Experience PlatformUI](https://platform.adobe.com)中，從左側導覽器選擇&#x200B;**[!UICONTROL Sources]**&#x200B;以存取[!UICONTROL Sources]工作區，然後從上方標題中選擇&#x200B;**[!UICONTROL Dataflows]**。

![目錄](../../images/tutorials/delete/catalog.png)

此時將顯示&#x200B;**[!UICONTROL Dataflows]**&#x200B;頁。 本頁列出了可查看的資料流，包括其目標資料集、源、帳戶名和建立日期的相關資訊。

選取左上角的篩選圖示(![filter-icon](../../images/tutorials/delete/filter.png))，以啟動排序面板。

![資料流](../../images/tutorials/delete/dataflows.png)

排序面板提供所有來源的清單。 您可以從清單中選擇多個源，以訪問與所選特定源關聯的資料流的篩選選擇。

選擇要使用的源，以查看其現有資料流的清單。 確定要刪除的資料流後，請選擇資料流名稱旁邊的省略號(`...`)。

![資料流過濾器](../../images/tutorials/delete/dataflows-filter.png)

此時將顯示一個下拉菜單，為您提供了編輯資料流時間表、禁用資料流或完全刪除資料流的選項。

選擇&#x200B;**[!UICONTROL Delete]**&#x200B;以刪除資料流。

![刪除](../../images/tutorials/delete/delete.png)

將出現最終確認對話框。 選擇&#x200B;**[!UICONTROL Delete]**&#x200B;以完成該過程。

![confirm](../../images/tutorials/delete/confirm.png)

片刻後，畫面底部會顯示確認方塊，以確認刪除成功。

![確認](../../images/tutorials/delete/confirmed.png)

## 後續步驟

按照本教程，您已成功使用[!UICONTROL Sources]工作區刪除現有資料流。

有關如何使用API調用以寫程式方式執行這些操作的步驟，請參見有關使用流服務API](../../tutorials/api/delete-dataflows.md)刪除資料流的教程。[
