---
title: 設定資料流覆蓋
description: 了解如何在資料流UI中設定資料流覆寫，並透過Web SDK啟用。
source-git-commit: ce2e80a7ea7385be98bbcda6a0704cd0814c62b2
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 0%

---


# 設定資料流覆蓋

資料流覆寫可讓您定義資料流的其他設定，這些設定會透過Web SDK傳遞至邊緣網路。

這可協助您觸發與預設資料流不同的資料流行為，而不需建立新資料流或修改現有設定。

資料流配置覆蓋是兩個步驟：

1. 首先，您必須在 [datastream配置頁](configure.md).
2. 然後，您必須透過Web SDK命令或使用Web SDK將覆寫傳送至邊緣網路 [標籤擴充功能](../extension/web-sdk-extension-configuration.md).

本文說明每種支援覆蓋類型的端到端資料流配置覆蓋過程。

## 在資料流UI中設定資料流覆蓋 {#configure-overrides}

資料流配置覆蓋允許您修改以下資料流配置：

* Experience Platform事件資料集
* Adobe Target屬性Token
* Audience ManagerID同步容器
* Adobe Analytics報表套裝

### Adobe Target的資料流覆蓋 {#target-overrides}

若要為Adobe Target資料流設定資料流覆寫，您必須先建立Adobe Target資料流。 請依照 [設定資料流](configure.md) 和 [Adobe Target](configure.md#target) 服務。

建立資料流後，請編輯 [Adobe Target](configure.md#target) 您已新增的服務，並使用 **[!UICONTROL 屬性代號覆蓋]** 區段來新增所需的資料流覆寫，如下圖所示。 每行新增一個屬性代號。

![Datastreams UI螢幕擷取畫面顯示Adobe Target服務設定，並反白顯示屬性代號覆寫。](../assets/datastreams/overrides/override-target.png)

新增所需的覆寫後，請儲存資料流設定。

您現在應已設定Adobe Target資料流覆寫。 現在您可以 [透過Web SDK將覆寫傳送至邊緣網路](#send-overrides).

### Adobe Analytics的資料流覆蓋 {#analytics-overrides}

若要設定Adobe Analytics資料流的資料流覆寫，您必須先 [Adobe Analytics](configure.md#analytics) 資料流已建立。 請依照 [設定資料流](configure.md) 和 [Adobe Analytics](configure.md#analytics) 服務。

建立資料流後，請編輯 [Adobe Analytics](configure.md#target) 您已新增的服務，並使用 **[!UICONTROL 報表套裝覆寫]** 區段來新增所需的資料流覆寫，如下圖所示。

選擇 **[!UICONTROL 顯示批模式]** 啟用報表套裝覆寫的批次編輯。 您可以複製並貼上報表套裝覆寫清單，每行輸入一個報表套裝。

![Datastreams UI螢幕擷取畫面顯示Adobe Analytics服務設定，並反白顯示報表套裝覆寫。](../assets/datastreams/overrides/override-analytics.png)

新增所需的覆寫後，請儲存資料流設定。

您現在應已設定Adobe Analytics資料流覆寫。 現在您可以 [透過Web SDK將覆寫傳送至邊緣網路](#send-overrides).

### Experience Platform事件資料集的資料流覆寫 {#event-dataset-overrides}

若要為Experience Platform事件資料集設定資料流覆寫，您必須先 [Adobe Experience Platform](configure.md#aep) 資料流已建立。 請依照 [設定資料流](configure.md) 和 [Adobe Experience Platform](configure.md#aep) 服務。

建立資料流後，請編輯 [Adobe Experience Platform](configure.md#aep) 已添加的服務，並選擇 **[!UICONTROL 新增事件資料集]** 新增一或多個覆寫事件資料集的選項，如下圖所示。

![Datastreams UI螢幕擷取畫面，顯示Adobe Experience Platform服務設定，並反白顯示事件資料集覆寫。](../assets/datastreams/overrides/override-aep.png)

新增所需的覆寫後，請儲存資料流設定。

您現在應已設定Adobe Experience Platform資料流覆寫。 現在您可以 [透過Web SDK將覆寫傳送至邊緣網路](#send-overrides).

### 第三方ID同步容器的資料流覆蓋 {#container-overrides}

若要為第三方ID同步容器設定資料流覆寫，您必須先建立資料流。 請依照 [設定資料流](configure.md) 來建立。

建立資料流後，請前往 **[!UICONTROL 進階選項]** 並啟用 **[!UICONTROL 第三方ID同步]** 選項。

然後，使用 **[!UICONTROL 容器ID覆寫]** 區段來新增您要覆寫預設設定的容器ID，如下圖所示。

>[!IMPORTANT]
>
>容器ID必須是數值，例如 `1234567`，而非字串，例如 `"1234567"`. 如果您透過Web SDK以容器ID覆寫的形式傳送字串值，便會收到錯誤。

![資料流UI螢幕擷圖，顯示資料流設定，並反白顯示第三方ID同步容器覆蓋。](../assets/datastreams/overrides/override-container.png)

新增所需的覆寫後，請儲存資料流設定。

您現在應已設定ID同步容器覆寫。 現在您可以 [透過Web SDK將覆寫傳送至邊緣網路](#send-overrides).

## 透過Web SDK將覆寫傳送至邊緣網路 {#send-overrides}

>[!NOTE]
>
>除了透過Web SDK命令傳送設定覆寫外，您也可以將設定覆寫新增至Web SDK [標籤擴充功能](../extension/web-sdk-extension-configuration.md).

之後 [設定資料流覆蓋](#configure-overrides) 在資料收集UI中，您現在可以透過Web SDK將覆寫傳送至邊緣網路。

透過Web SDK將覆寫傳送至邊緣網路，是啟動資料流設定覆寫的第二步，也是最後一步。

資料流配置覆蓋通過 `edgeConfigOverrides` Web SDK命令。 此命令會建立傳遞至 [!DNL Edge Network] 在下一個命令上，或 `configure` 命令，用於每個請求。

此 `edgeConfigOverrides` 命令建立傳遞到的資料流覆蓋 [!DNL Edge Network] 在下一個命令上，或者 `configure`，針對每個要求。

當設定覆寫連同 `configure` 命令，則它將包含在以下支援的命令中。

* [sendEvent](../fundamentals/tracking-events.md)
* [setConsent](../consent/iab-tcf/overview.md)
* [getIdentity](../identity/overview.md)
* [appendIdentityToUrl](../identity/id-sharing.md#cross-domain-sharing)
* [設定](../fundamentals/configuring-the-sdk.md)

可以通過各個命令上的配置選項覆蓋全局指定的選項。

### 透過 `sendEvent` 命令 {#send-event}

下列範例顯示設定覆寫在 `sendEvent` 命令。

```js {line-numbers="true" highlight="5-25"}
alloy("sendEvent", {
  xdm: {
    /* ... */
  },
  edgeConfigOverrides: {
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

### 透過 `configure` 命令 {#send-configure}

下列範例顯示設定覆寫在 `configure` 命令。

```js {line-numbers="true" highlight="8-30"}
alloy("configure", {
  defaultConsent: "in",
  edgeDomain: "etc",
  edgeBasePath: "ee",
  edgeConfigId: "etc",
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

上述範例會產生 [!DNL Edge Network] 裝載如下所示：

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

