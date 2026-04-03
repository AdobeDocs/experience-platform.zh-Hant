---
title: 在資料收集中使用identityMap
description: 瞭解如何建構並傳送identityMap裝載，以在您的Web SDK實作中識別跨名稱空間的已知訪客。
source-git-commit: 696e5098ebf556bfc0fa4fc22ff637cb0835eee0
workflow-type: tm+mt
source-wordcount: '1671'
ht-degree: 0%

---

# 在資料收集中使用identityMap

`identityMap`裝載物件是您告知Edge Network哪些訪客超出其裝置層級[ECID](./overview.md)的方式。 當訪客登入、完成購買或以其他方式得知時，您可以與ECID一併傳送人員層級識別碼（CRM ID、雜湊電子郵件、忠誠度ID等）。 這些人員層級識別碼為下游服務提供重要資訊，讓下游服務可以：

* **跨裝置和管道將活動彙整至使用者。** [身分識別服務](/help/identity-service/home.md)將您傳送的身分識別連結至[身分識別圖形](/help/identity-service/features/identity-graph-viewer.md)，將匿名裝置層級的行為連線至已知人員。
* **建置統一的客戶設定檔。** [即時客戶個人檔案](/help/profile/home.md)會使用您設定為錨定事件和屬性至單一個人檔案的主要身分，以啟用個人層級細分和對象建立。
* **在下游目的地啟用對象。**&#x200B;許多[目的地](/help/destinations/home.md)都需要解析的個人層級身分（雜湊電子郵件、電話號碼等），才能讓您的對象與其使用者基礎相符。
* **協調跨頻道歷程。** [Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=zh-Hant)會使用已解析的身分，根據訪客的驗證行為，跨電子郵件、推播和應用程式內頻道觸發及個人化歷程。

本頁涵蓋如何建構`identityMap`負載、為每個身分選擇正確的設定，以及處理常見的實作案例。

## 承載結構 {#structure}

`identityMap`是JSON物件，其中每個最上層索引鍵都是名稱空間，而值是身分描述元的陣列。 您可以在單一承載中包含一或多個名稱空間，每個描述項都包含三個欄位： `id`、`authenticatedState`和`primary`。

