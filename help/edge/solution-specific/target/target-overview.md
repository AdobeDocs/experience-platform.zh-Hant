---
title: 'Adobe Target和Adobe Experience Platform Web SDK。 '
seo-title: Adobe Experience Platform Web SDK與使用Adobe Target
description: 瞭解如何使用Adobe Target使用Experience Platform Web SDK來呈現個人化內容
seo-description: 瞭解如何使用Adobe Target使用Experience Platform Web SDK來呈現個人化內容
translation-type: tm+mt
source-git-commit: db4bfec04a1116ce2b6a0be7ca0e8cb2f9639ad6

---


# Target概觀

Adobe Experience Platform Web SDK透過個人化功能與Adobe Target整 [合](../../fundamentals/rendering-personalization-content.md) ，讓您輕鬆提供個人化內容和決策。

## 啟用Adobe Target

若要啟用Target，您必須執行下列動作：

- 使用適當的用戶 [端程式碼](../../fundamentals/edge-configuration.md) ，在邊緣設定中啟用Target。
- 將選項 `renderDecisions` 新增至事件。

您也可以選擇：

- 新增 `scopes` 至事件以擷取特定活動（對於以表單為基礎的撰寫器所建立的活動非常有用）。
- 新增預 [先隱藏的程式碼片段](../../fundamentals/managing-flicker.md) ，只隱藏頁面的某些部分。

## 使用VEC

在SDK中，您可正常使用VEC，但有一個例外，您將需要安裝 [目標VEC協助延伸模組](https://docs.adobe.com/content/help/en/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html) ，並啟用。

## 使用表單式撰寫器

表單撰寫器也可用來傳回內容。 範圍會以位置(mBox)顯示在Target UI。 此外，如果您決定使用範圍，您也需要確定您的開發人員正在尋找回應。

## XDM中的觀眾

在Target XDM中，資料會以自訂參數顯示在Audience Builder中。 XDM使用點標籤（例如，XDM）序列化。 `web.webPageDetails.name`)

## 術語

__決策__ -在Target中，這些決策會關聯至從活動中選取的體驗。

__範圍__ -決定範圍。 在Target中，這是mBox。 全域mBox是范 `__view__` 圍。

__方案__ -決策的方案是Target中的選件類型。

__XDM__ - XDM會序列化為點符號，然後以mBox參數的形式放入Target。