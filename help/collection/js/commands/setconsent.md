---
title: setConsent
description: 用於每個頁面上，以追蹤使用者的同意偏好設定。
exl-id: d01a6ef1-4fa7-4a60-a3a1-19568b4e0d23
source-git-commit: 364b9adc406f732ea5ba450730397c4ce1bf03cf
workflow-type: tm+mt
source-wordcount: '1289'
ht-degree: 3%

---


# `setConsent`

`setConsent`命令會告訴網頁SDK是否應該傳送資料（選擇加入）、捨棄資料（選擇退出）或使用[`defaultConsent`](configure/defaultconsent.md) （同意不明）。

Web SDK支援下列標準：

* **[Adobe standard](/help/landing/governance-privacy-security/consent/adobe/overview.md)**：同時支援1.0和2.0標準。
* **[IAB透明與同意架構](/help/landing/governance-privacy-security/consent/iab/overview.md)**：若您使用此標準，若您的實作已正確設定，訪客的即時客戶設定檔會以同意資訊更新：
   1. XDM個別設定檔結構描述包含[IAB TCF 2.0同意欄位群組](/help/xdm/field-groups/profile/iab.md)。
   1. 體驗事件結構描述包含[IAB TCF 2.0同意欄位群組](/help/xdm/field-groups/event/iab.md)。
   1. 您在事件[XDM物件](sendevent/xdm.md)中包含IAB同意資訊。 Web SDK在傳送事件資料時不會自動包含同意資訊。

使用此命令後，Web SDK會將使用者的偏好設定寫入Cookie。 下次使用者在瀏覽器中載入您的網站時，SDK會擷取這些持續存在的偏好設定，以判斷事件是否可以傳送至Adobe。

Adobe建議您將「同意」對話方塊偏好設定與Web SDK同意分開儲存。 Web SDK並未提供擷取同意的方式。 若要確保使用者偏好設定與SDK保持同步，您可以在每次載入頁面時呼叫`setConsent`命令。 Web SDK只會在同意變更時進行伺服器呼叫。

## 身分同步考量事項 {#identity-considerations}

`setConsent`命令僅使用識別對應中的`ECID`，因為該命令在裝置層級運作。 `setConsent`命令不會考慮來自身分對應的其他身分。

## 將`defaultConsent`與`setConsent`一起使用 {#using-consent}

Web SDK提供兩種互補的同意設定命令：

* [`defaultConsent`](configure/defaultconsent.md)：此命令旨在使用Web SDK擷取Adobe客戶的同意偏好設定。
* [`setConsent`](setconsent.md)：這個命令的用意是擷取網站訪客的同意偏好設定。

搭配使用時，這些設定可能會產生不同的資料收集和Cookie設定結果，具體取決於其設定的值。

請參閱下表以瞭解何時進行資料收集，以及何時根據同意設定設定Cookie。

| `defaultConsent` | `setConsent` | 發生資料收集 | 網頁SDK設定瀏覽器Cookie |
|---------|----------|---------|---------|
| `in` | `in` | 是 | 是 |
| `in` | `out` | 無 | 是 |
| `in` | 未設定 | 是 | 是 |
| `pending` | `in` | 是 | 是 |
| `pending` | `out` | 無 | 是 |
| `pending` | 未設定 | 無 | 無 |
| `out` | `in` | 是 | 是 |
| `out` | `out` | 無 | 是 |
| `out` | 未設定 | 無 | 無 |

同意設定允許時，將會設定下列Cookie：

| 名稱 | 最大年齡 | 說明 |
|---|---|---|
| **`AMCV_###@AdobeOrg`** | 34128000 （395天） | [`idMigrationEnabled`](configure/idmigrationenabled.md)啟用時出現。 當網站某些部分仍在使用`visitor.js`時，轉換為Web SDK會有所幫助。 |
| **`Demdex cookie`** | 15552000 （180天） | 在啟用ID同步時顯示。 Audience Manager設定此Cookie以指派唯一ID給網站訪客。 demdex Cookie可協助Audience Manger執行基本功能，例如：訪客身分識別、ID同步化、分割、模型、報告等。 |
| **`kndctr_orgid_cluster`** | 1800 （30分鐘） | 儲存Edge Network區域以提供目前使用者的請求。 URL路徑會使用地區，這樣Edge Network就能將請求路由至正確的地區。 如果使用者使用不同的IP位址或在不同的工作階段中連線，則請求會再次路由到最近的區域。 |
| **`kndct_orgid_identity`** | 34128000 （395天） | 儲存ECID以及與ECID相關的其他資訊。 |
| **`kndctr_orgid_consent`** | 15552000 （180天） | 儲存網站的使用者同意偏好設定。 |
| **`s_ecid`** | 63115200 （2年） | 包含Experience Cloud ID ([!DNL ECID])或MID的復本。 MID 儲存在遵循下列語法的機碼-值組中：`s_ecid=MCMID\|<ECID>`。 |

