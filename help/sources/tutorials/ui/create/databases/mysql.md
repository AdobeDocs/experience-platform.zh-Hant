---
keywords: Experience Platform；首頁；熱門主題；mysql;MySQL
solution: Experience Platform
title: 在UI中建立MySQL源連接
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI建立MySQL源連接。
exl-id: 75e74bde-6199-4970-93d2-f95ec3a59aa5
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 1%

---

# 建立 [!DNL MySQL] UI中的源連接

Adobe Experience Platform中的來源連接器可讓您依排程內嵌外部來源資料。 本教學課程提供建立 [!DNL MySQL] 來源連線。

## 快速入門

本教學課程需要妥善了解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化架構。
   * [結構構成基本概念](../../../../../xdm/schema/composition.md):了解XDM結構描述的基本建置組塊，包括結構描述的主要原則和最佳實務。
   * [結構編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用結構編輯器UI建立自訂結構。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。

如果您已有 [!DNL MySQL] 連線，您可以略過本檔案的其餘部分，並繼續進行有關 [配置資料流](../../dataflow/databases.md).

### 收集所需憑據

若要存取 [!DNL MySQL] 帳戶 [!DNL Platform]，您必須提供下列值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `connectionString` | 此 [!DNL MySQL] 與您的帳戶相關聯的連線字串。 此 [!DNL MySQL] 連線字串模式為： `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. 您可以閱讀 [[!DNL MySQL] 檔案](https://dev.mysql.com/doc/connector-net/en/connector-net-connections-string.html). |

## 連接您的 [!DNL MySQL] 帳戶

收集完所需憑證後，您可以依照下列步驟連結您的 [!DNL MySQL] 帳戶 [!DNL Platform].

登入 [Adobe Experience Platform](https://platform.adobe.com) 然後選取 **[!UICONTROL 來源]** 從左側導覽列存取 **[!UICONTROL 來源]** 工作區。 此 **[!UICONTROL 目錄]** 畫面會顯示您可以為其建立帳戶的各種來源。

在 **[!UICONTROL 資料庫]** 類別，選擇 **[!UICONTROL MySQL]**. 如果這是您第一次使用此連接器，請選取 **[!UICONTROL 設定]**. 否則，請選取 **[!UICONTROL 新增資料]** 建立新 [!DNL MySQL] 連接器。

![](../../../../images/tutorials/create/my-sql/catalog.png)

此 **[!UICONTROL 連接到MySQL]** 頁。 在此頁面上，您可以使用新憑證或現有憑證。

### 新帳戶

如果使用新憑據，請選擇 **[!UICONTROL 新帳戶]**. 在顯示的輸入表單中，提供名稱、選用說明和您的 [!DNL MySQL] 憑證。 完成後，請選取 **[!UICONTROL Connect]** 然後讓新連接建立一段時間。

![](../../../../images/tutorials/create/my-sql/new.png)

### 現有帳戶

若要連線現有帳戶，請選取 [!DNL MySQL] 要連接的帳戶，然後選擇 **[!UICONTROL 下一個]** 繼續。

![](../../../../images/tutorials/create/my-sql/existing.png)

## 後續步驟

按照本教程，您已建立到MySQL帳戶的連接。 您現在可以繼續下一個教學課程，以及 [配置資料流以將資料帶入 [!DNL Platform]](../../dataflow/databases.md).
