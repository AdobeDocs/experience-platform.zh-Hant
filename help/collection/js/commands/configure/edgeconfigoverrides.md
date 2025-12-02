---
title: edgeConfigOverrides
description: 為您的實作設定資料流覆寫。
source-git-commit: f4a2778c71ad6a48621212f3ece1776d1b3ac643
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---

# `edgeConfigOverrides` （`configure`命令）

`edgeConfigOverrides`物件可讓您覆寫目前頁面上執行之命令的組態設定。 如果您有不同國家/地區的不同網站或子網域，或您有多個Experience Platform沙箱來儲存不同業務單位的特定資料，此物件相當實用。 如果您只想覆寫頁面上單一命令的組態設定，請考慮在[`edgeConfigOverrides`命令`sendEvent`中使用](../sendevent/edgeconfigoverrides.md)物件。

資料流設定覆寫程式包含兩個主要步驟：

1. 首先，當[在資料流UI中設定資料流](/help/datastreams/configure.md)時，您必須定義資料流設定覆寫。 請參閱資料串流檔案中的[資料串流設定覆寫](/help/datastreams/overrides.md)，以取得如何設定覆寫的指示。
1. 在資料串流UI中設定資料串流覆寫後，您就可以設定`edgeConfigOverrides`物件。

當您在`edgeConfigOverrides`命令中設定`configure`物件時，它會套用至傳送到Adobe的所有資料。 下列命令&#x200B;_也_&#x200B;支援`edgeConfigOverrides`物件：

* [&#39;sendEvent&#39;](../sendevent/edgeconfigoverrides.md)
* [&#39;setConsent&#39;](../setconsent.md)
* [&#39;getIdentity&#39;](../getidentity.md)
* [&#39;appendIdentityToUrl&#39;](../appendidentitytourl.md)

若兩者皆已設定，則上述任一命令中的`edgeConfigOverrides`設定優先於`edgeConfigOverrides`命令中的`configure`物件。 如果其中任何命令不包含`edgeConfigOverrides`物件，則會使用`edgeConfigOverrides`命令中的`configure`物件。

## 範例

如果您的資料流設定已啟用所有支援的服務，則以下範例會覆寫此設定並停用所有服務。

```js
alloy("configure", {
  orgId: "97D1F3F459CE0AD80A495CBE@AdobeOrg",
  datastreamId: "db9c70a1-6f11-4563-b0e9-b5964ab3a858",
  edgeConfigOverrides: {
    com_adobe_experience_platform: {
      enabled: false,
      datasets: {
        event: {
          datasetId: "64b6f930753dd41ca8d4fd77"
        }
      },
      com_adobe_edge_ode: {
        enabled: false
      },
      com_adobe_edge_segmentation: {
        enabled: false
      },
      com_adobe_edge_destinations: {
        enabled: false
      },
      com_adobe_edge_ajo: {
        enabled: false
      },
    },
    com_adobe_analytics: {
      enabled: false,
      reportSuites: ["exampleoverridersid","exampleoverridersid2"]
    },
    com_adobe_identity: {
      idSyncContainerId: 34373
    },
    com_adobe_target: {
      enabled: false,
      propertyToken: "01dbc634-07c1-d8f9-ca69-b489a5ac5e94"
    },
    com_adobe_audience_manager: {
      enabled: false
    },
    com_adobe_launch_ssf: {
      enabled: false
    }
  }
});
```

| 參數 | 類型 | 說明 |
| --- | --- | --- |
| **`orgId`** | `string` | 您公司的IMS組織ID。 |
| **`datastreamId`** | `string` | 要傳送資料的目的地資料串流ID。 |
| **`com_adobe_experience_platform`** | `object` | 定義Adobe Experience Platform服務的動態資料流設定。 |
| **`com_adobe_experience_platform.enabled`** | `boolean` | 決定是否將事件傳送至Adobe Experience Platform。 |
| **`com_adobe_experience_platform.datasets`** | `object` | 定義用於事件的資料集。 |
| **`com_adobe_experience_platform.com_adobe_edge_ode.enabled`** | `boolean` | 決定是否將事件傳送至Offer Decisioning。 |
| **`com_adobe_experience_platform.com_adobe_edge_segmentation.enabled`** | `boolean` | 決定是否將事件傳送至「Edge分段」。 |
| **`com_adobe_experience_platform.com_adobe_edge_destinations.enabled`** | `boolean` | 決定是否將事件傳送至Edge目的地。 |
| **`com_adobe_experience_platform.com_adobe_edge_ajo.enabled`** | `boolean` | 決定是否在Adobe Journey Optimizer傳送事件。 |
| **`com_adobe_analytics.enabled`** | `boolean` | 決定是否將事件傳送至Adobe Analytics。 |
| **`com_adobe_analytics.reportSuites[]`** | `string[]` | 字串陣列，決定要將Analytics資料傳送至哪些報表套裝。 |
| **`com_adobe_audience_manager.enabled`** | `boolean` | 決定是否將事件傳送至Adobe Audience Manager。 |
| **`com_adobe_identity.idSyncContainerId`** | `integer` | 您要在Audience Manager中使用的第三方ID同步容器。 需要`com_adobe_audience_manager.enabled`設定為`true`。 否則，會停用Audience Manager服務。 |
| **`com_adobe_target.enabled`** | `boolean` | 決定是否將事件傳送至Adobe Target。 |
| **`com_adobe_target.propertyToken`** | `string` | Adobe Target目的地屬性的Token。 |
| **`com_adobe_launch_ssf`** | `boolean` | 決定是否將事件傳送至伺服器端轉送。 |

## 使用網頁SDK標籤擴充功能設定覆寫

設定標籤延伸時，此欄位的Web SDK標籤延伸對應項位於[設定覆寫](/help/tags/extensions/client/web-sdk/configure/configuration-overrides.md)之下。
