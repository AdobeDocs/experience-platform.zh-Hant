---
keywords: Experience Platform；首頁；熱門主題；源；連接器；oracle;
title: (Beta)使用平台UI建立Oracle響應系統源連接
description: 瞭解如何使用平台UI將Adobe Experience Platform連接到Oracle響應系統。
hide: true
hidefromtoc: true
exl-id: 9ec5e1c2-3d9e-4729-be81-89a85d5ea782
source-git-commit: 784ec5f799c591185620e8376a6980b4930d914a
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 1%

---

# (Beta)建立 [!DNL Oracle Responsys] 使用平台UI的源連接

>[!NOTE]
>
>的 [!DNL Oracle Responsys] 源為beta。 查看 [源概述](../../../../home.md#terms-and-conditions) 的子菜單。

本教程為您提供建立 [[!DNL Oracle Responsys]](../../../../connectors/marketing-automation/oracle-responsys.md) 源連接，使用Adobe Experience Platform用戶介面。

## 快速入門

本指南要求對平台的以下元件有良好的理解：

* [源](../../../../home.md):平台允許從各種源接收資料，同時讓您能夠使用平台服務構建、標籤和增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md):平台提供虛擬沙箱，將單個平台實例分區為獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

如果您已經通過身份驗證 [!DNL Oracle Responsys] 平台上的帳戶，則您可以跳過本文檔的其餘部分，繼續學習有關 [建立資料流，將營銷自動化資料帶到平台](../../dataflow/marketing-automation.md)。

### 收集所需憑據

為了連接 [!DNL Oracle Responsys] 到平台，必須提供以下驗證屬性的值：

| 憑據 | 說明 |
| --- | --- |
| 端點 | 您的REST身份驗證終結點URL [!DNL Oracle Responsys] 實例。 |
| 客戶端ID | 您的客戶端ID [!DNL Oracle Responsys] 實例。 |
| 客戶端密碼 | 你的客戶機密碼 [!DNL Oracle Responsys] 實例。 |

有關的身份驗證憑據的詳細資訊 [!DNL Oracle Responsys]，請參見 [[!DNL Oracle Responsys] 認證指南](https://docs.oracle.com/en/cloud/saas/marketing/responsys-develop/API/GetStarted/authentication.htm)。

收集了所需的憑據後，您可以按照以下步驟連結 [!DNL Oracle Responsys] 帳戶到平台。

## 連接 [!DNL Oracle Responsys] 帳戶

在平台UI中，選擇 **[!UICONTROL 源]** 從左側導航 [!UICONTROL 源] 工作區。 的 [!UICONTROL 目錄] 螢幕顯示可建立帳戶的各種源。

可以從螢幕左側的目錄中選擇相應的類別。 或者，您可以使用搜索選項找到要使用的特定源。

在 [!UICONTROL 營銷自動化] 類別，選擇 **[!UICONTROL Oracle響應系統]**，然後選擇 **[!UICONTROL 添加資料]**。

![Adobe Experience Platform源目錄與Oracle響應系統源目錄突出顯示。](../../../../images/tutorials/create/oracle-responsys/catalog.png)

的 **[!UICONTROL 連接Oracle響應系統帳戶]** 的子菜單。 在此頁上，您可以使用新憑據或現有憑據。

### 現有帳戶

要使用現有帳戶，請選擇 [!DNL Oracle Responsys] 要使用建立新資料流的帳戶，然後選擇 **[!UICONTROL 下一個]** 繼續。

![oracle響應系統的現有帳戶驗證螢幕。](../../../../images/tutorials/create/oracle-responsys/existing.png)

### 新帳戶

要建立新帳戶，請選擇 **[!UICONTROL 新帳戶]**，然後為您提供名稱、可選說明和相應的值 [!DNL Oracle Responsys] 憑據。 完成後，選擇 **[!UICONTROL 連接到源]** 然後再給新連接建立一段時間。

![oracle響應系統的新帳戶身份驗證螢幕。](../../../../images/tutorials/create/oracle-eloqua/new.png)

## 後續步驟

按照本教程，您已經驗證並建立了源連接 [!DNL Oracle Responsys] 帳戶和平台。 現在，您可以繼續下一個教程， [建立資料流，將營銷自動化資料帶到平台](../../dataflow/marketing-automation.md)。
