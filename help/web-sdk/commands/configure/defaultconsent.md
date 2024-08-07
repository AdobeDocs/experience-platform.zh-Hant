---
title: defaultConsent
description: 為您的Web屬性設定預設同意收集方法。
exl-id: 2a22fa8b-a234-4d3e-9b55-c7482a928fe6
source-git-commit: 8fc0fd96f13f0642f7671d0e0f4ecfae8ab6761f
workflow-type: tm+mt
source-wordcount: '799'
ht-degree: 5%

---


# `defaultConsent`

`defaultConsent`屬性決定您在呼叫[`setConsent`](../setconsent.md)命令之前如何處理資料收集同意。 如果您不想不小心從居住於收集資料前需要同意之區域的個人收集資料，此屬性就十分實用。

根據預設，使用者會選擇加入所有用途，而Web SDK獲准執行下列工作：

* 傳送資料至Adobe的伺服器並從中傳送。
* 讀取和寫入Cookie或Web儲存專案。

如果使用者選擇退出所有用途，Web SDK不會執行任何這些工作。

`defaultConsent`屬性支援三個值：

* **`in`**：資料收集會正常進行，直到使用者選擇退出為止。
* **`out`**：資料會永久捨棄，直到使用者選擇加入為止。
* **`pending`**：資料會儲存在本機，直到使用者使用[`setConsent`](../setconsent.md)命令選擇加入為止。 當一般用途的預設同意設定為`pending`時，嘗試執行任何依賴使用者選擇加入偏好設定的命令（例如[`sendEvent`](../sendevent/overview.md)命令）會導致命令在Web SDK中排入佇列。 只有在您將使用者的選擇加入偏好設定傳達給Web SDK後，才會處理佇列的命令。

>[!NOTE]
>
> 同意資料不會在頁面載入之間持續存在。

如果您的訪客不在一般資料保護規範(GDPR)的管轄範圍內，則預設同意可設為`in`。 GDPR管轄區內的訪客可將其預設同意設定為`pending`。 您的同意管理平台(CMP)可以偵測客戶的區域，並向IAB TCF 2.0提供標幟`gdprApplies`。此旗標可用於設定預設同意。

如果您不想收集在設定使用者的選擇加入偏好設定之前發生的事件，您可以在Web SDK設定期間傳遞`"defaultConsent": "out"`。 在您將使用者的選擇加入偏好設定傳達給Web SDK之前，嘗試執行任何取決於使用者選擇加入偏好設定的命令將不會生效。

>[!NOTE]
>
>目前，Web SDK僅支援單一「全有」或「全無」用途。 雖然我們計畫建立更強大的用途或類別集，以便對應不同的Adobe功能和產品方案，但目前的實作方式是全有或全無選擇加入。  這僅適用於[!DNL Web SDK]，不適用於其他AdobeJavaScript資料庫。

## 將`defaultConsent`與`setConsent`一起使用 {#using-consent}

Web SDK提供兩種互補的同意設定命令：

* [`defaultConsent`](defaultconsent.md)：這個命令的用意是擷取使用Web SDK的Adobe客戶的同意偏好設定。
* [`setConsent`](../setconsent.md)：這個命令的用意是擷取網站訪客的同意偏好設定。

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
| **AMCV_###@AdobeOrg** | 34128000 （395天） | [`idMigrationEnabled`](../configure/idmigrationenabled.md)啟用時出現。 當網站某些部分仍在使用`visitor.js`時，轉換為Web SDK會有所幫助。 |
| **Demdex Cookie** | 15552000 （180天） | 在啟用ID同步時顯示。 Audience Manager設定此Cookie以指派唯一ID給網站訪客。 demdex Cookie可協助Audience Manger執行基本功能，例如：訪客身分識別、ID同步化、分割、模型、報告等。 |
| **kndctr_orgid_cluster** | 1800 （30分鐘） | 儲存Edge Network區域，為目前使用者的請求提供服務。 URL路徑會使用地區，這樣Edge Network就能將請求路由至正確的地區。 如果使用者使用不同的IP位址或在不同的工作階段中連線，則請求會再次路由到最近的區域。 |
| **kndct_orgid_identity** | 34128000 （395天） | 儲存ECID以及與ECID相關的其他資訊。 |
| **kndctr_orgid_consent** | 15552000 （180天） | 儲存網站的使用者同意偏好設定。 |
| **s_ecid** | 63115200 （2年） | 包含Experience CloudID ([!DNL ECID])或MID的復本。 MID 儲存在遵循下列語法的機碼-值組中：`s_ecid=MCMID\|<ECID>`。 |

## 使用Web SDK標籤擴充功能設定預設同意

在[設定標籤延伸模組](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)時，在&#x200B;**[!UICONTROL 預設同意]**&#x200B;下選取所需的選項按鈕。

1. 使用您的Adobe ID憑證登入[experience.adobe.com](https://experience.adobe.com)。
1. 導覽至&#x200B;**[!UICONTROL 資料彙集]** > **[!UICONTROL 標籤]**。
1. 選取所需的標籤屬性。
1. 導覽至&#x200B;**[!UICONTROL 擴充功能]**，然後按一下[!UICONTROL Adobe Experience Platform Web SDK]卡片上的&#x200B;**[!UICONTROL 設定]**。
1. 向下捲動至[!UICONTROL 隱私權]區段，然後選取所需的&#x200B;**[!UICONTROL 預設同意]**。
1. 按一下&#x200B;**[!UICONTROL 儲存]**，然後發佈您的變更。

## 使用Web SDK JavaScript資料庫設定預設同意

執行`configure`命令時，將`defaultConsent`字串屬性設定為所需的同意等級。 此屬性區分大小寫，僅支援下列三個值： `"in"`、`"out"`及`"pending"`。 如果您嘗試使用任何其他值，程式庫會擲回錯誤。

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  defaultConsent: "pending"
});
```
