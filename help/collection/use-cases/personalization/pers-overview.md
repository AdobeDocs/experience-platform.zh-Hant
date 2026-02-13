---
title: Personalization使用案例概觀
description: 瞭解如何使用Adobe Experience Platform Web SDK實施個人化使用案例，包括呈現內容和追蹤顯示的模式。
keywords: 個人化；sendEvent；renderDecisions；applyPropositions；decisionScopes；顯示事件；閃爍；
exl-id: 6beccbfd-fddb-4e19-8a56-caba276e1643
source-git-commit: caaf5cad7276d6429fbbf35585fd4845de6ff60c
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 0%

---

# Personalization使用案例概觀

Adobe Experience Platform Web SDK可為Web屬性啟用各種個人化使用案例。 它支援靈活的架構（使用者端、伺服器端和混合式），因此您可以請求決策，並以符合網站需求的方式呈現內容。

## 呈現個人化內容

網頁SDK可以擷取個人化決定（也稱為&#x200B;_建議_），並協助您在頁面上轉譯這些決定。 轉譯為非同步，因此請避免假設套用內容時的指定時間。

選擇符合您收到的主張專案的模式：

1. **自動轉譯DOM動作主張**：當主張包含`dom-action`個具有選取器和Web SDK可自動套用的動作型別的專案時使用。 請參閱[自動轉譯DOM動作主張](render-auto-pers-content.md)。
1. **使用applyPropositions呈現不含選取器的HTML選件**：當您收到HTML內容時使用，但您必須透過中繼資料提供套用的位置及方式（選取器+動作型別）。 請參閱[呈現不含選取器的HTML選件](render-html-offers.md)。
1. **手動轉譯主張**：當您需要完全控制轉譯邏輯時使用（例如，從JSON撰寫UI或套用自訂商業規則）。 請參閱[手動轉譯主張](render-manual-propositions.md)。

>[!TIP]
>
>這些模式可以合併。 例如，您可以啟用自動DOM動作呈現，同時手動呈現特定決定範圍中的內容。

## 常見隨附主題

大部分的個人化實作都涉及以下常見主題：

* **防止忽隱忽現** （選擇性）：在個人化期間隱藏及顯示容器。 請參閱[管理忽隱忽現情形](manage-flicker.md)。
* **追蹤顯示內容**：記錄呈現內容的顯示事件。 請參閱[管理顯示事件](display-events.md)。
* **頁面頂端擷取/頁面底部量度**：提早要求決定，然後稍後包含測量。 請參閱[設定頁面事件的頂端和底端](top-bottom-page-events.md)。

## 網頁SDK範例

除了此資料夾中的檔案頁面外，Adobe還會維護您可參考的範例應用程式存放庫。 如需其他個人化案例，請參閱GitHub上的[網頁SDK範例](https://github.com/adobe/alloy-samples/)，包括：

* 使用者端個人化
* 伺服器端個人化
* 混合個人化
* 單頁應用程式中的Personalization
