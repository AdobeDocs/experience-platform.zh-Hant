---
title: 資料流設定覆寫
description: 瞭解如何透過Web SDK設定資料流覆寫。
exl-id: 8e327892-9520-43f5-abf4-d65a5ca34e6d
source-git-commit: 2b8ca4bc1d5cf896820a5de95dcdfcd15edc2392
workflow-type: tm+mt
source-wordcount: '1159'
ht-degree: 10%

---

# 設定資料流覆寫

`edgeConfigOverrides`物件可讓您覆寫目前頁面上執行之命令的組態設定。 此覆寫物件不是命令，而是您可以包含在大多數Web SDK命令中的物件。

如果您在不同國家/地區擁有不同的網站或子網域，或您擁有多個Experience Platform沙箱來儲存不同業務單位的特定資料時，此物件相當實用。

>[!IMPORTANT]
>
>如需資料流覆寫的詳細端對端設定指示，請參閱[資料流設定覆寫](../../datastreams/overrides.md#configure-overrides)檔案。

資料流設定覆寫分為兩個步驟：

1. 首先，您必須在Datastreams UI的[資料流設定頁面](../../datastreams/configure.md)中定義資料流設定覆寫。 如需如何設定覆寫的說明，請參閱[資料流設定覆寫](../../datastreams/overrides.md#configure-overrides)檔案。
2. 在UI中設定資料流覆寫後，您必須透過下列其中一種方式將覆寫傳送給Edge Network：
   * 透過Web SDK [標籤擴充功能](#tag-extension)。
   * 透過[`sendEvent`](../commands/sendevent/overview.md)或[`configure`](../commands/configure/overview.md) Web SDK命令。
   * 透過Mobile SDK [`sendEvent`](https://developer.adobe.com/client-sdks/home/getting-started/track-events/#send-events-to-edge-network)命令。

如果您同時在Web SDK設定和特定命令（例如[`sendEvent`](sendevent/overview.md)）中設定覆寫，則特定命令中的覆寫優先。

>[!NOTE]
>
>如果您想要設定覆寫以&#x200B;*停用* Experience Cloud服務，您必須確定該服務在資料流設定中是第一個&#x200B;*啟用*。 請參閱有關如何[設定資料串流](../../datastreams/configure.md#add-services)的檔案，以取得有關如何將服務新增至資料串流的詳細資訊。

## 透過Web SDK標籤擴充功能將資料流覆寫傳送至Edge Network {#tag-extension}

如需詳細的設定指示，請參閱有關Web SDK標籤擴充功能中[設定資料流覆寫](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#datastrea-overrides)的檔案。

如果您想從Web SDK標籤延伸設定資料流覆寫，請在[設定標籤延伸時](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)設定&#x200B;**[!UICONTROL 資料流設定覆寫]**&#x200B;下的每個所需欄位。

1. 使用您的Adobe ID憑證登入[experience.adobe.com](https://experience.adobe.com)。
1. 導覽至&#x200B;**[!UICONTROL 資料彙集]** > **[!UICONTROL 標籤]**。
1. 選取所需的標籤屬性。
1. 導覽至&#x200B;**[!UICONTROL 擴充功能]**，然後按一下[!UICONTROL Adobe Experience Platform Web SDK]卡片上的&#x200B;**[!UICONTROL 設定]**。
1. 向下捲動至&#x200B;**[!UICONTROL 資料流設定覆寫]**&#x200B;區段。 設定每個所需的覆寫值。
1. 按一下&#x200B;**[!UICONTROL 儲存]**，然後發佈您的變更。

如果您只想為特定命令設定覆寫，請在標籤規則的動作中設定每個所需欄位。

1. 使用您的Adobe ID憑證登入[experience.adobe.com](https://experience.adobe.com)。
1. 導覽至&#x200B;**[!UICONTROL 資料彙集]** > **[!UICONTROL 標籤]**。
1. 選取所需的標籤屬性。
1. 導覽至&#x200B;**[!UICONTROL 規則]**，然後選取所要的規則。
1. 在[!UICONTROL 動作]下，選取現有動作或建立動作。
1. 將[!UICONTROL 擴充功能]下拉式清單欄位設為&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]**，並將[!UICONTROL 動作型別]設為&#x200B;**[!UICONTROL 傳送事件]**。
1. 向下捲動至標示為&#x200B;**[!UICONTROL 資料流設定覆寫]**&#x200B;的區段。
1. 將此區段中的每個欄位設定為所需的覆寫值。
1. 按一下&#x200B;**[!UICONTROL 保留變更]**，然後執行您的發佈工作流程。

為[!UICONTROL 開發]、[!UICONTROL 暫存]和[!UICONTROL 生產]環境提供了單獨的欄位。 請務必填寫每個環境的每個所需欄位。

## 透過Web SDK JavaScript資料庫將覆寫傳送至Edge Network {#library}

在資料收集UI中[設定資料流覆寫](../../datastreams/overrides.md)後，您現在可以透過Web SDK JavaScript資料庫將覆寫傳送給Edge Network。

如果您使用Web SDK，透過`edgeConfigOverrides`命令傳送覆寫至Edge Network是啟動資料流設定覆寫的第二個也是最後一個步驟。

透過 `edgeConfigOverrides`Web SDK 命令傳送資料流設定覆寫到 Edge Network。這個命令會建立資料流覆寫，這些覆寫會在下一個命令上傳遞到[!DNL Edge Network]。 如果您使用`configure`命令，則會針對每個要求傳遞覆寫。

`edgeConfigOverrides`命令會建立資料串流覆寫，這些覆寫會在下一個命令上傳遞至[!DNL Edge Network]。

設定覆寫和 `configure` 命令一起傳送時，會隨附在下列 Web SDK 命令中。

* [sendEvent](../commands/sendevent/overview.md)
* [setConsent](../commands/setconsent.md)
* [getIdentity](../commands/getidentity.md)
* [appendIdentityToUrl](../commands/appendidentitytourl.md)
* [configure](../commands/configure/overview.md)

個別命令的設定選項可能會覆寫全域指定的選項。

### 透過Web SDK `sendEvent`命令傳送設定覆寫 {#send-event}

以下範例顯示`sendEvent`呼叫支援的所有動態資料流設定選項。

如果您的資料流設定已啟用所有支援的服務，則下列範例將覆寫此設定並停用所有服務（請參閱每個服務上的`enabled: false`設定）。

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
      reportSuites: ["ujslconfigoverrides3"],
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

| 參數 | 說明 |
|---|---|
| `renderDecisions` |  |
| `edgeConfigOverrides.datastreamId` | 使用此參數讓單一要求可前往和 `configure` 命令所定義的資料流不同的資料流。 |
| `edgeConfigOverrides.com_adobe_experience_platform` | 定義Experience Platform服務的動態資料流設定。 |
| `edgeConfigOverrides.com_adobe_experience_platform.enabled` | 定義是否將事件傳送至Experience Platform服務。 |
| `edgeConfigOverrides.com_adobe_experience_platform.datasets` | 定義用於事件的資料集。 |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_ode.enabled` | 定義是否將事件傳送至Offer decisioning服務。 |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_segmentation.enabled` | 定義是否將事件傳送至邊緣劃分服務。 |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_destinations.enabled` | 定義是否將事件資料傳送至邊緣目的地。 |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_ajo.enabled` | 定義是否將事件資料傳送至Adobe Journey Optimizer服務。 |
| `com_adobe_analytics.enabled` | 定義是否將事件資料傳送至Adobe Analytics。 |
| `com_adobe_analytics.reportSuites[]` | 字串陣列，決定您要將Analytics資料傳送至哪些報表套裝。 |
| `com_adobe_identity.idSyncContainerId` | 您要用於Audience Manager的第三方ID同步容器。 若要讓此ID同步容器運作，您必須將`com_adobe_audience_manager.enabled`設定為`true`。 否則，會停用Audience Manager服務。 |
| `com_adobe_target.enabled` | 定義是否將事件資料傳送至Adobe Target。 |
| `com_adobe_target.propertyToken` | Adobe Target目的地屬性的Token。 |
| `com_adobe_audience_manager.enabled` | 定義是否將事件資料傳送至Audience Manager服務。 |
| `com_adobe_launch_ssf` | 定義是否將事件資料傳送至伺服器端轉送。 |

### 透過Web SDK `configure`命令傳送設定覆寫 {#send-configure}

下面的範例會顯示在 `configure` 命令時設定覆寫可能的情況。

如果您的資料流設定已啟用所有支援的服務，則下列範例將覆寫此設定並停用所有服務（請參閱每個服務上的`enabled: false`設定）。

```js
alloy("configure", {
  orgId: "97D1F3F459CE0AD80A495CBE@AdobeOrg",
  datastreamId: "db9c70a1-6f11-4563-b0e9-b5964ab3a858",
  edgeConfigOverrides: {
    com_adobe_experience_platform: {
      enabled: false,
      datasets: {
        event: {
          datasetId: "64b6f930753dd41ca8d4fd77",
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
      reportSuites: ["ujslconfigoverrides2"],
    },
    com_adobe_identity: {
      idSyncContainerId: 34373,
    },
    com_adobe_target: {
      enabled: false,
      propertyToken: "01dbc634-07c1-d8f9-ca69-b489a5ac5e94",
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

| 參數 | 說明 |
|---|---|
| `orgId` | 與您的Adobe帳戶相對應的IMS組織ID。 |
| `edgeConfigOverrides.datastreamId` | 使用此參數讓單一要求可前往和 `configure` 命令所定義的資料流不同的資料流。 |
| `edgeConfigOverrides.com_adobe_experience_platform` | 定義Experience Platform服務的動態資料流設定。 |
| `edgeConfigOverrides.com_adobe_experience_platform.enabled` | 定義是否將事件傳送至Experience Platform服務。 |
| `edgeConfigOverrides.com_adobe_experience_platform.datasets` | 定義用於事件的資料集。 |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_ode.enabled` | 定義是否將事件傳送至Offer decisioning服務。 |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_segmentation.enabled` | 定義是否將事件傳送至邊緣劃分服務。 |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_destinations.enabled` | 定義是否將事件資料傳送至邊緣目的地。 |
| `edgeConfigOverrides.com_adobe_experience_platform.com_adobe_edge_ajo.enabled` | 定義是否將事件資料傳送至Adobe Journey Optimizer服務。 |
| `com_adobe_analytics.enabled` | 定義是否將事件資料傳送至Adobe Analytics。 |
| `com_adobe_analytics.reportSuites[]` | 字串陣列，決定您要將Analytics資料傳送至哪些報表套裝。 |
| `com_adobe_identity.idSyncContainerId` | 您要用於Audience Manager的第三方ID同步容器。 若要讓此ID同步容器運作，您必須將`com_adobe_audience_manager.enabled`設定為`true`。 否則，會停用Audience Manager服務。 |
| `com_adobe_target.enabled` | 定義是否將事件資料傳送至Adobe Target。 |
| `com_adobe_target.propertyToken` | Adobe Target目的地屬性的Token。 |
| `com_adobe_audience_manager.enabled` | 定義是否將事件資料傳送至Audience Manager服務。 |
| `com_adobe_launch_ssf` | 定義是否將事件資料傳送至伺服器端轉送。 |

