---
title: 配置資料流覆蓋
description: 瞭解如何在資料流UI中配置資料流覆蓋，並通過Web SDK激活這些覆蓋。
exl-id: 7829f411-acdc-49a1-a8fe-69834bcdb014
source-git-commit: d76d596818db67c99aca0606b6b6fb1a9aa977aa
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 0%

---

# 配置資料流覆蓋

資料流覆蓋允許您為資料流定義其他配置，這些配置通過Web SDK傳遞到邊緣網路。

這有助於您觸發與預設資料流行為不同的資料流行為，而無需建立新資料流或修改現有設定。

資料流配置覆蓋是兩個步驟：

1. 首先，必須在 [資料流配置頁](configure.md)。
2. 然後，您必須通過Web SDK命令或使用Web SDK將替代發送到邊緣網路 [標籤擴展](../extension/web-sdk-extension-configuration.md)。

本文將介紹每種支援的覆蓋類型的端到端資料流配置覆蓋過程。

## 在資料流UI中配置資料流覆蓋 {#configure-overrides}

資料流配置覆蓋允許您修改以下資料流配置：

* Experience Platform事件資料集
* Adobe Target地產令牌
* Audience ManagerID同步容器
* Adobe Analytics報告套房

### 資料流覆蓋Adobe Target {#target-overrides}

要為Adobe Target資料流配置資料流覆蓋，必須先建立Adobe Target資料流。 按照說明 [配置資料流](configure.md) 和 [Adobe Target](configure.md#target) 服務。

建立資料流後，編輯 [Adobe Target](configure.md#target) 添加的服務並使用 **[!UICONTROL 屬性令牌覆蓋]** 的子菜單。 每行添加一個屬性令牌。

![顯示Adobe Target服務設定的資料流UI螢幕快照，並突出顯示屬性令牌覆蓋。](../assets/datastreams/overrides/override-target.png)

添加所需的替代後，請保存資料流設定。

您現在應配置Adobe Target資料流覆蓋。 現在你可以 [通過Web SDK將覆蓋發送到邊緣網路](#send-overrides)。

### 資料流覆蓋Adobe Analytics {#analytics-overrides}

要配置Adobe Analytics資料流的資料流覆蓋，必須首先 [Adobe Analytics](configure.md#analytics) 已建立資料流。 按照說明 [配置資料流](configure.md) 和 [Adobe Analytics](configure.md#analytics) 服務。

建立資料流後，編輯 [Adobe Analytics](configure.md#target) 添加的服務並使用 **[!UICONTROL 報表套件覆蓋]** 的子菜單。

選擇 **[!UICONTROL 顯示批模式]** 啟用報表套件替代的批處理編輯。 您可以複製和貼上報表套件覆蓋的清單，每行輸入一個報表套件。

![顯示Adobe Analytics服務設定的資料流UI螢幕抓圖，並突出顯示了報告套件覆蓋。](../assets/datastreams/overrides/override-analytics.png)

添加所需的替代後，請保存資料流設定。

您現在應配置Adobe Analytics資料流覆蓋。 現在你可以 [通過Web SDK將覆蓋發送到邊緣網路](#send-overrides)。

### 用於Experience Platform事件資料集的資料流覆蓋 {#event-dataset-overrides}

要為Experience Platform事件資料集配置資料流覆蓋，必須首先 [Adobe Experience Platform](configure.md#aep) 已建立資料流。 按照說明 [配置資料流](configure.md) 和 [Adobe Experience Platform](configure.md#aep) 服務。

建立資料流後，編輯 [Adobe Experience Platform](configure.md#aep) 添加的服務，並選擇 **[!UICONTROL 添加事件資料集]** 選項添加一個或多個覆蓋事件資料集，如下圖所示。

![顯示Adobe Experience Platform服務設定的資料流UI螢幕快照，並突出顯示事件資料集覆蓋。](../assets/datastreams/overrides/override-aep.png)

添加所需的替代後，請保存資料流設定。

您現在應配置Adobe Experience Platform資料流覆蓋。 現在你可以 [通過Web SDK將覆蓋發送到邊緣網路](#send-overrides)。

### 第三方ID同步容器的資料流覆蓋 {#container-overrides}

要為第三方ID同步容器配置資料流覆蓋，必須首先建立資料流。 按照說明 [配置資料流](configure.md) 建立一個。

建立資料流後，轉到 **[!UICONTROL 高級選項]** 並啟用 **[!UICONTROL 第三方ID同步]** 的雙曲餘切值。

然後，使用 **[!UICONTROL 容器ID覆蓋]** 部分，以添加要覆蓋預設設定的容器ID，如下圖所示。

>[!IMPORTANT]
>
>容器ID必須是數值，如 `1234567`，而不是字串，如 `"1234567"`。 如果通過Web SDK以容器ID覆蓋的形式發送字串值，則會收到錯誤。

![顯示資料流設定的資料流UI螢幕快照，並突出顯示第三方ID同步容器覆蓋。](../assets/datastreams/overrides/override-container.png)

添加所需的替代後，請保存資料流設定。

現在應配置ID同步容器覆蓋。 現在你可以 [通過Web SDK將覆蓋發送到邊緣網路](#send-overrides)。

## 通過Web SDK將覆蓋發送到邊緣網路 {#send-overrides}

>[!NOTE]
>
>作為通過Web SDK命令發送配置替代的替代方法，您可以將配置替代添加到Web SDK [標籤擴展](../extension/web-sdk-extension-configuration.md)。

之後 [配置資料流覆蓋](#configure-overrides) 在「資料收集UI」中，您現在可以通過Web SDK將覆蓋發送到邊緣網路。

通過Web SDK將覆蓋發送到邊緣網路是激活資料流配置覆蓋的第二步也是最後一步。

資料流配置覆蓋通過 `edgeConfigOverrides` Web SDK命令。 此命令建立傳遞給 [!DNL Edge Network] 下一個命令，或者 `configure` 命令。

的 `edgeConfigOverrides` 命令建立傳遞到的資料流覆蓋 [!DNL Edge Network] 下一個命令，或者 `configure`，以滿足每個請求。

當與 `configure` 命令，它包含在以下受支援的命令中。

* [sendEvent](../fundamentals/tracking-events.md)
* [setConnence](../consent/iab-tcf/overview.md)
* [getIdentity](../identity/overview.md)
* [appendIdentityToUrl](../identity/id-sharing.md#cross-domain-sharing)
* [配置](../fundamentals/configuring-the-sdk.md)

全局指定的選項可由單個命令上的配置選項覆蓋。

### 通過 `sendEvent` 命令 {#send-event}

以下示例顯示了配置覆蓋在 `sendEvent` 的子菜單。

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

### 通過 `configure` 命令 {#send-configure}

以下示例顯示了配置覆蓋在 `configure` 的子菜單。

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

### 負載示例 {#payload-example}

以上示例生成 [!DNL Edge Network] 載荷如下：

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
