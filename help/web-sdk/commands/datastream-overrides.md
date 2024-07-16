---
title: 資料流設定覆寫
description: 瞭解如何透過Web SDK設定資料流覆寫。
exl-id: 8e327892-9520-43f5-abf4-d65a5ca34e6d
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 14%

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
   * 透過`sendEvent`或`configure` Web SDK命令。
   * 透過Mobile SDK `sendEvent`命令。

如果您同時在Web SDK設定和特定命令（例如[`sendEvent`](sendevent/overview.md)）中設定覆寫，則特定命令中的覆寫優先。

## 物件屬性

此物件中有以下屬性：

* **資料流覆寫**：將呼叫傳送至不同的資料流。 如果您設定此值，則其他需要資料流設定的覆寫必須在此處設定的資料流中設定。
* **協力廠商ID同步容器**： Adobe Audience Manager中目的地協力廠商ID同步容器的識別碼。 使用此欄位之前，必須先在資料流的設定中設定協力廠商ID容器覆寫。
* **Target屬性Token**： Adobe Target中目的地屬性的語彙基元。 使用此欄位之前，必須先在資料流的設定中設定Target屬性Token覆寫。
* **報表套裝**：要在Adobe Analytics中覆寫報表套裝ID。 使用此欄位之前，必須先在資料流的設定中設定報表套裝覆寫。

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

### 透過Web SDK `configure`命令傳送設定覆寫 {#send-configure}

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
