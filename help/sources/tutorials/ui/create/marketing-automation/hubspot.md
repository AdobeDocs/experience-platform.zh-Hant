---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中建立HubSpot來源連接器
topic: overview
translation-type: tm+mt
source-git-commit: 7328226b8349ffcdddadbd27b74fc54328b78dc5
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 0%

---


# 在UI中建立HubSpot來源連接器

> [!NOTE]
> HubSpot連接器處於測試階段。 如需使用 [測試版標籤連接器的詳細資訊](../../../../home.md#terms-and-conditions) ，請參閱來源概觀。

Adobe Experience Platform中的來源連接器可讓您依計畫吸收外部來源的資料。 本教學課程提供使用平台使用者介面建立HubSpot來源連接器的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列元件有正確的認識：

* [體驗資料模型(XDM)系統](../../../../../xdm/home.md): Experience Platform組織客戶體驗資料的標準化架構。
   * [架構構成基礎](../../../../../xdm/schema/composition.md): 瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md): 瞭解如何使用架構編輯器UI建立自訂架構。
* [即時客戶個人檔案](../../../../../profile/home.md): 根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

如果您已有HubSpot基本連線，則可略過本檔案的其餘部分，並繼續有關設定行銷自動化 [資料流的教學課程](../../dataflow/marketing-automation.md)。

### 收集必要的認證

要訪問平台上的HubSpot帳戶，必須提供以下值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `clientId` | 與您的HubSpot應用程式相關聯的用戶端ID。 |
| `clientSecret` | 與您的HubSpot應用程式相關聯的用戶端密碼。 |
| `accessToken` | 首次驗證您的OAuth整合時取得的存取Token。 |
| `refreshToken` | 初次驗證您的OAuth整合時取得的重新整理Token。 |

有關快速入門的詳細資訊，請參閱此 [HubSpot檔案](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview)。

## 連接您的HubSpot帳戶

收集完所需憑證後，您可以遵循下列步驟，建立新的入站基本連線，將您的HubSpot帳戶連結至平台。

登入 <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> ，然後從左側導覽列選取 **Sources** ，以存取 ** Sources工作區。 「目 *錄* 」螢幕顯示各種源，您可以為其建立入站基本連接，而每個源顯示與其關聯的現有基本連接數。

在「行 *銷自動化* 」類別下，選取 **HubSpot** ，以在螢幕右側顯示資訊列。 資訊列提供所選來源的簡短說明，以及與來源連線或檢視其檔案的選項。 要建立新的入站基本連接，請選擇「 **連接源」**。

![目錄](../../../../images/tutorials/create/hubspot/catalog.png)

此時 *將顯示「連接到HubSpot* 」頁。 在此頁上，您可以使用新認證或現有認證。

### 新帳戶

如果您使用新認證，請選擇「新 **帳戶」**。 在顯示的輸入表單上，提供基本連線名稱、可選說明和HubSpot憑證。 完成後，選擇 **Connect** ，然後為建立新的基本連接留出一些時間。

![連接](../../../../images/tutorials/create/hubspot/connect.png)

### 現有帳戶

要連接現有帳戶，請選擇要連接的HubSpot帳戶，然後選擇「下 **一步** 」繼續。

![現有](../../../../images/tutorials/create/hubspot/existing.png)

## 後續步驟

在本教程中，您建立了與HubSpot帳戶的基本連接。 您現在可以繼續下一個教學課程，並設 [定資料流，將行銷自動化系統資料匯入平台](../../dataflow/marketing-automation.md)。