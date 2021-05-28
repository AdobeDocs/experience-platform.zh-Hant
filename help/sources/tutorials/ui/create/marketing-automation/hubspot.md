---
keywords: Experience Platform；首頁；熱門主題；Hubspot;Hubspot
solution: Experience Platform
title: 在UI中建立HubSpot源連接
topic-legacy: overview
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI建立HubSpot來源連線。
exl-id: 452b7290-b9e8-4728-8b58-0e0c76bd9449
source-git-commit: e150f05df2107d7b3a2e95a55dc4ad072294279e
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 1%

---

# 在UI中建立[!DNL HubSpot]源連接

Adobe Experience Platform中的來源連接器可讓您依排程內嵌外部來源資料。 本教學課程提供使用[!DNL Platform]使用者介面建立[!DNL HubSpot]來源連接器的步驟。

## 快速入門

本教學課程需要妥善了解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):組織客戶體驗資 [!DNL Experience Platform] 料的標準化架構。
   * [結構構成基本概念](../../../../../xdm/schema/composition.md):了解XDM結構描述的基本建置組塊，包括結構描述的主要原則和最佳實務。
   * [結構編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用結構編輯器UI建立自訂結構。
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。

如果您已有[!DNL HubSpot]連接，則可跳過本文檔的其餘部分，並繼續參閱有關[配置資料流](../../dataflow/marketing-automation.md)的教程。

### 收集所需憑據

若要在[!DNL Platform]上存取您的[!DNL HubSpot]帳戶，您必須提供下列值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `clientId` | 與您的[!DNL HubSpot]應用程式相關聯的用戶端ID。 |
| `clientSecret` | 與您的[!DNL HubSpot]應用程式相關聯的用戶端密碼。 |
| `accessToken` | 初次驗證OAuth整合時取得的存取權杖。 |
| `refreshToken` | 初次驗證OAuth整合時取得的重新整理代號。 |

有關入門的詳細資訊，請參閱此[[!DNL HubSpot] document](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview)。

## 連接您的[!DNL HubSpot]帳戶

收集到所需憑據後，可以按照以下步驟將[!DNL HubSpot]帳戶連結到[!DNL Platform]。

登入[Adobe Experience Platform](https://platform.adobe.com)，然後從左側導覽列選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取&#x200B;**[!UICONTROL 來源]**&#x200B;工作區。 **[!UICONTROL 目錄]**&#x200B;螢幕顯示了各種源，您可以用這些源建立帳戶。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在&#x200B;**[!UICONTROL 行銷自動化]**&#x200B;類別下，選取&#x200B;**[!UICONTROL HubSpot]**。 如果這是您第一次使用此連接器，請選擇&#x200B;**[!UICONTROL 配置]**。 否則，選擇&#x200B;**[!UICONTROL 添加資料]**&#x200B;以建立新的[!DNL HubSpot]連接器。

![目錄](../../../../images/tutorials/create/hubspot/catalog.png)

此時將顯示「**[!UICONTROL 連接到HubSpot]**」頁。 在此頁面上，您可以使用新憑證或現有憑證。

### 新帳戶

如果您正在使用新憑據，請選擇&#x200B;**[!UICONTROL 新帳戶]**。 在顯示的輸入表單中，提供名稱、可選說明和您的[!DNL HubSpot]憑證。 完成後，選擇&#x200B;**[!UICONTROL Connect]**，然後允許一些時間建立新連接。

![connect](../../../../images/tutorials/create/hubspot/connect.png)

### 現有帳戶

要連接現有帳戶，請選擇要連接的[!DNL HubSpot]帳戶，然後選擇&#x200B;**[!UICONTROL Next]**&#x200B;以繼續。

![現有](../../../../images/tutorials/create/hubspot/existing.png)

## 後續步驟

依照本教學課程，您已建立與[!DNL HubSpot]帳戶的連線。 您現在可以繼續下一個教學課程和[配置資料流，將行銷自動化系統資料帶入 [!DNL Platform]](../../dataflow/marketing-automation.md)。
