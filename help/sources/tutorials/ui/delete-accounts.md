---
keywords: Experience Platform; home；熱門主題；刪除帳戶
description: Adobe Experience Platform的來源連接器提供按計畫接收外部來源資料的能力。 本教學課程提供從「來源」工作區刪除帳戶的步驟。
solution: Experience Platform
title: 在UI中刪除源連接帳戶
topic-legacy: overview
type: Tutorial
exl-id: 7cb65d17-d99d-46ff-b28f-7469d0b57d07
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---

# 刪除源連接帳戶

Adobe Experience Platform的來源連接器提供按計畫接收外部來源資料的能力。 本教學課程提供從&#x200B;**[!UICONTROL Sources]**&#x200B;工作區刪除帳戶的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列部分有正確的理解：

- [[!DNL Experience Data Model (XDM)] 系統](../../../xdm/home.md):組織客戶體驗資 [!DNL Experience Platform] 料的標準化架構。
   - [架構構成基礎](../../../xdm/schema/composition.md):瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   - [架構編輯器教程](../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自訂架構。
- [[!DNL Real-time Customer Profile]](../../../profile/home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

## 使用UI刪除帳戶

登入[Adobe Experience Platform](https://platform.adobe.com)，然後從左側導覽列選擇&#x200B;**[!UICONTROL Sources]**&#x200B;以存取&#x200B;**[!UICONTROL Sources]**&#x200B;工作區。 **[!UICONTROL Catalog]**&#x200B;螢幕顯示了各種源，您可以為其建立帳戶和資料流。 每個源顯示與其關聯的現有帳戶和資料流的數量。

選擇&#x200B;**[!UICONTROL Accounts]**&#x200B;以訪問&#x200B;**[!UICONTROL Accounts]**&#x200B;頁。

![catalog-accounts](../../images/tutorials/delete-accounts/catalog.png)

現有帳戶的清單隨即出現。 此頁面是現有帳戶的可排序資訊清單，如源帳戶、用戶名、關聯資料流和建立日期。 選擇左上角的&#x200B;**漏斗表徵圖**&#x200B;進行排序。

![dataflows-list](../../images/tutorials/delete-accounts/accounts.png)

排序面板會出現在畫面的左側，其中包含可用來源的清單。 您可以使用排序函式選擇多個源。

選擇要訪問的源，並從主介面的帳戶清單中找到要刪除的帳戶。 在示例中，所選源為&#x200B;**[!DNL Azure Blob Storage]** ，帳戶名為&#x200B;**[!UICONTROL blobTestConnector]**。 從排序面板中選取多個來源時，您最近建立的帳戶會優先顯示，因為清單會依建立日期排序。

選擇您要刪除的帳戶。

![dataflows-sort](../../images/tutorials/delete-accounts/sort.png)

**[!UICONTROL Properties]**&#x200B;面板會出現在畫面的右側，其中包含有關選取帳戶的資訊。

選取您要刪除之帳戶名稱旁的省略號(`...`)。 此時會出現一個彈出式面板，提供&#x200B;**[!UICONTROL Add data]**、**[!UICONTROL Edit details]**&#x200B;和&#x200B;**[!UICONTROL Delete]**&#x200B;的選項。 選擇&#x200B;**[!UICONTROL Delete]**&#x200B;刪除帳戶。

![dataflows-sort](../../images/tutorials/delete-accounts/delete.png)

最後出現確認對話框，選擇&#x200B;**[!UICONTROL Delete]**&#x200B;以完成該過程。

![刪除](../../images/tutorials/delete-accounts/confirm.png)

## 後續步驟

在本教學課程中，您已成功使用&#x200B;**[!UICONTROL Sources]**&#x200B;工作區刪除現有帳戶。

有關如何使用[!DNL Flow Service] API以程式設計方式執行這些作業的步驟，請參閱有關使用流式服務API](../../tutorials/api/delete.md)刪除連線的[教學課程
