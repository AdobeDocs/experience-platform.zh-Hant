---
title: 組態設定概觀
description: 瞭解設定網頁SDK標籤擴充功能時可用的選項。
source-git-commit: 5f0203cfff3cb5c8b892142ff9b1c121925c3c46
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 0%

---

# 組態設定概觀

Adobe Experience Platform Web SDK標籤擴充功能提供數個可自訂的選項。 這些組態設定等同於使用JavaScript資料庫中的[`configure`](/help/collection/js/commands/configure/overview.md)命令。

1. 使用您的Adobe ID憑證登入[experience.adobe.com](https://experience.adobe.com)。
1. 導覽至&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**。
1. 選取所需的標籤屬性。
1. 導覽至&#x200B;**[!UICONTROL Extensions]**，然後選取&#x200B;**[!UICONTROL Configure]**&#x200B;卡片上的[!UICONTROL Adobe Experience Platform Web SDK]。

## 自訂建置元件

如果貴組織優先考慮最佳化組建大小，您可以停用您不用來減少擴充功能組建大小的特定功能。 如需詳細資訊，請參閱[自訂組建元件](custom-build-components.md)。

## SDK執行個體

大部分實施通常需要單一SDK執行個體。 不過，如果您的組織需要多個Web SDK追蹤例項，您可以使用&#x200B;**[!UICONTROL Add instance]**&#x200B;按鈕。 設定每個Web SDK標籤例項時，以下是可用的總體區段：

* [**[!UICONTROL SDK instance]**](general.md)：執行個體的一般設定。 此區段中的所有欄位都是必要欄位。
* [**[!UICONTROL Datastreams]**](datastreams.md)：您希望每個標籤環境的資料移至何處。
* [**[!UICONTROL Consent]**](consent.md)：擴充功能的預設同意設定。
* [**[!UICONTROL Identity]**](identity.md)： Cookie和訪客移轉設定。
* [**[!UICONTROL Personalization]**](personalization.md)：自訂個別層級的訪客體驗。
* [**[!UICONTROL Data collection]**](data-collection.md)：包含或省略自動收集的專案。
* [**[!UICONTROL Streaming media]**](streaming-media.md)：串流媒體集合的專屬設定。
* [**[!UICONTROL Datastream configuration overrides]**](configuration-overrides.md)：當符合某些條件時，修改組態設定。
* [**[!UICONTROL Advanced settings]**](advanced-settings.md)：指定Edge Network的基本路徑。
