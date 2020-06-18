---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中建立Google AdWords來源連接器
topic: overview
translation-type: tm+mt
source-git-commit: b9e9207741044f118d53ab8eb3d3d6cd7451132d
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 0%

---


# 在UI中建立Google AdWords來源連接器

>[!NOTE]
>Google AdWords連接器是測試版。 如需使用 [測試版標籤連接器的詳細資訊](../../../../home.md#terms-and-conditions) ，請參閱來源概觀。

Adobe Experience Platform中的來源連接器可讓您依計畫吸收外部來源的資料。 本教學課程提供使用平台使用者介面建立Google AdWords來源連接器的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列元件有正確的認識：

* [體驗資料模型(XDM)系統](../../../../../xdm/home.md): Experience Platform組織客戶體驗資料的標準化架構。
   * [架構構成基礎](../../../../../xdm/schema/composition.md): 瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md): 瞭解如何使用架構編輯器UI建立自訂架構。
* [即時客戶個人檔案](../../../../../profile/home.md): 根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

如果您已有Google AdWords連線，則可略過本檔案的其餘部分，並繼續有關設定資料 [流的教學課程](../../dataflow/payments.md)

### 收集必要的認證

若要存取您的Google AdWords帳戶平台，您必須提供下列值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `clientCustomerId` | AdWords帳戶的客戶客戶ID。 |
| `developerToken` | 與管理員帳戶關聯的開發人員Token。 |
| `refreshToken` | 從Google取得的重新整理Token，以授權存取AdWords。 |
| `clientId` | 用來取得重新整理Token之Google應用程式的用戶端ID。 |
| `clientSecret` | 用來取得重新整理Token之Google應用程式的用戶端密碼。 |

如需快速入門的詳細資訊，請參閱此 [Google AdWords檔案](https://developers.google.com/adwords/api/docs/guides/authentication)。

## 連線您的Google AdWords帳戶

收集完所需的認證後，您可以依照下列步驟建立新的傳入基本連線，將您的Google AdWords帳戶連結至平台。

登入 [Adobe Experience Platform](https://platform.adobe.com) ，然後從左側導覽列選取 **Sources** ，以存取 ** Sources工作區。 「目 *錄* 」螢幕顯示各種源，您可以為其建立入站基本連接，而每個源顯示與其關聯的現有基本連接數。

在「 *廣告* 」類別下，選取 **Google AdWords** ，以在螢幕右側顯示資訊列。 資訊列提供所選來源的簡短說明，以及與來源連線或檢視其檔案的選項。 要建立新的入站基本連接，請選擇「 **連接源」**。

![目錄](../../../../images/tutorials/create/ads/catalog.png)

此時 *會顯示「連線至Google AdWords* 」頁面。 在此頁上，您可以使用新認證或現有認證。

### 新帳戶

如果您使用新認證，請選擇「新 **帳戶」**。 在出現的輸入表單上，提供基本連線以及名稱、選用說明和您的Google AdWords憑證。 完成後，選擇 **Connect** ，然後為建立新的基本連接留出一些時間。

![連接](../../../../images/tutorials/create/ads/connect.png)

### 現有帳戶

若要連線現有帳戶，請選取您要連線的Google AdWords帳戶，然後選取「下 **一** 步」繼續。

![現有](../../../../images/tutorials/create/ads/existing.png)

## 後續步驟

在本教學課程中，您已建立Google AdWords帳戶的基本連線。 您現在可以繼續下一個教學課程，並 [設定資料流，將廣告資料匯入Platform](../../dataflow/advertising.md)。