---
keywords: Experience Platform；首頁；熱門主題；來源；連接器；來源連接器；來源sdk;sdk; SDK
title: （測試版）在UI中建立Mixpanel來源連線
description: 了解如何使用Adobe Experience Platform UI建立Mixpanel來源連線。
exl-id: 2a02f6a4-08ed-468c-8052-f5b7be82d183
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '874'
ht-degree: 10%

---

# （測試版）建立 [!DNL Mixpanel] UI中的源連接

>[!NOTE]
>
>此 [!DNL Mixpanel] 來源為測試版。 請參閱 [來源概觀](../../../../home.md#terms-and-conditions) 以取得使用測試版標籤來源的詳細資訊。

本教學課程提供建立 [!DNL Mixpanel] 來源連線(使用Adobe Experience Platform Platform使用者介面)。

## 快速入門

本教學課程需要妥善了解下列Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。
   * [結構構成基本概念](../../../../../xdm/schema/composition.md):了解XDM結構描述的基本建置組塊，包括結構描述的主要原則和最佳實務。
   * [結構編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用結構編輯器UI建立自訂結構。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。

### 收集所需憑據

為了連接 [!DNL Mixpanel] 若要使用Platform，您必須提供下列連線屬性的值：

| 憑據 | 說明 | 範例 |
| --- | --- | --- |
| 使用者名稱 | 與您的 [!DNL Mixpanel] 帳戶。 請參閱 [[!DNL Mixpanel] 服務帳戶檔案](https://developer.mixpanel.com/reference/service-accounts#authenticating-with-a-service-account) 以取得更多資訊。 | `Test8.6d4ee7.mp-service-account` |
| 密碼 | 與您的 [!DNL Mixpanel] 帳戶。 | `dLlidiKHpCZtJhQDyN2RECKudMeTItX1` |
| 專案 ID | 您的 [!DNL Mixpanel] 專案ID。 建立源連接時需要此ID。 請參閱 [[!DNL Mixpanel] 專案設定檔案](https://help.mixpanel.com/hc/en-us/articles/115004490503-Project-Settings) 和 [[!DNL Mixpanel] 建立和管理項目的指南](https://help.mixpanel.com/hc/en-us/articles/115004505106-Create-and-Manage-Projects) 以取得更多資訊。 | `2384945` |
| 時區 | 與 [!DNL Mixpanel] 專案。 建立源連接需要時區。 請參閱 [Mixpanel專案設定檔案](https://help.mixpanel.com/hc/en-us/articles/115004490503-Project-Settings) 以取得更多資訊。 | `Pacific Standard Time` |

如需驗證 [!DNL Mixpanel] 來源，請參閱 [[!DNL Mixpanel] 來源概觀](../../../../connectors/analytics/mixpanel.md).

## 連接您的 [!DNL Mixpanel] 帳戶

在平台UI中，選取 **[!UICONTROL 來源]** 從左側導覽列存取 [!UICONTROL 來源] 工作區。 此 [!UICONTROL 目錄] 畫面會顯示您可建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在 *Analytics* 類別，選擇 [!DNL Mixpanel]，然後選取 **[!UICONTROL 新增資料]**.

![目錄](../../../../images/tutorials/create/mixpanel-export-events/catalog.png)

此 **[!UICONTROL 連接Mixpanel帳戶]** 頁。 在此頁面上，您可以使用新憑證或現有憑證。

### 現有帳戶

若要使用現有帳戶，請選取 [!DNL Mixpanel] 要使用建立新資料流的帳戶，然後選擇 **[!UICONTROL 下一個]** 繼續。

![現有](../../../../images/tutorials/create/mixpanel-export-events/existing.png)

### 新帳戶

如果您要建立新帳戶，請選取 **[!UICONTROL 新帳戶]**，然後提供名稱、選用說明和您的憑證。 完成後，請選取 **[!UICONTROL 連接到源]** 然後讓新連接建立一段時間。

![new](../../../../images/tutorials/create/mixpanel-export-events/new.png)

## 選取您的專案ID和時區 {#project-id-and-timezone}

>[!CONTEXTUALHELP]
>id="platform_sources_mixpanel_timezone"
>title="設定 Mixpanel 擷取的時區"
>abstract="該時區必須和您的 Mixpanel 設定檔時區設定相同，因為平台會使用指定的專案時區從 Mixpanel 擷取相關資料。將事件記錄到 Mixpanel 資料存放區之前，Mixpanel 會調整其時區以和您的專案時區協調一致。"
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/analytics/mixpanel.html?lang=zh-Hant#project-id-and-timezone" text="了解文件的詳細資訊"

驗證來源後，請提供您的專案ID和時區，然後選取 **[!UICONTROL 選擇]**.

擷取您的 [!DNL Mixpanel] Platform的資料必須與 [!DNL Mixpanel] 設定檔時區設定。 對您資料時區的任何變更都只會套用至新事件，而舊事件則會保留在您先前指定的時區。 [!DNL Mixpanel] 因應日光節約時間，並適當調整您的擷取時間戳記。 如需時區如何影響資料的詳細資訊，請參閱 [!DNL Mixpanel] 指南 [管理專案的時區](https://help.mixpanel.com/hc/en-us/articles/115004547203-Manage-Timezones-for-Projects-in-Mixpanel).

幾分鐘後，正確的介面將更新到預覽面板，允許您在建立資料流之前檢查您的架構。 完成後，請選取 **[!UICONTROL 下一個]**.

![配置](../../../../images/tutorials/create/mixpanel-export-events/authentication-configuration.png)

## 後續步驟

依照本教學課程，您已建立與 [!DNL Mixpanel] 帳戶。 您現在可以繼續下一個教學課程，以及 [設定資料流以將analytics資料匯入Platform](../../dataflow/analytics.md).

## 其他資源 {#additional-resources}

以下各節提供您在使用 [!DNL Mixpanel] 來源。

### 驗證 {#validation}

以下概述驗證您已成功連線時可採取的步驟 [!DNL Mixpanel] 來源 [!DNL Mixpanel] 事件正在擷取至Platform。

在平台UI中，選取 **[!UICONTROL 資料集]** 從左側導覽列存取 [!UICONTROL 資料集] 工作區。 此 [!UICONTROL 資料集活動] 畫面會顯示執行的詳細資訊。

![資料集 — 活動](../../../../images/tutorials/create/mixpanel-export-events/dataset-activity.png)

接下來，選擇要查看的資料流的資料流運行ID，以查看該資料流運行的特定詳細資訊。

![資料流監視](../../../../images/tutorials/create/mixpanel-export-events/dataflow-monitoring.png)

最後，選取 **[!UICONTROL 預覽資料集]** 以顯示擷取的資料。

![預覽資料集](../../../../images/tutorials/create/mixpanel-export-events/preview-dataset.png)

您可以根據 [!DNL Mixpanel] > [!DNL Events] 頁面。 請參閱 [[!DNL Mixpanel] 事件檔案](https://help.mixpanel.com/hc/en-us/articles/4402837164948-Events-formerly-Live-View-) 以取得更多資訊。

![mixpanel-events](../../../../images/tutorials/create/mixpanel-export-events/mixpanel-events.png)

### Mixpanel結構

下表列出必須為 [!DNL Mixpanel].

>[!TIP]
>
>請參閱 [事件匯出API >下載](https://developer.mixpanel.com/reference/raw-event-export) 以取得API的詳細資訊。


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

* 您最多可以每小時有100個同時查詢和60個查詢，如 [匯出API速率限制](https://help.mixpanel.com/hc/en-us/articles/115004602563-Rate-Limits-for-API-Endpoints).
