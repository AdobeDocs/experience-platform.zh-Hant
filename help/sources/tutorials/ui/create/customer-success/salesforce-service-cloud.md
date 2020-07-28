---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中建立Salesforce Service Cloud來源連接器
topic: overview
translation-type: tm+mt
source-git-commit: d3c725c4760acb3857a67d0d30b24732c963a030
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 0%

---


# 在UI中 [!DNL Salesforce Service Cloud] 建立來源連接器

>[!NOTE]
>連接 [!DNL Salesforce Service Cloud] 器為測試版。 如需使用 [測試版標籤連接器的詳細資訊](../../../../home.md#terms-and-conditions) ，請參閱來源概觀。

Adobe Experience Platform中的來源連接器可讓您依計畫吸收外部來源的資料。 本教程提供使用用戶 [!DNL Salesforce Service Cloud] 介面建立源連接器（以下稱為「SSC」）的 [!DNL Platform] 步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列元件有正確的認識：

* [體驗資料模型(XDM)系統](../../../../../xdm/home.md): 組織客戶體驗資料 [!DNL Experience Platform] 的標準化架構。
   * [架構構成基礎](../../../../../xdm/schema/composition.md): 瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md): 瞭解如何使用架構編輯器UI建立自訂架構。
* [即時客戶個人檔案](../../../../../profile/home.md): 根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

如果您已經有有效的SSC連接，則可以跳過本文檔的其餘部分並繼續有關配置資料 [流的教程](../../dataflow/customer-success.md)

### 收集必要的認證

要訪問您的SSC帳戶， [!DNL Platform]必須提供以下值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `username` | 使用者帳戶的使用者名稱。 |
| `password` | 使用者帳戶的密碼。 |
| `securityToken` | 使用者帳戶的安全性Token。 |

如需快速入門的詳細資訊，請參 [閱此Salesforce Service Cloud檔案](https://developer.salesforce.com/docs/atlas.en-us.api_iot.meta/api_iot/qs_auth_access_token.htm)。

## 連線您的帳 [!DNL Salesforce Service Cloud] 戶

在收集到所需憑據後，您可以按照以下步驟建立新的SSC帳戶以連接到 [!DNL Platform]。

登入 <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> ，然後從左側導覽列選取 **[!UICONTROL Sources]** ，以存取 ** Sources工作區。 「目 *[!UICONTROL 錄]* 」畫面會顯示多種來源，您可以為這些來源建立傳入帳戶，而每個來源會顯示與這些來源相關聯的現有帳戶和資料集流數。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在「 *[!UICONTROL 客戶成功]* 」類別下，選取 **[!UICONTROL Salesforce Service Cloud]** ，以在螢幕右側顯示資訊列。 資訊列提供所選來源的簡短說明，以及與來源連線或檢視其檔案的選項。 要建立新入站連接，請選擇「連 **[!UICONTROL 接源」]**。

![目錄](../../../../images/tutorials/create/ssc/catalog.png)

此時 *[!UICONTROL 會顯示「連線至Salesforce Service Cloud]* 」頁面。 在此頁上，您可以使用新認證或現有認證。

### 新帳戶

如果您使用新認證，請選擇「新 **[!UICONTROL 帳戶」]**。 在顯示的輸入表單上，為連接提供名稱、可選說明和SSC憑據。 完成後，選擇 **[!UICONTROL Connect]** ，然後為新帳戶建立留出一些時間。

![連接](../../../../images/tutorials/create/ssc/connect.png)

### 現有帳戶

要連接現有帳戶，請選擇要連接的SSC帳戶，然後選擇「下 **[!UICONTROL 一步]** 」繼續。

![現有](../../../../images/tutorials/create/ssc/existing.png)

## 後續步驟

通過本教程，您已建立了與SSC帳戶的連接。 您現在可以繼續下一個教學課程，並 [設定資料流，將客戶成功資料匯入平台](../../dataflow/customer-success.md)。