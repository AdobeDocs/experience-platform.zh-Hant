---
title: 疑難排解資料收集中的身分
description: 診斷Web SDK實作中的常見身分問題，包括訪客數量膨脹、ECID不一致、Cookie衝突和FPID問題。
source-git-commit: 696e5098ebf556bfc0fa4fc22ff637cb0835eee0
workflow-type: tm+mt
source-wordcount: '1034'
ht-degree: 0%

---

# 疑難排解資料收集中的身分

身分問題通常會顯示為下游報告中的症狀（膨脹的訪客計數、分散的個人資料或損毀的個人化），而不是實作本身的錯誤。 此頁面可協助您診斷並解決Web SDK實作中最常見的身分問題。 如需識別在資料收集中如何運作的背景，請參閱[識別總覽](./overview.md)。

## 檢查身分值 {#inspect-identity}

在疑難排解特定問題之前，請先擷取Web SDK目前使用的身分值。 使用[`getIdentity`](/help/collection/js/commands/getidentity.md)命令檢視ECID和其他身分識別訊號：

```js
alloy("getIdentity", { namespaces: ["ECID", "CORE"] }).then(function(result) {
  console.log("ECID:", result.identity.ECID);
  console.log("CORE ID:", result.identity.CORE);
  console.log("Edge region:", result.edge.regionID);
});
```

您也可以在瀏覽器的開發人員工具中檢查身分值：

1. 開啟&#x200B;**應用程式**&#x200B;標籤(Chrome/Edge)或&#x200B;**儲存**&#x200B;標籤(Firefox/Safari)。
2. 在您的網域中尋找以`kndctr_`為前置詞的Cookie。 `kndctr_<ORG_ID>_AdobeOrg_identity` Cookie包含ECID。
3. 開啟「**網路**」標籤，尋找Edge Network的`interact`或`collect`要求。 檢查`identityMap`的要求裝載和身分控制碼的回應裝載。

## 常見問題 {#common-issues}

+++**訪客計數膨脹**

**症狀**： Analytics報告顯示的不重複訪客數超過預期，或同一個人跨工作階段顯示為多個訪客。

**可能的原因**：

