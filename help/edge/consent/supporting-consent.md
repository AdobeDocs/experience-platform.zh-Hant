---
title: 使用Adobe Experience Platform Web SDK支援客戶同意偏好設定
description: 了解如何使用Adobe Experience Platform Web SDK支援同意偏好設定。
keywords: 同意；預設同意；預設同意；setConsent；設定檔隱私權欄位群組；體驗事件隱私權欄位群組；隱私權欄位群組；
exl-id: 647e4a84-4a66-45d6-8b05-d78786bca63a
source-git-commit: bd312024a1a3fb6da840a38d6e9d19fcbd6eab5a
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 0%

---

# 支援客戶同意偏好設定

為了尊重使用者的隱私權，您可能會想在允許SDK將使用者特定資料用於特定用途之前，要求使用者同意。 目前，SDK僅允許使用者選擇加入或退出所有用途，但未來Adobe希望針對特定用途提供更精細的控制。

如果使用者選擇使用所有用途，則允許SDK執行下列工作：

* 將資料傳送至Adobe的伺服器，或從伺服器傳送資料。
* 讀取和寫入Cookie或Web儲存項。

如果使用者選擇不執行所有用途，SDK將不會執行任何這些工作。

## 設定同意

依預設，使用者會選擇加入至所有用途。 為防止SDK在使用者選擇加入前執行上述工作，請在SDK設定期間傳遞`"defaultConsent": "pending"`，如下所示：

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "imsOrgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "defaultConsent": "pending"
});
```

當一般用途的預設同意設為「擱置中」時，嘗試執行任何依賴使用者選擇加入偏好設定的命令（例如`sendEvent`命令）時，會導致命令在SDK中排入佇列。 在您將使用者的選擇加入偏好設定傳遞至SDK後，才會處理這些命令。

>[!NOTE]
>
>命令僅在記憶體中排隊。 不會在頁面載入時儲存。

如果您不想收集在設定使用者的選擇加入偏好設定之前發生的事件，您可以在SDK設定期間傳遞`"defaultConsent": "out"`。 在您將使用者的選擇加入偏好設定傳遞至SDK之前，嘗試執行任何依賴使用者選擇加入偏好設定的命令將沒有作用。

>[!NOTE]
>
>目前，SDK僅支援單一全部或無任何用途。 雖然我們打算建立一組更健全的用途或類別，以對應不同的Adobe功能和產品，但目前的實作只是選擇加入的一種方式，或完全不是。  這僅適用於Adobe Experience Platform [!DNL Web SDK]，而不適用於其他AdobeJavaScript程式庫。

此時，您可能偏好要求使用者在您的使用者介面中的某個位置選擇加入。 收集使用者偏好設定後，將這些偏好設定傳達給SDK。

## 透過Adobe Experience Platform標準傳達同意偏好設定

SDK支援1.0版和2.0版Adobe Experience Platform同意標準。 目前，1.0和2.0標準僅支援自動執行全部或無同意偏好設定。 1.0標準正在逐步淘汰，以支援2.0標準。 2.0標準可讓您新增其他同意偏好設定，以用於手動強制執行同意偏好設定。

### 使用Adobe標準2.0版

如果您使用Adobe Experience Platform，則需要將隱私權結構欄位群組包含在您的設定檔結構中。 請參閱[Adobe Experience Platform](../../landing/governance-privacy-security/overview.md)中的控管、隱私和安全性，以了解有關Adobe標準2.0版的詳細資訊。您可以在下面的值對象內添加資料，該對象與[!UICONTROL 同意和首選項]配置檔案欄位組的`consents`欄位的架構相對應。

如果用戶選擇加入，請執行`setConsent`命令，並按如下方式將收集首選項設定為`y`:

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

時間欄位應指定使用者上次更新同意偏好設定的時間。 如果用戶選擇退出，請執行`setConsent`命令，並將收集首選項設定為`n`，如下所示：

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

>[!NOTE]
>
>使用者選擇退出後，SDK將不允許您將使用者收集同意設定為`y`。

### 使用Adobe標準1.0版

如果用戶選擇加入，請執行`general`選項設定為`in`的`setConsent`命令，如下所示：

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

如果用戶選擇退出，請執行`general`選項設定為`out`的`setConsent`命令，如下所示：

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

## 透過IAB TCF標準傳達同意偏好設定

SDK支援記錄透過Interactive Advertising Bureau Europe(IAB)透明與同意架構(TCF)標準提供的使用者同意偏好設定。 同意字串可透過與上述相同的`setConsent`命令進行設定，如下所示：

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

以此方式設定同意時，即時客戶設定檔會更新為同意資訊。 為了讓此功能發揮作用，設定檔XDM架構必須包含[設定檔隱私權架構欄位群組](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/profile/profile-privacy.schema.md)。 傳送事件時，需要手動將IAB同意資訊新增至事件XDM物件。 SDK不會自動在事件中加入同意資訊。 若要在事件中傳送同意資訊，需要將[體驗事件隱私權欄位群組](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/experience-event/experienceevent-privacy.schema.md)新增至體驗事件結構。

## 在一個請求中發送多個標準

SDK也支援在要求中傳送多個同意物件。

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

## 同意偏好設定的持續性

在您使用`setConsent`命令將使用者偏好設定傳送至SDK後，SDK會將使用者偏好設定保存至Cookie。 下次使用者在瀏覽器中載入您的網站時，SDK將擷取並使用這些持續的偏好設定，以判斷事件是否可傳送至Adobe。

您需要單獨儲存使用者偏好設定，才能顯示具有目前偏好設定的同意對話方塊。 無法從SDK擷取使用者偏好設定。 若要確保使用者偏好設定與SDK保持同步，您可以在每次頁面載入時呼叫`setConsent`命令。 只有在偏好設定已變更時，SDK才會進行伺服器呼叫。

## 在設定同意時同步身分

當預設同意擱置或結束時，`setConsent`可能是第一個送出並建立身分的要求。 因此，在第一個要求上同步身分識別可能很重要。 身份映射可以像`sendEvent`命令一樣添加到`setConsent`命令。 請參閱[擷取Experience CloudID](../identity/overview.md)
