---
keywords: Experience Platform；首頁；熱門主題； Veeva CRM; Veeva
solution: Experience Platform
title: 在UI中建立Veva CRM來源連線
topic-legacy: overview
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI建立Veva CRM來源連線。
source-git-commit: 3235c48ec1f449e45b3f4b096585b67e14600407
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 1%

---

# 在UI中建立[!DNL Veeva CRM]源連接

Adobe Experience Platform中的來源連接器可讓您排程內嵌外部來源的CRM資料。 本教學課程提供使用[!DNL Platform]使用者介面建立[!DNL Veeva CRM]來源連接器的步驟。

## 快速入門

本教學課程需要妥善了解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):組織客戶體驗資 [!DNL Experience Platform] 料的標準化架構。
   * [結構構成基本概念](../../../../../xdm/schema/composition.md):了解XDM結構描述的基本建置組塊，包括結構描述的主要原則和最佳實務。
   * [結構編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用結構編輯器UI建立自訂結構。
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。

如果您已經擁有有效的[!DNL Veeva CRM]帳戶，則可以跳過本文檔的其餘部分，並繼續參閱有關[配置資料流](../../dataflow/crm.md)的教程。

### 收集所需憑據

| 憑據 | 說明 |
| ---------- | ----------- |
| `environmentUrl` | [!DNL Veeva CRM]源實例的URL。 |
| `username` | [!DNL Veeva CRM]使用者帳戶的使用者名稱。 |
| `password` | [!DNL Veeva CRM]用戶帳戶的密碼。 |
| `securityToken` | [!DNL Veeva CRM]使用者帳戶的安全權杖。 |

有關入門的詳細資訊，請參閱[此Veeva CRM文檔]

## 連接您的[!DNL Veeva CRM]帳戶

收集到所需憑據後，可以按照以下步驟將[!DNL Veeva CRM]帳戶連結到[!DNL Platform]。

在平台UI中，從左側導覽列選取&#x200B;**[!UICONTROL Sources]**&#x200B;以存取[!UICONTROL Sources]工作區。 [!UICONTROL 目錄]螢幕顯示了各種源，您可以用這些源建立帳戶。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在[!UICONTROL CRM]類別下，選擇&#x200B;**[!UICONTROL Veeva CRM]**，然後選擇&#x200B;**[!UICONTROL Add data]**。

![目錄](../../../../images/tutorials/create/veeva/catalog.png)

此時將顯示&#x200B;**[!UICONTROL 連接Veva CRM帳戶]**&#x200B;頁。 在此頁面上，您可以使用新憑證或現有憑證。

### 現有帳戶

要使用現有帳戶，請選擇要使用建立新資料流的[!DNL Veeva CRM]帳戶，然後選擇&#x200B;**[!UICONTROL Next]**&#x200B;以繼續。

![現有](../../../../images/tutorials/create/veeva/existing.png)

### 新帳戶

如果要建立新帳戶，請選擇&#x200B;**[!UICONTROL 新帳戶]**，然後提供名稱、可選說明和您的[!DNL Veeva CRM]憑證。 完成後，選擇&#x200B;**[!UICONTROL 連接到源]**，然後允許一些時間建立新連接。

![new](../../../../images/tutorials/create/veeva/new.png)

## 後續步驟

依照本教學課程，您已建立與[!DNL Veeva CRM]帳戶的連線。 您現在可以繼續下一個教學課程，並[配置資料流以將資料帶入Platform](../../dataflow/crm.md)。