| 原因 | 如何識別 | 解決方法 |
| --- | --- | --- |
| Cookie存留期短 | 檢查瀏覽器中`kndctr_`個Cookie的到期日。 如果期限在7天或更短時間內到期，瀏覽器原則可能會限制Cookie的持續時間。 | 使用DNS A/AAAA記錄實作從伺服器設定的[第一方裝置識別碼(FPID)](./fpid.md)，以獲得較長的Cookie持續性。 |
| 第一個請求遺失FPID | 在頁面載入時檢查第一個Edge Network請求。 如果沒有FPID Cookie，Edge Network會產生新的ECID。 如果FPID是在第一個要求後設定，則第一個要求上產生的ECID會遭到孤立。 | 在Web SDK傳送其第一個要求之前設定FPID Cookie。 請參閱[何時設定Cookie](./fpid.md#when-to-set-cookie)。 |
| 網域間的`orgId`不相符 | 比較您網域中的`orgId`設定值。 不相符的值會導致個別的身分識別範圍。 | 在您組織內的所有網域上使用相同的[`orgId`](/help/collection/js/commands/configure/orgid.md)。 |
| 同意橫幅刪除Cookie | 如果您的同意實作在授予同意之前清除所有Cookie，然後初始化網頁SDK，則會產生新的ECID。 | 設定您的同意橫幅以保留`kndctr_` Cookie，或延遲Web SDK初始化，直到同意建立為止。 另請參閱[同意與身分](./consent.md)。 |
| JavaScript設定的FPID Cookie | 使用`document.cookie`設定的Cookie受到瀏覽器限制(ITP、ETP)的約束，其存留期有時限製為24小時。 | 使用DNS A/AAAA記錄從伺服器設定FPID Cookie，而不是從JavaScript。 |

+++

+++**ECID在頁面之間意外變更**

**症狀**： ECID在同一個網域的不同頁面上不同，或在每次載入頁面時變更。

**診斷步驟**：

1. 確認`kndctr_`身分Cookie存在於兩個頁面上。 如果某個頁面上遺漏此專案，請檢查是否已在該頁面上設定網頁SDK。
2. 確認Cookie網域設定得夠廣泛。 在`shop.example.com`上設定的Cookie在`www.example.com`上無法使用。 請確定第一方收集和Cookie設定基礎結構使用相同的網域範圍。
3. 檢查可在導覽上清除Cookie的JavaScript （例如，主動式Cookie同意指令碼或隱私權工具）。
4. 如果使用單頁應用程式，請確認應用程式初始化時已設定一次Web SDK，而不是在每次路由變更時都重新初始化。 重新初始化可產生新的ECID。

+++

+++**FPID未內建ECID**

**症狀**：您已設定FPID Cookie，但`getIdentity`傳回的ECID跨瀏覽不一致，或FPID未出現在Edge Network要求裝載中。

**診斷步驟**：

1. **驗證FPID Cookie格式**： FPID必須是有效的[UUIDv4](https://datatracker.ietf.org/doc/html/rfc4122)。 開啟瀏覽器的開發人員工具，尋找FPID Cookie，並確認值與模式`xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx`相符。
2. **檢查資料流中的Cookie名稱**：如果您使用[資料流Cookie方法](./fpid.md#setting-cookie-datastreams)，資料流中設定的Cookie名稱必須與伺服器設定的Cookie名稱完全相符。
3. **確認已在要求上傳送Cookie**：在[網路]索引標籤中，檢查Edge Network要求上的`Cookie`標頭。 必須包含FPID Cookie。
4. **檢查身分優先順序**：如果現有ECID已儲存在`kndctr_` Cookie中，則會優先於FPID。 FPID只會在不存在現有ECID時植入新的ECID。 如需完整的優先順序，請參閱[&#x200B; FPID的運作方式](./fpid.md#how-fpids-work)。
5. **驗證CNAME**：如果使用Datastream Cookie方法，請確認您的第一方集合CNAME已正確設定，且請求已透過它進行路由。

+++

+++**跨網域身分識別無法運作**

**症狀**：訪客從您的某個網域點按到另一個網域，即被視為目的地網域的新訪客。

**診斷步驟**：

1. **檢查URL**：當訪客按一下連結時，檢查目的地URL。 它必須包含`adobe_mc`查詢字串引數。 如果引數遺失，來源網域不會附加它。 請參閱[實作跨網域共用](./cross-domain-sharing.md#implement-cross-domain-sharing)。
2. **檢查時間**： `adobe_mc`引數會在5分鐘後到期。 如果載入目的地頁面花太長時間（例如，由於重新導向或網路速度緩慢），引數可能會在Web SDK讀取之前過期。
3. **驗證`orgId`是否符合**：兩個網域必須使用相同的[`orgId`](/help/collection/js/commands/configure/orgid.md)。 不相符的組織ID會導致目的地網域拒絕已傳遞的身分。
4. **確認Web SDK位於目的地**：目的地頁面必須已安裝並設定Web SDK。 若沒有它，`adobe_mc`引數會被忽略。
5. **檢查URL是否移除**：某些重新導向服務、CDN或伺服器端邏輯會移除未知的查詢字串引數。 確認`adobe_mc`在來源頁面和目的地頁面之間儲存任何中繼重新導向。

+++

+++**行動裝置對網頁的身分識別切換失敗**

**症狀**：從行動應用程式開始並開啟WebView或行動瀏覽器的訪客，在網頁端被視為新訪客。

**診斷步驟**：

1. **驗證URL**：記錄傳遞至WebView的URL。 它必須包含由`adobe_mc`[`getUrlVariables`產生的](https://developer.adobe.com/client-sdks/edge/identity-for-edge-network/api-reference/#geturlvariables)引數。
2. **檢查SDK版本**： Edge Network擴充功能的行動識別必須為1.1.0版或更新版本，而Web SDK必須為2.11.0版或更新版本。
3. **檢查時間**：如同跨網域共用，`adobe_mc`引數會在5分鐘後過期。 請確保WebView在建構URL後立即載入。
4. **確認`orgId`相符**： Experience Cloud組織ID在行動SDK和Web SDK設定中必須相同。

+++
