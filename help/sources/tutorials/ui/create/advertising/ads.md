---
title: 在UI中建立Google廣告源連接
description: 瞭解如何使用GoogleUI建立Adobe Experience Platform廣告源連接。
exl-id: 33dd2857-aed3-4e35-bc48-1c756a8b3638
source-git-commit: ac87434c857a39f4be3714cba57519cbb4fa54a6
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 0%

---

# 在UI中建立Google廣告源連接

>[!NOTE]
>
>Google廣告的來源是β 查看 [源概述](../../../../home.md#terms-and-conditions) 的子菜單。

本教程提供了使用Google用戶介面建立Adobe Experience Platform廣告源連接的步驟。

## 快速入門

本教程需要對以下Experience Platform組成部分進行有效理解：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化框架。
   * [架構組合的基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本構建基塊，包括架構組成中的關鍵原則和最佳做法。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自定義架構。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):基於來自多個源的聚合資料提供統一、即時的用戶配置檔案。

如果您已經具有有效的Google廣告連接，則可以跳過本文檔的其餘部分，繼續學習有關 [配置資料流](../../dataflow/advertising.md)

### 收集所需憑據

要訪問您的Google廣告帳戶平台，必須提供以下值：

| 憑據 | 說明 |
| ---------- | ----------- |
| 客戶端客戶ID | 客戶端客戶ID是與您要使用Google廣告API管理的Google廣告客戶端帳戶對應的帳號。 此ID位於的模板後 `123-456-7890`。 |
| 登錄客戶ID | 登錄客戶ID是與您的Google廣告經理帳戶相對應的帳號，用於從特定操作客戶獲取報告資料。 有關登錄客戶ID的詳細資訊，請閱讀 [Google廣告API文檔](https://developers.google.com/google-ads/api/docs/migration/login-customer-id)。 |
| 開發人員令牌 | 開發人員令牌允許您訪問Google廣告API。 您可以使用同一開發人員令牌對所有Google廣告帳戶發出請求。 檢索開發人員令牌的方式 [登錄到您的Manager帳戶](https://ads.google.com/home/tools/manager-accounts/) 然後導航到「API中心」頁。 |
| 刷新標籤 | 刷新令牌是 [!DNL OAuth2] 驗證。 此令牌允許您在訪問令牌過期後重新生成它們。 |
| 客戶端ID | 客戶機ID與客戶機密碼一起使用，作為 [!DNL OAuth2] 驗證。 客戶端ID和客戶端密碼共同使您的應用程式能夠代表您的帳戶運行，方法是將您的應用程式標識到Google。 |
| 客戶端密碼 | 客戶機密碼與客戶機ID一起用作 [!DNL OAuth2] 驗證。 客戶端ID和客戶端密碼共同使您的應用程式能夠代表您的帳戶運行，方法是將您的應用程式標識到Google。 |

閱讀API概述文檔 [有關開始使用Google廣告的詳細資訊](https://developers.google.com/google-ads/api/docs/first-call/overview)。

## 連接您的Google廣告帳戶

在平台UI中，選擇 **[!UICONTROL 源]** 從左導航欄訪問 [!UICONTROL 源] 工作區。 的 [!UICONTROL 目錄] 螢幕顯示可建立帳戶的各種源。

可以從螢幕左側的目錄中選擇相應的類別。 或者，您可以使用搜索選項找到要使用的特定源。

在 **[!UICONTROL 廣告]** 類別，選擇 **[!UICONTROL Google廣告]**，然後選擇 **[!UICONTROL 添加資料]**。

![Experience PlatformUI中的源目錄。](../../../../images/tutorials/create/ads/catalog.png)。

的 **[!UICONTROL 連接到Google廣告]** 的子菜單。 在此頁上，您可以使用新憑據或現有憑據。

### 現有帳戶

要連接現有帳戶，請選擇要連接的Google廣告帳戶，然後選擇 **[!UICONTROL 下一個]** 繼續。

![源工作流中現有帳戶的選擇頁。](../../../../images/tutorials/create/ads/existing.png)。

### 新帳戶

如果使用新憑據，請選擇 **[!UICONTROL 新帳戶]**。 在顯示的輸入表單上，提供名稱、可選說明和您的Google廣告憑據。 完成後，選擇 **[!UICONTROL 連接到源]** 然後再給新連接建立一段時間。

![源工作流中的新帳戶介面。](../../../../images/tutorials/create/ads/new.png)。

## 後續步驟

通過學完本教程，您已建立了與Google廣告帳戶的連接。 現在，您可以繼續下一個教程， [配置資料流，將廣告資料引入平台](../../dataflow/advertising.md)。
