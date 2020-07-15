---
title: Launch快速入門
seo-title: Launch讓您快速入門Adobe Experience Platform Web SDK
description: 使用Experience Platform Web SDK擴充功能收集資料的快速入門手冊
seo-description: 使用Experience Platform Web SDK擴充功能收集資料的快速入門手冊
translation-type: tm+mt
source-git-commit: 9d58693646f472e84f04a64c4ad66f61dc5d3eba
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 4%

---


# 歡迎

本指南將引導您逐步瞭解如何在Adobe Launch中設定Adobe Experience Platform Web SDK。 您必須擁有權限並位於允許清單上才能使用此功能。 如果您想要加入等候清單，請聯絡您的CSM。 此外，若要使用此功能，您必須：

- 啟用 [第一方網域(CNAME)](https://docs.adobe.com/content/help/zh-Hant/core-services/interface/ec-cookies/cookies-first-party.html) 。 如果您已擁有Adobe Analytics的CNAME，則應使用該CNAME。 在開發中進行測試時不需要CNAME，但您在開始生產之前需要CNAME
- 正在使用最新版的訪客ID服務

## 建立設定ID

您可以使用Adobe Launch中的 [Edge設定工具](../fundamentals/edge-configuration.md) ，來建立設定ID。 這可讓您讓邊緣網路傳送資料至各種解決方案。 如需如何 [尋找每個選項的詳細資訊](../fundamentals/edge-configuration.md) ，請參閱Edge Configuration Tool頁面。

>[!NOTE]
>
>您的組織必須位於功能的允許清單中。 請連絡您的CSM以新增至允許清單。

## 準備架構

Experience Platform Edge Network將資料視為XDM。 XDM是一種資料格式，可讓您定義結構描述。 此架構定義邊緣網路預期資料格式化的方式。 若要傳送資料，您需要定義您的架構。 請確定您已完成下列工作：

1. [建立架構](../../xdm/tutorials/create-schema-ui.md)
2. 將AEP Web SDK ExperienceEvent Mixin新增至您建立的架構。
3. 從您建立的架構建立資料集。

以下視訊旨在支援您建立Web SDK資料的架構、資料集和串流來源連接器。

>[!VIDEO](https://video.tv.adobe.com/v/35395?quality=12&learn=on)

## 在Adobe Launch中安裝SDK

登入Adobe Launch並安裝擴充 `AEP Web SDK` 功能。 在安裝SDK時，將會提示您設定擴充功能。 輸入您在上面請求的配置ID。 擴充功能會自動填入您的組織ID。

如需不同設定選項的詳細資訊，請參 [閱設定SDK](../fundamentals/configuring-the-sdk.md)。

## 根據方案建立資料元素

在Adobe Launch中，將副檔名變更為AEP Web SDK並將類型設為XDM物件，以建立參照架構的資料元素。 這會載入您的架構，並允許您將資料元素映射至架構的不同部分。

![啟動中的日期元素](../../assets/edge_data_element.png)

## 傳送事件

在安裝擴充功能後，從AEP Web SDK擴充功能新增「sendEvent」動作至規則，開始傳送事件。 請務必將您剛建立的資料元素新增至事件，做為XDM資料。 建議您每次載入頁面時至少傳送一個事件。

如需追蹤事件的詳細資訊，請參閱追 [蹤事件](../fundamentals/tracking-events.md)。

## 後續步驟

一旦您有資料流動，您可以執行下列動作：

- [建立您的架構](https://docs.adobe.com/content/help/zh-Hant/experience-platform/xdm/schema/composition.html)
- [瞭解除錯](../fundamentals/debugging.md)
- 瞭解如何個 [人化體驗](../fundamentals/rendering-personalization-content.md)
- 瞭解如何將資料傳送至多個解決方案
   - [Adobe Analytics](../solution-specific/analytics/analytics-overview.md)
   - [Adobe Audience Manager](../solution-specific/audience-manager/audience-manager-overview.md)
   - [Adobe Target](../solution-specific/target/target-overview.md)
