---
keywords: Experience Platform;home；熱門主題；Oracle資料庫；oracle資料庫
solution: Experience Platform
title: 在UI中建立Oracle資料庫源連接
topic-legacy: overview
type: Tutorial
description: 瞭解如何使用Adobe Experience PlatformUI建立Oracle資料庫源連接。
exl-id: 4ca6ecc6-0382-4cee-acc5-1dec7eeb9443
translation-type: tm+mt
source-git-commit: b2384bfe26fa3d111c342062b2d9bb37c4226857
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 1%

---

# 在UI中建立[!DNL Oracle DB]來源連線

Adobe Experience Platform的來源連接器提供按計畫接收外部來源資料的能力。 本教程提供使用[!DNL Platform]用戶介面建立[!DNL Oracle DB]源連接器的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列部分有正確的理解：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):組織客戶體驗資 [!DNL Experience Platform] 料的標準化架構。
   * [架構構成基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自訂架構。
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

如果您已經有有效的[!DNL Oracle DB]連接，則可跳過本文檔的其餘部分，繼續[配置資料流](../../dataflow/databases.md)的教程。

### 收集必要的認證

若要存取[!DNL Platform]上的[!DNL Oracle DB]帳戶，您必須提供下列值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `connectionString` | 用於連接到[!DNL Oracle DB]的連接字串。 [!DNL Oracle DB]連接字串模式是：`Host={HOST};Port={PORT};Sid={SID};User Id={USERNAME};Password={PASSWORD}`。 |
| `connectionSpec.id` | 建立連線所需的唯一識別碼。 [!DNL Oracle DB]的連接規範ID為`d6b52d86-f0f8-475f-89d4-ce54c8527328`。 |

有關入門的詳細資訊，請參閱[本Oracle文檔](https://docs.oracle.com/database/121/ODPNT/featConnecting.htm#ODPNT199)。

## 連接您的[!DNL Oracle DB]帳戶

收集完所需憑證後，您可以按照以下步驟將[!DNL Oracle DB]帳戶連結到[!DNL Platform]。

登入[Adobe Experience Platform](https://platform.adobe.com)，然後從左側導覽列選擇&#x200B;**[!UICONTROL Sources]**&#x200B;以存取&#x200B;**[!UICONTROL Sources]**&#x200B;工作區。 **[!UICONTROL Catalog]**&#x200B;畫面會顯示各種來源，您可以用來建立帳戶。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在&#x200B;**[!UICONTROL Databases]**&#x200B;類別下，選擇&#x200B;**[!UICONTROL Oracle DB]**。 如果這是您第一次使用此連接器，請選擇&#x200B;**[!UICONTROL Configure]**。 否則，請選擇&#x200B;**[!UICONTROL Add data]**&#x200B;以建立新的[!DNL Oracle DB]連接器。

![目錄](../../../../images/tutorials/create/oracle/catalog.png)

此時將顯示&#x200B;**[!UICONTROL Connect to Oracle DB]**&#x200B;頁。 在此頁上，您可以使用新認證或現有認證。

### 新帳戶

如果使用新憑據，請選擇&#x200B;**[!UICONTROL New account]**。 在顯示的輸入表單上，提供名稱、可選說明和您的[!DNL Oracle DB]憑證。 完成後，選擇&#x200B;**[!UICONTROL Connect]** ，然後允許一些時間建立新連接。

![連接](../../../../images/tutorials/create/oracle/new.png)

### 現有帳戶

要連接現有帳戶，請選擇要連接的[!DNL Oracle DB]帳戶，然後選擇&#x200B;**[!UICONTROL Next]**&#x200B;繼續。

![現有](../../../../images/tutorials/create/oracle/existing.png)

## 後續步驟

在本教學課程之後，您已建立與[!DNL Oracle DB]帳戶的連線。 現在，您可以繼續下一個教程，並[配置資料流以將資料導入 [!DNL Platform]](../../dataflow/databases.md)。
