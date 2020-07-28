---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中建立PayPal來源連接器
topic: overview
translation-type: tm+mt
source-git-commit: 4f7d7e2bf255afe1588dbe7cfb2ec055f2dcbf75
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 1%

---


# 在UI中 [!DNL PayPal] 建立來源連接器

>[!NOTE]
> 連接 [!DNL PayPal] 器為測試版。 如需使用 [測試版標籤連接器的詳細資訊](../../../../home.md#terms-and-conditions) ，請參閱來源概觀。

Adobe Experience Platform中的來源連接器可讓您依計畫吸收外部來源的資料。 本教學課程提供使用使用者介 [!DNL PayPal] 面建立來源連接器 [!DNL Platform] 的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列元件有正確的認識：

* [體驗資料模型(XDM)系統](../../../../../xdm/home.md): 組織客戶體驗資料 [!DNL Experience Platform] 的標準化架構。
   * [架構構成基礎](../../../../../xdm/schema/composition.md): 瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md): 瞭解如何使用架構編輯器UI建立自訂架構。
* [即時客戶個人檔案](../../../../../profile/home.md): 根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

如果您已有基 [!DNL PayPal] 本連接，則可以跳過本文檔的其餘部分，並繼續有關配置資料 [流的教程](../../dataflow/payments.md)

### 收集必要的認證

若要存取您的帳 [!DNL PayPal] 戶 [!DNL Platform]，您必須提供下列值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `host` | 實例的URL [!DNL PayPal] 。 |
| `clientID` | 與您的應用程式相關聯的用戶 [!DNL PayPal] 端ID。 |
| `clientSecret` | 與您的應用程式相關聯的用戶端 [!DNL PayPal] 密碼。 |

如需快速入門的詳細資訊，請參閱本 [PayPal檔案](https://developer.paypal.com/docs/api/overview/#get-credentials)

## 連線您的帳 [!DNL PayPal] 戶

收集完所需憑證後，您可依照下列步驟建立新的入站基本連線，將帳戶連結 [!DNL PayPal] 至 [!DNL Platform]。

登入 <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> ，然後從左側導覽列選取 **[!UICONTROL Sources]** ，以存取 ** Sources工作區。 「目 *[!UICONTROL 錄]* 」螢幕顯示各種源，您可以為其建立入站基本連接，而每個源顯示與其關聯的現有基本連接數。

在「 *[!UICONTROL CRM]* 」類別下 **[!UICONTROL ，選取「]** PayPal」以在螢幕右側顯示資訊列。 資訊列提供所選來源的簡短說明，以及與來源連線或檢視其檔案的選項。 要建立新的入站基本連接，請選擇「 **[!UICONTROL 連接源」]**。

![目錄](../../../../images/tutorials/create/paypal/catalog.png)

此時 *[!UICONTROL 會顯示「連線至PayPal]* 」頁面。 在此頁上，您可以使用新認證或現有認證。

### 新帳戶

如果您使用新認證，請選擇「新 **[!UICONTROL 帳戶」]**。 在出現的輸入表單上，提供基本連線名稱、選用說明和您的認 [!DNL PayPal] 證。 完成後，選擇 **[!UICONTROL Connect]** ，然後為建立新的基本連接留出一些時間。

![連接](../../../../images/tutorials/create/paypal/connect.png)

### 現有帳戶

若要連線現有帳戶，請選 [!DNL PayPal] 取您要連線的帳戶，然後選取「下 **[!UICONTROL 一]** 步」繼續。

![現有](../../../../images/tutorials/create/paypal/existing.png)

## 後續步驟

在本教學課程中，您已建立了與帳戶的基本連 [!DNL PayPal] 接。 您現在可以繼續下一個教學課程， [並設定資料流，將CRM資料匯入平台](../../dataflow/payments.md)。