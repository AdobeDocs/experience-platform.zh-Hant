---
keywords: Experience Platform；首頁；熱門主題；Azure Data Lake Storage Gen2;ADLS Gen2;adls gen2;adls連接器
solution: Experience Platform
title: 在UI中建立Azure Data Lake Storage Gen2源連接
type: Tutorial
description: 瞭解如何使用Adobe Experience PlatformUI建立Azure Data Lake Storage Gen2源連接。
exl-id: d81b7593-08a3-43f8-a8bc-f5547a6cd55a
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 1%

---

# 建立 [!DNL Azure Data Lake Storage Gen2] UI中的源連接

Adobe Experience Platform的源連接器提供了定期接收外部源資料的能力。 本教程提供了驗證 [!DNL Azure Data Lake Storage Gen2] (以下簡稱：[!DNL ADLS Gen2]&quot;)使用 [!DNL Platform] 用戶介面。

## 快速入門

本教程需要對Adobe Experience Platform的以下部分進行有效的理解：

- [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。
   - [架構組合的基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本構建基塊，包括架構組成中的關鍵原則和最佳做法。
   - [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自定義架構。
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):基於來自多個源的聚合資料提供統一、即時的用戶配置檔案。

如果您已經有有效的ADLS Gen2連接，則可以跳過本文檔的其餘部分，繼續學習有關 [配置資料流](../../dataflow/batch/cloud-storage.md)。

### 收集所需憑據

為了驗證 [!DNL ADLS Gen2] 源連接器，必須為以下連接屬性提供值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `url` | 的終結點 [!DNL ADLS Gen2]。 |
| `servicePrincipalId` | 應用程式的客戶端ID。 |
| `servicePrincipalKey` | 應用程式的密鑰。 |
| `tenant` | 包含應用程式的租戶資訊。 |

有關這些值的詳細資訊，請參閱 [這個 [!DNL ADLS Gen2] 文檔](https://docs.microsoft.com/en-us/azure/data-factory/connector-azure-data-lake-storage)。

## 連接 [!DNL ADLS Gen2] 帳戶

收集了所需的憑據後，您可以按照以下步驟連結 [!DNL ADLS Gen2] 連接帳戶 [!DNL Platform]。

登錄到 [Adobe Experience Platform](https://platform.adobe.com) ，然後選擇 **[!UICONTROL 源]** 從左導航欄訪問 **[!UICONTROL 源]** 工作區。 的 **[!UICONTROL 目錄]** 螢幕顯示可為其建立帳戶的各種源。

可以從螢幕左側的目錄中選擇相應的類別。 或者，您可以使用搜索選項找到要使用的特定源。

在 **[!UICONTROL 資料庫]** 類別，選擇 **[!UICONTROL Azure資料湖第2代]**。 如果這是您第一次使用此連接器，請選擇 **[!UICONTROL 配置]**。 否則，選擇 **[!UICONTROL 添加資料]** 建立新的ADLS Gen2連接器。

![](../../../../images/tutorials/create/adls-gen2/catalog.png)

的 **[!UICONTROL 連接到Azure Data Lake Gen2]** 對話框。 在此頁上，您可以使用新憑據或現有憑據。

### 新帳戶

如果使用新憑據，請選擇 **[!UICONTROL 新帳戶]**。 在顯示的輸入表單上，提供名稱、可選說明和 [!DNL ADLS Gen2] 憑據。 完成後，選擇 **[!UICONTROL 連接]** 然後再給新連接建立一段時間。

![](../../../../images/tutorials/create/adls-gen2/connect.png)

### 現有帳戶

要連接現有帳戶，請選擇 [!DNL ADLS Gen2] 要連接的帳戶，然後選擇 **[!UICONTROL 下一個]** 繼續。

![](../../../../images/tutorials/create/adls-gen2/existing.png)

## 後續步驟

按照本教程，您已建立到 [!DNL ADLS Gen2] 帳戶。 現在，您可以繼續下一個教程， [配置資料流，將雲儲存中的資料 [!DNL Platform]](../../dataflow/batch/cloud-storage.md)。
