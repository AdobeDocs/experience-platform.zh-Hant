---
title: renderDecisions
description: 呈現符合自動呈現資格的個人化內容。
exl-id: 6f7a3531-c2b6-4e90-a7ad-9f0fe4dc39e9
source-git-commit: c6a2b9700f0a688f65fec9febf5622c6c7b6aafa
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# `renderDecisions`

`renderDecisions`屬性可讓您強制網頁SDK轉譯任何符合自動轉譯條件的個人化內容。

執行`renderDecisions`命令時設定`sendEvent`布林值。 如果省略，此屬性會預設為`false`。 如果您要自動轉譯個人化內容，請將此屬性設定為`true`。

>[!IMPORTANT]
>
>`renderDecisions`屬性與[`documentUnloading`](documentunloading.md)屬性不相容。 避免同時設定兩個屬性為`true`。

```js
alloy("sendEvent", {
  "xdm": adobeDataLayer.getState(reference),
  "renderDecisions": true
});
```

當將此屬性設定為`true`時，請確定您也包含關聯的範圍或表面。 這些範圍或表面可以自動要求（例如在頁面上的第一個`sendEvent`命令上），或明確要求（使用[`personalization.decisionScopes`](personalization.md#personalizationdecisionscopes)或[`personalization.surfaces`](personalization.md#personalizationsurfaces)）。 呈現個人化時的常見問題為下列情況：

1. `sendEvent`命令會在頁面上及早執行，要求未設定`renderDecisions`的預設個人化（預設為`false`）。 主張會擷取但未轉譯。
1. 稍後在頁面上，另一個`sendEvent`觸發程式將`renderDecisions`設為`true`，但不包含任何範圍或介面。 由於此第二次呼叫中沒有範圍或介面，因此不會轉譯任何內容。

您可以透過以下其中一種方式來避免此問題：

* 在第一個`renderDecisions`呼叫中將`true`設定為`sendEvent`；或
* 將`decisionScopes`設定為`surfaces`時，在後續`sendEvent`呼叫上明確設定`renderDecisions`或`true`。

## 使用網頁SDK標籤擴充功能轉譯決策

這個屬性的Web SDK標籤延伸等效專案是&#39;[**&#39;動作中的**](/help/tags/extensions/client/web-sdk/actions/send-event.md#personalization-fields)&#x200B;轉譯視覺化個人化決定[!UICONTROL Send event]核取方塊。
