---
title: 設定資料流覆寫
description: 了解如何在資料流 UI 中設定資料流覆寫並透過 Web SDK 啟動它們。
exl-id: 7829f411-acdc-49a1-a8fe-69834bcdb014
source-git-commit: 32f36d96e3aa6beb72121adcc74f2da0bd2c9473
workflow-type: tm+mt
source-wordcount: '997'
ht-degree: 97%

---

# 設定資料流覆寫

資料流覆寫可讓您定義資料流的額外設定，這些設定會透過 Web SDK 傳遞到 Edge Network。

這可協助您觸發和預設行為不同的資料流行為，且無須建立新的資料流或修改現有設定。

資料流設定覆寫的流程包含兩個步驟：

1. 首先，您必須在[資料流設定頁面](configure.md)中定義您的資料流設定覆寫。
2. 接著，您必須透過 Web SDK 命令或使用 Web SDK [標記擴充功能](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)將覆寫傳送至 Edge Network。

本文會介紹每種受支援的覆寫類型的端對端資料流設定覆寫流程。

>[!IMPORTANT]
>
>僅支援資料流覆寫 [Web SDK](../edge/home.md) 整合。 [行動SDK](https://developer.adobe.com/client-sdks/documentation/) 和 [伺服器API](../server-api/overview.md) 整合目前不支援資料流覆寫。

## 在資料流 UI 中設定資料流覆寫 {#configure-overrides}

資料流設定覆寫可讓您修改下列資料流設定：

* Experience Platform 事件資料集
* Adobe Target 屬性權杖
* Audience Manager ID 同步容器
* Adobe Analytics 報告套裝

### Adobe Target 的資料流覆寫 {#target-overrides}

若要設定 Adob&#x200B;&#x200B;e Target 資料流的資料流覆寫，您首先必須建立 Adob&#x200B;&#x200B;e Target 資料流。請依照說明[設定資料流](configure.md)和 [Adobe Target](configure.md#target) 服務。

建立資料流後，請編輯已新增的 [Adobe Target](configure.md#target) 服務，並在&#x200B;**[!UICONTROL 屬性權杖覆寫]**&#x200B;區段中新增所需的資料流覆寫，如下圖所示。每行新增一個屬性權杖。

![顯示 Adob&#x200B;&#x200B;e Target 服務設定的資料流 UI 螢幕擷圖，並醒目顯示屬性權杖覆寫。](assets/overrides/override-target.png)

新增所需的覆寫後，請儲存資料流設定。

您現在應該設定了 Adob&#x200B;&#x200B;e Target 資料流覆寫。現在您可以[透過 Web SDK 將覆寫傳送到 Edge Network](#send-overrides)。

### 適用於 Adobe Analytics 的資料流覆寫 {#analytics-overrides}

若要設定 Adob&#x200B;&#x200B;e Analytics 資料流的資料流覆寫，您首先必須建立 [Adobe Analytics](configure.md#analytics)。請依照說明[設定資料流](configure.md)和 [Adobe Analytics](configure.md#analytics) 服務。

建立資料流後，請編輯已新增的 [Adobe Target](configure.md#target) 服務，並在&#x200B;**[!UICONTROL 報告套裝覆寫]**&#x200B;區段中新增所需的資料流覆寫，如下圖所示。

若要啟用報告套裝覆寫的批次編輯，請選取&#x200B;**[!UICONTROL 顯示批次模式]**。您可以複製並貼上報告套裝覆寫的清單，每行輸入一個報告套裝。

![顯示 Adob&#x200B;&#x200B;e Analytics 服務設定的資料流 UI 螢幕擷圖，並醒目顯示報告套裝覆寫。](assets/overrides/override-analytics.png)

新增所需的覆寫後，請儲存資料流設定。

您現在應該設定了 Adob&#x200B;&#x200B;e Analytics 資料流覆寫。現在您可以[透過 Web SDK 將覆寫傳送到 Edge Network](#send-overrides)。

### 適用於 Experience Platform 事件資料集的資料流覆寫 {#event-dataset-overrides}

若要設定 Experience Platform 事件資料集的資料流覆寫，您首先必須建立 [Adobe Experience Platform](configure.md#aep)。請依照說明[設定資料流](configure.md)和 [Adobe Experience Platform](configure.md#aep) 服務。

建立資料流後，請編輯已新增的 [Adobe Experience Platform](configure.md#aep) 服務，並選取&#x200B;**[!UICONTROL 新增事件資料集]**&#x200B;選項，以新增一或多個覆寫事件資料集，如下圖所示。

![顯示 Adobe Experience Platform 服務設定的資料流 UI 螢幕擷圖，並醒目顯示事件資料集覆寫。](assets/overrides/override-aep.png)

新增所需的覆寫後，請儲存資料流設定。

您現在應該設定了 Adobe Experience Platform 資料流覆寫。現在您可以[透過 Web SDK 將覆寫傳送到 Edge Network](#send-overrides)。

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

## 透過 Web SDK 將覆寫傳送至 Edge Network {#send-overrides}

>[!NOTE]
>
>如果不透過 Web SDK 命令傳送設定覆寫，也可選擇將設定覆寫新增到 Web SDK [標記擴充功能](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)。

在資料集合 UI 中[設定資料流覆寫](#configure-overrides)後，現在即可透過 Web SDK 將覆寫傳送到 Edge Network。

透過 Web SDK 將覆寫傳送到 Edge Network 是啟動資料流設定覆寫的第二個步驟也是最後步驟。

透過 `edgeConfigOverrides`Web SDK 命令傳送資料流設定覆寫到 Edge Network。此命令會建立資料流覆寫並在下一個命令時傳遞給 [!DNL Edge Network]，或者，如果是 `configure` 命令，則適用於每個要求。

`edgeConfigOverrides` 命令會建立資料流覆寫並在下一個命令時傳遞給 [!DNL Edge Network]，或者，如果是 `configure`，則適用於每個要求。

設定覆寫和 `configure` 命令一起傳送時，會隨附在下列 Web SDK 命令中。

* [sendEvent](../edge/fundamentals/tracking-events.md)
* [setConsent](../edge/consent/iab-tcf/overview.md)
* [getIdentity](../edge/identity/overview.md)
* [appendIdentityToUrl](../edge/identity/id-sharing.md#cross-domain-sharing)
* [configure](../edge/fundamentals/configuring-the-sdk.md)

個別命令的設定選項可能會覆寫全域指定的選項。

### 透過 `sendEvent` 命令傳送設定覆寫 {#send-event}

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
          datasetId: "MyOverrideDataset"
        },
        profile: {
          datasetId: "www"
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

### 透過 `configure` 命令傳送設定覆寫 {#send-configure}

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
          datasetId: "MyOverrideDataset"
        },
        "profile": { 
          datasetId: "www"
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

### 裝載範例 {#payload-example}

上述範例產生的 [!DNL Edge Network] 裝載看起來如下所示：

```json
{
  "meta": {
    "configOverrides": {
      "com_adobe_experience_platform": {
        "datasets": {
          "event": {
            "datasetId": "MyOverrideDataset"
          },
          "profile": {
            "datasetId": "www"
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
  "events": [  ],
  "query": {
    "identity": {
      "fetch": [
        "ECID"
      ]
    }
  }
}
```
