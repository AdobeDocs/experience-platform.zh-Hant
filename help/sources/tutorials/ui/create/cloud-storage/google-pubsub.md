---
keywords: Experience Platform；首頁；熱門主題；GooglePubSub;google pubsub
solution: Experience Platform
title: 在UI中建立GooglePubSub源連接
topic-legacy: overview
type: Tutorial
description: 瞭解如何使用平台用戶介面建立GooglePubSub源連接器。
exl-id: fb8411f2-ccae-4bb5-b1bf-52b1144534ed
source-git-commit: da7b6fe8f9d274b8e5f27138a1baf8caf63a0c01
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 1%

---

# 建立 [!DNL Google PubSub] UI中的源連接

本教程提供建立 [!DNL Google PubSub] (以下簡稱：[!DNL PubSub]&quot;)使用平台用戶介面。

## 快速入門

本教程需要對Adobe Experience Platform的以下部分進行有效的理解：

* [源](../../../../home.md):Experience Platform允許從各種源接收資料，同時讓您能夠使用平台服務構建、標籤和增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供虛擬沙箱，將單個平台實例分區為獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

如果您已經有 [!DNL PubSub] 連接，您可以跳過本文檔的其餘部分並繼續學習有關 [配置資料流](../../dataflow/batch/cloud-storage.md)。

### 收集所需憑據

為了連接 [!DNL PubSub] 要使用平台，必須為以下憑據提供有效值：

| 憑據 | 說明 |
| ---------- | ----------- |
| `projectId` | 驗證所需的項目ID [!DNL PubSub]。 |
| `credentials` | 驗證所需的憑據或私鑰ID [!DNL PubSub]。 |

有關這些值的詳細資訊，請參閱以下 [PubSub身份驗證](https://cloud.google.com/pubsub/docs/authentication) 的子菜單。 如果使用基於服務帳戶的身份驗證，請參閱以下內容 [PubSub指南](https://cloud.google.com/docs/authentication/production#create_service_account) 有關如何生成憑據的步驟。

>[!TIP]
>
>如果您使用基於服務帳戶的身份驗證，請確保在複製和貼上憑據時，已授予用戶對服務帳戶的足夠訪問權限，並且JSON中沒有額外的空白。

收集了所需的憑據後，您可以按照以下步驟連結 [!DNL PubSub] 帳戶到平台。

## 連接 [!DNL PubSub] 帳戶

在 [平台UI](https://platform.adobe.com)選中 **[!UICONTROL 源]** 從左導航欄訪問 [!UICONTROL 源] 工作區。 的 [!UICONTROL 目錄] 螢幕顯示可為其建立帳戶的各種源。

可以從螢幕左側的目錄中選擇相應的類別。 或者，您可以使用搜索欄找到要使用的特定源。

在 [!UICONTROL 雲儲存] 類別，選擇 **[!UICONTROL Google酒吧]**，然後選擇 **[!UICONTROL 添加資料]**。

![目錄](../../../../images/tutorials/create/google-pubsub/catalog.png)

的 **[!UICONTROL 連接到GooglePubSub]** 的子菜單。 在此頁上，您可以使用新憑據或現有憑據。

### 現有帳戶

要使用現有帳戶，請選擇 [!DNL PubSub] 要使用建立新資料流的帳戶，然後選擇 **[!UICONTROL 下一個]** 繼續。

![現有](../../../../images/tutorials/create/google-pubsub/existing.png)

### 新帳戶

如果要建立新帳戶，請選擇 **[!UICONTROL 新帳戶]**，然後提供名稱、可選說明，以及 [!DNL PubSub] 輸入表單上的驗證憑據。 完成後，選擇 **[!UICONTROL 連接到源]** 然後再給新連接建立一段時間。

![新](../../../../images/tutorials/create/google-pubsub/new.png)

## 後續步驟

按照本教程，您將在 [!DNL PubSub] 帳戶和平台。 現在，您可以繼續下一個教程， [配置資料流，將雲儲存中的流資料引入平台](../../dataflow/streaming/cloud-storage-streaming.md)。
