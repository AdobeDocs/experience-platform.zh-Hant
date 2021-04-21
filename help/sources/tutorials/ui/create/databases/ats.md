---
keywords: Experience Platform；首頁；熱門主題；Azure表儲存；azure表儲存；ats;ATS
solution: Experience Platform
title: 在UI中建立Azure表格儲存來源連線
topic-legacy: overview
type: Tutorial
description: 瞭解如何使用Adobe Experience PlatformUI建立Azure表格儲存來源連線。
exl-id: 045cb954-e3e1-439d-a3cd-170d688dfbc8
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 1%

---

# 在UI中建立[!DNL Azure Table Storage]來源連線

>[!NOTE]
>
>[!DNL Azure Table Storage]介面處於測試狀態。 有關使用beta標籤連接器的詳細資訊，請參閱[ Sources綜覽](../../../../home.md#terms-and-conditions)。

Adobe Experience Platform的來源連接器提供按計畫接收外部來源資料的能力。 本教學課程提供使用[!DNL Platform]使用者介面建立[!DNL Azure Table Storage]（以下稱為「ATS」）來源連接器的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列部分有正確的理解：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):組織客戶體驗資 [!DNL Experience Platform] 料的標準化架構。
   * [架構構成基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自訂架構。
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

如果您已經有有效的ATS連接，則可以跳過本文檔的其餘部分，繼續[配置資料流](../../dataflow/databases.md)的教程。

### 收集必要的認證

若要存取[!DNL Platform]上的ATS帳戶，您必須提供下列值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `connectionString` | 要連接到[!DNL Azure Table Storage]實例的連接字串。 連線至ATS例項的連線字串。 ATS的連接字串模式是`DefaultEndpointsProtocol=https;AccountName={ACCOUNT_NAME};AccountKey={ACCOUNT_KEY}`。 |

有關入門的詳細資訊，請參閱[this [!DNL Azure Table Storage] document](https://docs.microsoft.com/en-us/azure/storage/common/storage-introduction)。

## 連接您的[!DNL Azure Table Storage]帳戶

收集完所需的認證後，您可依照下列步驟將ATS帳戶連結至[!DNL Platform]。

登入[Adobe Experience Platform](https://platform.adobe.com)，然後從左側導覽列選擇&#x200B;**[!UICONTROL Sources]**&#x200B;以存取&#x200B;**[!UICONTROL Sources]**&#x200B;工作區。 **[!UICONTROL Catalog]**&#x200B;畫面會顯示各種來源，您可以用來建立帳戶。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在&#x200B;**[!UICONTROL Databases]**&#x200B;類別下，選擇&#x200B;**[!UICONTROL Azure Table Storage]**。 如果這是您第一次使用此連接器，請選擇&#x200B;**[!UICONTROL Configure]**。 否則，請選擇&#x200B;**[!UICONTROL Add data]**&#x200B;以建立新的ATS連接器。

![目錄](../../../../images/tutorials/create/ats/catalog.png)

此時將顯示&#x200B;**[!UICONTROL Connect to Azure Table Storage]**&#x200B;頁。 在此頁上，您可以使用新認證或現有認證。

### 新帳戶

如果使用新憑據，請選擇&#x200B;**[!UICONTROL New account]**。 在出現的輸入表單上，提供名稱、選用說明和您的ATS認證。 完成後，選擇&#x200B;**[!UICONTROL Connect]** ，然後允許一些時間建立新連接。

![連接](../../../../images/tutorials/create/ats/new.png)

### 現有帳戶

若要連線現有帳戶，請選取您要連線的ATS帳戶，然後選取&#x200B;**[!UICONTROL Next]**&#x200B;以繼續。

![現有](../../../../images/tutorials/create/ats/existing.png)

## 後續步驟

在本教學課程中，您已建立與ATS帳戶的連線。 現在，您可以繼續下一個教程，並[配置資料流以將資料導入 [!DNL Platform]](../../dataflow/databases.md)。
