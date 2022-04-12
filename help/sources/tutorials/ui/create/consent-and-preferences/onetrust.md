---
keywords: Experience Platform；首頁；熱門主題；onetrust;OneTrust
solution: Experience Platform
title: (Beta)在UI中建立OneTrust源連接
topic-legacy: overview
type: Tutorial
description: 瞭解如何使用Adobe Experience PlatformUI建立OneTrust源連接。
source-git-commit: adefaeb895c91d45727f791b73b73a17a2b1ccf9
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 1%

---

# (Beta)建立 [!DNL OneTrust Integration] UI中的源連接

>[!NOTE]
>
>的 [!DNL OneTrust Integration] 源為beta。 其功能和文檔可能會更改。 有關使用Beta標籤源的資訊，請參見 [源概述](../../../../home.md#terms-and-conditions)。

本教程提供建立 [[!DNL OneTrust Integration]](https://my.onetrust.com/s/contactsupport?language=en_US) 源連接，使用平台用戶介面將歷史和計畫同意資料同時錄入Adobe Experience Platform。

## 先決條件

>[!IMPORTANT]
>
>的 [!DNL OneTrust Integration] 源連接器和文檔由 [!DNL OneTrust Integration] 團隊。 有關任何查詢或更新請求，請聯繫 [[!DNL OneTrust] 團隊](https://my.onetrust.com/s/contactsupport?language=en_US) 直接輸入。

在連接之前 [!DNL OneTrust Integration] 到平台時，必須先檢索訪問令牌。 有關查找訪問令牌的詳細說明，請參閱 [[!DNL OneTrust Integration] OAuth 2指南](https://developer.onetrust.com/docs/api-docs-v3/b3A6MjI4OTUyOTc-generate-access-token)。

訪問令牌在過期後不會自動刷新，因為系統到系統的刷新令牌不受支援 [!DNL OneTrust]。 因此，必須確保在連接過期之前更新您的訪問令牌。 訪問令牌的最大可配置使用期限為一年。 要瞭解有關更新訪問令牌的詳細資訊，請參閱 [[!DNL OneTrust] 有關管理OAuth 2.0客戶端憑據的文檔](https://developer.onetrust.com/docs/documentation/ZG9jOjIyODk1MTUw-managing-o-auth-2-0-client-credentials)。

### 收集所需憑據

為了連接 [!DNL OneTrust Integration] 在平台中，必須提供以下驗證憑據的值：

| 憑據 | 說明 | 範例 |
| --- | --- | --- |
| Host | 環境 [!DNL OneTrust Integration] 資料需要從中提取。 | `https://uat.onetrust.com/` |
| 授權TestURL | （可選）授權testURL用於在建立基連接時驗證憑據。 如果未提供，則在建立源連接步驟期間會自動檢查憑據。 |  |
| 訪問令牌 | 與您的 [!DNL OneTrust Integration] 帳戶。 | `ZGFkZDMyMjFhMmEyNDQ2ZGFhNTdkZjNkZjFmM2IyOWE6QjlUSERVUTNjOFVsRmpEZTJ6Vk9oRnF3Sk8xNlNtcm4=` |

有關這些憑據的詳細資訊，請參見 [[!DNL OneTrust Integration] 驗證文檔](https://developer.onetrust.com/docs/api-docs-v3/b3A6MjI4OTUyOTc-generate-access-token)。

## 連接 [!DNL OneTrust Integration] 帳戶

>[!NOTE]
>
>的 [!DNL OneTrust Integration] API規範正與Adobe共用，用於資料接收。

在平台UI中，選擇 **[!UICONTROL 源]** 從左側導航 [!UICONTROL 源] 工作區。 的 [!UICONTROL 目錄] 螢幕顯示可建立帳戶的各種源。

可以從螢幕左側的目錄中選擇相應的類別。 或者，您可以使用搜索選項找到要使用的特定源。

在 *[!UICONTROL 同意和首選項]* 類別，選擇 [!DNL OneTrust Integration]，然後選擇 **[!UICONTROL 添加資料]**。

![目錄](../../../../images/tutorials/create/onetrust/catalog.png)

的 **[!UICONTROL 連接OneTrust整合帳戶]** 的子菜單。 在此頁上，您可以使用新憑據或現有憑據。

### 現有帳戶

要使用現有帳戶，請選擇 [!DNL OneTrust Integration] 要使用建立新資料流的帳戶，然後選擇 **[!UICONTROL 下一個]** 繼續。

![現有](../../../../images/tutorials/create/onetrust/existing.png)

### 新帳戶

如果要建立新帳戶，請選擇 **[!UICONTROL 新帳戶]**，然後提供名稱、可選說明和您的憑據。 完成後，選擇 **[!UICONTROL 連接到源]** 然後再給新連接建立一段時間。

![新](../../../../images/tutorials/create/onetrust/new.png)

## 後續步驟

按照本教程，您已建立到 [!DNL OneTrust Integration] 帳戶。 現在，您可以繼續下一個教程， [配置資料流以將同意資料引入平台](../../dataflow/consent-and-preferences.md)。