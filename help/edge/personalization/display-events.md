---
title: 在Web SDK中管理顯示事件
description: 本文說明什麼是顯示事件，以及如何在Web SDK中使用它們。
source-git-commit: da506cd5de69047e326790d0fae56f76c728e7a5
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---


# 在Web SDK中管理顯示事件

當頁面上顯示特定個人化內容時，Web SDK會使用顯示事件來通知您的個人化或分析服務。

傳送顯示事件可改善個人化量度的準確性，並提供使用者在您頁面上所看到內容的準確概覽。

Web SDK可讓您以兩種方式傳送顯示事件：

* [自動](#send-automatically)，即個人化內容在頁面上呈現之後立即執行。 請參閱檔案，瞭解如何 [呈現個人化內容](rendering-personalization-content.md) 以取得詳細資訊。
* [手動](#send-sendEvent-calls)，透過後續 `sendEvent` 呼叫。

>[!NOTE]
>
>在呼叫時，顯示事件不會自動傳送 `applyPropositions` 函式。

## 自動傳送顯示事件 {#send-automatically}

傳送顯示事件會自動提供更精確的分析量度，因為事件會在個人化載入後立即傳送。 此實作也有更簡化的實作方法。

若要在頁面上呈現個人化內容後自動傳送顯示事件，您必須設定下列引數：

* `renderDecisions: true`
* `personalization.sendDisplayNotifications: true` 或未指定

Web SDK會在任何個人化轉譯為結果後，立即傳送顯示事件。 `sendEvent` 呼叫。

## 在後續sendEvent呼叫中傳送顯示事件 {#send-sendEvent-calls}

比較 [自動](#send-automatically) 傳送顯示事件（當您將其納入後續活動時） `sendEvent` 呼叫您也可以有機會在呼叫中包含有關頁面載入的詳細資訊。 這可能是額外的資訊，在請求個人化內容時無法取得。

此外，傳送顯示事件於 `sendEvent` 使用Adobe Analytics時，呼叫可將跳出率錯誤降至最低。

>[!IMPORTANT]
>
>使用手動呈現的主張時，顯示事件僅支援透過 `sendEvent` 呼叫。 在此情況下，您無法自動傳送顯示事件。

### 傳送自動呈現主張的顯示事件 {#auto-rendered-propositions}

若要傳送自動呈現主張的顯示事件，您必須在下列欄位中設定下列引數： `sendEvent` 呼叫：

* `renderDecisions: true`
* `personalization.sendDisplayNotifications: false` 用於頁面點選的頂端

若要傳送顯示事件，請呼叫 `sendEvent` 替換為 `personalization.includePendingDisplayNotifications: true`

### 傳送手動呈現主張的顯示事件 {#manually-rendered-propositions}

若要傳送手動呈現主張的顯示事件，您必須將其納入 `_experience.decisioning.propositions` XDM欄位，包括 `id`， `scope`、和 `scopeDetails` 中的欄位。

此外，設定 `include _experience.decisioning.propositionEventType.display` 欄位至 `1`.