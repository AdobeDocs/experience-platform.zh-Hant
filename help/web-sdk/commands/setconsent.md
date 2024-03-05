---
title: setConsent
description: 用於每個頁面上以追蹤使用者的同意。
source-git-commit: 90493d179e620604337bda96cb3b7f5401ca4a81
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 1%

---

# setConsent

此 `setConsent` 命令會告知Web SDK是否應傳送資料（選取加入）、捨棄資料（選取退出）或使用 [`defaultConsent`](configure/defaultconsent.md) （同意不明）。

Web SDK支援下列標準：

* **[Adobe標準](/help/landing/governance-privacy-security/consent/adobe/overview.md)**：同時支援1.0和2.0標準。
* **[IAB透明與同意架構](/help/landing/governance-privacy-security/consent/iab/overview.md)**：如果您使用此標準，而您的實施已正確設定，訪客的即時客戶設定檔會以同意資訊更新：
   1. XDM個別設定檔結構描述包含 [IAB TCF 2.0同意欄位群組](/help/xdm/field-groups/profile/iab.md).
   1. 體驗事件結構包含 [IAB TCF 2.0同意欄位群組](/help/xdm/field-groups/event/iab.md).
   1. 事件中需包含IAB同意資訊 [xdm物件](sendevent/xdm.md). Web SDK在傳送事件資料時不會自動包含同意資訊。

使用此命令後，Web SDK會將使用者的偏好設定寫入Cookie。 下次使用者在瀏覽器中載入您的網站時，SDK會擷取這些儲存的偏好設定，以判斷事件是否可以傳送給Adobe。

Adobe建議您將「同意」對話方塊偏好設定與Web SDK同意分開儲存。 Web SDK並未提供擷取同意的方式。 若要確保使用者偏好設定與SDK保持同步，您可以呼叫 `setConsent` 命令於每個頁面載入。 Web SDK只會在同意變更時進行伺服器呼叫。

## 使用Web SDK標籤擴充功能設定同意

在Adobe Experience Platform資料收集標籤介面的規則中，將同意設定為動作。

1. 登入 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID憑證。
1. 瀏覽至 **[!UICONTROL 資料彙集]** > **[!UICONTROL 標籤]**.
1. 選取所需的標籤屬性。
1. 瀏覽至 **[!UICONTROL 規則]**，然後選取所需的規則。
1. 在 [!UICONTROL 動作]，選取現有動作或建立動作。
1. 設定 [!UICONTROL 副檔名] 下拉式欄位至 **[!UICONTROL Adobe Experience Platform Web SDK]**，並設定 [!UICONTROL 動作型別] 至 **[!UICONTROL 設定同意]**.
1. 在右側設定所要的欄位，包括 **[!UICONTROL 標準]** 和 **[!UICONTROL 一般同意]**.
1. 按一下 **[!UICONTROL 保留變更]**，然後執行您的發佈工作流程。

您可以在此動作中包含多個同意物件。

## 使用Web SDK JavaScript程式庫設定同意

執行 `setConsent` 命令來呼叫Web SDK的已設定執行個體。 您可以在此命令中包含下列物件：

* **`consent[]`**：陣列 `consent` 物件。 根據您選擇的標準和版本，同意物件的格式會有所不同。
* **`identityMap`**：此物件可控制產生ECID的方式以及要將哪些ID同意資訊繫結至此。 Adobe建議將此物件納入 `setConsent` 在其他命令之前執行，例如 [`sendEvent`](sendevent/overview.md).
* **`edgeConfigOverrides`**：包含 [資料流設定覆寫](datastream-overrides.md).

>[!BEGINTABS]

>[!TAB Adobe2.0]

### Adobe2.0標準 `consent` 物件

* **`standard`**：您選擇的同意標準。 將此屬性設為 `"Adobe"` 適用於Adobe 2.0標準。
* **`version`**：代表同意標準版本的字串。 將此屬性設為 `"2.0"` 適用於Adobe 2.0標準。
* **`value`**：包含同意值的物件。
   * **`value.collect.val`**：同意值。 有效值為 `"y"` （選擇加入）和 `"n"` （選擇退出）。
   * **`value.metadata.time`**：使用者設定同意值的時間戳記。

```js
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

### IAB TCF 2.0標準 `consent` 物件

* **`standard`**：您選擇的同意標準。 將此屬性設為 `"IAB TCF"` 適用於IAB TCF 2.0標準。
* **`version`**：代表同意標準版本的字串。 將此屬性設為 `"2.0"` 適用於IAB TCF 2.0標準。
* **`value`**：包含同意值的字串。
* **`gdprApplies`**：判斷GDPR是否適用於此同意值的布林值。 其預設值為 `true`。
* **`gdprContainsPersonalData`**：判斷與此使用者關聯的事件資料是否包含個人資料的布林值。 其預設值為 `false`。

```js
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

>[!TAB Adobe1.0]

### Adobe1.0標準 `consent` 物件

* **`standard`**：您選擇的同意標準。 將此屬性設為 `"Adobe"` 適用於Adobe 1.0標準。
* **`version`**：代表同意標準版本的字串。 將此屬性設為 `"1.0"` 適用於Adobe 1.0標準。
* **`value.general`**：同意值。 有效值為 `"in"` （選擇加入）和 `"out"` （選擇退出）。

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
