---
keywords: Experience Platform;home;popular topics;Salesforce;salesforce
solution: Experience Platform
title: 在UI中建立Salesforce來源連接器
topic: overview
description: 本教學課程提供使用平台使用者介面建立Salesforce來源連接器的步驟。
translation-type: tm+mt
source-git-commit: f82dfee2c75a0b8b2ec1615266780b309152ead4
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 1%

---


# 在UI中 [!DNL Salesforce] 建立來源連接器

Adobe Experience Platform中的來源連接器可讓您依計畫吸收外部來源的CRM資料。 本教學課程提供使用使用者介 [!DNL Salesforce] 面建立來源連接器 [!DNL Platform] 的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列元件有正確的認識：

* [[!DNL Experience Data Model] (XDM)系統](../../../../../xdm/home.md):組織客戶體驗資料 [!DNL Experience Platform] 的標準化架構。
   * [架構構成基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自訂架構。
* [[!DNL即時客戶基本資料]](../../../../../profile/home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

如果您已經擁有有效的 [!DNL Salesforce] 帳戶，則可以跳過本文檔的其餘部分，並繼續有關配置資料 [流的教程](../../dataflow/crm.md)。

### 收集必要的認證

| 憑證 | 說明 |
| ---------- | ----------- |
| `environmentUrl` | 來源例項的 [!DNL Salesforce] URL。 |
| `username` | 使用者帳戶的 [!DNL Salesforce] 使用者名稱。 |
| `password` | 使用者帳戶 [!DNL Salesforce] 的密碼。 |
| `securityToken` | 使用者帳戶的安 [!DNL Salesforce] 全性Token。 |

如需快速入門的詳細資訊，請參 [閱此Salesforce檔案](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm)。

## 連線您的帳 [!DNL Salesforce] 戶

收集完所需的認證後，您可依照下列步驟將帳戶連結 [!DNL Salesforce] 至 [!DNL Platform]。

登入 [Adobe Experience Platform](https://platform.adobe.com) ，然後從左側導覽列選取 **[!UICONTROL Sources]** ，以存取 **** Sources工作區。 「目 **[!UICONTROL 錄]** 」畫面會顯示多種來源，您可以用來建立帳戶。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在「資料 **[!UICONTROL 庫]** 」類別下，選 **[!UICONTROL 取Salesforce]**。 如果這是您第一次使用此連接器，請選擇「配 **[!UICONTROL 置」]**。 否則，請選 **[!UICONTROL 取「新增資料]** 」以建立新的Salesforce連接器。

![目錄](../../../../images/tutorials/create/salesforce/catalog.png)

此時 **[!UICONTROL 會顯示「連線至Salesforce]** 」頁面。 在此頁上，您可以使用新認證或現有認證。

### 新帳戶

如果您使用新認證，請選擇「新 **[!UICONTROL 帳戶」]**。 在出現的輸入表單上，提供名稱、選用說明和您的認 [!DNL Salesforce] 證。 完成後，選擇 **[!UICONTROL Connect]** ，然後為建立新連接留出一些時間。

![連接](../../../../images/tutorials/create/salesforce/new.png)

### 現有帳戶

若要連線現有帳戶，請 [!DNL Salesforce] 選取您要連線的帳戶，然後選取右上角的 **[!UICONTROL Next]** （下一步）以繼續。

![現有](../../../../images/tutorials/create/salesforce/existing.png)

## 後續步驟

遵循本教學課程，您已建立與帳戶的 [!DNL Salesforce] 連線。 您現在可以繼續下一個教程，並 [配置資料流以將資料導入 [!DNL Platform]](../../dataflow/crm.md)。