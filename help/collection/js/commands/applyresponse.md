---
title: applyResponse
description: 使用來自Edge Network的回應來初始化網頁SDK。
exl-id: 0653b8f7-33f0-43a1-97f5-59a51270f660
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---

# `applyResponse`

`applyResponse`命令可讓您根據Edge Network的回應執行各種動作。 它通常用於混合部署，即伺服器對Edge Network進行初始呼叫的情況。 此命令會從該呼叫取得回應，並在瀏覽器中初始化Web SDK。

呼叫您設定的Web SDK執行個體時執行`applyResponse`命令。 包含組態選項的物件支援下列欄位：

* **`renderDecisions`**：布林值，會強制網頁SDK轉譯任何符合自動轉譯條件的個人化內容。 與[`renderDecisions`](sendevent/renderdecisions.md)命令中的[`sendEvent`](sendevent/overview.md)相同。
* **`responseHeaders`**：字串標頭名稱與字串標頭值的對應。
* **`responseBody`**：必要。 來自對Edge Network的伺服器呼叫的JSON回應內文。
* **`personalization.sendDisplayEvent`**：在[`personalization.sendDisplayEvent`](sendevent/personalization.md)命令中與`sendEvent`運作相同的布林值。

```js
alloy("applyResponse",{
  "renderDecisions": true,
  "responseHeaders": {},
  "responseBody": {},
  "personalization": {
    "sendDisplayEvent": true
  }
});
```

## 回應物件

如果您決定使用此命令[處理回應](command-responses.md)，則回應物件中有以下屬性：

* **`propositions`**： Edge Network傳回的主張陣列。 自動演算的建議包含設為`renderAttempted`的旗標`true`。
* **`inferences`**：推斷物件的陣列，其中包含此使用者的機器學習資訊。
* **`destinations`**： Edge Network傳回的目的地物件陣列。

## 使用網頁SDK標籤擴充功能套用回應

等同於這個命令的網頁SDK標籤延伸是[**[!UICONTROL Apply response]**](/help/tags/extensions/client/web-sdk/actions/apply-response.md)動作。
