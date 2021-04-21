---
keywords: Experience Platform;home；熱門主題；mysql;MySQL
solution: Experience Platform
title: 在UI中建立MySQL源連接
topic-legacy: overview
type: Tutorial
description: 瞭解如何使用Adobe Experience PlatformUI建立MySQL源連接。
exl-id: 75e74bde-6199-4970-93d2-f95ec3a59aa5
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 1%

---

# 在UI中建立[!DNL MySQL]源連接

Adobe Experience Platform的來源連接器提供按計畫接收外部來源資料的能力。 本教學課程提供使用Adobe Experience PlatformUI建立[!DNL MySQL]源連接的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列部分有正確的理解：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化架構。
   * [架構構成基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自訂架構。
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

如果您已有[!DNL MySQL]連接，則可跳過本文檔的其餘部分，繼續[配置資料流](../../dataflow/databases.md)的教程。

### 收集必要的認證

若要存取[!DNL Platform]上的[!DNL MySQL]帳戶，您必須提供下列值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `connectionString` | 與您的帳戶關聯的[!DNL MySQL]連線字串。 [!DNL MySQL]連接字串模式是：`Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`。 您可閱讀[[!DNL MySQL] document](https://dev.mysql.com/doc/connector-net/en/connector-net-connections-string.html)，進一步瞭解連線字串以及如何取得。 |

## 連接您的[!DNL MySQL]帳戶

收集完所需憑證後，您可以按照以下步驟將[!DNL MySQL]帳戶連結至[!DNL Platform]。

登入[Adobe Experience Platform](https://platform.adobe.com)，然後從左側導覽列選擇&#x200B;**[!UICONTROL Sources]**&#x200B;以存取&#x200B;**[!UICONTROL Sources]**&#x200B;工作區。 **[!UICONTROL Catalog]**&#x200B;畫面會顯示各種來源，您可以用來建立帳戶。

在&#x200B;**[!UICONTROL Databases]**&#x200B;類別下，選擇&#x200B;**[!UICONTROL MySQL]**。 如果這是您第一次使用此連接器，請選擇&#x200B;**[!UICONTROL Configure]**。 否則，請選擇&#x200B;**[!UICONTROL Add data]**&#x200B;以建立新的[!DNL MySQL]連接器。

![](../../../../images/tutorials/create/my-sql/catalog.png)

此時將顯示&#x200B;**[!UICONTROL Connect to MySQL]**&#x200B;頁。 在此頁上，您可以使用新認證或現有認證。

### 新帳戶

如果使用新憑據，請選擇&#x200B;**[!UICONTROL New account]**。 在顯示的輸入表單上，提供名稱、可選說明和您的[!DNL MySQL]憑證。 完成後，選擇&#x200B;**[!UICONTROL Connect]** ，然後允許一些時間建立新連接。

![](../../../../images/tutorials/create/my-sql/new.png)

### 現有帳戶

要連接現有帳戶，請選擇要連接的[!DNL MySQL]帳戶，然後選擇&#x200B;**[!UICONTROL Next]**&#x200B;繼續。

![](../../../../images/tutorials/create/my-sql/existing.png)

## 後續步驟

通過本教程，您已建立了與MySQL帳戶的連接。 現在，您可以繼續下一個教程，並[配置資料流以將資料導入 [!DNL Platform]](../../dataflow/databases.md)。
