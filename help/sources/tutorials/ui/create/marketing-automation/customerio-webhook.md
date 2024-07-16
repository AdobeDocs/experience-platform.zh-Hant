---
title: 在UI中建立Customer.io Source連線和資料流
description: 瞭解如何使用Adobe Experience Platform UI建立Customer.io來源連線。
badge: Beta
exl-id: 7655a34c-808a-46e3-94e3-022a433755a4
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '1213'
ht-degree: 1%

---

# 在UI中建立[!DNL Customer.io]來源連線和資料流

>[!NOTE]
>
>[!DNL Customer.io]來源是測試版。 如需使用Beta版標籤來源的相關資訊，請參閱[來源概觀](../../../../home.md#terms-and-conditions)。

本教學課程提供使用Adobe Experience Platform使用者介面建立[!DNL Customer.io]來源連線和資料流的步驟。

## 快速入門 {#getting-started}

本教學課程需要您實際瞭解下列Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)： [!DNL Experience Platform]用來組織客戶體驗資料的標準化架構。
   * [結構描述組合的基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器使用者介面建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

## 先決條件 {#prerequisites}

下節提供建立[!DNL Customer.io]來源連線之前必須完成的必要條件資訊。

### 定義[!DNL Customer.io]之來源結構描述的JSON範例 {#prerequisites-json-schema}

建立[!DNL Customer.io]來源連線之前，您需要提供來源結構描述。 您可以使用以下JSON。

```
{
  "event_id": "01E4C4CT6YDC7Y5M7FE1GWWPQJ",
  "object_type": "customer",
  "metric": "subscribed",
  "timestamp": 1613063089,
  "data": {
    "customer_id": "42",
    "email_address": "test@example.com",
    "identifiers": {
      "id": "42",
      "email": "test@example.com",
      "cio_id": "d9c106000001"
    }
  }
}
```

### 建立[!DNL Customer.io]的平台結構描述 {#create-platform-schema}

您也必須確保建立用於來源的Platform結構。 請參閱有關[建立Platform結構描述](../../../../../xdm/schema/composition.md)的教學課程，以瞭解如何建立結構描述的完整步驟。

![Platform UI熒幕擷圖顯示Customer.io](../../../../images/tutorials/create/marketing-automation/customerio-webhook/schema.png)的範例結構描述

## 連線您的[!DNL Customer.io]帳戶 {#connect-account}

在Platform UI中，從左側導覽選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取[!UICONTROL 來源]工作區，並檢視Experience Platform中可用的來源目錄。

使用&#x200B;*[!UICONTROL 類別]*&#x200B;功能表，依類別篩選來源。 或者，在搜尋列中輸入來源名稱，從目錄中尋找特定來源。

移至[!UICONTROL 行銷自動化]類別以檢視[!DNL Customer.io]來源卡。 若要開始，請選取&#x200B;**[!UICONTROL 新增資料]**。

![具有Customer.io卡之目錄的Platform UI熒幕擷圖](../../../../images/tutorials/create/marketing-automation/customerio-webhook/catalog.png)

## 選取資料 {#select-data}

**[!UICONTROL 選取資料]**&#x200B;步驟隨即顯示，提供介面供您選取要帶到Platform的資料。

* 介面的左側是瀏覽器，可讓您檢視帳戶內的可用資料流；
* 介面的右側部分可讓您預覽JSON檔案中最多100列的資料。

選取&#x200B;**[!UICONTROL 上傳檔案]**&#x200B;以從您的本機系統上傳JSON檔案。 或者，您也可以將要上傳的JSON檔案拖放至[!UICONTROL 拖放檔案]面板。

![來源工作流程的新增資料步驟。](../../../../images/tutorials/create/marketing-automation/customerio-webhook//add-data.png)

上傳檔案後，預覽介面會更新，以顯示您上傳的結構描述預覽。 預覽介面可讓您檢查檔案的內容和結構。 您也可以使用[!UICONTROL 搜尋欄位]公用程式來存取結構描述中的特定專案。

完成後，選取&#x200B;**[!UICONTROL 下一步]**。

![來源工作流程的預覽步驟。](../../../../images/tutorials/create/marketing-automation/customerio-webhook//preview.png)

## 資料流詳細資料 {#dataflow-detail}

**資料流詳細資料**&#x200B;步驟隨即顯示，為您提供使用現有資料集或建立資料流新資料集的選項，以及提供資料流名稱和說明的機會。 在此步驟中，您還可以配置設定檔擷取、錯誤診斷、部分擷取和警報的設定。

完成後，選取&#x200B;**[!UICONTROL 下一步]**。

![來源工作流程的資料流詳細資料步驟。](../../../../images/tutorials/create/marketing-automation/customerio-webhook//dataflow-detail.png)

## 對應 {#mapping}

[!UICONTROL 對應]步驟出現，為您提供介面，用於將來源結構描述中的來源欄位對應到目標結構描述中適當的目標XDM欄位。

Platform會根據您選取的目標結構或資料集，為自動對應的欄位提供智慧型建議。 您可以手動調整對應規則以符合您的使用案例。 您可以根據自己的需求，選擇直接對應欄位，或使用資料準備函式來轉換來源資料，以衍生計算或計算的值。 如需使用對應程式介面和計算欄位的完整步驟，請參閱[資料準備UI指南](../../../../../data-prep/ui/mapping.md)。

下列所有對應都是強制性的，在繼續進行[!UICONTROL 檢閱]階段之前應先進行設定。

| 目標欄位 | 說明 |
| --- | --- |
| `object_type` | 物件型別，請參閱支援型別的[!DNL Customer.io] [事件](https://customer.io/docs/webhooks/#events)檔案。 |
| `id` | 物件的識別碼。 |
| `email` | 與物件關聯的電子郵件地址。 |
| `event_id` | 事件的唯一識別碼。 |
| `cio_id` | 事件的[!DNL Customer.io]識別碼。 |
| `metric` | 事件型別。 如需詳細資訊，請參閱支援型別的[!DNL Customer.io] [事件](https://customer.io/docs/webhooks/#events)檔案。 |
| `timestamp` | 事件發生時的時間戳記。 |

>[!IMPORTANT]
>
>在`test mode`中執行[!DNL Customer.io] webhook時不要對應`cio_id`，因為沒有從[!DNL Customer.io]傳送的相關欄位。

成功對應來源資料後，請選取&#x200B;**[!UICONTROL 下一步]**。

![來源工作流程的對應步驟。](../../../../images/tutorials/create/marketing-automation/customerio-webhook/mapping.png)

## 檢閱 {#review}

**[!UICONTROL 檢閱]**&#x200B;步驟隨即顯示，可讓您在建立新資料流之前先檢閱該資料流。 詳細資料會分組到以下類別中：

* **[!UICONTROL 連線]**：顯示來源型別、所選來源檔案的相關路徑，以及該來源檔案中的欄數。
* **[!UICONTROL 指派資料集與對應欄位]**：顯示要將來源資料擷取到哪個資料集，包括資料集所堅持的結構描述。

檢閱您的資料流後，請選取&#x200B;**[!UICONTROL 完成]**，並等待一些時間來建立資料流。

![來源工作流程的稽核步驟。](../../../../images/tutorials/create/marketing-automation/customerio-webhook/review.png)

## 取得您的串流端點URL {#get-streaming-endpoint}

建立串流資料流後，您現在可以擷取串流端點URL。 此端點將用於訂閱您的webhook，允許您的串流來源與Experience Platform通訊。

若要建構用來在[!DNL Customer.io]上設定webhook的URL，您必須擷取下列專案：

* **[!UICONTROL 資料流ID]**
* **[!UICONTROL 串流端點]**

若要擷取您的&#x200B;**[!UICONTROL 資料流ID]**&#x200B;和&#x200B;**[!UICONTROL 串流端點]**，請移至您剛才建立之資料流的[!UICONTROL 資料流活動]頁面，並從[!UICONTROL 屬性]面板底部複製詳細資料。

![資料流活動中的串流端點。](../../../../images/tutorials/create/marketing-automation/customerio-webhook/endpoint-test.png)

擷取串流端點與資料流ID後，請根據下列模式建置URL： ```{STREAMING_ENDPOINT}?x-adobe-flow-id={DATAFLOW_ID}```。 例如，建構的webhook URL可能如下所示： ``https://dcs.adobedc.net/collection/febc116d22ba0ea2868e9c93b199375302afb8a589617700991bb8f3f0341ad7?x-adobe-flow-id=439b3fc4-3042-4a3a-b5e0-a494898d3fb0``

## 在[!DNL Customer.io]中設定報告webhook {#set-up-webhook}

建立webhook URL後，您現在可以使用[!DNL Customer.io]使用者介面設定報告webhook。 如需設定報告Webhook的步驟，請參閱關於設定Webhook的[[!DNL Customer.io] 指南](https://customer.io/docs/webhooks/#setup)。

在[!DNL Customer.io]使用者介面的[!DNL WEBHOOK ENDPOINT]欄位中輸入您的[webhook URL](#get-streaming-endpoint-url)。

![Customer.io使用者介面顯示webhook端點欄位](../../../../images/tutorials/create/marketing-automation/customerio-webhook/webhook.png)

>[!TIP]
>
>您可以訂閱報表webhook的各種不同事件。 當符合[!DNL Customer.io]動作事件觸發條件時，每個事件的訊息都會內嵌至Platform。 如需不同事件的詳細資訊，請參閱[[!DNL Customer.io] 事件檔案](https://customer.io/docs/webhooks/#events)。

## 後續步驟 {#next-steps}

依照本教學課程中的指示，您已成功設定串流資料流，以將您的[!DNL Customer.io]資料帶入Experience Platform。 若要監視正在擷取的資料，請參閱[使用Platform UI監視串流資料流](../../monitor-streaming.md)的指南。

## 其他資源 {#additional-resources}

以下各節提供在使用[!DNL Customer.io]來源時可以參考的其他資源。

### 護欄 {#guardrails}

有關護欄的資訊，請參閱[[!DNL Customer.io] 逾時和失敗頁面](https://customer.io/docs/webhooks/#timeouts-and-failures)。

### 驗證 {#validation}

若要驗證您已正確設定來源，而且正在擷取[!DNL Customer.io]則訊息，請遵循下列步驟：

* 您可以檢查[!DNL Customer.io] **[!UICONTROL 活動記錄]**&#x200B;頁面，以識別[!DNL Customer.io]擷取的事件。

![Customer.io UI熒幕擷圖顯示活動記錄](../../../../images/tutorials/create/marketing-automation/customerio-webhook/activity-logs.png)

* 在Platform UI中，選取來源目錄上[!DNL Customer.io]卡片功能表旁的&#x200B;**[!UICONTROL 檢視資料流程]**。 接著，選取&#x200B;**[!UICONTROL 預覽資料集]**&#x200B;以驗證針對您在[!DNL Customer.io]內選取的事件所擷取的資料。

![顯示內嵌事件的平台UI熒幕擷取畫面](../../../../images/tutorials/create/marketing-automation/customerio-webhook/platform-dataset.png)
