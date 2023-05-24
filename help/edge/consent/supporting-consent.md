---
title: 使用Adobe Experience PlatformWeb SDK支援客戶同意首選項
description: 瞭解如何支援使用Adobe Experience PlatformWeb SDK的同意首選項。
keywords: 同意；預設同意；預設同意；setConnence；配置檔案隱私欄位組；體驗事件隱私欄位組；隱私欄位組；
exl-id: 647e4a84-4a66-45d6-8b05-d78786bca63a
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 0%

---

# 支援客戶同意首選項

為了尊重用戶的隱私，您可能希望在允許SDK出於某些目的使用用戶特定的資料之前徵求用戶的同意。 目前，SDK僅允許用戶選擇加入或退出所有目的，但在未來Adobe中希望能夠對特定目的提供更精細的控制。

如果用戶選擇所有目的，則允許SDK執行以下任務：

* 向和從Adobe的伺服器發送資料。
* 讀取和寫入Cookie或Web儲存項。

如果用戶出於所有目的而選擇，則SDK不執行任何這些任務。

## 配置同意

預設情況下，用戶將被選擇用於所有目的。 要防止SDK執行上述任務，直到用戶開啟，請通過 `"defaultConsent": "pending"` 在SDK配置過程中，如下所示：

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "imsOrgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "defaultConsent": "pending"
});
```

當一般用途的預設同意設定為掛起時，嘗試執行任何依賴於用戶選擇加入首選項的命令(例如， `sendEvent` 命令)導致命令在SDK中排隊。 在將用戶的選擇加入首選項傳遞到SDK之前，不會處理這些命令。

>[!NOTE]
>
>命令僅在記憶體中排隊。 不會在頁載入中保存它們。

如果您不想收集在設定用戶的選擇加入首選項之前發生的事件，則可以通過 `"defaultConsent": "out"` 在SDK配置過程中。 嘗試執行任何依賴於用戶選擇加入首選項的命令在您將用戶的選擇加入首選項傳送到SDK之前將無效。

>[!NOTE]
>
>目前，SDK僅支援單一的全部或無用途。 儘管我們計畫構建一組更強健的目標或類別，這些目標或類別將與不同的Adobe功能和產品選項相對應，但當前的實施是選擇加入的全部或全部方法。  這隻適用於Adobe Experience Platform [!DNL Web SDK] 和NOT其他AdobeJavaScript庫。

此時，您可能希望用戶選擇在用戶介面中的某個位置。 收集用戶首選項後，將這些首選項通知SDK。

## 通過Adobe Experience Platform標準傳達同意偏好

SDK支援1.0和2.0版的Adobe Experience Platform同意標準。 目前，1.0和2.0標準僅支援自動執行全部或無許可優先。 1.0標準正在逐步取消，以利於2.0標準。 2.0標準允許您添加附加的同意首選項，這些首選項可用於手動強制實施同意首選項。

### 使用Adobe標準版本2.0

如果使用Adobe Experience Platform，則需要將隱私架構欄位組包含到您的配置檔案架構中。 請參閱 [Adobe Experience Platform的治理、隱私和安全](../../landing/governance-privacy-security/overview.md) 的子菜單。您可以在下面的值對象中添加與 `consents` 的 [!UICONTROL 同意和首選項] 配置檔案欄位組。

如果用戶選擇，請執行 `setConsent` 將collect首選項設定為的命令 `y` 如下：

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "2.0",
      value: {
        collect: {
          val: "y"
        },
        metadata: {
          time: "2021-03-17T15:48:42-07:00"
        }
      }
    }]
});
```

時間欄位應指定用戶上次更新其同意首選項的時間。 如果用戶選擇退出，則執行 `setConsent` 將collect首選項設定為的命令 `n` 如下：

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "2.0",
      value: {
        collect: {
          val: "n"
        },
        metadata: {
          time: "2021-03-17T15:51:30-07:00"
        }
      }
    }]
});
```

### 使用Adobe標準版本1.0

如果用戶選擇，請執行 `setConsent` 命令 `general` 選項設定為 `in` 如下：

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "1.0",
      value: {
        general: "in"
      }
    }]
});
```