呼叫您設定的Web SDK執行個體時執行`setConsent`命令。 您可以在此命令中包含下列物件：

* **`consent[]`**： `consent`物件的陣列。 根據您選擇的標準和版本，同意物件的格式會有所不同。 視同意標準而定，請參閱下方標籤以取得每個同意物件的範例。
* **`identityMap`**：控制如何產生ECID以及哪些ID同意資訊繫結的物件。 Adobe建議在`setConsent`在其他命令（例如[`sendEvent`](sendevent/overview.md)）之前執行時包含此物件。
* **`edgeConfigOverrides`**：包含[資料流組態的物件會覆寫](configure/edgeconfigoverrides.md)。

>[!BEGINTABS]

>[!TAB Adobe 2.0]

### Adobe 2.0標準`consent`物件

如果您將資料傳送至Adobe Experience Platform，您會在設定檔結構描述中包含隱私權結構描述欄位群組。 如需Adobe Experience Platform 2.0標準的詳細資訊，請參閱[Adobe中的治理、隱私權和安全性](/help/landing/governance-privacy-security/overview.md)。 您可以在對應於`consents`設定檔欄位群組[!UICONTROL Consents and Preferences]欄位之結構描述的下方值物件中新增資料。

* **`standard`**：您選擇的同意標準。 針對Adobe 2.0標準將此屬性設定為`"Adobe"`。
* **`version`**：代表同意標準版本的字串。 針對Adobe 2.0標準將此屬性設定為`"2.0"`。
* **`value`**：包含同意值的物件。
   * **`value.collect.val`**：同意值。 當使用者選擇加入時，將此項設為`"y"`，而當使用者選擇退出時，則設為`"n"`。
   * **`value.metadata.time`**：使用者上次更新其同意設定的時間戳記。

```js
// Set consent using the Adobe 2.0 standard
alloy("setConsent", {
  "consent": [{
    "standard": "Adobe",
    "version": "2.0",
    "value": {
      "collect": {
        "val": "y"
      },
      "metadata": {
        "time": "YYYY-03-17T15:48:42-07:00"
      }
    }
  }]
});
```

>[!TAB IAB TCF 2.0]

### iab TCF 2.0標準`consent`物件

若要記錄透過Interactive Advertising Bureau Europe (IAB) Transparency and Consent Framework (TCF)標準提供的使用者同意偏好設定，請設定同意字串，如下所示。

以這種方式設定同意時，即時客戶設定檔會更新同意資訊。 為了讓此功能發揮作用，設定檔XDM結構描述需要包含[設定檔隱私權結構描述欄位群組](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/profile/profile-privacy.schema.md)。 傳送事件時，需要手動將IAB同意資訊新增至事件XDM物件。 Web SDK不會自動在事件中包含同意資訊。

