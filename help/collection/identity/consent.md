---
title: 資料收集中的同意與身分
description: 瞭解同意選擇如何影響Web SDK實作中的身分行為，包括ECID產生、Cookie持續性和訪客持續性。
source-git-commit: 696e5098ebf556bfc0fa4fc22ff637cb0835eee0
workflow-type: tm+mt
source-wordcount: '1149'
ht-degree: 2%

---

# 資料收集中的同意與身分

在Web SDK實作中，同意和身分是緊密相連的。 收集同意的方式和時間會直接影響網站SDK何時產生ECID、設定身分識別Cookie，以及將資料傳送至Edge Network。 若未妥善處理同意，結果通常是未預期的訪客數量膨脹、身分連續性差距或兩者皆有。

此頁面說明同意選擇如何與身分行為互動，並提供設定實施以避免常見陷阱的指引。 如需Web SDK如何處理ECID、FPID與其他身分訊號的背景資訊，請參閱資料彙集[中的](./overview.md)身分識別。

## 同意如何影響身分 {#how-consent-affects-identity}

網頁SDK同時使用[`defaultConsent`](/help/collection/js/commands/configure/defaultconsent.md)設定變數和[`setConsent`](/help/collection/js/commands/setconsent.md)命令來控制它是否要將資料傳送至Edge Network。 同意狀態會直接決定產生ECID以及身分Cookie設定的時間。

下表顯示`defaultConsent`和`setConsent`對資料收集、Cookie設定和身分識別行為的組合影響。

| `defaultConsent` | `setConsent` | 發生資料收集 | 已設定瀏覽器Cookie | 身分行為 |
| --- | --- | --- | --- | --- |
| `in` | 未設定 | 是 | 是 | ECID會在第一個要求時立即產生。 身分Cookie是在頁面載入時設定。 |
| `in` | `in` | 是 | 是 | 訪客的現有ECID會保留。 身分行為未變更。 |
| `in` | `out` | 無 | 是 | 資料收集停止。 現有的ECID和`kndctr_`身分Cookie會保留在瀏覽器中，直到過期為止。 |
| `pending` | 未設定 | 無 | 無 | 不會產生任何ECID。 未設定任何Cookie。 事件會在本機排入佇列，直到呼叫`setConsent`為止。 |
| `pending` | `in` | 是 | 是 | 已排入佇列的事件會傳送。 ECID會在第一個要求上產生，並設定身分Cookie。 |
| `pending` | `out` | 無 | 是 | 已排入佇列的事件會遭捨棄。 不會產生任何ECID。 同意Cookie會設定為記錄訪客的偏好設定。 |
| `out` | 未設定 | 無 | 無 | 不會產生任何ECID。 未設定任何Cookie。 不會傳送任何事件。 |
| `out` | `in` | 是 | 是 | ECID會在第一個要求上產生，並設定身分Cookie。 |
| `out` | `out` | 無 | 是 | 不會產生任何ECID。 同意Cookie會設定為記錄訪客的偏好設定。 |

