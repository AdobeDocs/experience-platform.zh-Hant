---
title: Launch快速入門
seo-title: Launch讓您快速入門Adobe Experience Platform Web SDK
description: 使用Experience Platform Web SDK擴充功能收集資料的快速入門手冊
seo-description: 使用Experience Platform Web SDK擴充功能收集資料的快速入門手冊
translation-type: tm+mt
source-git-commit: d958e323df2535c168edd3a35b878fcc4bb73370
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 5%

---


# 歡迎

本指南會引導您以不同的方式在Launch中設定Adobe Experience Platform Web SDK。 若要使用此功能，您必須列入白名單。 如果您想要加入等候清單，請聯絡您的CSM。

- 啟用 [第一方網域(CNAME)](https://docs.adobe.com/content/help/zh-Hant/core-services/interface/ec-cookies/cookies-first-party.html) 。 如果您已有Analytics的CNAME，則應使用該CNAME。 在開發中進行測試沒有CNAME，但您在投入生產前需要CNAME。
- 取得Adobe Experience Platform的權益。 如果您尚未購買Platform,Adobe將提供您Experience Platform Data Services Foundation，讓您以有限方式與SDK搭配使用，不需額外付費。
- 使用最新版的訪客ID服務。

## 準備架構

Experience Platform Edge Network將資料視為XDM。 XDM是一種資料格式，可讓您定義結構描述。 此架構定義邊緣網路預期資料格式化的方式。 若要傳送資料，您必須定義您的結構。

1. [建立架構](../../xdm/tutorials/create-schema-ui.md)
2. 將AEP [!DNL Web SDK ExperienceEvent] Mixin新增至您建立的架構。
3. 從您建立的架構建立資料集。

以下視訊旨在支援您建立資料的架構、資料集和串流來源連 [!DNL Web SDK] 接器。

登入啟動並安裝擴充 `AEP Web SDK` 功能。 當您安裝SDK時，系統會提示您設定擴充功能。 輸入上述請求的配置ID。 擴充功能會自動填入您的組織ID。


如需不同設定選項的詳細資訊，請參 [閱設定SDK](../fundamentals/configuring-the-sdk.md)。

## 建立設定ID

您可以使用Launch中的邊配置工 [具來建立配](../fundamentals/edge-configuration.md) 置ID。 這可讓您讓邊緣網路傳送資料至各種解決方案。 如需如何尋找每個選項的詳細資訊，請參閱「 [Edge Configuration Tool](../fundamentals/edge-configuration.md) 」（邊緣設定工具）頁面。

>[!NOTE]
>
>您的組織必須列入此功能的白名單。 請連絡您的CSM以取得最終白名單。

## 根據您的架構建立資料元素

在Launch中，將副檔名變更為AEP Web SDK並將類型設為，以建立參照架構的資料元素 `XDM Object`。 這會載入您的架構，並允許您將資料元素映射至架構的不同部分。

![啟動中的日期元素](../../assets/edge_data_element.png)

## 傳送事件

安裝擴充功能後，從AEP Web SDK擴充功能 `sendEvent` 新增動作至規則，開始傳送事件。 將您剛建立的資料元素新增至事件，做為XDM資料。 Adobe建議您每次載入頁面時至少傳送一個事件。

如需追蹤事件的詳細資訊，請參閱追 [蹤事件](../fundamentals/tracking-events.md)。

## 後續步驟

在資料流動後，您可以執行下列動作。

- [建立您的架構](https://docs.adobe.com/content/help/zh-Hant/experience-platform/xdm/schema/composition.html)
- [瞭解除錯](../fundamentals/debugging.md)
- 瞭解如何個 [人化體驗](../fundamentals/rendering-personalization-content.md)
- 瞭解如何將資料傳送至多個解決方案
   - [Adobe Analytics](../solution-specific/analytics/analytics-overview.md)
   - [Adobe Audience Manager](../solution-specific/audience-manager/audience-manager-overview.md)
   - [Adobe Target](../solution-specific/target/target-overview.md)