若要在事件中傳送同意資訊，您必須將體驗事件隱私權欄位群組新增至已啟用[!DNL Profile]的[!DNL XDM ExperienceEvent]結構描述。 請參閱資料集準備指南中有關[更新ExperienceEvent結構描述](/help/landing/governance-privacy-security/consent/iab/dataset.md#event-schema)的章節，以瞭解如何設定此內容的步驟。

* **`standard`**：您選擇的同意標準。 針對IAB TCF 2.0標準將此屬性設定為`"IAB TCF"`。
* **`version`**：代表同意標準版本的字串。 針對IAB TCF 2.0標準將此屬性設定為`"2.0"`。
* **`value`**：包含同意值的字串。
* **`gdprApplies`**：判斷GDPR是否適用於此同意值的布林值。 其預設值為`true`。
* **`gdprContainsPersonalData`**：布林值，可判斷與此使用者關聯的事件資料是否包含個人資料。 其預設值為`false`。

```js
// Set consent using the IAB TCF 2.0 standard
alloy("setConsent", {
  consent: [{
    "standard": "IAB TCF",
    "version": "2.0",
    "value": "CO052l-O052l-DGAMBFRACBgAIBAAAAABIYgEawAQEagAAAA",
    "gdprApplies": true,
    "gdprContainsPersonalData": true
  }]
});
```

IAB TCF 2.0 API會提供客戶更新同意時適用的事件。 當客戶最初設定其偏好設定以及客戶更新其偏好設定時，就會發生這種情況。 您可以新增事件接聽程式來執行`setConsent`命令：

```js
const identityMap = { ... };
window.__tcfapi('addEventListener', 2, function (tcData, success) {
  if (success && tcData.eventStatus === 'useractioncomplete') {
    window.alloy("setConsent", {
      identityMap,
      consent: [
        {
          standard: "IAB TCF",
          version: "2.0",
          value: tcData.tcString,
          gdprApplies: tcData.gdprApplies
        }
      ]
    });
  }
});
```

上述程式碼區塊會接聽`useractioncomplete`事件，然後設定同意，傳遞同意字串和`gdprApplies`標幟。 如果您有客戶的自訂身分，請務必填寫`identityMap`變數。

>[!TAB Adobe 1.0]

### Adobe 1.0標準`consent`物件

* **`standard`**：您選擇的同意標準。 針對Adobe 1.0標準將此屬性設定為`"Adobe"`。
* **`version`**：代表同意標準版本的字串。 針對Adobe 1.0標準將此屬性設定為`"1.0"`。
* **`value.general`**：同意值。 當使用者選擇加入時，將此項設為`"in"`，而當使用者選擇退出時，則設為`"out"`。

```js
// Set consent using the Adobe 1.0 standard
alloy("setConsent", {
  "consent": [{
    "standard": "Adobe",
    "version": "1.0",
    "value": {
      "general": "in"
    }
  }]
});
```

>[!ENDTABS]

### 在一個請求中傳送多個標準 {#multiple-standards}

Web SDK也支援在請求中傳送多個同意物件，如下列範例所示。

```js
alloy("setConsent", {
    consent: [{
        standard: "Adobe",
        version: "2.0",
        value: {
            collect: {
                val: "y"
            },
            metadata: {
                time: "YYYY-03-17T15:48:42-07:00"
            }
        }
    }, {
        standard: "IAB TCF",
        version: "2.0",
        value: "CO1Z4yuO1Z4yuAcABBENArCsAP_AAH_AACiQGCNX_T5eb2vj-3Zdt_tkaYwf55y3o-wzhhaIse8NwIeH7BoGP2MwvBX4JiQCGBAkkiKBAQdtHGhcCQABgIhRiTKMYk2MjzNKJLJAilsbe0NYCD9mnsHT3ZCY70--u__7P3fAwQgkwVLwCRIWwgJJs0ohTABCOICpBwCUEIQEClhoACAnYFAR6gAAAIDAACAAAAEEEBAIABAAAkIgAAAEBAKACIBAACAEaAhAARIEAsAJEgCAAVA0JACKIIQBCDgwCjlACAoAAAAA.YAAAAAAAAAAA",
        gdprApplies: true
    }]
});
```

## 同意偏好設定的持續性 {#persistence}

在您使用`setConsent`命令將使用者偏好設定傳送至Web SDK後，SDK會儲存使用者偏好設定至Cookie。 下次使用者在瀏覽器中載入您的網站時，網頁SDK會擷取並使用這些持續存在的偏好設定來判斷是否可將事件傳送至Adobe。

單獨儲存使用者的偏好設定，以便您能使用目前的偏好設定顯示同意對話方塊。 無法從網頁SDK擷取使用者偏好設定。 若要確保使用者偏好設定與SDK保持同步，您可以在每次載入頁面時呼叫`setConsent`命令。 網頁SDK只會在偏好設定變更時進行伺服器呼叫。

## 使用網頁SDK標籤擴充功能設定同意

等同於這個命令的網頁SDK標籤延伸是[**[!UICONTROL Set consent]**](/help/tags/extensions/client/web-sdk/actions/set-consent.md)動作。
