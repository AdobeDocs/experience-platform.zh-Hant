---
title: 設定資料流覆寫
description: 了解如何在資料流 UI 中設定資料流覆寫並透過 Web SDK 啟動它們。
exl-id: 3f17a83a-dbea-467b-ac67-5462c07c884c
source-git-commit: 11feeae0409822f0b1ccba2df263f0be466d54e3
workflow-type: tm+mt
source-wordcount: '1303'
ht-degree: 67%

---

# 設定資料流覆寫

資料流覆寫可讓您定義資料流的額外設定，這些設定會透過 Web SDK 傳遞到 Edge Network。

這可幫助您觸發與預設資料流不同的資料流行為，而無需建立資料流或修改現有設定。

資料流設定覆寫分為兩個步驟：

1. 首先，您必須在以下位置定義資料流設定覆蓋： [資料流設定頁面](configure.md).
2. 然後，您必須以下列其中一種方式將覆寫傳送至Edge Network：
   * 透過 `sendEvent` 或 `configure` [Web SDK](#send-overrides-web-sdk) 命令。
   * 透過Web SDK [標籤延伸模組](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).
   * 透過行動SDK [sendEvent](#send-overrides-mobile-sdk) 命令。

本文會介紹每種受支援的覆寫類型的端對端資料流設定覆寫流程。

>[!IMPORTANT]
>
>僅支援資料流覆寫 [Web SDK](../edge/home.md) 和 [行動SDK](https://developer.adobe.com/client-sdks/home/) 整合。 [伺服器API](../server-api/overview.md) 整合目前不支援資料流覆寫。
><br>
>當您需要將不同的資料發送到不同的資料流時，應使用資料流覆寫。請勿對個人化使用案例或同意資料使用資料流覆寫。

## 使用案例 {#use-cases}

為了幫助您更加了解如何以及何時使用資料流覆寫，以下是 Adobe Experience Platform 客戶可以使用此功能解決的一些使用案例。

**多區域資料收集**

一家公司在營運所在各個國家/地區擁有不同的網站或子網域。他們已透過對應的分析特定報告套裝、國家/地區特定的 Adobe Target 屬性語彙基元、國家/地區特定的架構、資料集、Journey Optimizer 設定等來[設定](configure.md)各別的資料流。該公司還擁有一套全球設定，彙總所有國家/地區特定的資料。

透過使用資料流覆寫，該公司可採用機動方式將資料流切換到不同的資料流，而不是向一個資料流發送資料的預設行為。

常見的使用案例可能是將資料傳送到特定國家/地區的資料流，以及傳送到客戶執行重要動作（例如下訂單或更新其使用者設定檔）的全球資料流。

**區分不同業務部門的個人資料檔和身分識別**

擁有多個業務單位的公司想要使用多個Experience Platform沙箱，以儲存每個業務單位的特定資料。

該公司可以採用資料流覆寫來確保每個業務部門都有自己的資料流來接收資料，而不是將資料發送到預設資料流。

## 在資料流 UI 中設定資料流覆寫 {#configure-overrides}

資料流設定覆寫可讓您修改下列資料流設定：

* Experience Platform 事件資料集
* Adobe Target 屬性語彙基元
* Audience Manager ID 同步容器
* Adobe Analytics 報告套裝

### Adobe Target 的資料流覆寫 {#target-overrides}

若要設定 Adobe Target 資料流的資料流覆寫，您首先必須建立 Adobe Target 資料流。請依照說明[設定資料流](configure.md)和 [Adobe Target](configure.md#target) 服務。

建立資料流後，請編輯 [Adobe Target](configure.md#target) 您已新增並使用的 **[!UICONTROL 屬性代號覆寫]** 區段來新增所需的資料流覆寫，如下圖所示。 每行新增一個屬性語彙基元。

![顯示 Adobe Target 服務設定的資料流 UI 螢幕擷圖，並醒目顯示屬性語彙基元覆寫。](assets/overrides/override-target.png)

新增所需的覆寫後，請儲存資料流設定。

您現在應該設定了 Adobe Target 資料流覆寫。現在您可以[透過 Web SDK 將覆寫發送到 Edge Network](#send-overrides)。

### 適用於 Adobe Analytics 的資料流覆寫 {#analytics-overrides}

若要設定 Adobe Analytics 資料流的資料流覆寫，您首先必須建立 [Adobe Analytics](configure.md#analytics)。請依照說明[設定資料流](configure.md)和 [Adobe Analytics](configure.md#analytics) 服務。

建立資料流後，請編輯 [Adobe Analytics](configure.md#target) 您已新增並使用的 **[!UICONTROL 報表套裝覆寫]** 區段來新增所需的資料流覆寫，如下圖所示。

若要啟用報告套裝覆寫的批次編輯，請選取&#x200B;**[!UICONTROL 顯示批次模式]**。您可以複製並貼上報告套裝覆寫的清單，每行輸入一個報告套裝。

![顯示 Adobe Analytics 服務設定的資料流 UI 螢幕擷圖，並醒目顯示報告套裝覆寫。](assets/overrides/override-analytics.png)

新增所需的覆寫後，請儲存資料流設定。

您現在應該設定了 Adobe Analytics 資料流覆寫。現在您可以[透過 Web SDK 將覆寫發送到 Edge Network](#send-overrides)。

### 適用於 Experience Platform 事件資料集的資料流覆寫 {#event-dataset-overrides}

若要設定 Experience Platform 事件資料集的資料流覆寫，您首先必須建立 [Adobe Experience Platform](configure.md#aep)。請依照說明[設定資料流](configure.md)和 [Adobe Experience Platform](configure.md#aep) 服務。

建立資料流後，請編輯 [Adobe Experience Platform](configure.md#aep) 您已新增的服務，並選取 **[!UICONTROL 新增事件資料集]** 用於新增一或多個覆寫事件資料集的選項，如下圖所示。

![顯示 Adobe Experience Platform 服務設定的資料流 UI 螢幕擷圖，並醒目顯示事件資料集覆寫。](assets/overrides/override-aep.png)

新增所需的覆寫後，請儲存資料流設定。

您現在應該設定了 Adobe Experience Platform 資料流覆寫。現在您可以[透過 Web SDK 將覆寫發送到 Edge Network](#send-overrides)。

### 適用於協力廠商 ID 同步容器的資料流覆寫 {#container-overrides}

若要設定協力廠商 ID 同步容器的資料流覆寫，您首先必須建立資料流。請依照說明[設定資料流](configure.md)，以建立一個。

建立資料流後，請前往&#x200B;**[!UICONTROL 進階選項]**，並啟用&#x200B;**[!UICONTROL 協力廠商 ID 同步]**&#x200B;選項。

然後，在&#x200B;**[!UICONTROL 容器 ID 覆寫]**&#x200B;區段中新增要覆寫預設設定的容器 ID，如下圖所示。

>[!IMPORTANT]
>
>容器 ID 必須為數值，例如 `1234567`，而不是字串，例如 `"1234567"`。如果您以容器 ID 覆寫透過 Web SDK 傳送字串值，您將收到錯誤訊息。

![顯示資料流設定的資料流 UI 螢幕擷圖，並醒目顯示協力廠商 ID 同步容器覆寫。](assets/overrides/override-container.png)

新增所需的覆寫後，請儲存資料流設定。

您現在應該設定了 ID 同步容器覆寫。現在您可以[透過 Web SDK 將覆寫傳送到 Edge Network](#send-overrides)。

## 透過 Web SDK 將覆寫傳送至 Edge Network {#send-overrides-web-sdk}

>[!NOTE]
>
>如果不透過 Web SDK 命令傳送設定覆寫，也可選擇將設定覆寫新增到 Web SDK [標記擴充功能](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)。

在資料收集 UI 中[設定資料流覆寫](#configure-overrides)後，現在即可透過 Web SDK 將覆寫傳送到 Edge Network。

如果您使用Web SDK，請透過將覆寫傳送至Edge Network `edgeConfigOverrides` command是啟動資料流設定覆寫的第二個也是最後一個步驟。

透過 `edgeConfigOverrides`Web SDK 命令傳送資料流設定覆寫到 Edge Network。這個命令會建立傳遞至的資料流覆寫 [!DNL Edge Network] 在下一個指令上。 如果您使用 `configure` 命令，則會針對每個請求傳遞覆寫。

此 `edgeConfigOverrides` 命令會建立資料流覆寫，這些覆寫會傳遞至 [!DNL Edge Network] 在下一個指令上。

設定覆寫和 `configure` 命令一起傳送時，會隨附在下列 Web SDK 命令中。

* [sendEvent](../edge/fundamentals/tracking-events.md)
* [setConsent](../edge/consent/iab-tcf/overview.md)
* [getIdentity](../edge/identity/overview.md)
* [appendIdentityToUrl](../edge/identity/id-sharing.md#cross-domain-sharing)
* [configure](../edge/fundamentals/configuring-the-sdk.md)

個別命令的設定選項可能會覆寫全域指定的選項。

### 透過Web SDK傳送設定覆寫 `sendEvent` 命令 {#send-event}

下面的範例會顯示在 `sendEvent` 命令時設定覆寫可能的情況。

```js {line-numbers="true" highlight="5-25"}
alloy("sendEvent", {
  xdm: {
    /* ... */
  },
  edgeConfigOverrides: {
    datastreamId: "{DATASTREAM_ID}"
    com_adobe_experience_platform: {
      datasets: {
        event: {
          datasetId: "SampleEventDatasetIdOverride"
        }
      }
    },
    com_adobe_analytics: {
      reportSuites: [
        "MyFirstOverrideReportSuite",
        "MySecondOverrideReportSuite",
        "MyThirdOverrideReportSuite"
        ]
    },
    com_adobe_identity: {
      idSyncContainerId: "1234567"
    },
    com_adobe_target: {
      propertyToken: "63a46bbc-26cb-7cc3-def0-9ae1b51b6c62"
    }
  }
});
```

| 參數 | 說明 |
|---|---|
| `edgeConfigOverrides.datastreamId` | 使用此參數讓單一要求可前往和 `configure` 命令所定義的資料流不同的資料流。 |

### 透過Web SDK傳送設定覆寫 `configure` 命令 {#send-configure}

下面的範例會顯示在 `configure` 命令時設定覆寫可能的情況。

```js {line-numbers="true" highlight="8-30"}
alloy("configure", {
  defaultConsent: "in",
  edgeDomain: "etc",
  edgeBasePath: "ee",
  datastreamId: "{DATASTREAM_ID}",
  orgId: "org",
  debugEnabled: true,
  edgeConfigOverrides: {
    "com_adobe_experience_platform": {
      "datasets": {
        "event": {
          datasetId: "SampleProfileDatasetIdOverride"
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
  onBeforeEventSend: function() { /* … */ });
};
```

## 透過Mobile SDK將覆寫傳送至Edge Network {#send-overrides-mobile-sdk}

晚於 [設定資料流覆寫](#configure-overrides) 在資料收集UI中，您現在可以透過Mobile SDK將覆寫傳送至Edge Network。

若要瞭解如何將覆寫傳送至Edge Network，請參閱 [使用sendEvent傳送覆寫的相關指南](https://developer.adobe.com/client-sdks/edge/edge-network/tutorials/send-overrides-sendevent/) 或 [使用規則傳送覆寫的指南](https://developer.adobe.com/client-sdks/edge/edge-network/tutorials/send-overrides-rules/).

## 裝載範例 {#payload-example}

上述範例會產生 [!DNL Edge Network] 有效負載類似於以下有效負載。

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
