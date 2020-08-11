---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中建立Azure資料總管來源連接器
topic: overview
translation-type: tm+mt
source-git-commit: 41fe3e5b2a830c3182b46b3e0873b1672a1f1b03
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 0%

---


# 在UI中 [!DNL Azure Data Explorer] 建立來源連接器

>[!NOTE]
> 連接 [!DNL Azure Data Explorer] 器為測試版。 如需使用 [測試版標籤連接器的詳細資訊](../../../../home.md#terms-and-conditions) ，請參閱來源概觀。

Adobe Experience Platform中的來源連接器可讓您依計畫吸收外部來源的資料。 本教學課程提供使用使 [!DNL Azure Data Explorer] 用者介面建立(以下稱為「[!DNL Data Explorer]」)來源連接器 [!DNL Platform] 的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列元件有正確的認識：

* [體驗資料模型(XDM)系統](../../../../../xdm/home.md):組織客戶體驗資料 [!DNL Experience Platform] 的標準化架構。
   * [架構構成基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自訂架構。
* [即時客戶個人檔案](../../../../../profile/home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

如果您已經有有效的 [!DNL Data Explorer] 連接，則可以跳過本文檔的其餘部分，並繼續有關配置資料 [流的教程](../../dataflow/databases.md)。

### 收集必要的認證

若要存取您的帳 [!DNL Data Explorer] 戶， [!DNL Platform]您必須提供下列值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `endpoint` | The endpoint of the [!DNL Data Explorer] server. |
| `database` | The name of the [!DNL Data Explorer] database. |
| `tenant` | 用來連線至資料庫的唯一租用戶 [!DNL Data Explorer] ID。 |
| `servicePrincipalId` | 用於連接到Data Explorer資料庫的唯一服務承擔者ID。 |
| `servicePrincipalKey` | 用於連接到Data Explorer資料庫的唯一服務主體鍵。 |

有關快速入門的詳細資訊，請參 [閱此資料總管檔案](https://docs.microsoft.com/en-us/azure/data-explorer/kusto/management/access-control/how-to-authenticate-with-aad)。

## 連線您的帳 [!DNL Azure Data Explorer] 戶

收集完所需的認證後，您可依照下列步驟建立新帳戶以 [!DNL Data Explorer] 連接至 [!DNL Platform]。

登入 [Adobe Experience Platform](https://platform.adobe.com) ，然後從左側導覽列選取 **[!UICONTROL Sources]** ，以存取 ** Sources工作區。 「目 *[!UICONTROL 錄]* 」畫面會顯示多種來源，您可以為這些來源建立傳入帳戶，而每個來源會顯示與這些來源相關聯的現有帳戶和資料集流數。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在「數 *[!UICONTROL 據庫]* 」類別下，選擇「 **[!UICONTROL Azure Data Explorer]** 」，然後選 **[!UICONTROL 擇「添加資料]** 」以建立新的「資料資源管理器」連接器。

![目錄](../../../../images/tutorials/create/data-explorer/catalog.png)

此時 *[!UICONTROL 會顯示「連線至Azure資料總管]* 」頁面。 在此頁上，您可以使用新認證或現有認證。

### 新帳戶

如果您使用新認證，請選擇「新 **[!UICONTROL 帳戶」]**。 在出現的輸入表單上，提供連線名稱、選用說明和您的認 [!DNL Data Explorer] 證。 完成後，選擇 **[!UICONTROL Connect]** ，然後為新帳戶建立留出一些時間。

![連接](../../../../images/tutorials/create/data-explorer/new.png)

### 現有帳戶

若要連線現有帳戶，請選 [!DNL Data Explorer] 取您要連線的帳戶，然後選取「下 **[!UICONTROL 一]** 步」繼續。

![現有](../../../../images/tutorials/create/data-explorer/existing.png)

## 後續步驟

遵循本教學課程，您已建立與帳戶的 [!DNL Data Explorer] 連線。 您現在可以繼續下一個教程，並 [配置資料流以將資料導入平台](../../dataflow/databases.md)。