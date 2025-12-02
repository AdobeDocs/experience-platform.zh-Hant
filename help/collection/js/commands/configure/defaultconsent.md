---
title: defaultConsent
description: 為您的Web屬性設定預設同意收集方法。
exl-id: 2a22fa8b-a234-4d3e-9b55-c7482a928fe6
source-git-commit: 1e272eb18fac2f59f9737756d48947a25573d772
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 5%

---


# `defaultConsent`

`defaultConsent`屬性決定您在呼叫[`setConsent`](../setconsent.md)命令之前如何處理資料收集同意。 如果您不想不小心從居住於收集資料前需要同意之區域的個人收集資料，此屬性就十分實用。

如果您的訪客不在一般資料保護規範(GDPR)的管轄範圍內，則預設同意可設為`in`。 GDPR管轄區內的訪客可將其預設同意設定為`pending`。 您的同意管理平台(CMP)可以偵測客戶的區域，並向IAB TCF 2.0提供標幟`gdprApplies`。此旗標可用於設定預設同意。

執行`defaultConsent`命令時，將`configure`字串屬性設定為所需的同意等級。 此屬性區分大小寫，僅支援下列三個值： `"in"`、`"out"`及`"pending"`。 如果您嘗試使用任何其他值，程式庫會擲回錯誤。 如果未在`configure`命令中設定，預設值為&#x200B;**`in`**。

>[!IMPORTANT]
>
>`defaultConsent`值不會在頁面載入之間持續存在。 請務必在每次呼叫`configure`命令時設定所要的預設同意。

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  defaultConsent: "pending"
});
```

* **`in`**：資料收集會正常運作，直到使用者選擇退出為止。
* **`out`**：資料會永久捨棄，直到使用者選擇加入為止。
* **`pending`**：資料會儲存在本機，直到使用者使用[`setConsent`](../setconsent.md)命令選擇加入為止。

>[!NOTE]
>
>雖然Adobe計畫建立更強大的用途或類別集，以便對應至Adobe功能與產品方案，但目前的實作方式是全有或全無選擇加入。 此限制僅適用於Web SDK，不適用於其他Adobe JavaScript資料庫。

## 將`defaultConsent`與`setConsent`一起使用 {#using-consent}

Web SDK提供兩種互補的同意選項：

* `defaultConsent` （此頁面）：決定預設的同意偏好設定。
* [`setConsent`](../setconsent.md)：擷取訪客的同意偏好設定。

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

如需程式庫設定的Cookie清單，請參閱[Adobe Experience Platform Web SDK Cookie](https://experienceleague.adobe.com/zh-hant/docs/core-services/interface/data-collection/cookies/web-sdk)。

>[!NOTE]
>
>即使訪客選擇退出追蹤，身分和同意Cookie仍會設定。 這些Cookie對於遵循其資料收集偏好設定是必要的。

## 根據`gdprApplies`設定預設同意

有些CMP提供判斷一般資料保護規範(GDPR)是否適用於客戶的功能。 如果您希望客戶同意GDPR不適用的情況，可在TCF API呼叫中使用`gdprApplies`標幟。 例如：

```js
var alloyConfiguration = { ... };
window.__tcfapi('getTCData', 2, function (tcData, success) {
  if (success) {
    alloyConfiguration.defaultConsent = tcData.gdprApplies ? "pending" : "in";
    window.alloy("configure", alloyConfiguration);
  }
});
```

在上述程式碼區塊中，從TCF API取得`configure`後會呼叫`tcData`命令。 如果`gdprApplies`為true，則預設同意設定為`pending`。 如果`gdprApplies`為false，則預設同意設定為`in`。 請務必以您的設定填入`alloyConfiguration`變數。

## 使用網頁SDK標籤擴充功能的預設同意

請參閱Web SDK標籤擴充功能檔案中的[同意設定](/help/tags/extensions/client/web-sdk/configure/consent.md)，瞭解如何使用標籤執行這些動作。
