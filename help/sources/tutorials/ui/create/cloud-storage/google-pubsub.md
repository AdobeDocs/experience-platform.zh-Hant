---
title: 在UI中建立GooglePubSub源連接
description: 瞭解如何使用平台用戶介面建立GooglePubSub源連接器。
exl-id: fb8411f2-ccae-4bb5-b1bf-52b1144534ed
source-git-commit: 79149274c28507041ad89be9d7afdefaedb6aaa0
workflow-type: tm+mt
source-wordcount: '1010'
ht-degree: 0%

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
| 專案 ID | 驗證所需的項目ID [!DNL PubSub]。 |
| 憑據 | 驗證所需的憑據或私鑰ID [!DNL PubSub]。 |
| 主題名稱 | 您的名稱 [!DNL PubSub] 訂閱。 在 [!DNL PubSub]，訂閱允許您通過訂閱已發佈消息的主題來接收消息。 **注釋**:單 [!DNL PubSub] 訂閱只能用於一個資料流。 要建立多個資料流，必須有多個預訂。 |
| 訂閱名稱 | 您的名稱 [!DNL PubSub] 訂閱。 在 [!DNL PubSub]，訂閱允許您通過訂閱已發佈消息的主題來接收消息。 |

有關這些值的詳細資訊，請參閱以下 [PubSub身份驗證](https://cloud.google.com/pubsub/docs/authentication) 的子菜單。 如果使用基於服務帳戶的身份驗證，請參閱以下內容 [PubSub指南](https://cloud.google.com/docs/authentication/production#create_service_account) 有關如何生成憑據的步驟。

>[!TIP]
>
>如果您使用基於服務帳戶的身份驗證，請確保在複製和貼上憑據時，已授予用戶對服務帳戶的足夠訪問權限，並且JSON中沒有額外的空白。

收集了所需的憑據後，您可以按照以下步驟連結 [!DNL PubSub] 帳戶到平台。

## 連接 [!DNL PubSub] 帳戶

在平台UI中，選擇 **[!UICONTROL 源]** 從左側導航 [!UICONTROL 源] 工作區。 的 [!UICONTROL 目錄] 螢幕顯示可以建立帳戶的各種源。

可以從螢幕左側的目錄中選擇相應的類別。 或者，您可以使用搜索選項找到要使用的特定源。

在 [!UICONTROL 雲儲存] 類別，選擇 **[!UICONTROL Google酒吧]**，然後選擇 **[!UICONTROL 添加資料]**。

![Experience PlatformUI上的源目錄。](../../../../images/tutorials/create/google-pubsub/catalog.png)

的 **[!UICONTROL 連接到GooglePubSub]** 的子菜單。 在此頁上，您可以使用新憑據或現有憑據。

### 現有帳戶

要使用現有帳戶，請選擇 [!DNL PubSub] 要使用建立新資料流的帳戶，然後選擇 **[!UICONTROL 下一個]** 繼續。

![源工作流中的現有帳戶選擇。](../../../../images/tutorials/create/google-pubsub/existing.png)

### 新帳戶

>[!TIP]
>
>建立具有受限訪問權限的帳戶時，必須至少提供一個主題名稱或訂閱名稱。 如果兩個值都缺失，驗證將失敗。

如果要建立新帳戶，請選擇 **[!UICONTROL 新帳戶]**，然後提供新名稱和可選說明 [!DNL PubSub] 帳戶。

![源工作流中GooglePubSub源的新帳戶介面](../../../../images/tutorials/create/google-pubsub/new.png)

的 [!DNL PubSub] 源允許您指定在驗證期間允許的訪問類型。 您可以設定帳戶，使其具有基於項目的身份驗證或基於主題和訂閱的身份驗證。 基於項目的身份驗證允許您授予對帳戶中根級別項目的訪問權限，而基於主題和基於訂閱的身份驗證允許您限制對特定項目的訪問權限 [!DNL PubSub] 主題和訂閱。

>[!BEGINTABS]

>[!TAB 基於項目的身份驗證]

建立具有訪問根帳戶權限的帳戶 [!DNL PubSub] 項目資料夾。 選擇 **[!UICONTROL GooglePubSub身份驗證憑據]** 作為驗證類型，並提供項目ID和憑據。 完成後，選擇 **[!UICONTROL 連接到源]** 然後再給新連接建立一段時間。

![已選擇根訪問的GooglePubSub源的新帳戶介面。](../../../../images/tutorials/create/google-pubsub/root.png)

>[!TAB 基於主題和訂閱的身份驗證]

建立僅限特定帳戶的受限訪問權限的帳戶 [!DNL PubSub] 主題和訂閱，選擇 **[!UICONTROL GooglePubSub作用域身份驗證憑據]** 然後提供您的憑據、主題名和/或訂閱名。 完成後，選擇 **[!UICONTROL 連接到源]** 然後再給新連接建立一段時間。

![已選擇範圍訪問的GooglePubSub源的新帳戶介面。](../../../../images/tutorials/create/google-pubsub/scoped.png)

>[!ENDTABS]

>[!NOTE]
>
>分配給的承擔者（角色） [!DNL PubSub] 項目在建立於 [!DNL PubSub] 項目。 如果希望承擔者（角色）有權訪問特定主題，則還必須將該承擔者（角色）添加到主題的相應訂閱中。 有關詳細資訊，請閱讀 [[!DNL PubSub] 訪問控制文檔](<https://cloud.google.com/pubsub/docs/access-control>)。

## 選擇資料

成功的身份驗證將帶您 [!UICONTROL 選擇資料] 步驟，您可以在 [!DNL PubSub] 資料層次，並選擇要將其帶到Experience Platform的資料。

>[!BEGINTABS]

>[!TAB 基於項目的身份驗證]

如果您已通過基於項目的訪問驗證， [!UICONTROL 選擇資料] interface將顯示項目中附加了主題的所有訂閱。

![使用基於項目的身份驗證的源工作流的選擇資料步驟。](../../../../images/tutorials/create/google-pubsub/root-folders.png)

>[!TAB 基於主題和訂閱的身份驗證]

如果您已通過主題和基於訂閱的訪問驗證， [!UICONTROL 選擇資料] 介面顯示可能因您提供的資訊而異。

* 如果僅提供主題名稱，則介面將顯示與提供的主題對應的所有主題預訂對。
* 如果僅提供訂閱名稱，則介面將顯示與提供的訂閱名稱對應的所有主題訂閱對。
* 如果同時提供了主題名和訂閱名，則介面將顯示與兩個提供的值對應的主題訂閱對。

![具有主題和基於訂閱的身份驗證的源工作流的選擇資料步驟。](../../../../images/tutorials/create/google-pubsub/scoped-folders.png)

>[!ENDTABS]

## 後續步驟

按照本教程，您已在 [!DNL PubSub] 帳戶和平台。 現在，您可以繼續下一個教程， [配置資料流，將雲儲存中的流資料引入平台](../../dataflow/streaming/cloud-storage-streaming.md)。
