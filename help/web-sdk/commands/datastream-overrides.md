---
title: 資料流設定覆寫
description: 瞭解如何透過Web SDK設定資料流覆寫。
source-git-commit: 9cb46957a1c9755dcad6279aae5f5cc04eb6b305
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 14%

---


# 設定資料流覆寫

此 `edgeConfigOverrides` 物件可讓您覆寫目前頁面上執行之命令的組態設定。 此覆寫物件不是命令，而是您可以包含在大多數Web SDK命令中的物件。

如果您在不同國家/地區擁有不同的網站或子網域，或您擁有多個Experience Platform沙箱來儲存不同業務單位的特定資料時，此物件相當實用。

>[!IMPORTANT]
>
>如需資料流覆寫的詳細端對端設定指示，請參閱 [資料流設定覆寫](../../datastreams/overrides.md#configure-overrides) 檔案。

資料流設定覆寫分為兩個步驟：

1. 首先，您必須在以下位置定義資料流設定覆蓋： [資料流設定頁面](../../datastreams/configure.md)，位於資料串流UI中。 請參閱 [資料流設定覆寫](../../datastreams/overrides.md#configure-overrides) 有關如何設定覆寫的說明檔案。
2. 在UI中設定資料流覆寫後，您必須透過下列其中一種方式將覆寫傳送至Edge Network：
   * 透過Web SDK [標籤延伸模組](#tag-extension).
   * 透過 `sendEvent` 或 `configure` Web SDK命令。
   * 透過行動SDK `sendEvent` 命令。

如果您同時在Web SDK設定和特定命令(例如 [`sendEvent`](sendevent/overview.md))，則特定命令中的覆寫優先。

## 物件屬性

此物件中有以下屬性：

* **資料流覆寫**：傳送呼叫至不同的資料流。 如果您設定此值，則其他需要資料流設定的覆寫必須在此處設定的資料流中設定。
* **協力廠商ID同步容器**：Adobe Audience Manager中目的地協力廠商ID同步容器的ID。 使用此欄位之前，必須先在資料流的設定中設定協力廠商ID容器覆寫。
* **目標屬性Token**：Adobe Target中目的地屬性的Token。 使用此欄位之前，必須先在資料流的設定中設定Target屬性Token覆寫。
* **報表套裝**：要在Adobe Analytics中覆寫的報告套裝ID。 使用此欄位之前，必須先在資料流的設定中設定報表套裝覆寫。

## 透過Web SDK標籤擴充功能將資料流覆寫傳送至Edge Network {#tag-extension}

請參閱以下檔案： [設定資料流覆寫](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#datastrea-overrides) 從Web SDK標籤擴充功能取得詳細的設定指示。

如果您想要從Web SDK標籤擴充功能設定資料流覆寫，請在 **[!UICONTROL 資料流設定覆寫]** 當 [設定標籤擴充功能](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. 登入 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID憑證。
1. 瀏覽至 **[!UICONTROL 資料彙集]** > **[!UICONTROL 標籤]**.
1. 選取所需的標籤屬性。
1. 瀏覽至 **[!UICONTROL 擴充功能]**，然後按一下 **[!UICONTROL 設定]** 於 [!UICONTROL Adobe Experience Platform Web SDK] 卡片。
1. 向下捲動至 **[!UICONTROL 資料流設定覆寫]** 區段。 設定每個所需的覆寫值。
1. 按一下 **[!UICONTROL 儲存]**，然後發佈您的變更。

如果您只想為特定命令設定覆寫，請在標籤規則的動作中設定每個所需欄位。

1. 登入 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID憑證。
1. 瀏覽至 **[!UICONTROL 資料彙集]** > **[!UICONTROL 標籤]**.
1. 選取所需的標籤屬性。
1. 瀏覽至 **[!UICONTROL 規則]**，然後選取所需的規則。
1. 在 [!UICONTROL 動作]，選取現有動作或建立動作。
1. 設定 [!UICONTROL 副檔名] 下拉式欄位至 **[!UICONTROL Adobe Experience Platform Web SDK]**，並設定 [!UICONTROL 動作型別] 至 **[!UICONTROL 傳送事件]**.
1. 向下捲動至標示為的區段 **[!UICONTROL 資料流設定覆寫]**.
1. 將此區段中的每個欄位設定為所需的覆寫值。
1. 按一下 **[!UICONTROL 保留變更]**，然後執行您的發佈工作流程。

為以下專案提供單獨的欄位： [!UICONTROL 開發]， [!UICONTROL 分段]、和 [!UICONTROL 生產] 環境。 請務必填寫每個環境的每個所需欄位。

## 透過Web SDK JavaScript程式庫將覆寫傳送至Edge Network {#library}

晚於 [設定資料流覆寫](../../datastreams/overrides.md) 在資料收集UI中，您現在可以透過Web SDK JavaScript程式庫將覆寫傳送至Edge Network。

如果您使用Web SDK，請透過將覆寫傳送至Edge Network `edgeConfigOverrides` command是啟動資料流設定覆寫的第二個也是最後一個步驟。

透過 `edgeConfigOverrides`Web SDK 命令傳送資料流設定覆寫到 Edge Network。這個命令會建立傳遞至的資料流覆寫 [!DNL Edge Network] 在下一個指令上。 如果您使用 `configure` 命令，則會針對每個請求傳遞覆寫。

此 `edgeConfigOverrides` 命令會建立資料流覆寫，這些覆寫會傳遞至 [!DNL Edge Network] 在下一個指令上。

設定覆寫和 `configure` 命令一起傳送時，會隨附在下列 Web SDK 命令中。

* [sendEvent](../commands/sendevent/overview.md)
* [setConsent](../commands/setconsent.md)
* [getIdentity](../commands/getidentity.md)
* [appendIdentityToUrl](../commands/appendidentitytourl.md)
* [configure](../commands/configure/overview.md)

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
| `com_adobe_analytics.reportSuites[]` | 字串陣列，決定要將分析資料傳送至哪些報表套裝。 |
| `com_adobe_identity.idSyncContainerId` | 您要用於Audience Manager的第三方ID同步容器。 |
| `com_adobe_target.propertyToken` | Adobe Target目的地屬性的Token。 |

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

| 參數 | 說明 |
|---|---|
| `edgeConfigOverrides.datastreamId` | 使用此參數讓單一要求可前往和 `configure` 命令所定義的資料流不同的資料流。 |
| `com_adobe_analytics.reportSuites[]` | 字串陣列，決定要將分析資料傳送至哪些報表套裝。 |
| `com_adobe_identity.idSyncContainerId` | 您要用於Audience Manager的第三方ID同步容器。 |
| `com_adobe_target.propertyToken` | Adobe Target目的地屬性的Token。 |