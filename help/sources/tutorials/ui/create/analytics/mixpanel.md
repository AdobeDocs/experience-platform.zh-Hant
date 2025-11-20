---
title: 在UI中建立Mixpanel Source連線
description: 瞭解如何使用Adobe Experience Platform UI建立Mixpanel來源連線。
exl-id: 2a02f6a4-08ed-468c-8052-f5b7be82d183
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 11%

---

# 在 UI 中建立 [!DNL Mixpanel] 一個來源連線

本教學課程提供使用Adobe Experience Platform Experience Platform使用者介面建立[!DNL Mixpanel]來源連線的步驟。

## 快速入門

本教學課程需要您實際瞭解下列Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)： [!DNL Experience Platform]用來組織客戶體驗資料的標準化架構。
   * [結構描述組合的基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [Schema Editor 教學](../../../../../xdm/tutorials/create-schema-ui.md)：學習如何使用 Schema Editor 介面建立自訂 Schema。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：提供基於多個來源彙整數據的統一即時消費者檔案。

### 蒐集所需的證件

若要連接 [!DNL Mixpanel] Experience Platform，您必須為以下連線屬性提供數值：

| 學歷 | 說明 | 範例 |
| --- | --- | --- |
| 使用者名稱 | 與您的[!DNL Mixpanel]帳戶對應的服務帳戶使用者名稱。 如需詳細資訊，請參閱[[!DNL Mixpanel] 服務帳戶檔案](https://developer.mixpanel.com/reference/service-accounts#authenticating-with-a-service-account)。 | `Test8.6d4ee7.mp-service-account` |
| 密碼 | 與您的[!DNL Mixpanel]帳戶對應的服務帳戶密碼。 | `dLlidiKHpCZtJhQDyN2RECKudMeTItX1` |
| 專案ID | 您的[!DNL Mixpanel]專案識別碼。 建立來源連線需要此ID。 如需詳細資訊，請參閱[[!DNL Mixpanel] 專案設定檔案](https://help.mixpanel.com/hc/en-us/articles/115004490503-Project-Settings)以及建立和管理專案的[[!DNL Mixpanel] 指南](https://help.mixpanel.com/hc/en-us/articles/115004505106-Create-and-Manage-Projects)。 | `2384945` |
| 時區 | 與您的[!DNL Mixpanel]專案對應的時區。 建立來源連線需要時區。 更多資訊請參閱 [Mixpanel 專案設定文件](https://help.mixpanel.com/hc/en-us/articles/115004490503-Project-Settings) 。 | `Pacific Standard Time` |

如需驗證[!DNL Mixpanel]來源的詳細資訊，請參閱[[!DNL Mixpanel] 來源概觀](../../../../connectors/analytics/mixpanel.md)。

## 連線您的[!DNL Mixpanel]帳戶

在Experience Platform UI中，從左側導覽列選取「**[!UICONTROL Sources]**」以存取[!UICONTROL Sources]工作區。 [!UICONTROL Catalog]畫面會顯示您可以建立帳戶的各種來源。

您可以從熒幕左側的目錄中選取適當的類別。 或者，你也可以透過搜尋功能找到你想合作的特定來源。

在分析&#x200B;**&#x200B;分類中，選擇 [!DNL Mixpanel]，然後選擇 &#x200B;** [!UICONTROL Add data]**。

![目錄](../../../../images/tutorials/create/mixpanel-export-events/catalog.png)

**[!UICONTROL Connect Mixpanel account]**&#x200B;頁面出現了。在這個頁面上，你可以選擇使用新的憑證或現有的憑證。

### 現有帳戶

若要使用現有帳戶，請選取您要用來建立新資料流的[!DNL Mixpanel]帳戶，然後選取&#x200B;**[!UICONTROL Next]**&#x200B;以繼續。

![現有](../../../../images/tutorials/create/mixpanel-export-events/existing.png)

### 新帳戶

如果您正在建立新帳戶，請選取&#x200B;**[!UICONTROL New account]**，然後提供名稱、選擇性說明和您的認證。 完成時，請選取&#x200B;**[!UICONTROL Connect to source]**，然後等待一段時間以建立新連線。

![新](../../../../images/tutorials/create/mixpanel-export-events/new.png)

## 選取您的專案 ID 和時區 {#project-id-and-timezone}

>[!CONTEXTUALHELP]
>id="platform_sources_mixpanel_timezone"
>title="設定 Mixpanel 攝取的時區"
>abstract="該時區必須和您的 Mixpanel 輪廓時區設定相同，因為 Experience Platform 會使用指定的專案時區從 Mixpanel 攝取相關資料。將事件記錄到 Mixpanel 資料存放區之前，Mixpanel 會調整其時區以和您的專案時區協調一致。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/analytics/mixpanel.html#project-id-and-timezone" text="如需了解詳細資訊，請參閱文件"

一旦你的來源認證完成，請提供你的專案 ID 和時區，然後選擇 **[!UICONTROL Select]**。

你在將 [!DNL Mixpanel] 資料輸入 Experience Platform 前指定的時區必須與你的 [!DNL Mixpanel] 個人檔案時區設定相同。 你資料時區的任何變更只會套用在新事件上，舊事件則會保留在你先前指定的時區。 [!DNL Mixpanel] 它符合夏令時間，並會適當調整你的攝取時間戳。 想了解更多時區如何影響你的資料，請參閱[!DNL Mixpanel]專案時區[管理指南](https://help.mixpanel.com/hc/en-us/articles/115004547203-Manage-Timezones-for-Projects-in-Mixpanel)。

幾分鐘後，右側介面會更新到預覽面板，讓你能先檢查結構，然後再建立資料流。 完成後，選擇 **[!UICONTROL Next]**。

![配置](../../../../images/tutorials/create/mixpanel-export-events/authentication-configuration.png)

## 後續步驟

依照本教學課程中的指示，您已建立與[!DNL Mixpanel]帳戶的連線。 您現在可以繼續進行下一個教學課程，並[設定資料流，將分析資料匯入Experience Platform](../../dataflow/analytics.md)。

## 其他資源 {#additional-resources}

以下各節提供在使用[!DNL Mixpanel]來源時可以參考的其他資源。

### 驗證 {#validation}

以下概述您可以採取的步驟，以驗證您是否已成功連線[!DNL Mixpanel]來源，以及[!DNL Mixpanel]事件是否正在內嵌至Experience Platform。

在Experience Platform UI中，從左側導覽列選取「**[!UICONTROL Datasets]**」以存取[!UICONTROL Datasets]工作區。 [!UICONTROL Dataset Activity]畫面會顯示執行的詳細資訊。

![資料集活動](../../../../images/tutorials/create/mixpanel-export-events/dataset-activity.png)

接著，選取您要檢視之資料流程的資料流程執行ID，以檢視有關該資料流程執行的特定詳細資訊。

![資料流監視](../../../../images/tutorials/create/mixpanel-export-events/dataflow-monitoring.png)

最後，選擇 **[!UICONTROL Preview dataset]** 顯示已擷取的資料。

![預覽資料集](../../../../images/tutorials/create/mixpanel-export-events/preview-dataset.png)

您可以根據[!DNL Mixpanel] > [!DNL Events]頁面上的資料來驗證此資料。 如需詳細資訊，請參閱有關事件[[!DNL Mixpanel] 的](https://help.mixpanel.com/hc/en-us/articles/4402837164948-Events-formerly-Live-View-)檔案。

![mixpanel-events](../../../../images/tutorials/create/mixpanel-export-events/mixpanel-events.png)

### Mixpanel結構描述

下表列出了必須為 [!DNL Mixpanel]設定的支援映射。

>[!TIP]
>
>欲了解更多 API 資訊，請參閱 [事件匯出 API > 下載](https://developer.mixpanel.com/reference/raw-event-export) 。


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

* 根據匯出 API 速率限制[，您最多可同時查詢 100 次，每小時](https://help.mixpanel.com/hc/en-us/articles/115004602563-Rate-Limits-for-API-Endpoints)查詢 60 次。
