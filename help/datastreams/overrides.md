---
title: 設定資料流覆寫
description: 瞭解如何在資料串流UI中設定資料串流覆寫，並透過Web SDK或Mobile SDK加以啟用。
exl-id: 3f17a83a-dbea-467b-ac67-5462c07c884c
source-git-commit: 79d724eec4903b8a3eee6f717d94fcd70a4ffcb7
workflow-type: tm+mt
source-wordcount: '958'
ht-degree: 38%

---

# 設定資料流覆寫

使用資料流覆寫來定義資料流的其他設定，這些資料流會透過Web SDK或Mobile SDK傳遞到[!DNL Edge Network]。

觸發不同的資料流行為，而不建立新的資料流或修改現有的設定。

資料流設定覆寫分為兩個步驟：

1. 首先，您必須在[資料流設定頁面](/help/datastreams/configure.md)中定義資料流設定覆寫。
2. 然後，您必須以下列其中一種方式將覆寫傳送至[!DNL Edge Network]：
   * 透過`sendEvent`或`configure` [網頁SDK](#send-overrides)命令。
   * 透過Web SDK [標籤延伸模組](/help/tags/extensions/client/web-sdk/configure/configuration-overrides.md)。
   * 透過Mobile SDK [sendEvent](#send-overrides) API或使用[規則](#send-overrides)。

本文會介紹每種受支援的覆寫類型的端對端資料流設定覆寫流程。

>[!IMPORTANT]
>
>[!DNL Edge Network] API整合目前不支援資料流覆寫。
>
>當您需要將不同的資料發送到不同的資料流時，應使用資料流覆寫。 請勿對個人化使用案例或同意資料使用資料流覆寫。

## 使用案例 {#use-cases}

下列使用案例顯示如何使用及何時使用資料流覆寫。

### 多區域資料收集 {#multi-region}

一家公司在營運所在各個國家/地區擁有不同的網站或子網域。 它們具有[已設定的](/help/datastreams/configure.md)個個別資料串流，其中包含對應的分析特定報表套裝、國家/地區特定的[!DNL Adobe Target]屬性權杖、國家/地區特定的結構描述、資料集、[!DNL Journey Optimizer]設定等。 該公司還擁有一套全球設定，彙總所有國家/地區特定的資料。

透過使用資料流覆寫，該公司可採用機動方式將資料流切換到不同的資料流，而不是向一個資料流發送資料的預設行為。

常見的使用案例是傳送資料至特定國家/地區的資料流，以及當客戶執行重要動作（例如下訂單或更新其使用者設定檔）時傳送至全球資料流。

### 區分不同業務單位的設定檔和身分 {#multiple-business-units}

擁有多個業務單位的公司想要使用多個Experience Platform沙箱，以儲存每個業務單位的特定資料。

該公司可以採用資料流覆寫來確保每個業務部門都有自己的資料流來接收資料，而不是將資料發送到預設資料流。

## 在資料流 UI 中設定資料流覆寫 {#configure-overrides}

資料流設定覆寫可讓您修改下列資料流設定：

* Experience Platform 事件資料集
* [!DNL Adobe Target]屬性Token
* Audience Manager ID 同步容器
* [!DNL Adobe Analytics]個報告套裝

### Adobe Target 的資料流覆寫 {#target-overrides}

若要設定[!DNL Adobe Target]資料流的資料流覆寫，您必須先建立[!DNL Adobe Target]資料流。 請依照說明[設定資料流](/help/datastreams/configure.md)和 [Adobe Target](/help/datastreams/configure.md#target) 服務。

建立資料流後，請編輯您新增的[Adobe Target](/help/datastreams/configure.md#target)服務，並使用&#x200B;**[!UICONTROL Property Token Overrides]**&#x200B;區段來新增所需的資料流覆寫。 每行新增一個屬性語彙基元。

![顯示 Adobe Target 服務設定的資料流 UI 螢幕擷圖，並醒目顯示屬性語彙基元覆寫。](assets/overrides/override-target.png)

新增所需的覆寫之後，請儲存資料流設定。

現已設定[!DNL Adobe Target]資料流覆寫。 您現在可以[透過Web SDK或Mobile SDK](#send-overrides)將覆寫傳送至 [!DNL Edge Network] 。

### 適用於 Adobe Analytics 的資料流覆寫 {#analytics-overrides}

若要設定[!DNL Adobe Analytics]資料流的資料流覆寫，您必須先建立[Adobe Analytics](/help/datastreams/configure.md#analytics)資料流。 請依照說明[設定資料流](/help/datastreams/configure.md)和 [Adobe Analytics](/help/datastreams/configure.md#analytics) 服務。

建立資料流後，請編輯您新增的[Adobe Analytics](/help/datastreams/configure.md#analytics)服務，並使用&#x200B;**[!UICONTROL Report Suite Overrides]**&#x200B;區段來新增所需的資料流覆寫。

選取&#x200B;**[!UICONTROL Show Batch Mode]**&#x200B;以啟用報告套裝覆寫的批次編輯。 您可以複製並貼上報告套裝覆寫的清單，每行輸入一個報告套裝。

![顯示 Adobe Analytics 服務設定的資料流 UI 螢幕擷圖，並醒目顯示報告套裝覆寫。](assets/overrides/override-analytics.png)

新增所需的覆寫之後，請儲存資料流設定。

現已設定[!DNL Adobe Analytics]資料流覆寫。 您現在可以[透過Web SDK或Mobile SDK](#send-overrides)將覆寫傳送至 [!DNL Edge Network] 。

### 適用於 Experience Platform 事件資料集的資料流覆寫 {#event-dataset-overrides}

若要設定 Experience Platform 事件資料集的資料流覆寫，您首先必須建立 [Adobe Experience Platform](/help/datastreams/configure.md#aep)。 請依照說明[設定資料流](/help/datastreams/configure.md)和 [Adobe Experience Platform](/help/datastreams/configure.md#aep) 服務。

建立資料流後，編輯您新增的[Adobe Experience Platform](/help/datastreams/configure.md#aep)服務，並選取&#x200B;**[!UICONTROL Add Event Dataset]**&#x200B;選項以新增一或多個覆寫事件資料集。

![顯示 Adobe Experience Platform 服務設定的資料流 UI 螢幕擷圖，並醒目顯示事件資料集覆寫。](assets/overrides/override-aep.png)

新增所需的覆寫之後，請儲存資料流設定。

現已設定[!DNL Adobe Experience Platform]資料流覆寫。 您現在可以[透過Web SDK或Mobile SDK](#send-overrides)將覆寫傳送至 [!DNL Edge Network] 。

### 適用於協力廠商 ID 同步容器的資料流覆寫 {#container-overrides}

若要設定協力廠商 ID 同步容器的資料流覆寫，您首先必須建立資料流。 請依照說明[設定資料流](/help/datastreams/configure.md)，以建立一個。

建立資料串流後，移至&#x200B;**[!UICONTROL Advanced Options]**&#x200B;並啟用&#x200B;**[!UICONTROL Third Party ID Sync]**&#x200B;選項。

然後，使用&#x200B;**[!UICONTROL Container ID Overrides]**&#x200B;區段來新增您要覆寫預設設定的容器ID。

>[!IMPORTANT]
>
>容器 ID 必須為數值，例如 `1234567`，而不是字串，例如 `"1234567"`。 如果您以容器 ID 覆寫透過 Web SDK 傳送字串值，您將收到錯誤訊息。

![顯示資料流設定的資料流 UI 螢幕擷圖，並醒目顯示協力廠商 ID 同步容器覆寫。](assets/overrides/override-container.png)

新增所需的覆寫之後，請儲存資料流設定。

現在已設定ID同步容器覆寫。 您現在可以[透過Web SDK或Mobile SDK](#send-overrides)將覆寫傳送至 [!DNL Edge Network] 。

## 將覆寫傳送至Edge Network {#send-overrides}

在資料收集UI中設定資料流覆寫後，您可以透過Web SDK或Mobile SDK將覆寫傳送至[!DNL Edge Network]。

* **網頁SDK**：如需JavaScript程式庫程式碼範例，請參閱[資料流設定覆寫](/help/collection/js/commands/configure/edgeconfigoverrides.md)。
* **行動SDK**：您可以使用[sendEvent API](https://developer.adobe.com/client-sdks/edge/edge-network/tutorials/send-overrides-sendevent/)或使用[規則](https://developer.adobe.com/client-sdks/edge/edge-network/tutorials/send-overrides-rules/)來傳送資料串流ID覆寫。

## 裝載範例 {#payload-example}

上述範例會產生與以下範例類似的[!DNL Edge Network]裝載。

```json
{
  "meta": {
    "configOverrides": {
      "com_adobe_experience_platform": {
        "datasets": {
          "event": {
            "datasetId": "SampleProfileDatasetIdOverride"
          }
        }
      },
      "com_adobe_analytics": {
        "reportSuites": [
        "MyFirstOverrideReportSuite",
        "MySecondOverrideReportSuite",
        "MyThirdOverrideReportSuite"
        ]
      },
      "com_adobe_identity": {
        "idSyncContainerId": "1234567"
      },
      "com_adobe_target": {
        "propertyToken": "63a46bbc-26cb-7cc3-def0-9ae1b51b6c62"
      }
    },
    "state": {  }
  },
  "events": [  ]
}
```
