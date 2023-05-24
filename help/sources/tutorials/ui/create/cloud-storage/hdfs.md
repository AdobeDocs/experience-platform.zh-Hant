---
keywords: Experience Platform；主題；熱門主題；Apache HDFS;HDFS;hdfs
solution: Experience Platform
title: 在UI中建立Apache HDFS源連接
type: Tutorial
description: 瞭解如何使用Adobe Experience PlatformUI建立ApacheHadoop分佈式檔案系統源連接。
exl-id: 3b8bf210-13b6-44e6-9090-152998f67452
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 1%

---

# 建立 [!DNL Apache] UI中的HDFS源連接

>[!NOTE]
>
>的 [!DNL Apache] HDFS接頭為beta。 查看 [源概述](../../../../home.md#terms-and-conditions) 的子菜單。

源連接器 [!DNL Adobe Experience Platform] 提供按計畫接收外部來源資料的能力。 本教程提供了驗證 [!DNL Apache Hadoop Distributed File System] （下稱「HDFS」）源介面 [!DNL Platform] 用戶介面。

## 快速入門

本教程需要對以下元件進行有效的瞭解 [!DNL Platform]:

- [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。
   - [架構組合的基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本構建基塊，包括架構組成中的關鍵原則和最佳做法。
   - [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自定義架構。
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):基於來自多個源的聚合資料提供統一、即時的用戶配置檔案。

如果您已經有有效的HDFS連接，則可以跳過本文檔的其餘部分並繼續上的教程 [配置資料流](../../dataflow/batch/cloud-storage.md)。

### 收集所需憑據

為了驗證HDFS源連接器，必須為以下連接屬性提供值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `url` | URL定義匿名連接到HDFS所需的身份驗證參數。 有關如何獲取此值的詳細資訊，請參閱以下文檔， [HDFS的HTTPS身份驗證](https://hadoop.apache.org/docs/r1.2.1/HttpAuthentication.html)。 |

## 連接HDFS帳戶

收集所需憑據後，您可以按照以下步驟將您的HDFS帳戶連結至 [!DNL Platform]。

登錄到 [Adobe Experience Platform](https://platform.adobe.com) ，然後選擇 **[!UICONTROL 源]** 從左導航欄訪問 **[!UICONTROL 源]** 工作區。 的 **[!UICONTROL 目錄]** 螢幕顯示可為其建立帳戶的各種源。

可以從螢幕左側的目錄中選擇相應的類別。 或者，您可以使用搜索選項找到要使用的特定源。

在 **[!UICONTROL 雲儲存]** 類別，選擇 **[!UICONTROL Apache HDFS]**。 如果這是您第一次使用此連接器，請選擇 **[!UICONTROL 配置]**。 否則，選擇 **[!UICONTROL 添加資料]** 建立新的HDFS連接器。

![目錄](../../../../images/tutorials/create/hdfs/catalog.png)

的 **[!UICONTROL 連接到HDFS]** 的子菜單。 在此頁上，您可以使用新憑據或現有憑據。

### 新帳戶

如果使用新憑據，請選擇 **[!UICONTROL 新帳戶]**。 在顯示的輸入表單上，提供名稱、可選說明和HDFS憑據。 完成後，選擇 **[!UICONTROL 連接到源]** 然後再給新連接建立一段時間。

![連接](../../../../images/tutorials/create/hdfs/new.png)

### 現有帳戶

要連接現有帳戶，請選擇要連接的HDFS帳戶，然後選擇 **[!UICONTROL 下一個]** 繼續。

![現有](../../../../images/tutorials/create/hdfs/existing.png)

## 後續步驟

按照本教程，您已建立到HDFS帳戶的連接。 現在，您可以繼續下一個教程， [配置資料流，將雲儲存中的資料 [!DNL Platform]](../../dataflow/batch/cloud-storage.md)。
