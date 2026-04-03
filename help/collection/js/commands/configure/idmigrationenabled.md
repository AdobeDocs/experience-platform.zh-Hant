---
title: idMigrationEnabled
description: 允許網頁SDK讀取AMCV Cookie。
exl-id: 33b9d645-0fbe-4fe4-8847-e6f9e78557b6
source-git-commit: bf0bb72777cacd822fd6e887ac3ef71764784214
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 0%

---

# `idMigrationEnabled`

`idMigrationEnabled`屬性可讓Web SDK讀取先前Adobe Experience Cloud實作所設定的AMCV Cookie。 如果您的組織將實作升級至Web SDK，此設定可讓您更順利轉換至目前的Adobe Experience Cloud ID服務。 此設定十分實用，可讓您在升級至網頁SDK時，不會看到不重複訪客大幅增加。

如果您的組織執行全新的網頁SDK實作，啟用此設定對資料收集或訪客身分識別沒有影響。 讓所有實施都啟用它沒有壞處。

## 身分移轉的運作方式 {#how-it-works}

訪客API會將Experience Cloud ID (ECID)儲存在名為`AMCV_<ORG_ID>`的Cookie中。 當`idMigrationEnabled`為`true` （預設值）時，Web SDK會自動從AMCV Cookie中讀取ECID，並在第一個Edge Network請求中將其用作訪客的身分。

1. 訪客進入的頁面現在使用Web SDK而不是訪客API。
1. Web SDK會檢查是否有現有的`kndctr_`身分Cookie （自己的Cookie格式）。 如果未找到，則會尋找`AMCV_` Cookie。
1. 如果找到`AMCV_` Cookie，Web SDK會擷取ECID並使用它來初始化訪客的身分。
1. Web SDK會設定具有相同ECID的新`kndctr_`身分識別Cookie。
1. 後續的造訪中，Web SDK會直接使用`kndctr_` Cookie。 不再需要`AMCV_` Cookie。

為了讓移轉能夠運作，Web SDK必須設定為與訪客API使用的相同[`orgId`](/help/collection/js/commands/configure/orgid.md)，且必須部署在設定AMCV Cookie的相同網域（或相同父網域的子網域）上。

## 支援的移轉案例

ID移轉支援下列轉換模式：

* **某些頁面仍使用訪客API，而其他頁面則使用網頁SDK**： SDK會讀取現有的AMCV Cookie，並使用現有的ECID寫入新的Cookie。 它會寫入AMCV Cookie，讓仍使用訪客API的頁面可繼續辨識相同訪客。
* **網頁SDK和訪客API都存在於相同頁面**：如果未設定AMCV Cookie，SDK會在頁面上尋找訪客API並使用它來取得ECID。
* **網站已完全移至Web SDK**：您可以保留一段時間的移轉功能，讓現有的AMCV型訪客在轉換Cookie時仍可維持連續性。

>[!IMPORTANT]
>
>除非您已確認AMCV Cookie已設定，否則請勿同時在同一頁載入訪客API和網頁SDK。 在單一頁面上執行兩個程式庫可能會導致競爭情況，使每個程式庫都嘗試獨立管理身分識別，這可能會產生重複或衝突的ECID。

## 關閉移轉 {#turn-off-migration}

在您整個網站在Web SDK上執行且沒有任何訪客只攜帶`AMCV_` Cookie而沒有對應的`kndctr_` Cookie後，您可以將`idMigrationEnabled`設定為`false`安全地停用身分移轉。 這是微幅的效能最佳化，可縮小身分邏輯的表面區域。

建議您在移轉最後一頁後，等待AMCV Cookie的期限上限過後。 如果您的AMCV Cookie有2年的有效期，請在最後一頁切換至網路SDK後等待兩年。 實際上，大多陣列織會在幾個月後更早停用移轉，並接受在長時間缺席後首次回訪的少數訪客所帶來的微不足道的膨脹量。

## Audience Manager特徵更新

移轉期間若將XDM格式的資料傳入Audience Manager，該資料必須轉換為訊號。 必須更新您的特徵，以反映XDM提供的新索引鍵。 使用[BAAAM工具](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/bulk-management-tools/bulk-management-intro.html?lang=zh-Hant#getting-started-with-bulk-management)可簡化此程式。

## 第三方ID移轉 {#third-party-id}

如果您的訪客API實作使用協力廠商ID (`demdex.net` Cookie)，Web SDK也可以移轉它們。 在網頁SDK設定中將[`thirdPartyCookiesEnabled`](/help/collection/js/commands/configure/thirdpartycookiesenabled.md)設定為`true`。 網頁SDK會讀取現有的Demdex Cookie，並在其Edge Network請求中包含第三方身分識別，遵循與AMCV Cookie相同的移轉模式。

## 驗證 {#validation}

驗證身分移轉是否正常運作：

1. 在已有現有`AMCV_` Cookie的瀏覽器中，開啟先前使用訪客API （現在使用網頁SDK）的頁面。
2. 在開發人員工具中，確認已設定`kndctr_`身分Cookie，且ECID符合`AMCV_` Cookie中的專案。
3. 部署後，比較相同時段內移轉前後的不重複訪客計數。 不重複訪客數量大幅增加可能表示移轉作業並未推進身分識別。

>[!TIP]
>
>使用`getIdentity`以程式擷取ECID以進行比較：
>
>```js
>alloy("getIdentity", { namespaces: ["ECID"] }).then(function(result) {
>   console.log("ECID:", result.identity.ECID);
>});
>```

## 設定 `idMigrationEnabled` {#configure}

執行`idMigrationEnabled`命令時設定`configure`布林值。 如果您在設定Web SDK時省略此屬性，其預設值為`true`。 如果您想要停用讀取由訪客API設定的AMCV Cookie的功能，請設定此屬性。 大部分的組織不需要設定此屬性。

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  idMigrationEnabled: false
});
```

## 使用網頁SDK標籤擴充功能啟用訪客ID移轉

可以使用[身分組態設定](/help/tags/extensions/client/web-sdk/configure/identity.md)，在Web SDK標籤擴充功能中設定這些設定。
