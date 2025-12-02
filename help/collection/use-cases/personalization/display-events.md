---
title: 在網頁SDK中管理顯示事件
description: 說明什麼是顯示事件，以及如何在網頁SDK中使用這些事件。
exl-id: 7150ad6e-7693-4f4d-917e-8d08a39a0b41
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# 在網頁SDK中管理顯示事件

顯示事件是網頁SDK在頁面上顯示特定個人化內容時，用來通知您的個人化或分析服務。 傳送顯示事件可改善個人化量度的準確性，並提供使用者在您頁面上所看到內容的準確概覽。

>[!NOTE]
>
>呼叫`applyPropositions`函式時，顯示事件不會自動傳送。

## 自動傳送顯示事件

傳送顯示事件會自動提供更精確的分析量度，因為事件會在個人化載入後立即傳送。 此實作也有更簡化的實作方法。

若要在頁面上呈現個人化內容後自動傳送顯示事件，您必須設定下列引數：

* `renderDecisions: true`
* `personalization.sendDisplayEvent: true`或未指定

Web SDK會在任何個人化轉譯為`sendEvent`呼叫的結果後，立即傳送顯示事件。

## 在後續sendEvent呼叫中傳送顯示事件

相較於自動傳送顯示事件，當您將其納入後續`sendEvent`呼叫時，您還有機會在呼叫中包含更多有關頁面載入的資訊。 這可能是額外的資訊，在請求個人化內容時無法取得。

此外，在`sendEvent`呼叫中傳送顯示事件可在使用Adobe Analytics時將跳出率錯誤降至最低。

>[!IMPORTANT]
>
>使用手動轉譯的主張時，僅透過`sendEvent`呼叫支援顯示事件。 在此情況下，您無法自動傳送顯示事件。

### 傳送自動呈現主張的顯示事件

若要傳送自動轉譯主張的顯示事件，您必須在`sendEvent`呼叫中設定下列引數：

* `renderDecisions: true`
* 頁面點選頂端的`personalization.sendDisplayEvent: false`

若要傳送顯示事件，請使用`sendEvent`呼叫`personalization.includeRenderedPropositions: true`

### 傳送手動呈現主張的顯示事件

若要傳送手動呈現主張的顯示事件，您必須將其納入`_experience.decisioning.propositions` XDM欄位中，包括主張的`id`、`scope`和`scopeDetails`欄位。

此外，將`include _experience.decisioning.propositionEventType.display`欄位設為`1`。
