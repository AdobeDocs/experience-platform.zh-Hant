---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中建立Azure Synapse Analytics來源連接器
topic: overview
translation-type: tm+mt
source-git-commit: 0a2247a9267d4da481b3f3a5dfddf45d49016e61
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 1%

---


# 在UI中建立Azure Synapse Analytics來源連接器

> [!NOTE]
> Azure Synapse Analytics連接器處於測試階段。 功能和檔案可能會有所變更。

Adobe Experience Platform中的來源連接器可讓您依計畫吸收外部來源的資料。 本教學課程提供使用平台使用者介面建立Azure Synapse Analytics（以下稱為「Synapse」）來源連接器的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列元件有正確的認識：

* [體驗資料模型(XDM)系統](../../../../../xdm/home.md): Experience Platform組織客戶體驗資料的標準化架構。
   * [架構構成基礎](../../../../../xdm/schema/composition.md): 瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md): 瞭解如何使用架構編輯器UI建立自訂架構。
* [即時客戶個人檔案](../../../../../profile/home.md): 根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

如果已經有Synapse基連接，則可以跳過本文檔的其餘部分，並繼續有關配置資料 [流的教程](../../dataflow/databases.md)。

### 收集必要的認證

要訪問平台上的Synapse帳戶，必須提供以下值：

| 憑證 | 說明 |
| ---------- | ----------- |
| `connectionString` | 與Synapse驗證關聯的連接字串。 Synapse連接字串模式是 `Server=tcp:{SERVER_NAME}.database.windows.net,1433;Database={DATABASE};User ID={USERNAME}@{SERVER_NAME};Password={PASSWORD};Trusted_Connection=False;Encrypt=True;Connection Timeout=30`。 |

有關此值的詳細資訊，請參 [閱Synapse文檔](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-sql-data-warehouse)。

## 連接Synapse帳戶

收集到所需憑據後，可以按照以下步驟建立新的入站基本連接，以將Synapse帳戶連結到平台。

登入 <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> ，然後從左側導覽列選取 **Sources** ，以存取 ** Sources工作區。 「目 *錄* 」螢幕顯示各種源，您可以為其建立入站基本連接，而每個源顯示與其關聯的現有基本連接數。

在「資 *料庫* 」類別下，選取 **Azure Synapse Analytics** ，以在螢幕右側顯示資訊列。 資訊列提供所選來源的簡短說明，以及與來源連線或檢視其檔案的選項。 要建立新的入站基本連接，請選擇「 **連接源」**。

![](../../../../images/tutorials/create/azure-synapse-analytics/sources-catalog.png)

此時 *會顯示「連線至Azure突觸分析* 」頁面。 在此頁上，您可以使用新認證或現有認證。

### 新帳戶

如果您使用新認證，請選擇「新 **帳戶」**。 在顯示的輸入表單上，提供基本連接的名稱、可選說明和Synapse憑據。 完成後，選擇 **Connect** ，然後為建立新的基本連接留出一些時間。

![](../../../../images/tutorials/create/azure-synapse-analytics/new-credentials.png)

### 現有帳戶

要連接現有帳戶，請選擇要連接的Synapse帳戶，然後選擇「下 **一步** 」繼續。

![](../../../../images/tutorials/create/azure-synapse-analytics/existing-credentials.png)

## 後續步驟

通過本教程，您已建立了與Synapse帳戶的基本連接。 您現在可以繼續下一個教程，並 [配置資料流以將資料導入平台](../../dataflow/databases.md)。