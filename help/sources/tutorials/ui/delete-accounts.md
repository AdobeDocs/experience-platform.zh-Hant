---
keywords: Experience Platform；首頁；熱門主題；刪除帳戶
description: Adobe Experience Platform中的來源連接器可讓您依排程內嵌外部來源資料。 本教學課程提供從來源工作區刪除帳戶的步驟。
solution: Experience Platform
title: 刪除UI中的源連接帳戶
topic-legacy: overview
type: Tutorial
exl-id: 7cb65d17-d99d-46ff-b28f-7469d0b57d07
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---

# 刪除源連接帳戶

Adobe Experience Platform中的來源連接器可讓您依排程內嵌外部來源資料。 本教學課程提供從 **[!UICONTROL 來源]** 工作區。

## 快速入門

本教學課程需要妥善了解下列Adobe Experience Platform元件：

- [[!DNL Experience Data Model (XDM)] 系統](../../../xdm/home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。
   - [結構構成基本概念](../../../xdm/schema/composition.md):了解XDM結構描述的基本建置組塊，包括結構描述的主要原則和最佳實務。
   - [結構編輯器教學課程](../../../xdm/tutorials/create-schema-ui.md):了解如何使用結構編輯器UI建立自訂結構。
- [[!DNL Real-Time Customer Profile]](../../../profile/home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。

## 使用UI刪除帳戶

>[!TIP]
>
>在刪除源帳戶之前，必須先刪除與源帳戶關聯的任何現有資料流。 要刪除現有資料流，請參閱 [刪除UI中的源資料流](./delete.md).

登入 [Adobe Experience Platform](https://platform.adobe.com) 然後選取 **[!UICONTROL 來源]** 從左側導覽列存取 **[!UICONTROL 來源]** 工作區。 此 **[!UICONTROL 目錄]** 螢幕顯示了各種源，您可以用這些源建立帳戶和資料流。 每個源顯示與其關聯的現有帳戶和資料流的數量。

選擇 **[!UICONTROL 帳戶]** 若要存取 **[!UICONTROL 帳戶]** 頁面。

![catalog-accounts](../../images/tutorials/delete-accounts/catalog.png)

現有帳戶的清單隨即出現。 本頁列出現有帳戶的可排序資訊，如源、用戶名、關聯資料流和建立日期。 選取 **漏斗圖示** 排序。

![dataflows-list](../../images/tutorials/delete-accounts/accounts.png)

排序面板會顯示在畫面左側，其中包含可用來源清單。 您可以使用排序函式選擇多個源。

選擇您要訪問的源，並從主介面的帳戶清單中找到要刪除的帳戶。 在示例中，所選源為 **[!DNL Azure Blob Storage]** 而帳戶名稱是 **[!UICONTROL blobTestConnector]**. 從排序面板中選取多個來源時，最近建立的帳戶會先顯示，因為清單會依建立日期排序。

選擇要刪除的帳戶。

![dataflows sort](../../images/tutorials/delete-accounts/sort.png)

此 **[!UICONTROL 屬性]** 面板會顯示在畫面的右側，其中包含有關所選帳戶的資訊。

選取點(`...`)，並在您要刪除的帳戶名稱旁邊。 此時將出現彈出式面板，提供以下選項 **[!UICONTROL 新增資料]**, **[!UICONTROL 編輯詳細資訊]**，和 **[!UICONTROL 刪除]**. 選擇 **[!UICONTROL 刪除]** 刪除帳戶。

![dataflows sort](../../images/tutorials/delete-accounts/delete.png)

最後確認對話框出現，請選擇 **[!UICONTROL 刪除]** 來完成此程式。

![刪除](../../images/tutorials/delete-accounts/confirm.png)

## 後續步驟

依照本教學課程，您已成功使用 **[!UICONTROL 來源]** 工作區以刪除現有帳戶。

有關如何以程式設計方式使用 [!DNL Flow Service] API，請參閱 [使用流服務API刪除連接](../../tutorials/api/delete.md)
