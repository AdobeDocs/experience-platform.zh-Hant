---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中建立Azure資料總管來源連接器
topic: overview
translation-type: tm+mt
source-git-commit: 2162c66b1664ecaaf0b609fe3f7ccf58c4a5d31d
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 0%

---


# 在UI中建立Azure資料總管來源連接器

> [!NOTE]
> Azure資料總管連接器正在測試中。 功能和檔案可能會有所變更。

Adobe Experience Platform中的來源連接器可讓您依計畫吸收外部來源的資料。 本教學課程提供使用平台使用者介面建立Azure資料總管（以下稱為「資料總管」）來源連接器的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列元件有正確的認識：

* [體驗資料模型(XDM)系統](../../../../../xdm/home.md): Experience Platform組織客戶體驗資料的標準化架構。
   * [架構構成基礎](../../../../../xdm/schema/composition.md): 瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md): 瞭解如何使用架構編輯器UI建立自訂架構。
* [即時客戶個人檔案](../../../../../profile/home.md): 根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

如果您已經有有效的Data Explorer連接，則可以跳過本文檔的其餘部分，並繼續有關配置資料流 [的教程](../../dataflow/databases.md)。

### 收集必要的認證

若要存取您在平台上的Data Explorer帳戶，您必須提供下列值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `endpoint` | Data Explorer伺服器的端點。 |
| `database` | Data Explorer資料庫的名稱。 |
| `tenant` | 用來連線至資料總管資料庫的唯一租用戶ID。 |
| `servicePrincipalId` | 用於連接到Data Explorer資料庫的唯一服務承擔者ID。 |
| `servicePrincipalKey` | 用於連接到Data Explorer資料庫的唯一服務主體鍵。 |

有關快速入門的詳細資訊，請參 [閱此資料總管檔案](https://docs.microsoft.com/en-us/azure/data-explorer/kusto/management/access-control/how-to-authenticate-with-aad)。

## 連接您的Azure資料總管帳戶

收集完所需的憑證後，您可依照下列步驟建立新的資料總管帳戶以連接至平台。

登入 [Adobe Experience Platform](https://platform.adobe.com) ，然後從左側導覽列選取 **[!UICONTROL Sources]** ，以存取 ** Sources工作區。 「目 *[!UICONTROL 錄]* 」畫面會顯示多種來源，您可以為這些來源建立傳入帳戶，而每個來源會顯示與這些來源相關聯的現有帳戶和資料集流數。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在「資 *[!UICONTROL 料庫]* 」類別下，選取「 **[!UICONTROL Azure資料總管]** 」並按一 **下+圖示(+)** ，以建立新的資料總管連接器。

![目錄](../../../../images/tutorials/create/data-explorer/catalog.png)

此時 *[!UICONTROL 會顯示「連線至Azure資料總管]* 」頁面。 在此頁上，您可以使用新認證或現有認證。

### 新帳戶

如果您使用新認證，請選擇「新 **[!UICONTROL 帳戶」]**。 在顯示的輸入表單上，提供名稱、選用說明和資料總管憑證的連線。 完成後，選擇 **[!UICONTROL Connect]** ，然後為新帳戶建立留出一些時間。

![連接](../../../../images/tutorials/create/data-explorer/new.png)

### 現有帳戶

若要連線現有帳戶，請選取您要連線的資料總管帳戶，然後選取「下一 **[!UICONTROL 步]** 」繼續。

![現有](../../../../images/tutorials/create/data-explorer/existing.png)

## 後續步驟

遵循本教學課程，您已建立與資料總管帳戶的連線。 您現在可以繼續下一個教程，並 [配置資料流以將資料導入平台](../../dataflow/databases.md)。