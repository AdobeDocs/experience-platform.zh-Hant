---
title: 常見Analytics擴充功能概觀
description: 瞭解Adobe Experience Platform中的常見Analytics標籤擴充功能。
exl-id: 9eeb4589-df90-4356-b927-b2c29c32370b
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 68%

---

# 常見Analytics外掛程式擴充功能概觀

>[!NOTE]
>
>Adobe Experience Platform Launch已經過品牌重塑，現在是Adobe Experience Platform中的一套資料收集技術。 因此，所有產品檔案中出現了幾項術語變更。 請參閱下列[檔案](../../../term-updates.md)，以取得術語變更的彙總參考資料。

此參考資料會說明設定常見 Analytics 外掛程式擴充功能的相關資訊，以及使用此擴充功能擴大 [!DNL Adobe Analytics] 擴充功能時可用的選項。

## 設定常見 Analytics 外掛程式擴充功能

本節提供設定常見 Analytics 外掛程式擴充功能時可用的選項，以供參考。

>[!IMPORTANT]
>
>常見 Analytics 外掛程式擴充功能可擴大 [!DNL Adobe Analytics] 擴充功能。您必須在您的屬性上安裝 [!DNL Adobe Analytics] 擴充功能，才能順利運作。此外，您必須在 [!DNL Adobe Analytics] 擴充功能中將追蹤器設為全域皆可使用。

不必額外設定擴充功能層級。

## 在 [!DNL Adobe Analytics] 擴充功能新增外掛程式

若要使用此擴充功能所提供的外掛程式，您必須先初始化要在其本身的規則中使用的外掛程式。

1. 建立新規則。
1. 新增核心 - 資料庫載入 (頁面頂端) 事件。
1. 使用以下任一初始化方法。

## 常見 Analytics 外掛程式擴充功能動作類型

本節說明常見 Analytics 外掛程式擴充功能中可使用的動作類型。

常見 Analytics 外掛程式擴充功能提供下列動作：

* [初始化](#initialize)
* [初始化外掛程式](#initialize-plugin)

### 初始化

>[!IMPORTANT]
>
>雖然此動作比較容易實作，但 Adobe 諮詢服務不建議您使用此動作，因為這會增加外掛程式的權重。

此動作中，您可以選取要實作的每個外掛程式，並儲存變更。選取您要在實作期間使用的數量。

### 初始化外掛程式

這些動作會初始化您要個別使用的特定外掛程式。若要初始化您要在屬性中使用的所有外掛程式，只需將對應動作新增至規則並儲存規則即可。雖然以這種方式設定擴充功能需花費更多心力，但能提高程式碼運作效率。因此，Adobe 建議採取此方法。

## 常見Analytics外掛程式擴充功能資料元素

常見Analytics外掛程式擴充功能中提供下列資料元素，這些功能會運用標籤功能在Analytics中設定其對應的外掛程式：

* `getGeoCoordinates`
* `getNewRepeat`
* `getPageName`
* `getResponsiveLayout`
* `getTimeParting`
* `getTimeSinceLastVisit`
* `getVisitDuration`
* `getVisitNum`

>[!NOTE]
>
>如需上述外掛程式的詳細資訊，請參閱[Analytics檔案](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/impl-plugins.html?lang=zh-Hant)。
