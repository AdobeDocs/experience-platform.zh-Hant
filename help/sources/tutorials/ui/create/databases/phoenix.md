---
keywords: Experience Platform；主題；熱門主題；鳳凰；phoenix
solution: Experience Platform
title: 在UI中建立Phoenix源連接
type: Tutorial
description: 瞭解如何使用Adobe Experience PlatformUI建立Phoenix源連接。
exl-id: 2ed469bc-1c72-4f04-a5f0-6a0bb519a6c2
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 0%

---

# 建立 [!DNL Phoenix] UI中的源連接

>[!NOTE]
>
> 的 [!DNL Phoenix] 連接器位於beta中。 查看 [源概述](../../../../home.md#terms-and-conditions) 的子菜單。

Adobe Experience Platform的源連接器提供了定期接收外部源資料的能力。 本教程提供建立 [!DNL Phoenix] 源連接器使用 [!DNL Platform] 用戶介面。

## 快速入門

本教程需要對Adobe Experience Platform的以下部分進行有效的理解：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。
   * [架構組合的基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本構建基塊，包括架構組成中的關鍵原則和最佳做法。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自定義架構。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):基於來自多個源的聚合資料提供統一、即時的用戶配置檔案。

如果您已經有 [!DNL Phoenix] 連接，您可以跳過本文檔的其餘部分並繼續學習有關 [配置資料流](../../dataflow/databases.md)

### 收集所需憑據

為了訪問 [!DNL Phoenix] 帳戶 [!DNL Platform]，必須提供以下值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `host` | 的IP地址或主機名 [!DNL Phoenix] 伺服器。 |
| `port` | TCP埠 [!DNL Phoenix] 伺服器用於偵聽客戶端連接。 如果連接到 [!DNL Azure HDInsights]，將埠指定為443。 |
| `httpPath` | 與 [!DNL Phoenix] 伺服器。 如果使用 [!DNL Azure HDInsights] 群集。 |
| `username` | 用於訪問 [!DNL Phoenix] 伺服器。 |
| `password` | 與用戶對應的密碼。 |
| `enableSsl` | 一個切換，指定是否使用SSL加密與伺服器的連接。 |

有關入門的詳細資訊，請參閱 [這個 [!DNL Phoenix] 文檔](https://python-phoenixdb.readthedocs.io/en/latest/api.html)。

## 連接 [!DNL Phoenix] 帳戶

收集了所需的憑據後，您可以按照以下步驟連結 [!DNL Phoenix] 連接帳戶 [!DNL Platform]。

登錄到 [Adobe Experience Platform](https://platform.adobe.com) ，然後選擇 **[!UICONTROL 源]** 從左導航欄訪問 **[!UICONTROL 源]** 工作區。 的 **[!UICONTROL 目錄]** 螢幕顯示可為其建立帳戶的各種源。

可以從螢幕左側的目錄中選擇相應的類別。 或者，您可以使用搜索選項找到要使用的特定源。

在 **[!UICONTROL 資料庫]** 類別，選擇 **[!UICONTROL 鳳凰]**。 如果這是您第一次使用此連接器，請選擇 **[!UICONTROL 配置]**。 否則，選擇 **[!UICONTROL 添加資料]** 新建 [!DNL Phoenix] 帳戶。

![目錄](../../../../images/tutorials/create/phoenix/catalog.png)

的 **[!UICONTROL 連接到鳳凰城]** 的子菜單。 在此頁上，您可以使用新憑據或現有憑據。

### 新帳戶

如果使用新憑據，請選擇 **[!UICONTROL 新帳戶]**。 在顯示的輸入表單上，提供名稱、可選說明和 [!DNL Phoenix] 憑據。 完成後，選擇 **[!UICONTROL 連接]** 然後再給新連接建立一段時間。

![連接](../../../../images/tutorials/create/phoenix/new.png)

### 現有帳戶

要連接現有帳戶，請選擇 [!DNL Phoenix] 要連接的帳戶，然後選擇 **[!UICONTROL 下一個]** 繼續。

![現有](../../../../images/tutorials/create/phoenix/existing.png)

## 後續步驟

按照本教程，您已建立到 [!DNL Phoenix] 帳戶。 現在，您可以繼續下一個教程， [配置資料流以將資料 [!DNL Platform]](../../dataflow/databases.md)。
