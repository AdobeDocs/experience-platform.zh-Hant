---
title: defaultConsent
description: 為您的Web屬性設定預設同意收集方法。
exl-id: 2a22fa8b-a234-4d3e-9b55-c7482a928fe6
source-git-commit: d3591053939147589dae24e1e4c20d53b1f87dd3
workflow-type: tm+mt
source-wordcount: '799'
ht-degree: 5%

---


# `defaultConsent`

此 `defaultConsent` 屬性會決定您呼叫前如何處理資料收集同意 [`setConsent`](../setconsent.md) 命令。 如果您不想不小心從居住於收集資料前需要同意之區域的個人收集資料，此屬性就十分實用。

根據預設，使用者會選擇加入所有用途，而Web SDK獲准執行下列工作：

* 傳送資料至Adobe的伺服器並從中傳送。
* 讀取和寫入Cookie或Web儲存專案。

如果使用者選擇退出所有用途，Web SDK不會執行任何這些工作。

此 `defaultConsent` 屬性支援三個值：

* **`in`**：資料收集會正常進行，直到使用者選擇退出為止。
* **`out`**：資料會永久捨棄，直到使用者選擇加入為止。
* **`pending`**：資料會儲存在本機，直到使用者選擇使用為止 [`setConsent`](../setconsent.md) 命令。 當一般用途的預設同意設定為 `pending`，嘗試執行任何取決於使用者選擇加入偏好設定的命令(例如 [`sendEvent`](../sendevent/overview.md) command)會導致命令在Web SDK中排入佇列。 只有在您將使用者的選擇加入偏好設定傳達給Web SDK後，才會處理佇列的命令。

>[!NOTE]
>
> 同意資料不會在頁面載入之間持續存在。

如果您的訪客不在一般資料保護規範(GDPR)的管轄範圍內，則預設同意可設為 `in`. GDPR管轄區內的訪客可將預設同意設定為 `pending`. 您的同意管理平台(CMP)可以偵測客戶區域並提供標幟 `gdprApplies` 至IAB TCF 2.0。此旗標可用於設定預設同意。

如果您不想收集在設定使用者的選擇加入偏好設定之前發生的事件，您可以傳遞 `"defaultConsent": "out"` 在Web SDK設定期間。 在您將使用者的選擇加入偏好設定傳達給Web SDK之前，嘗試執行任何取決於使用者選擇加入偏好設定的命令將不會生效。

>[!NOTE]
>
>目前，Web SDK僅支援單一「全有」或「全無」用途。 雖然我們計畫建立更強大的用途或類別集，以便對應不同的Adobe功能和產品方案，但目前的實作方式是全有或全無選擇加入。  這僅適用於 [!DNL Web SDK] 而不是其他AdobeJavaScript程式庫。

## 使用 `defaultConsent` 搭配 `setConsent` {#using-consent}

Web SDK提供兩種互補的同意設定命令：

* [`defaultConsent`](defaultconsent.md)：這個命令的目的在於擷取使用Web SDK的Adobe客戶的同意偏好設定。
* [`setConsent`](../setconsent.md)：此命令用於擷取網站訪客的同意偏好設定。

搭配使用時，這些設定可能會產生不同的資料收集和Cookie設定結果，具體取決於其設定的值。

請參閱下表以瞭解何時進行資料收集，以及何時根據同意設定設定Cookie。

| defaultConsent | setConsent | 發生資料收集 | Web SDK會設定瀏覽器Cookie |
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
| **AMCV_###@AdobeOrg** | 34128000 （395天） | 顯示時機 [`idMigrationEnabled`](../configure/idmigrationenabled.md) 已啟用。 在網站某些部分仍在使用時，若轉換到Web SDK會很有幫助 `visitor.js`. |
| **Demdex Cookie** | 15552000 （180天） | 在啟用ID同步時顯示。 Audience Manager設定此Cookie以指派唯一ID給網站訪客。 demdex Cookie可協助Audience Manger執行基本功能，例如：訪客身分識別、ID同步化、分割、模型、報告等。 |
| **kndctr_orgid_cluster** | 1800 （30分鐘） | 儲存Edge Network區域，為目前使用者的請求提供服務。 URL路徑會使用地區，這樣Edge Network就能將請求路由至正確的地區。 如果使用者使用不同的IP位址或在不同的工作階段中連線，則請求會再次路由到最近的區域。 |
| **kndct_orgid_identity** | 34128000 （395天） | 儲存ECID以及與ECID相關的其他資訊。 |
| **kndctr_orgid_consent** | 15552000 （180天） | 儲存網站的使用者同意偏好設定。 |
| **s_ecid** | 63115200 （2年） | 包含Experience CloudID的復本([!DNL ECID])或MID。 MID 儲存在遵循下列語法的機碼-值組中：`s_ecid=MCMID\|<ECID>`。 |

## 使用Web SDK標籤擴充功能設定預設同意

選取底下所需的選項按鈕 **[!UICONTROL 預設同意]** 當 [設定標籤擴充功能](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. 登入 [experience.adobe.com](https://experience.adobe.com) 使用您的Adobe ID憑證。
1. 瀏覽至 **[!UICONTROL 資料彙集]** > **[!UICONTROL 標籤]**.
1. 選取所需的標籤屬性。
1. 瀏覽至 **[!UICONTROL 擴充功能]**，然後按一下 **[!UICONTROL 設定]** 於 [!UICONTROL Adobe Experience Platform Web SDK] 卡片。
1. 向下捲動至 [!UICONTROL 隱私權] 區段，然後選取所需的 **[!UICONTROL 預設同意]**.
1. 按一下 **[!UICONTROL 儲存]**，然後發佈您的變更。

## 使用Web SDK JavaScript程式庫設定預設同意

設定 `defaultConsent` 字串屬性執行時達到所需的同意層級 `configure` 命令。 此屬性區分大小寫，僅支援下列三個值： `"in"`， `"out"`、和 `"pending"`. 如果您嘗試使用任何其他值，程式庫會擲回錯誤。

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "defaultConsent": "pending"
});
```
