---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中建立PayPal來源連接器
topic: overview
translation-type: tm+mt
source-git-commit: 2162c66b1664ecaaf0b609fe3f7ccf58c4a5d31d
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 1%

---


# 在UI中建立PayPal來源連接器

> [!NOTE]
> PayPal連接器為beta版。 功能和檔案可能會有所變更。

Adobe Experience Platform中的來源連接器可讓您依計畫吸收外部來源的資料。 本教學課程提供使用平台使用者介面建立PayPal來源連接器的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列元件有正確的認識：

* [體驗資料模型(XDM)系統](../../../../../xdm/home.md): Experience Platform組織客戶體驗資料的標準化架構。
   * [架構構成基礎](../../../../../xdm/schema/composition.md): 瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md): 瞭解如何使用架構編輯器UI建立自訂架構。
* [即時客戶個人檔案](../../../../../profile/home.md): 根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

如果您已有PayPal基本連接，則可以略過本文檔的其餘部分，然後繼續有關配置資料 [流的教程](../../dataflow/payments.md)

### 收集必要的認證

若要存取您的PayPal帳戶平台，您必須提供下列值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `host` | PayPal例項的URL。 |
| `clientID` | 與您的PayPal應用程式相關聯的用戶端ID。 |
| `clientSecret` | 與您的PayPal應用程式相關聯的用戶端密碼。 |

如需快速入門的詳細資訊，請參閱本 [PayPal檔案](https://developer.paypal.com/docs/api/overview/#get-credentials)

## 連接您的PayPal帳戶

收集完所需憑證後，您可依照下列步驟建立新的傳入基本連線，將PayPal帳戶連結至平台。

登入 <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> ，然後從左側導覽列選取 **Sources** ，以存取 ** Sources工作區。 「目 *錄* 」螢幕顯示各種源，您可以為其建立入站基本連接，而每個源顯示與其關聯的現有基本連接數。

在「 *CRM* 」類別下 **，選取「** PayPal」以在螢幕右側顯示資訊列。 資訊列提供所選來源的簡短說明，以及與來源連線或檢視其檔案的選項。 要建立新的入站基本連接，請選擇「 **連接源」**。

![目錄](../../../../images/tutorials/create/paypal/catalog.png)

此時 *會顯示「連線至PayPal* 」頁面。 在此頁上，您可以使用新認證或現有認證。

### 新帳戶

如果您使用新認證，請選擇「新 **帳戶」**。 在出現的輸入表單上，提供基本連線名稱、選用說明和您的PayPal認證。 完成後，選擇 **Connect** ，然後為建立新的基本連接留出一些時間。

![連接](../../../../images/tutorials/create/paypal/connect.png)

### 現有帳戶

若要連線現有帳戶，請選取您要連線的PayPal帳戶，然後選取「下 **一** 步」繼續。

![現有](../../../../images/tutorials/create/paypal/existing.png)

## 後續步驟

在本教學課程中，您已建立PayPal帳戶的基本連線。 您現在可以繼續下一個教學課程， [並設定資料流，將CRM資料匯入平台](../../dataflow/payments.md)。