如果用戶選擇退出，則執行 `setConsent` 命令 `general` 選項設定為 `out` 如下：

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "1.0",
      value: {
        general: "out"
      }
    }]
});
```

## 通過IAB TCF標準傳達同意偏好

SDK支援記錄用戶通過互動式廣告局歐洲(IAB)透明度和同意框架(TCF)標準提供的同意偏好。 可以通過同一協定設定同意字串 `setConsent` 命令如下所示：

```javascript
alloy("setConsent", {
    consent: [{
      standard: "IAB TCF",
      version: "2.0",
      value: "CO1Z4yuO1Z4yuAcABBENArCsAP_AAH_AACiQGCNX_T5eb2vj-3Zdt_tkaYwf55y3o-wzhhaIse8NwIeH7BoGP2MwvBX4JiQCGBAkkiKBAQdtHGhcCQABgIhRiTKMYk2MjzNKJLJAilsbe0NYCD9mnsHT3ZCY70--u__7P3fAwQgkwVLwCRIWwgJJs0ohTABCOICpBwCUEIQEClhoACAnYFAR6gAAAIDAACAAAAEEEBAIABAAAkIgAAAEBAKACIBAACAEaAhAARIEAsAJEgCAAVA0JACKIIQBCDgwCjlACAoAAAAA.YAAAAAAAAAAA",
      gdprApplies: true
    }]
});
```

以此方式設定同意後，將使用同意資訊更新即時客戶配置檔案。 要使此功能正常運行，配置檔案XDM架構需要包含 [配置檔案隱私架構欄位組](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/profile/profile-privacy.schema.md)。 在發送事件時，需要將IAB同意資訊手動添加到事件XDM對象。 SDK不會自動在事件中包含同意資訊。 要在事件中發送同意資訊， [體驗事件隱私欄位組](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/experience-event/experienceevent-privacy.schema.md) 需要添加到「體驗事件」架構。

## 在一個請求中發送多個標準

SDK還支援在請求中發送多個同意對象。

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "2.0",
      value: {
        collect: {
          val: "y"
        },
        metadata: {
          time: "2021-03-17T15:48:42-07:00"
        }
      }
    },{
      standard: "IAB TCF",
      version: "2.0",
      value: "CO1Z4yuO1Z4yuAcABBENArCsAP_AAH_AACiQGCNX_T5eb2vj-3Zdt_tkaYwf55y3o-wzhhaIse8NwIeH7BoGP2MwvBX4JiQCGBAkkiKBAQdtHGhcCQABgIhRiTKMYk2MjzNKJLJAilsbe0NYCD9mnsHT3ZCY70--u__7P3fAwQgkwVLwCRIWwgJJs0ohTABCOICpBwCUEIQEClhoACAnYFAR6gAAAIDAACAAAAEEEBAIABAAAkIgAAAEBAKACIBAACAEaAhAARIEAsAJEgCAAVA0JACKIIQBCDgwCjlACAoAAAAA.YAAAAAAAAAAA",
      gdprApplies: true
    }]
});
```

## 同意偏好的持續存在

將用戶首選項通過 `setConsent` 命令， SDK將用戶的首選項保留為cookie。 下次用戶在瀏覽器中載入您的網站時，SDK將檢索並使用這些永續首選項來確定事件是否可以發送到Adobe。

您需要獨立儲存用戶首選項才能顯示與當前首選項的同意對話框。 無法從SDK檢索用戶首選項。 要確保用戶首選項與SDK保持同步，可以調用 `setConsent` 命令。 只有在首選項發生更改時，SDK才會進行伺服器調用。

## 在設定同意時同步身份

當預設同意被掛起或取消時， `setConsent` 可能是第一個發出並確定身份的請求。 因此，在第一個請求上同步身份可能很重要。 可以將標識映射添加到 `setConsent` 就像 `sendEvent` 的子菜單。 請參閱 [正在檢索Experience CloudID](../identity/overview.md)
