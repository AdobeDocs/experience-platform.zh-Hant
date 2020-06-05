---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中建立Salesforce來源連接器
topic: overview
translation-type: tm+mt
source-git-commit: 44c43afc653c147fa12e3e962904bfc79ee0fc64
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 1%

---


# 在UI中建立Salesforce來源連接器

Adobe Experience Platform中的來源連接器可讓您依計畫吸收外部來源的CRM資料。 本教學課程提供使用平台使用者介面建立Salesforce來源連接器的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列元件有正確的認識：

* [體驗資料模型(XDM)系統](../../../../../xdm/home.md): Experience Platform組織客戶體驗資料的標準化架構。
   * [架構構成基礎](../../../../../xdm/schema/composition.md): 瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md): 瞭解如何使用架構編輯器UI建立自訂架構。
* [即時客戶個人檔案](../../../../../profile/home.md): 根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

如果您已擁有有效的Salesforce帳戶，則可略過本檔案的其餘部分，並繼續有關設定資料流 [的教學課程](../../dataflow/crm.md)。

### 收集必要的認證

| 憑證 | 說明 |
| ---------- | ----------- |
| `environmentUrl` | Salesforce來源例項的URL。 |
| `username` | Salesforce使用者帳戶的使用者名稱。 |
| `password` | Salesforce使用者帳戶的密碼。 |
| `securityToken` | Salesforce使用者帳戶的安全性Token。 |

如需快速入門的詳細資訊，請造 [訪此Salesforce檔案](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm)。

## 連接您的Salesforce帳戶

收集完所需憑證後，您可依照下列步驟建立新的Salesforce帳戶以連線至平台。

登入 [Adobe Experience Platform](https://platform.adobe.com) ，然後從左側導覽列選取 **[!UICONTROL Sources]** ，以存取 ** Sources工作區。 「目 *[!UICONTROL 錄]* 」畫面會顯示多種來源，您可以為其建立傳入帳戶，而每個來源會顯示與其關聯的現有帳戶和資料集流量。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在「資 *[!UICONTROL 料庫]* 」類別下，選 **[!UICONTROL 取「Salesforce]** 」, **按一下+圖示(+)** ，以建立新的Salesforce連接器。

![目錄](../../../../images/tutorials/create/salesforce/catalog.png)

此時 *[!UICONTROL 會顯示「連線至Salesforce]* 」頁面。 在此頁上，您可以使用新認證或現有認證。

### 新帳戶

如果您使用新認證，請選擇「新 **[!UICONTROL 帳戶」]**。 在出現的輸入表單上，提供名稱、選用說明和您的Salesforce認證的連線。 完成後，選擇 **[!UICONTROL Connect]** ，然後為新帳戶建立留出一些時間。

![連接](../../../../images/tutorials/create/salesforce/new.png)

### 現有帳戶

若要連線現有帳戶，請選取您要連線的Salesforce帳戶，然後選取右上角的 **[!UICONTROL Next]** （下一步）以繼續。

![現有](../../../../images/tutorials/create/salesforce/existing.png)

## 後續步驟

在本教學課程中，您已建立與Salesforce帳戶的連線。 您現在可以繼續下一個教程，並 [配置資料流以將資料導入平台](../../dataflow/crm.md)。