```json
{
  "identityMap": {
    "CRMID": [
      {
        "id": "abc-123-xyz",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

| 欄位 | 類型 | 必要 | 說明 |
| --- | --- | --- | --- |
| `id` | 字串 | 是 | 識別碼值（例如，`user@example.com`或`ABC123`）。 |
| `authenticatedState` | 字串 | 是 | 您如何自信地知道此身分屬於訪客。 有效值包括`ambiguous`、`authenticated`和`loggedOut`。 |
| `primary` | 布林值 | 是 | 此身分是否應是事件的主要識別碼。 必須將所有名稱空間中的唯一識別標示為`primary: true`。 |

以下各節將詳細涵蓋裝載的每個部分。

### 名稱空間金鑰 {#namespace-keys}

`identityMap`中的每個最上層索引鍵都是[識別名稱空間](/help/identity-service/features/namespaces.md) — 將識別碼型別分類的字串（例如，`CRMID`、`Email`、`Phone`或`LoyaltyId`）。 名稱空間必須存在於Identity Service中，才能在承載中參照它們。 當訪客有多個識別碼時，您可以在相同事件中包含多個名稱空間索引鍵。

您不需要包含ECID作為名稱空間金鑰。 Edge Network會自動將ECID新增至身分裝載。 如果您明確包含ECID，同時存在人員層級的身分時，請勿將其標示為`primary`。

### `id` {#id}

`id`欄位是識別碼字串本身，此值可告知Experience Platform此識別代表的特定人員或裝置。 每個[身分名稱空間](/help/identity-service/features/namespaces.md)都需要特定的值格式，而以錯誤的格式傳送值會建立無法與正確格式化的版本合併的相異身分，導致設定檔碎片。

在`identityMap`中加入值之前，請先根據目標名稱空間預期的格式準備它：

| 常見的名稱空間型別 | 如何準備值 | 範例 |
| --- | --- | --- |
| **CRM /內部ID** | 使用記錄系統指派的確切識別碼。 保持所有事件（大小寫、前導零、字首）的格式一致。 | `ABC-12345`、`00098765` |
| **電子郵件（原始）** | 小寫完整電子郵件地址，並修剪前置與後置空格。 | `user@example.com` |
| **電子郵件（雜湊）** | 小寫並先修剪電子郵件地址，然後使用SHA-256進行雜湊。 傳送產生的64個字元的十六進位字串。 請勿新增Salt，除非您的名稱空間定義需要它。 | `a1b2c3d4e5f6a7b8c9...` |
| **電話(E.164)** | 以[E.164](https://en.wikipedia.org/wiki/E.164)格式設定數字：前導`+`、國碼，以及沒有空格或標點符號的訂閱者號碼。 | `+15551234567` |
| **FPID** | 產生[UUIDv4](https://datatracker.ietf.org/doc/html/rfc4122)字串。 如需產生需求，請參閱[第一方裝置識別碼](./fpid.md)。 | `123e4567-e89b-42d3-9456-426614174000` |

如需標準名稱空間及其定義的完整清單，請參閱[身分名稱空間概觀](/help/identity-service/features/namespaces.md#standard)。

>[!TIP]
>
>`id`值區分大小寫。 將`User@Example.com`和`user@example.com`視為兩個不同的身分。 標準化大小寫以避免在圖形中建立重複的身分，然後再傳送值（通常透過將電子郵件轉換為小寫並修剪空白字元）。

#### 在執行階段收集`id` {#collect-id}

您需要的識別碼很少直接在頁面上提供。 常見的收集策略包括：

* **資料層**：訪客登入後，從網站的資料層讀取識別碼。 此位置是最可靠的方法，因為資料層是由應用程式的後端填入，且會反映驗證的工作階段狀態。
* **驗證Token或工作階段Cookie**：從驗證系統設定的JWT或工作階段Cookie解碼或查詢識別碼。 使用值之前，請先驗證Token是否仍然有效。
* **伺服器端擴充**：使用[資料收集的「資料準備」](/help/datastreams/data-prep.md)或[事件轉送規則](/help/tags/ui/event-forwarding/overview.md)，在識別碼到達下游服務之前，在Edge對應或轉換識別碼。 當使用者端只有對應到伺服器端內部ID的不透明工作階段權杖時，此位置會很有用。

>[!TIP]
>
>如果指定的`id`值解析為空字串、`null`或`undefined`，請勿在`identityMap`中包含名稱空間。 傳送空白`id`會建立損毀的身分記錄。 在建置裝載之前，先使用檢查來保護您的實施。

### `authenticatedState` {#authenticated-state}

`authenticatedState`欄位會告訴下游服務要在指定識別中放置多少信任。 下列值適用於此欄位：

| 價值 | 使用時機 |
| --- | --- |
| **`authenticated`** | 訪客已在目前的工作階段中主動證明其身分（例如，使用憑證登入、完成MFA或類似驗證）。 |
| **`loggedOut`** | 訪客先前已驗證，但之後已登出。 身分仍與裝置相關聯，但工作階段已不在作用中。 |
| **`ambiguous`** | 無法確認身分屬於目前訪客。 此值用於裝置層級的識別碼（如FPID）或尚未發生驗證的任何識別碼。 |

>[!TIP]
>
>`authenticatedState`值會影響Adobe Experience Platform Identity Service建置及合併身分圖表的方式。 傳送`authenticated`以取得尚未驗證的身分，可能會建立不正確的跨裝置連結，而且難以復原。

### `primary` {#primary-identity}

每個`identityMap`裝載都必須有一個標示為`primary: true`的身分。 主要身分會決定在Experience Platform中作為事件錨點的身分。

設定主要身分時，請遵循下列准則：

* **當個人層級身分識別可用時** （訪客已登入），請將個人層級名稱空間標示為主要，並將ECID標示為非主要。 這會告訴Experience Platform將事件錨定在人員而非裝置。
* **當只有裝置層級的身分識別可用時** （訪客是匿名的），ECID會自動被當作主要身分識別。 您不需要在`identityMap`中加入ECID — Edge Network會自動新增。

```json
{
  "identityMap": {
    "CRMID": [
      {
        "id": "abc-123-xyz",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ],
    "Email": [
      {
        "id": "user@example.com",
        "authenticatedState": "authenticated",
        "primary": false
      }
    ]
  }
}
```

## 在您的實作中傳送identityMap {#send-identity}

>[!BEGINTABS]

>[!TAB JavaScript資料庫]

在`identityMap`呼叫的`xdm`物件中傳遞[`sendEvent`](/help/collection/js/commands/sendevent/overview.md)：

```js
alloy("sendEvent", {
  xdm: {
    identityMap: {
      CRMID: [
        {
          id: "abc-123-xyz",
          authenticatedState: "authenticated",
          primary: true
        }
      ]
    },
    eventType: "web.webpagedetails.pageViews"
  }
});
```

>[!TAB Web SDK標籤延伸模組]

使用[身分對應](/help/tags/extensions/client/web-sdk/data-element-types.md#identity-map)資料元素型別，在Tags UI中建置您的身分裝載：

1. 建立具有&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]**&#x200B;副檔名和&#x200B;**[!UICONTROL Identity map]**&#x200B;資料元素型別的資料元素。
2. 透過指定名稱空間、解析為識別碼的資料元素或值，以及驗證狀態來新增身分。
3. 將一個身分標示為主要身分。
4. 在&#x200B;**[!UICONTROL Send event]**&#x200B;底下的&#x200B;**[!UICONTROL Identity map]**&#x200B;動作中參考此資料元素。

>[!ENDTABS]

## 常見案例 {#common-scenarios}

+++**登入**

當訪客登入時，使用`authenticatedState: "authenticated"`和`primary: true`傳送其人員層級識別碼。 在驗證後的第一個事件上和工作階段中的所有後續事件上包含此身分。

```json
{
  "identityMap": {
    "CRMID": [
      {
        "id": "abc-123-xyz",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

+++

+++**登出**

訪客登出時，將`authenticatedState`更新為`loggedOut`，同時保留相同的識別碼。 這會保留裝置與人員之間的關聯，同時發出工作階段不再有效的訊號。

```json
{
  "identityMap": {
    "CRMID": [
      {
        "id": "abc-123-xyz",
        "authenticatedState": "loggedOut",
        "primary": false
      }
    ]
  }
}
```

登出後，ECID會恢復為有效的主要身分識別（Edge Network會自動套用它）。 除非訪客使用不同的帳戶登入，否則請勿將不同的人員層級身分標示為主要身分。

>[!IMPORTANT]
>
>登出後請勿完全停止傳送識別碼。 從`authenticated`切換到`loggedOut`會告知下游服務工作階段已結束。 省略識別碼會在身分圖表中留下空白，而造成設定檔片段。

+++

+++**多個名稱空間**

您可以在同一事件中傳送多個身分識別名稱空間。 當訪客登入且您有數個可用識別碼（例如CRM ID、雜湊電子郵件和熟客ID）時，這種情況很常見。 包含所有已知識別碼、僅將一個標示為主要，並將其他識別碼設為`primary: false`。

```json
{
  "identityMap": {
    "CRMID": [
      {
        "id": "abc-123-xyz",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ],
    "Email_LC_SHA256": [
      {
        "id": "a1b2c3d4e5f6...",
        "authenticatedState": "authenticated",
        "primary": false
      }
    ],
    "LoyaltyId": [
      {
        "id": "LOY-98765",
        "authenticatedState": "authenticated",
        "primary": false
      }
    ]
  }
}
```

>[!TIP]
>
>在相同事件上傳送多個具有相同`authenticatedState`的名稱空間，會為Identity Service提供連結這些身分的最強訊號。 在驗證時納入所有可用的識別碼，而不是將其分散到不同的事件中。

+++

+++**匿名訪客**

對於匿名訪客，您通常完全不需要傳送任何`identityMap`。 Edge Network會自動指派ECID並將其作為主要身分。 如果您使用[第一方裝置識別碼](./fpid.md)，則FPID是您需納入匿名訪客的唯一識別碼。

+++

## identityMap如何影響身分圖表 {#identity-graph}

到達Experience Platform的每個`identityMap`裝載都會由[身分服務](/help/identity-service/home.md)處理，此服務會將您傳送的身分連結至[身分圖表](/help/identity-service/features/identity-graph-viewer.md)。 您包含哪些名稱空間、如何設定`authenticatedState`以及您將哪個身分標示為`primary`，這些都直接影響Identity Service如何建置及合併這些圖形。

需留意的關鍵行為：

* **在相同事件上傳送的身分會連結在一起。**&#x200B;如果您在同一`sendEvent`呼叫上包含CRMID和電子郵件名稱空間，Identity Service會建立這兩個身分之間的連結。 將識別碼分散到不同的事件會產生較弱的連結，並可能導致圖形的片段。
* **身分識別`primary`錨定即時客戶設定檔中的事件。**&#x200B;設定檔使用主要身分來判斷事件所屬的設定檔。 將錯誤的身分標示為主要身分（例如，當有人員層級ID可用時，將ECID設為主要身分）可能會使事件根據裝置層級的設定檔而非人員層級的設定檔進行儲存。
* **`authenticatedState`會影響圖表信賴度。**&#x200B;傳送`authenticated`給尚未實際驗證的身分識別可能會建立不正確的跨裝置連結，而且這些連結很難復原。 只有當訪客在目前工作階段期間主動證明其身分時，才使用`authenticated`。

如果您的實作使用[身分圖表連結規則](/help/identity-service/identity-graph-linking-rules/overview.md) （例如名稱空間優先順序或身分最佳化演演算法），請檢閱[實作指南](/help/identity-service/identity-graph-linking-rules/implementation-guide.md)，以瞭解這些規則與您透過`identityMap`傳送的身分如何互動。

>[!NOTE]
>
>`identityMap`只會在網頁SDK向Edge Network提出要求時傳送，要求受到訪客同意狀態的限制。 如果您的實作使用`defaultConsent: "pending"`，在授予同意之前不會傳送身分。 如需詳細資訊，請參閱[同意與身分](./consent.md)。
