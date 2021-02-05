---
keywords: Experience Platform; home；熱門主題；Salesforce Service Cloud;salesforce Service Cloud
solution: Experience Platform
title: 在UI中建立Salesforce Service Cloud來源連線
topic: overview
type: Tutorial
description: 瞭解如何使用Adobe Experience Platform UI建立Salesforce Service Cloud來源連線。
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 1%

---


# 在UI中建立[!DNL Salesforce Service Cloud]源連接

>[!NOTE]
>
>[!DNL Salesforce Service Cloud]介面處於測試狀態。 有關使用beta標籤連接器的詳細資訊，請參閱[來源概觀](../../../../home.md#terms-and-conditions)。

Adobe Experience Platform中的來源連接器可讓您依計畫吸收外部來源的資料。 本教程提供使用[!DNL Platform]用戶介面建立[!DNL Salesforce Service Cloud]（下稱「SSC」）源連接器的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列元件有正確的認識：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):組織客戶體驗資 [!DNL Experience Platform] 料的標準化架構。
   * [架構構成基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自訂架構。
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

如果您已經有有效的SSC連接，則可以跳過本文檔的其餘部分，繼續[配置資料流](../../dataflow/customer-success.md)的教程

### 收集必要的認證

要訪問[!DNL Platform]上的SSC帳戶，必須提供以下值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `username` | 使用者帳戶的使用者名稱。 |
| `password` | 使用者帳戶的密碼。 |
| `securityToken` | 使用者帳戶的安全性Token。 |

有關入門的詳細資訊，請參閱[this [!DNL Salesforce Service Cloud] document](https://developer.salesforce.com/docs/atlas.en-us.api_iot.meta/api_iot/qs_auth_access_token.htm)。

## 連接您的[!DNL Salesforce Service Cloud]帳戶

收集到所需憑據後，您可以按照以下步驟將SSC帳戶連結到[!DNL Platform]。

登入[Adobe Experience Platform](https://platform.adobe.com)，然後從左側導覽列選擇&#x200B;**[!UICONTROL Sources]**&#x200B;以存取&#x200B;**[!UICONTROL Sources]**&#x200B;工作區。 **[!UICONTROL Catalog]**&#x200B;畫面會顯示多種來源，您可以用來建立帳戶。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在&#x200B;**[!UICONTROL 客戶成功]**&#x200B;類別下，選擇&#x200B;**[!UICONTROL Salesforce Service Cloud]**。 如果這是您第一次使用此連接器，請選擇&#x200B;**[!UICONTROL Configure]**。 否則，請選擇&#x200B;**[!UICONTROL 添加資料]**&#x200B;以建立新的SSC連接器。

![目錄](../../../../images/tutorials/create/ssc/catalog.png)

此時會顯示&#x200B;**[!UICONTROL 連線至Salesforce Service Cloud]**&#x200B;頁面。 在此頁上，您可以使用新認證或現有認證。

### 新帳戶

如果您使用新憑據，請選擇&#x200B;**[!UICONTROL 新建帳戶]**。 在顯示的輸入表單上，提供名稱、可選說明和您的SSC憑據。 完成後，選擇&#x200B;**[!UICONTROL Connect]** ，然後為建立新連接留出一些時間。

![連接](../../../../images/tutorials/create/ssc/connect.png)

### 現有帳戶

要連接現有帳戶，請選擇要連接的SSC帳戶，然後選擇&#x200B;**[!UICONTROL Next]**&#x200B;繼續。

![現有](../../../../images/tutorials/create/ssc/existing.png)

## 後續步驟

通過本教程，您已建立了與SSC帳戶的連接。 您現在可以繼續下一個教程，並[配置資料流以將客戶成功資料導入 [!DNL Platform]](../../dataflow/customer-success.md)。