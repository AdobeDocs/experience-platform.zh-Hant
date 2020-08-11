---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中建立Microsoft Dynamics來源連接器
topic: overview
translation-type: tm+mt
source-git-commit: 41fe3e5b2a830c3182b46b3e0873b1672a1f1b03
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 1%

---


# 在UI中 [!DNL Microsoft Dynamics] 建立來源連接器

Adobe Experience Platform中的來源連接器可讓您依計畫吸收外部來源的CRM資料。 本教學課程提供使用使 [!DNL Microsoft Dynamics] 用者介面建立(以下稱為「[!DNL Dynamics]」)來源連接器 [!DNL Platform] 的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列元件有正確的認識：

* [體驗資料模型(XDM)系統](../../../../../xdm/home.md):組織客戶體驗資料 [!DNL Experience Platform] 的標準化架構。
   * [架構構成基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自訂架構。
* [即時客戶個人檔案](../../../../../profile/home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

如果您已經擁有有效的 [!DNL Dynamics] 帳戶，則可以跳過本文檔的其餘部分，並繼續有關配置資料 [流的教程](../../dataflow/crm.md)。

### 收集必要的認證

| 憑證 | 說明 |
| ---------- | ----------- |
| `serviceUri` | 您實例的服務 [!DNL Dynamics] URL。 |
| `username` | 您使用者帳戶的 [!DNL Dynamics] 使用者名稱。 |
| `password` | 您的Dynamics帳戶的密碼。 |

如需快速入門的詳細資訊，請造訪 [此Dynamics檔案](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth)。

## 連線您的帳 [!DNL Dynamics] 戶

收集完所需的認證後，您可依照下列步驟建立新帳戶以 [!DNL Dynamics] 連接至 [!DNL Platform]。

登入 [Adobe Experience Platform](https://platform.adobe.com) ，然後從左側導覽列選取 **[!UICONTROL Sources]** ，以存取 ** Sources工作區。 「目 *[!UICONTROL 錄]* 」畫面會顯示多種來源，您可以為其建立傳入帳戶，而每個來源會顯示與其關聯的現有帳戶和資料集流量。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在「數 *[!UICONTROL 據庫]* 」類別下，選擇 **[!UICONTROL Dynamics]** , **[!UICONTROL 然後添加資料]** ，以建立新 [!DNL Dynamics] 連接器。

![目錄](../../../../images/tutorials/create/ms-dynamics/catalog.png)

此時將 *[!UICONTROL 顯示「連接到動態]* 」頁。 在此頁上，您可以使用新認證或現有認證。

### 新帳戶

如果您使用新認證，請選擇「新 **[!UICONTROL 帳戶」]**。 在出現的輸入表單上，提供連線名稱、選用說明和您的認 [!DNL Dynamics] 證。 完成後，選擇 **[!UICONTROL Connect]** ，然後為新帳戶建立留出一些時間。

![連接](../../../../images/tutorials/create/ms-dynamics/new.png)

### 現有帳戶

若要連線現有帳戶，請 [!DNL Dynamics] 選取您要連線的帳戶，然後選取右上角的 **[!UICONTROL Next]** （下一步）以繼續。

![現有](../../../../images/tutorials/create/ms-dynamics/existing.png)

## 後續步驟

遵循本教學課程，您已建立與帳戶的 [!DNL Dynamics] 連線。 您現在可以繼續下一個教程，並 [配置資料流以將資料導入平台](../../dataflow/crm.md)。