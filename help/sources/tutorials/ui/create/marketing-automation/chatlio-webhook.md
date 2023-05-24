---
title: 在UI中建立查看源連接
description: 瞭解如何使用Adobe Experience PlatformUI建立查特利奧源連接。
badge: β
exl-id: 55c10bcb-0332-45ff-970b-272d375b591d
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '1168'
ht-degree: 1%

---

# 建立 [!DNL Chatlio] UI中的源連接

>[!NOTE]
>
>的 [!DNL Chatlio] 源為beta。 請閱讀 [源概述](../../../../home.md#terms-and-conditions) 的子菜單。

本教程提供建立 [!DNL Chatlio] 源連接，使用Adobe Experience Platform用戶介面。

## 快速入門 {#getting-started}

本教程需要對以下Experience Platform組成部分進行有效理解：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。
   * [架構組合的基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本構建基塊，包括架構組成中的關鍵原則和最佳做法。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自定義架構。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):基於來自多個源的聚合資料提供統一、即時的用戶配置檔案。

## 先決條件 {#prerequisites}

以下部分提供了有關在建立 [!DNL Chatlio] 源連接。

### 定義源架構的示例JSON [!DNL Chatlio] {#prerequisites-json-schema}

在建立 [!DNL Chatlio] 源連接，需要提供源架構。 可以使用下面的JSON。

```
{
  "visitor": {
    "email": "test@example.com",
    "UUID": "2d3f4260-2235-903b-0a82-a23d326cc257"
  },
   "message": "Hi",
  "channelId": "C04J7M7LCMQ",
  "slackChannelName": "aep",
  "slackChannelId": "C04JVR71WKS"
}
```

### 建立平台架構 [!DNL Chatlio] {#create-platform-schema}

還必須確保建立用於源的平台架構。 閱讀上的教程 [建立平台架構](../../../../../xdm/schema/composition.md) 有關如何建立架構的全面步驟。

![顯示Chatlio示例架構的平台UI](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/schema.png)

## 連接 [!DNL Chatlio] 帳戶 {#connect-account}

在平台UI中，選擇 **[!UICONTROL 源]** 從左側導航 [!UICONTROL 源] 工作區，並查看Experience Platform中可用的源目錄。

使用 *[!UICONTROL 類別]* 按類別篩選源。 或者，在搜索欄中輸入源名稱以從目錄中查找特定源。

轉到 [!UICONTROL 營銷自動化] 類別以查看 [!DNL Chatlio] 源卡。 要開始，請選擇 **[!UICONTROL 添加資料]**。

![Chatlio卡平台UI目錄](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/catalog.png)

## 選擇資料 {#select-data}

的 **[!UICONTROL 選擇資料]** 步驟，為您提供一個介面，以選擇要帶到平台的資料。

* 介面的左側部分是一個瀏覽器，允許您查看帳戶中的可用資料流；
* 該介面的右部分允許您從JSON檔案預覽多達100行的資料。

選擇 **[!UICONTROL 上載檔案]** 從本地系統上載JSON檔案。 或者，可以將要上載的JSON檔案拖放到 [!UICONTROL 拖放檔案] 的子菜單。

![源工作流的添加資料步驟。](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/add-data.png)

上載檔案後，預覽介面將更新以顯示上載的架構的預覽。 預覽介面允許您檢查檔案的內容和結構。 您還可以使用 [!UICONTROL 搜索欄位] 用於從架構中訪問特定項的實用程式。

完成後，選擇 **[!UICONTROL 下一個]**。

![源工作流的預覽步驟。](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/preview.png)

## 資料流詳細資訊 {#dataflow-detail}

的 **資料流詳細資訊** 步驟，為您提供了使用現有資料集或為資料流建立新資料集的選項，以及為資料流提供名稱和說明的機會。 在此步驟中，您還可以配置配置檔案接收、錯誤診斷、部分接收和警報的設定。

完成後，選擇 **[!UICONTROL 下一個]**。

![源工作流的資料流詳細資訊步驟。](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/dataflow-detail.png)

## 映射 {#mapping}

的 [!UICONTROL 映射] 步驟，提供一個介面，用於將源欄位從源架構映射到目標架構中相應的目標XDM欄位。

平台根據您選擇的目標架構或資料集為自動映射欄位提供智慧建議。 您可以手動調整映射規則以適合您的使用情形。 根據您的需要，您可以選擇直接映射欄位，或使用資料準備函式轉換源資料以導出計算值或計算值。 有關使用映射器介面和計算欄位的全面步驟，請參見 [資料準備UI指南](../../../../../data-prep/ui/mapping.md)。

下面列出的映射是必需的，應先進行設定，然後再繼續到 [!UICONTROL 審閱] 。

| 目標欄位 | 說明 |
| --- | --- |
| `UUID` | 的 [!DNL Chatlio] 事件的標識符。 |

成功映射源資料後，選擇 **[!UICONTROL 下一個]**。

![源工作流的映射步驟。](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/mapping.png)

## 請檢閱 {#review}

的 **[!UICONTROL 審閱]** 步驟，允許您在建立新資料流之前查看它。 詳細資訊按以下類別分組：

* **[!UICONTROL 連接]**:顯示源類型、所選源檔案的相關路徑以及該源檔案中的列數。
* **[!UICONTROL 分配資料集和映射欄位]**:顯示源資料正被攝取到的資料集，包括該資料集所遵循的架構。

查看資料流後，選擇 **[!UICONTROL 完成]** 並為建立資料流留出一些時間。

![源工作流的審閱步驟。](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/review.png)

## 獲取流終結點URL {#get-streaming-endpoint-url}

建立流資料流後，現在可以檢索流終結點URL。 此終結點將用於訂閱Webhook，允許流源與Experience Platform通信。

為了構造用於在上配置Webhook的URL [!DNL Chatlio] 必須檢索以下內容：

* **[!UICONTROL 資料流ID]**
* **[!UICONTROL 流式處理終結點]**

要檢索 **[!UICONTROL 資料流ID]** 和 **[!UICONTROL 流式處理終結點]**，轉到 [!UICONTROL 資料流活動] 您剛建立的資料流的頁，並從 [!UICONTROL 屬性] 的子菜單。

![資料流活動中的流終結點。](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/endpoint-test.png)

檢索到流終結點和資料流ID後，基於以下模式生成URL: ```{STREAMING_ENDPOINT}?x-adobe-flow-id={DATAFLOW_ID}```。 例如，構造的Webhook URL可能如下所示： ``https://dcs.adobedc.net/collection/d56b47ee3985104beaf724efcd78a3e1a863d720471a482bebac0acc1ab95983``

## 在中設定網鈎 [!DNL Chatlio] {#set-up-webhook}

建立Webhook URL後，您現在可以使用 [!DNL Chatlio] 用戶介面。

登錄到 [[!DNL Chatlio]](https://chatlio.com/) 帳戶和跟蹤 [安裝和安裝指南](https://chatlio.com/docs/setup/) 建立小部件。

建立小部件後，導航到該小部件的設定頁面，以將網頁掛接URL添加到該小部件。

![Chatlio上的Webhook設定頁。](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/widget-settings.png)

接下來，選擇 **[!DNL Behavior]** 頁籤，並將網頁掛接URL添加到 *[!DNL Webhook when a new conversation starts]* 欄位和您要訂閱的任何其他webhook事件欄位。

![顯示webhook終結點欄位的Chatlio UI。](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/webhook.png)

>[!TIP]
>
>您可以訂閱各種不同的事件 [!DNL Chatlio] 網鈎。 有關不同事件的詳細資訊，請參閱 [[!DNL Chatlio] 事件文檔](https://chatlio.com/docs/webhooks/)。

## 後續步驟 {#next-steps}

通過遵循本教程，您已成功配置流資料流，以 [!DNL Chatlio] 資料到Experience Platform。 要監視正在攝取的資料，請參閱上的指南 [使用平台UI監視流資料流](../../monitor-streaming.md)。

## 其他資源 {#additional-resources}

以下各節提供了在使用 [!DNL Chatlio] 源。

### 驗證 {#validation}

驗證是否正確設定了源和 [!DNL Chatlio] 正在接收消息，請執行以下步驟：

* 您可以檢查 [!DNL Chatlio] **[!UICONTROL 報告]** > **[!UICONTROL 聊天歷史記錄]** 頁，用於標識捕獲的事件 [!DNL Chatlio]。

![顯示聊天歷史記錄的查特利奧UI螢幕快照](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/chatlio-chat-history.png)

* 在平台UI中，選擇 **[!UICONTROL 查看資料流]** 欄 [!DNL Chatlio] 源目錄上的卡菜單。 下一步，選擇 **[!UICONTROL 預覽資料集]** 驗證為您在中配置的Webhook所攝取的資料 [!DNL Chatlio]。

![顯示已接收事件的平台UI螢幕快照](../../../../images/tutorials/create/marketing-automation/chatlio-webhook/platform-dataset.png)

有關 [!DNL Chatlio]，訪問 [[!DNL Chatlio] 文檔](https://chatlio.com/docs/) 和 [常見問題](https://chatlio.com/pricing/#FAQ)。
