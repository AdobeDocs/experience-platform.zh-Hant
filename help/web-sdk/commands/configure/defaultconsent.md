---
title: defaultConsent
description: 設定預設的同意收集方法。
source-git-commit: b9db136a9077e3420bfeb44ae45e7d72c322acbb
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# `defaultConsent`

此 `defaultConsent` 屬性會決定您呼叫前如何處理資料收集同意 [`setConsent`](../setconsent.md) 命令。 如果您不想不小心從居住於收集資料前需要同意之區域的個人收集資料，此屬性就十分實用。

此屬性允許三個值：

* **在**：資料收集會正常進行，直到使用者選擇退出為止。
* **輸出**：資料會永久捨棄，直到使用者選擇加入為止。
* **擱置中**：資料會儲存在本機，直到使用者選擇使用為止 [`setConsent`](../setconsent.md) 命令。 資料不會在頁面載入之間持續存在。

如果您的訪客不在一般資料保護規範(GDPR)的管轄範圍內，則預設同意可設為 `in`. GDPR管轄區內的訪客可將預設同意設定為 `pending`. 您的同意管理平台(CMP)可以偵測客戶區域並提供標幟 `gdprApplies` 至IAB TCF 2.0。此旗標可用於設定預設同意。

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
