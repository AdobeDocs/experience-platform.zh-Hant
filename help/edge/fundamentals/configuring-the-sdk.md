---
title: 設定SDK
seo-title: 設定Adobe Experience Platform Web SDK
description: 瞭解如何設定Experience Platform Web SDK
seo-description: 瞭解如何設定Experience Platform Web SDK
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# （測試版）設定SDK

>[!IMPORTANT]
>
>Adobe Experience Platform Web SDK目前為測試版，並非所有使用者都能使用。 說明檔案和功能可能會有所變更。

SDK的設定是使用命令 `configure` 完成。

>[!I重要]
>`configure` 永遠 _是第_ 一個調用的命令。

```javascript
alloy("configure", {
  "configId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

在配置期間可以設定許多選項。 所有選項皆可在下方找到，依類別分組。

## 一般選項

### `configId`

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 字串 | 是 | none |

您指派的設定ID，會將SDK連結至適當的帳戶和設定。  在單一頁面中設定多個例項時，您必須為每個例項設 `configId` 定不同的例項。

### `context`

| **類型** | **必填** | **預設值** |
| ---------------- | ------------ | -------------------------------------------------- |
| 字串陣列 | 無 | `["web", "device", "environment", "placeContext"]` |

指出要自動收集哪些上下文類別，如「自動資訊」 [中所述](../reference/automatic-information.md)。  如果未指定此配置，則預設情況下會使用所有類別。

### `debugEnabled`

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 布林值 | 無 | `false` |

指出是否應啟用除錯。 將此配置設 `true` 置為啟用以下功能：

| **功能** |  |  |
| ---------------------- | ------------------ |
| 同步驗證 | 驗證針對架構收集的資料，並在下列標籤下的回應中傳回錯誤： `collect:error OR success` |
| 控制台記錄 | 啟用除錯訊息，以便顯示在瀏覽器的JavaScript主控台中 |

### `edgeDomain`

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ------------------ |
| 字串 | 無 | `beta.adobedc.net` |

用於與Adobe服務互動的網域。 只有當您有第一方網域(CNAME)，可代理Adobe Edge基礎架構的請求時，才會使用此功能。

### `errorsEnabled`

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 布林值 | 無 | `true` |

指示是否應隱藏錯誤。 如執行命 [令中所述](executing-commands.md)，無論Adobe Experience Platform Web SDK是否啟用除錯，未捕獲的 __ 錯誤都會記錄到開發人員主控台。 借由設 `errorsEnabled` 定 `false`為，Adobe Experience Platform Web SDK傳回的承諾永遠不會遭到拒絕，不過，如果在Adobe Experience Platform Web SDK中啟用記錄，錯誤仍會記錄至主控台。

### `orgId`

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 字串 | 是 | none |

您指派的Experience Cloud組織ID。  在頁面內設定多個例項時，您必須為每個例項設 `orgId` 定不同的例項。

## 資料收集

### `clickCollectionEnabled`

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 布林值 | 無 | `true` |

指出是否應自動收集與連結點按次數關聯的資料。 對於符合連結點按資格的點按，會收 [集下列Web Interaction](https://github.com/adobe/xdm/blob/master/docs/reference/context/webinteraction.schema.md) 資料：

| **屬性** |  |
| ------------ | ----------------------------------- |
| 連結名稱 | 由連結內容決定的名稱 |
| 連結 URL | 標準化URL |
| 連結類型 | 設為下載、退出或其他 |

### `onBeforeEventSend`

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 函數 | 無 | () => 未定義 |

設定此設定，以設定在每個事件傳送前呼叫的回呼。  包含該欄位的對 `xdm` 像將發送到回調。  修改xdm對象以更改所發送的內容。  在回呼中，物 `xdm` 件已在event命令中傳遞資料，並自動收集資訊。  有關此回呼的時間安排和示例的詳細資訊，請參 [閱全局修改事件](tracking-events.md#modifying-events-globally)。

## 隱私權選項

### `defaultConsent`

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 物件 | 無 | `{"general": "in"}` |

設定使用者的預設同意。 當使用者尚未儲存同意偏好設定時，就會使用此選項。 另一個有效值是 `{"general": "pending"}`。 設定後，工作將排入佇列，直到使用者提供同意偏好為止。 在提供使用者的偏好設定後，工作會根據使用者的偏好進行或中止。 如需詳 [細資訊](supporting-consent.md) ，請參閱支援同意。

## 個人化選項

### `prehidingStyle`

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 字串 | 無 | none |

用來建立CSS樣式定義，當從伺服器載入個人化內容時，會隱藏網頁的內容區域。 如果未提供此選項，SDK在載入個人化內容時不會嘗試隱藏任何內容區域，可能會導致「閃爍」。

例如，若您的網頁上有一個元素，其ID為您想要在從伺服器載入個人化內容時隱藏的預設內容，則預先隱藏樣式的範例如下： `container`

```javascript
  prehidingStyle: "#container { opacity: 0 !important }"
```

## 觀眾選項

### `cookieDestinationsEnabled`

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 布林值 | 無 | `true` |

啟用Cookie目標，允許根據區段限定設定Cookie。

### `urlDestinationsEnabled`

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 布林值 | 無 | `true` |

啟用URL目標，允許根據區段限定引發URL。

## 身分選項

### `idSyncContainerId`

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 數字 | 無 | none |

指定引發哪個ID同步的容器ID。 這是可從顧問處獲得的非負整數。

### `idSyncEnabled`

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 布林值 | 無 | `true` |

啟用ID同步功能，可讓觸發URL將Adobe唯一使用者ID與協力廠商資料來源的唯一使用者ID同步。

### `thirdPartyCookiesEnabled`

| **類型** | **必填** | **預設值** |
| -------- | ------------ | ----------------- |
| 布林值 | 無 | true |

啟用Adobe協力廠商Cookie的設定。 SDK可將訪客ID保留在協力廠商內容中，以便讓相同的訪客ID可跨網站使用。 如果您有多個網站或想要與合作夥伴共用資料，這項功能會很有用；但是，有時出於隱私權原因並不需要這麼做。
