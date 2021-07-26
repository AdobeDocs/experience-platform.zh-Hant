---
keywords: Experience Platform；首頁；熱門主題；salesforce marketing cloud;Salesforce Marketing Cloud
solution: Experience Platform
title: 在UI中建立SalesforceMarketing Cloud來源連線
topic-legacy: overview
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI建立SalesforceMarketing Cloud來源連線。
source-git-commit: f196da32f67578ad1d73f3200f6050a7ddab0d88
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 1%

---

# 在UI中建立[!DNL Salesforce Marketing Cloud]源連接

>[!NOTE]
>
> [!DNL Salesforce Marketing Cloud]源位於測試版。 有關使用測試版標籤的來源的詳細資訊，請參閱[來源概述](../../../../home.md#terms-and-conditions)。

Adobe Experience Platform中的來源連接器可讓您依排程內嵌外部來源資料。 本教學課程提供使用Platform使用者介面建立[!DNL Salesforce Marketing Cloud]來源連接器的步驟。

## 快速入門

本教學課程需要妥善了解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):組織客戶體驗資 [!DNL Experience Platform] 料的標準化架構。
   * [結構構成基本概念](../../../../../xdm/schema/composition.md):了解XDM結構描述的基本建置組塊，包括結構描述的主要原則和最佳實務。
   * [結構編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用結構編輯器UI建立自訂結構。
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。

如果您已有[!DNL Salesforce Marketing Cloud]連接，則可跳過本文檔的其餘部分，並繼續參閱有關[配置資料流](../../dataflow/marketing-automation.md)的教程。

### 收集所需憑據

若要在Platform上存取您的[!DNL Salesforce Marketing Cloud]帳戶，您必須提供下列值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `host` | 應用程式的主機伺服器。 這通常是您的子網域。 |
| `clientId` | 與您的[!DNL Salesforce Marketing Cloud]應用程式相關聯的用戶端ID。 |
| `clientSecret` | 與您的[!DNL Salesforce Marketing Cloud]應用程式相關聯的用戶端密碼。 |

有關入門的詳細資訊，請參閱此[[!DNL Salesforce Marketing Cloud] document](https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm)。

## 連接您的[!DNL Salesforce Marketing Cloud]帳戶

收集完所需憑證後，您可以依照下列步驟將您的[!DNL Salesforce Marketing Cloud]帳戶連結至Platform。

在平台UI中，從左側導覽中選取&#x200B;**[!UICONTROL Sources]**&#x200B;以存取[!UICONTROL Sources]工作區。 [!UICONTROL 目錄]螢幕顯示了各種源，您可以用這些源建立帳戶。

您可以從畫面左側的目錄中選取適當的類別。 您也可以使用搜尋列來縮小顯示的連接器。

在[!UICONTROL 行銷自動化]類別下，選擇&#x200B;**[!UICONTROL SalesforceMarketing Cloud]**，然後選擇&#x200B;**[!UICONTROL 設定]**。

![目錄](../../../../images/tutorials/create/salesforce-marketing-cloud/catalog.png)

此時將顯示&#x200B;**[!UICONTROL 連接到SalesforceMarketing Cloud]**&#x200B;頁。 在此頁面上，您可以使用新憑證或現有憑證。

### 新帳戶

如果您正在使用新憑據，請選擇&#x200B;**[!UICONTROL 新帳戶]**。 在顯示的輸入表單中，提供名稱、可選說明和您的[!DNL Salesforce Marketing Cloud]憑證。 完成後，選擇&#x200B;**[!UICONTROL Connect]**，然後允許一些時間建立新連接。

![new](../../../../images/tutorials/create/salesforce-marketing-cloud/new.png)

### 現有帳戶

要連接現有帳戶，請選擇要連接的[!DNL Salesforce Marketing Cloud]帳戶，然後選擇&#x200B;**[!UICONTROL Next]**&#x200B;以繼續。

![現有](../../../../images/tutorials/create/salesforce-marketing-cloud/existing.png)

## 後續步驟

依照本教學課程，您已建立與[!DNL Salesforce Marketing Cloud]帳戶的連線。 您現在可以繼續進行下一個教學課程和[設定資料流，將行銷自動化系統資料帶入Platform](../../dataflow/marketing-automation.md)。
