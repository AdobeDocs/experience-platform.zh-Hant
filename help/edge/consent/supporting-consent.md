---
title: 使用Adobe Experience PlatformWeb SDK支援客戶同意偏好
description: 瞭解如何使用Adobe Experience Platform網頁SDK支援同意偏好設定。
keywords: connence;defaultConnence;default connonce;setConnence;Profile Privacy Mixin; Experience Event Privacy Mixin; Privacy Mixin;
translation-type: tm+mt
source-git-commit: ff261c507d310b8132912680b6ddd1e7d5675d08
workflow-type: tm+mt
source-wordcount: '964'
ht-degree: 0%

---


# 支援客戶同意偏好

若要尊重使用者的隱私權，您可能會在允許SDK針對特定用途使用使用者特定資料之前，先要求使用者同意。 目前，SDK僅允許使用者選擇退出或退出所有用途，但未來Adobe希望提供更精細的特定用途控制。

如果使用者選擇用於所有用途，則允許SDK執行下列工作：

* 傳送資料至Adobe的伺服器或從伺服器傳送資料。
* 讀取和寫入Cookie或網頁儲存項目。

如果使用者退出所有用途，SDK不會執行任何這些工作。

## 設定同意

依預設，使用者會選擇加入所有用途。 若要防止SDK在使用者登入之前執行上述工作，請在SDK設定期間傳遞`"defaultConsent": "pending"`，如下所示：

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "imsOrgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "defaultConsent": "pending"
});
```

當一般用途的預設同意設為待決時，嘗試執行任何依賴使用者選擇加入偏好設定的命令（例如`sendEvent`命令），會導致命令在SDK中排隊。 在您將使用者的選擇加入偏好設定傳達至SDK之前，不會處理這些命令。

>[!NOTE]
>
>命令僅在記憶體中排隊。 不會在頁面載入時儲存。

如果您不想收集在使用者的選擇加入偏好設定設定設定之前發生的事件，則可在SDK設定期間傳遞`"defaultConsent": "out"`。 在您將使用者的選擇加入偏好設定傳達至SDK之前，嘗試執行任何依賴使用者選擇加入偏好設定的命令將無效。

>[!NOTE]
>
>目前，SDK僅支援單一或不支援任何目的。 雖然我們計畫建立一套更健全的用途或類別，以因應不同的Adobe功能和產品方案，但目前的實作是選擇加入的全部或全部方法。  這僅適用於Adobe Experience Platform[!DNL Web SDK]和NOT其他AdobeJavaScript庫。

此時，您可能會希望使用者在使用者介面中選擇加入。 收集使用者的偏好設定後，請將這些偏好設定傳達給SDK。

## 透過Adobe Experience Platform標準傳達同意偏好

SDK支援1.0版和2.0版的Adobe Experience Platform同意標準。 目前，1.0和2.0標準僅支援自動執行全部或零份同意偏好。 1.0標準正在逐步淘汰，以符合2.0標準。 2.0標準允許您添加其他許可偏好，這些許可偏好可用於手動強制執行許可偏好。

### 使用Adobe標準2.0版

如果您使用Adobe Experience Platform，您需要在描述檔架構中加入隱私權混音。 如需Adobe標準2.0版的詳細資訊，請參閱Adobe Experience Platform的[治理、隱私權與安全性。您可以在下面的值對象中添加資料，該對象與「同意與首選項」配置檔案混合的`consents`欄位的模式相對應。](../../landing/governance-privacy-security/overview.md)

如果用戶選擇，請執行`setConsent`命令，並按如下方式將收集首選項設定為`y`:

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "2.0",
      value: {
        collect: {
          val: "y"
        }
      }
    }]
});
```

如果用戶選擇退出，請執行`setConsent`命令，並將收集首選項設定為`n` ，如下所示：

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "2.0",
      value: {
        collect: {
          val: "n"
        }
      }
    }]
});
```

>[!NOTE]
>
>使用者選擇退出後，SDK將不允許您將使用者收集同意設定為`y`。

### 使用Adobe標準1.0版

如果用戶選擇，請執行`setConsent`命令，並將`general`選項設定為`in` ，如下所示：

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

如果用戶選擇退出，請執行`setConsent`命令，並將`general`選項設定為`out`，如下所示：

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

>[!NOTE]
>
>使用者選擇退出後，SDK將不允許您將使用者同意設定為`in`。

## 透過IAB TCF標準傳達同意偏好

SDK支援記錄使用者透過互動式廣告局歐洲(IAB)透明度與同意框架(TCF)標準提供的同意偏好。 同意字串可透過與上述相同的`setConsent`命令來設定，如下所示：

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

以此方式設定同意書時，即時客戶個人檔案會以同意書資訊進行更新。 要使此功能發揮作用，配置式XDM架構需要包含[配置式隱私混頻](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/profile/profile-privacy.schema.md)。 在發送事件時，需要手動將IAB許可資訊添加到事件XDM對象。 SDK不會自動在事件中包含同意資訊。 若要在事件中傳送同意資訊，[體驗事件隱私權Mixin](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/experience-event/experienceevent-privacy.schema.md)必須新增至「體驗事件」架構。

## 在單一請求中傳送多個標準

SDK也支援在請求中傳送多個同意物件。

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "2.0",
      value: {
        collect: {
          val: "y"
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

## 持續遵守同意偏好

在您使用`setConsent`命令將使用者偏好設定傳達至SDK後，SDK會將使用者偏好設定保留至Cookie。 下次使用者將您的網站載入瀏覽器時，SDK會擷取並使用這些持續的偏好設定，以決定事件是否可傳送至Adobe。

您需要獨立儲存使用者偏好設定，才能顯示同意對話方塊與目前偏好設定。 無法從SDK擷取使用者偏好設定。 為確保使用者偏好設定與SDK保持同步，您可在每次載入頁面時呼叫`setConsent`命令。 只有在偏好設定變更時，SDK才會進行伺服器呼叫。

## 同步身分並設定同意

當預設同意擱置或結束時，`setConsent`可能是第一個送出並建立身分的要求。 因此，在第一個要求上同步身分可能很重要。 身分映射可以像`sendEvent`命令一樣添加到`setConsent`命令中。 請參閱[檢索Experience CloudID](../identity/overview.md)