>[!NOTE]
>
>即使訪客選擇退出，身分和同意Cookie仍會設定。 這些Cookie是尊重訪客的資料收集偏好設定所必需的。 如需Web SDK設定的Cookie完整清單，請參閱[Web SDK Cookie](https://experienceleague.adobe.com/en/docs/core-services/interface/data-collection/cookies/web-sdk)。

當訪客在先前撤銷同意後重新授與同意（在`setConsent`後與`"general": "in"`呼叫`"general": "out"`）時，Web SDK會恢復傳送事件，並在Cookie中使用現有的ECID （如果尚未過期）。 訪客的身分會保留。

訪客授與或拒絕同意後，Web SDK會在`kndctr_`同意Cookie中保留其偏好設定。 後續頁面載入時，SDK會讀取此Cookie並自動套用儲存的偏好設定 — 除非訪客的偏好設定有所變更，否則您不需要再次呼叫`setConsent`。 請注意，`defaultConsent`設定值不會在頁面載入之間持續存在，但訪客的已解析同意（透過`setConsent`設定）會持續存在。

>[!NOTE]
>
>同意為`pending`時排入佇列的事件會保留在記憶體中，且不會在頁面重新載入後繼續存留。 如果訪客在同意解析前導覽至新頁面，則前一個頁面的佇列事件會遺失。

## 實作模式 {#implementation-patterns}

### 選擇加入模式（收集前必須先取得同意） {#opt-in}

法規（例如GDPR）在收集任何資料前需要明確同意時，請使用此模式。

```js
alloy("configure", {
  orgId: "YOUR_ORG_ID@AdobeOrg",
  edgeDomain: "data.example.com",
  defaultConsent: "pending"
});

// When the visitor grants consent:
alloy("setConsent", {
  consent: [{
    standard: "Adobe",
    version: "1.0",
    value: { general: "in" }
  }]
});
```

使用這個模式：
* 在授予同意前，不會產生任何ECID。
* 同意前觸發的事件（例如初始頁面檢視）會排入佇列，並在同意獲授後傳送。
* 身分Cookie只會在第一個成功的Edge Network要求後設定。

### 選擇退出模式（預設為集合，拒絕時停止） {#opt-out}

當法規預設允許資料收集並附帶選擇退出的選項時，請使用此模式。

```js
alloy("configure", {
  orgId: "YOUR_ORG_ID@AdobeOrg",
  edgeDomain: "data.example.com",
  defaultConsent: "in"
});

// If the visitor opts out:
alloy("setConsent", {
  consent: [{
    standard: "Adobe",
    version: "1.0",
    value: { general: "out" }
  }]
});
```

使用這個模式：
* ECID會在第一個頁面載入時立即產生。
* 所有事件都會傳送，直到訪客選擇退出為止。
* 選擇退出後，Web SDK會停止傳送事件，但現有的Cookie仍會保留。

## 使用第一方裝置ID的同意 {#consent-with-fpids}

如果您的實作使用[第一方裝置ID (FPID)](./fpid.md)，則您的伺服器會設定FPID Cookie，而不受Web SDK的同意狀態影響。 FPID Cookie是您在自己的基礎結構上管理的識別碼。 不過，FPID只會在Web SDK提出要求（由同意所管制）時傳送至Edge Network：

* 若使用`defaultConsent: "pending"`，瀏覽器中會存在FPID，但只有在獲得同意後，才會用來植入ECID。
* 透過`defaultConsent: "in"`，FPID會用於第一個要求，並立即植入ECID。

如果您的同意實作要求同意前不設定識別碼，請延遲設定FPID Cookie，直到傳達同意為止。 單獨Web SDK的同意閘道並不會阻止設定FPID Cookie，因為它是由您的伺服器管理。

## 常見陷阱 {#common-pitfalls}

+++**同意橫幅會清除身分Cookie**

**問題**：某些同意管理平台(CMP)在展示同意橫幅時，在訪客做出選擇之前，會清除所有Cookie，包括`kndctr_`身分Cookie。 訪客授與同意時，Web SDK會產生新的ECID，因為前一個ECID已刪除。 訪客在報表中顯示為新使用者。

**症狀**：
* 部署同意橫幅後，不重複訪客計數激增。
* 每次同意過期且再次與橫幅互動的回訪訪客都會計為新訪客。

**解決方案**：設定您的CMP以保留`kndctr_`個Cookie。 這些Cookie是身分識別Cookie，而非追蹤Cookie，可識別裝置且不含行為資料。 如果您的CMP需要清除Cookie，請將`kndctr_`首碼式Cookie新增至排除清單。 或者，延遲清除Cookie，直到訪客明確拒絕同意為止，而非先發制人地清除。

+++

+++**延遲同意導致重複身分**

**問題**：當`defaultConsent`設為`pending`時，Web SDK會先等待同意，再傳送任何資料。 如果在頁面生命週期的後期授予同意（例如，在觸發頁面重新載入的橫幅互動後），以下順序可能會導致問題：

1. 頁面載入。 `defaultConsent: "pending"`。Web SDK不會傳送要求。
2. 訪客授與同意。 CMP會觸發頁面重新載入。
3. 頁面會再次載入。 Web SDK會使用現在已授與的同意來初始化，並產生ECID。

此流程正常且運作正常。 當CMP或您的實作不慎清除步驟2和3之間的Cookie，或在重新載入時設定的Web SDK不同時，就會出現此問題。

**解決方案**：確定每個頁面載入的Web SDK設定（尤其是`orgId`和`defaultConsent`）都相同。 如果您的CMP在同意後觸發重新載入，請確認身分識別Cookie在重新載入後仍持續存在。

+++

+++**使用`defaultConsent: "in"`搭配同意橫幅**

**問題**：某些實作已設定`defaultConsent: "in"`，如果訪客拒絕，則使用`setConsent`呼叫`"general": "out"`。 此方法會產生ECID並傳送至少一個要求，之後才會拒絕同意。 根據您的法規要求，此初始資料收集可能不會符合您組織的隱私權政策。

**解決方案**：如果您的法規環境在任何資料收集或ECID產生前都需要同意，請改用`defaultConsent: "pending"`。 此設定可確保網頁SDK在明確授予同意之前不會與Edge Network通訊。

+++
