---
keywords: Experience Platform；首頁；熱門主題；源；連接器；源連接器；源sdk;sdk;SDK
title: (Beta)在UI中建立混合面板源連接
description: 瞭解如何使用Adobe Experience PlatformUI建立Mixpanel源連接。
exl-id: 2a02f6a4-08ed-468c-8052-f5b7be82d183
source-git-commit: 6b9e5da9e552d93ff174d1d65dabb0ffd3128c1a
workflow-type: tm+mt
source-wordcount: '874'
ht-degree: 10%

---

# (Beta)建立 [!DNL Mixpanel] UI中的源連接

>[!NOTE]
>
>的 [!DNL Mixpanel] 源為beta。 查看 [源概述](../../../../home.md#terms-and-conditions) 的子菜單。

本教程提供建立 [!DNL Mixpanel] 源連接使用Adobe Experience Platform平台用戶介面。

## 快速入門

本教程需要對以下Experience Platform組成部分進行有效理解：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。
   * [架構組合的基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本構建基塊，包括架構組成中的關鍵原則和最佳做法。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自定義架構。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):基於來自多個源的聚合資料提供統一、即時的用戶配置檔案。

### 收集所需憑據

為了連接 [!DNL Mixpanel] 到平台，必須提供以下連接屬性的值：

| 憑據 | 說明 | 範例 |
| --- | --- | --- |
| 用戶名 | 與您的服務帳戶對應的服務帳戶用戶名 [!DNL Mixpanel] 帳戶。 查看 [[!DNL Mixpanel] 服務帳戶文檔](https://developer.mixpanel.com/reference/service-accounts#authenticating-with-a-service-account) 的子菜單。 | `Test8.6d4ee7.mp-service-account` |
| 密碼 | 與您的 [!DNL Mixpanel] 帳戶。 | `dLlidiKHpCZtJhQDyN2RECKudMeTItX1` |
| 專案 ID | 您 [!DNL Mixpanel] 項目ID。 建立源連接需要此ID。 查看 [[!DNL Mixpanel] 項目設定文檔](https://help.mixpanel.com/hc/en-us/articles/115004490503-Project-Settings) 和 [[!DNL Mixpanel] 指南建立和管理項目](https://help.mixpanel.com/hc/en-us/articles/115004505106-Create-and-Manage-Projects) 的子菜單。 | `2384945` |
| 時區 | 與 [!DNL Mixpanel] 項目。 建立源連接需要時區。 查看 [混合面板項目設定文檔](https://help.mixpanel.com/hc/en-us/articles/115004490503-Project-Settings) 的子菜單。 | `Pacific Standard Time` |

有關驗證您 [!DNL Mixpanel] 源，請參閱 [[!DNL Mixpanel] 源概述](../../../../connectors/analytics/mixpanel.md)。

## 連接 [!DNL Mixpanel] 帳戶

在平台UI中，選擇 **[!UICONTROL 源]** 從左導航欄訪問 [!UICONTROL 源] 工作區。 的 [!UICONTROL 目錄] 螢幕顯示可建立帳戶的各種源。

可以從螢幕左側的目錄中選擇相應的類別。 或者，您可以使用搜索選項找到要使用的特定源。

在 *分析* 類別，選擇 [!DNL Mixpanel]，然後選擇 **[!UICONTROL 添加資料]**。

![目錄](../../../../images/tutorials/create/mixpanel-export-events/catalog.png)

的 **[!UICONTROL 連接Mixpanel帳戶]** 的子菜單。 在此頁上，您可以使用新憑據或現有憑據。

### 現有帳戶

要使用現有帳戶，請選擇 [!DNL Mixpanel] 要使用建立新資料流的帳戶，然後選擇 **[!UICONTROL 下一個]** 繼續。

![現有](../../../../images/tutorials/create/mixpanel-export-events/existing.png)

### 新帳戶

如果要建立新帳戶，請選擇 **[!UICONTROL 新帳戶]**，然後提供名稱、可選說明和您的憑據。 完成後，選擇 **[!UICONTROL 連接到源]** 然後再給新連接建立一段時間。

![新](../../../../images/tutorials/create/mixpanel-export-events/new.png)

## 選擇項目ID和時區 {#project-id-and-timezone}

>[!CONTEXTUALHELP]
>id="platform_sources_mixpanel_timezone"
>title="設定 Mixpanel 擷取的時區"
>abstract="該時區必須和您的 Mixpanel 設定檔時區設定相同，因為平台會使用指定的專案時區從 Mixpanel 擷取相關資料。將事件記錄到 Mixpanel 資料存放區之前，Mixpanel 會調整其時區以和您的專案時區協調一致。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/analytics/mixpanel.html?lang=en#project-id-and-timezone" text="了解文件的詳細資訊"

驗證源後，提供項目ID和時區，然後選擇 **[!UICONTROL 選擇]**。

在接收之前指定的時區 [!DNL Mixpanel] 到平台的資料必須與 [!DNL Mixpanel] 配置檔案時區設定。 對資料時區的任何更改將只應用於新事件，舊事件將保留在您以前指定的時區中。 [!DNL Mixpanel] 適應夏令時，並將適當調整您的接收時間戳。 有關時區如何影響資料的詳細資訊，請參閱 [!DNL Mixpanel] 指南 [管理項目時區](https://help.mixpanel.com/hc/en-us/articles/115004547203-Manage-Timezones-for-Projects-in-Mixpanel)。

過一會兒，右側介面將更新到預覽面板，允許您在建立資料流之前檢查架構。 完成後，選擇 **[!UICONTROL 下一個]**。

![配置](../../../../images/tutorials/create/mixpanel-export-events/authentication-configuration.png)

## 後續步驟

按照本教程，您已建立到 [!DNL Mixpanel] 帳戶。 現在，您可以繼續下一個教程， [配置資料流，將分析資料引入平台](../../dataflow/analytics.md)。

## 其他資源 {#additional-resources}

以下各節提供了在使用 [!DNL Mixpanel] 源。

### 驗證 {#validation}

以下概述了驗證您已成功連接時可以採取的步驟 [!DNL Mixpanel] 來源 [!DNL Mixpanel] 正在將事件接收到平台。

在平台UI中，選擇 **[!UICONTROL 資料集]** 從左導航欄訪問 [!UICONTROL 資料集] 工作區。 的 [!UICONTROL 資料集活動] 螢幕顯示執行的詳細資訊。

![資料集活動](../../../../images/tutorials/create/mixpanel-export-events/dataset-activity.png)

接下來，選擇要查看的資料流的資料流運行ID，以查看有關該資料流運行的特定詳細資訊。

![資料流監視](../../../../images/tutorials/create/mixpanel-export-events/dataflow-monitoring.png)

最後，選擇 **[!UICONTROL 預覽資料集]** 來顯示所攝資料。

![預覽資料集](../../../../images/tutorials/create/mixpanel-export-events/preview-dataset.png)

您可以根據 [!DNL Mixpanel] > [!DNL Events] 的子菜單。 查看 [[!DNL Mixpanel] 事件文檔](https://help.mixpanel.com/hc/en-us/articles/4402837164948-Events-formerly-Live-View-) 的子菜單。

![混合面板事件](../../../../images/tutorials/create/mixpanel-export-events/mixpanel-events.png)

### 混合面板架構

下表列出了必須為 [!DNL Mixpanel]。

>[!TIP]
>
>請參閱 [事件導出API >下載](https://developer.mixpanel.com/reference/raw-event-export) 的子菜單。


| 來源 | 類型 |
|---|---|
| `distinct_id` | 字串 |
| `event_name` | 字串 |
| `import` | 布林值 |
| `insert_id` | 字串 |
| `item_id` | 字串 |
| `item_name` | 字串 |
| `item_price` | 字串 |
| `mp_api_endpoint` | 字串 |
| `mp_api_timestamp_ms` | 整數 |
| `mp_processing_time_ms` | 整數 |
| `time` | 整數 |

### 限制 {#limits}

* 您每小時最多有100個併發查詢和60個查詢，如上所示 [導出API速率限制](https://help.mixpanel.com/hc/en-us/articles/115004602563-Rate-Limits-for-API-Endpoints)。
