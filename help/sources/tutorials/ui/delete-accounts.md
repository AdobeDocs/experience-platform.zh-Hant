---
keywords: Experience Platform；首頁；熱門主題；刪除帳戶
description: Adobe Experience Platform的源連接器提供了定期接收外部源資料的能力。 本教程提供了從「源」工作區刪除帳戶的步驟。
solution: Experience Platform
title: 刪除UI中的源連接帳戶
type: Tutorial
exl-id: 7cb65d17-d99d-46ff-b28f-7469d0b57d07
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 1%

---

# 刪除源連接帳戶

Adobe Experience Platform的源連接器提供了定期接收外部源資料的能力。 本教程提供了從 **[!UICONTROL 源]** 工作區。

## 快速入門

本教程需要對Adobe Experience Platform的以下部分進行有效的理解：

- [[!DNL Experience Data Model (XDM)] 系統](../../../xdm/home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。
   - [架構組合的基礎](../../../xdm/schema/composition.md):瞭解XDM架構的基本構建基塊，包括架構組成中的關鍵原則和最佳做法。
   - [架構編輯器教程](../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自定義架構。
- [[!DNL Real-Time Customer Profile]](../../../profile/home.md):基於來自多個源的聚合資料提供統一、即時的用戶配置檔案。

## 使用UI刪除帳戶

>[!TIP]
>
>在刪除源帳戶之前，必須先刪除與源帳戶關聯的任何現有資料流。 要刪除現有資料流，請參閱上的教程 [刪除UI中的源資料流](./delete.md)。

登錄到 [Adobe Experience Platform](https://platform.adobe.com) ，然後選擇 **[!UICONTROL 源]** 從左導航欄訪問 **[!UICONTROL 源]** 工作區。 的 **[!UICONTROL 目錄]** 螢幕顯示了各種源，您可以使用這些源建立帳戶和資料流。 每個源都顯示與它們關聯的現有帳戶和資料流的數量。

選擇 **[!UICONTROL 帳戶]** 訪問 **[!UICONTROL 帳戶]** 的子菜單。

![目錄帳戶](../../images/tutorials/delete-accounts/catalog.png)

此時將顯示現有帳戶的清單。 此頁上是現有帳戶（如源、用戶名、關聯資料流和建立日期）的可排序資訊清單。 選擇 **漏斗圖** 在左上角排序。

![資料流清單](../../images/tutorials/delete-accounts/accounts.png)

排序面板顯示在螢幕的左側，其中包含可用源的清單。 可以使用排序函式選擇多個源。

選擇要訪問的源，並從主介面中的帳戶清單中查找要刪除的帳戶。 在示例中，所選源為 **[!DNL Azure Blob Storage]** 帳戶名是 **[!UICONTROL blobTestConnector]**。 從排序面板中選擇多個源時，最近建立的帳戶將首先顯示，因為清單按建立日期排序。

選擇要刪除的帳戶。

![資料流排序](../../images/tutorials/delete-accounts/sort.png)

的 **[!UICONTROL 屬性]** 面板顯示在螢幕的右側，其中包含有關選定帳戶的資訊。

選取橢圓(`...`)。 出現一個彈出面板，提供選項 **[!UICONTROL 添加資料]**。 **[!UICONTROL 編輯詳細資訊]**, **[!UICONTROL 刪除]**。 選擇 **[!UICONTROL 刪除]** 刪除帳戶。

![資料流排序](../../images/tutorials/delete-accounts/delete.png)

出現最終確認對話框，選擇 **[!UICONTROL 刪除]** 來完成此過程。

![delete](../../images/tutorials/delete-accounts/confirm.png)

## 後續步驟

按照本教程，您已成功使用 **[!UICONTROL 源]** 工作區以刪除現有帳戶。

有關如何使用 [!DNL Flow Service] API，請參閱有關 [使用流服務API刪除連接](../../tutorials/api/delete.md)
