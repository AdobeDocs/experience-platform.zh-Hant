---
keywords: Experience Platform；首頁；熱門主題；Azure事件中心；事件中心；azure事件中心
solution: Experience Platform
title: 在UI中建立Azure事件中心源連接
type: Tutorial
description: 瞭解如何使用Adobe Experience PlatformUI建立Azure事件集線器源連接。
exl-id: 7e67e213-8ccb-4fa5-b09f-ae77aba8614c
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 1%

---


# 建立 [!DNL Azure Event Hubs] UI中的源連接

Adobe Experience Platform的源連接器提供了定期接收外部源資料的能力。 本教程提供了驗證 [!DNL Azure Event Hubs] (以下簡稱：[!DNL Event Hubs]&quot;)使用 [!DNL Platform] 用戶介面。

## 快速入門

本教程需要對Adobe Experience Platform的以下部分進行有效的理解：

- [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。
   - [架構組合的基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本構建基塊，包括架構組成中的關鍵原則和最佳做法。
   - [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自定義架構。
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):基於來自多個源的聚合資料提供統一、即時的用戶配置檔案。

如果您已經有 [!DNL Event Hubs] 連接，您可以跳過本文檔的其餘部分並繼續學習有關 [配置資料流](../../dataflow/streaming/cloud-storage-streaming.md)。

### 收集所需憑據

為了驗證 [!DNL Event Hubs] 源連接器，必須為以下連接屬性提供值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `sasKeyName` | 授權規則的名稱，也稱為SAS密鑰名稱。 |
| `sasKey` | 主鍵 [!DNL Event Hubs] 命名空間。 的 `sasPolicy` 那個 `sasKey` 必須對應 `manage` 為 [!DNL Event Hubs] 清單。 |
| `namespace` | 命名空間 [!DNL Event Hubs] 您正在訪問。 |

有關這些值的詳細資訊，請參閱 [這個 [!DNL Event Hubs] 文檔](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)。

## 連接 [!DNL Event Hubs] 帳戶

收集了所需的憑據後，您可以按照以下步驟連結 [!DNL Event Hubs] 帳戶 [!DNL Platform]。

登錄到 [Adobe Experience Platform](https://platform.adobe.com) ，然後選擇 **[!UICONTROL 源]** 從左導航欄訪問 **[!UICONTROL 源]** 工作區。 的 **[!UICONTROL 目錄]** 頁籤顯示可為其建立帳戶的各種源。

可以從螢幕左側的目錄中選擇相應的類別。 或者，您可以使用搜索選項找到要使用的特定源。

在 **[!UICONTROL 雲儲存]** 類別，選擇 **[!UICONTROL Azure事件中心]**。 如果這是您第一次使用此連接器，請選擇 **[!UICONTROL 配置]**。 否則，選擇 **[!UICONTROL 添加資料]** 新建事件集線器連接器。

![](../../../../images/tutorials/create/eventhub/catalog.png)

的 **[!UICONTROL 連接到Azure事件中心]** 對話框。 在此頁上，您可以使用新憑據或現有憑據。

### 新帳戶

如果使用新憑據，請選擇 **[!UICONTROL 新帳戶]**。 在顯示的輸入表單上，提供名稱、可選說明和 [!DNL Event Hubs] 憑據。 完成後，選擇 **[!UICONTROL 連接]** 然後再給新連接建立一段時間。

![](../../../../images/tutorials/create/eventhub/new.png)

### 現有帳戶

要連接現有帳戶，請選擇 [!DNL Event Hubs] 要連接的帳戶，然後選擇 **[!UICONTROL 下一個]** 繼續。

![](../../../../images/tutorials/create/eventhub/existing.png)

## 後續步驟

按照本教程，您已將 [!DNL Event Hubs] 帳戶 [!DNL Platform]。 現在，您可以繼續下一個教程， [配置資料流，將雲儲存中的資料 [!DNL Platform]](../../dataflow/streaming/cloud-storage-streaming.md)。
