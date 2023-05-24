---
keywords: Experience Platform；首頁；熱門主題；mysql;MySQL
solution: Experience Platform
title: 在UI中建立MySQL源連接
type: Tutorial
description: 瞭解如何使用Adobe Experience PlatformUI建立MySQL源連接。
exl-id: 75e74bde-6199-4970-93d2-f95ec3a59aa5
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 1%

---

# 建立 [!DNL MySQL] UI中的源連接

Adobe Experience Platform的源連接器提供了定期接收外部源資料的能力。 本教程提供建立 [!DNL MySQL] 源連接使用Adobe Experience PlatformUI。

## 快速入門

本教程需要對Adobe Experience Platform的以下部分進行有效的理解：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化框架。
   * [架構組合的基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本構建基塊，包括架構組成中的關鍵原則和最佳做法。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自定義架構。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):基於來自多個源的聚合資料提供統一、即時的用戶配置檔案。

如果你已經 [!DNL MySQL] 連接，您可以跳過本文檔的其餘部分並繼續學習有關 [配置資料流](../../dataflow/databases.md)。

### 收集所需憑據

為了訪問 [!DNL MySQL] 帳戶 [!DNL Platform]，必須提供以下值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `connectionString` | 的 [!DNL MySQL] 與你的帳戶關聯的連接字串。 的 [!DNL MySQL] 連接字串模式為： `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`。 您可以通過閱讀 [[!DNL MySQL] 文檔](https://dev.mysql.com/doc/connector-net/en/connector-net-connections-string.html)。 |

## 連接 [!DNL MySQL] 帳戶

收集了所需的憑據後，您可以按照以下步驟連結 [!DNL MySQL] 帳戶 [!DNL Platform]。

登錄到 [Adobe Experience Platform](https://platform.adobe.com) ，然後選擇 **[!UICONTROL 源]** 從左導航欄訪問 **[!UICONTROL 源]** 工作區。 的 **[!UICONTROL 目錄]** 螢幕顯示可為其建立帳戶的各種源。

在 **[!UICONTROL 資料庫]** 類別，選擇 **[!UICONTROL MySQL]**。 如果這是您第一次使用此連接器，請選擇 **[!UICONTROL 配置]**。 否則，選擇 **[!UICONTROL 添加資料]** 新建 [!DNL MySQL] 連接器。

![](../../../../images/tutorials/create/my-sql/catalog.png)

的 **[!UICONTROL 連接到MySQL]** 的子菜單。 在此頁上，您可以使用新憑據或現有憑據。

### 新帳戶

如果使用新憑據，請選擇 **[!UICONTROL 新帳戶]**。 在顯示的輸入表單上，提供名稱、可選說明和 [!DNL MySQL] 憑據。 完成後，選擇 **[!UICONTROL 連接]** 然後再給新連接建立一段時間。

![](../../../../images/tutorials/create/my-sql/new.png)

### 現有帳戶

要連接現有帳戶，請選擇 [!DNL MySQL] 要連接的帳戶，然後選擇 **[!UICONTROL 下一個]** 繼續。

![](../../../../images/tutorials/create/my-sql/existing.png)

## 後續步驟

按照本教程，您已建立到MySQL帳戶的連接。 現在，您可以繼續下一個教程， [配置資料流以將資料 [!DNL Platform]](../../dataflow/databases.md)。
