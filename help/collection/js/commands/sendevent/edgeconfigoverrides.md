---
title: edgeConfigOverrides
description: 只為sendEvent命令設定資料流覆寫。
exl-id: 8e327892-9520-43f5-abf4-d65a5ca34e6d
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---

# `edgeConfigOverrides` （`sendEvent`命令）

`edgeConfigOverrides`物件允許您覆寫目前`sendEvent`命令的組態設定。 當您想要以與其他Web SDK實作不同的組態設定執行的相同頁面上有特定命令時，此物件就相當實用。 如果您想要覆寫指定頁面上所有命令的組態設定，請考慮在[`edgeConfigOverrides`命令`configure`中使用](../configure/edgeconfigoverrides.md)物件。

包羅萬象的資料流設定覆寫程式包含兩個主要步驟：

1. 首先，當[在資料流UI中設定資料流](/help/datastreams/configure.md)時，您必須定義資料流設定覆寫。 請參閱資料串流檔案中的[資料串流設定覆寫](/help/datastreams/overrides.md)，以取得如何設定覆寫的指示。
1. 在資料串流UI中設定資料串流覆寫後，您就可以設定`edgeConfigOverrides`物件。

請注意，`configure`命令也支援`edgeConfigOverrides`物件；請參閱[`edgeConfigOverrides`](../configure/edgeconfigoverrides.md)命令底下的`configure`。 如果已設定`edgeConfigOverrides`命令中的`sendEvent`物件，優先於`edgeConfigOverrides`命令中的`configure`物件。

## 範例

如果您的資料流設定已啟用所有支援的服務，則下列範例會覆寫此設定並停用所有服務（請參閱每個服務上的`enabled: false`設定）。 此物件支援與[`edgeConfigOverrides`](../configure/edgeconfigoverrides.md)命令中的`configure`物件相同的屬性。

```js
alloy("sendEvent", {
  renderDecisions: true,
  edgeConfigOverrides: {
    datastreamId: "bfa8fe21-6157-42d3-b47a-78310920b39d",
    com_adobe_experience_platform: {
      enabled: false,
      datasets: {
        event: {
          datasetId: "64b6f949a8a6891ca8a28911",
        },
      },
      com_adobe_edge_ode: {
        enabled: false,
      },
      com_adobe_edge_segmentation: {
        enabled: false,
      },
      com_adobe_edge_destinations: {
        enabled: false,
      },
      com_adobe_edge_ajo: {
        enabled: false,
      },
    },
    com_adobe_analytics: {
      enabled: false,
      reportSuites: ["examplersid3"],
    },
    com_adobe_identity: {
      idSyncContainerId: 34374,
    },
    com_adobe_target: {
      enabled: false,
      propertyToken: "f3fd55e1-a06d-8650-9aa5-c8356c6e2223",
    },
    com_adobe_audience_manager: {
      enabled: false,
    },
    com_adobe_launch_ssf: {
      enabled: false,
    },
  },
});
```

## 使用網頁SDK標籤擴充功能進行資料流設定覆寫

此物件的Web SDK標籤延伸等效專案是在設定&#39;[&#39;動作時](/help/tags/extensions/client/web-sdk/actions/send-event.md#datastream-configuration-overrides)資料流設定覆寫[!UICONTROL Send event]區段。
