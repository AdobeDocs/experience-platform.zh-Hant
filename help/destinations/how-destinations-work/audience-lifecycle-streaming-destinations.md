---
title: Experience Platform和串流目的地的對象生命週期
description: 瞭解串流目的地平台如何反映Experience Platform的對象名稱和對應。
source-git-commit: 6b4dfa714e078fb5b97900811aade081ffef0d78
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 2%

---


# 串流目的地的對象生命週期

本頁面說明Experience Platform中對象名稱更新和對應如何與串流目的地平台同步。 當您在Experience Platform中修改對象名稱或移除對象對應時，行為會因目標平台的功能而異。

瞭解這些差異對於管理對象生命週期作業並確保您的目的地平台反映您在Experience Platform中的對象目前狀態非常重要。

## 對象名稱傳播行為 {#audience-name-propagation}

當您對串流目的地啟用對象時，對象名稱會在初始啟用期間傳送至目的地。 不過，對象名稱更新行為會因目的地而異：

* **[支援對象名稱更新的目的地](#name-update-supported)**：如果您在Experience Platform中變更對象名稱，更新的名稱會自動傳播到這些目的地。
* **[不支援對象名稱更新的目的地](#name-update-not-supported)**：如果您在Experience Platform中變更對象名稱，目的地將會繼續使用初始啟動的原始名稱。

### 支援對象名稱更新的目的地 {#name-update-supported}

當您在Experience Platform中修改對象名稱時，下列串流目的地支援自動對象名稱更新：

* [Acxiom對象連線](../catalog/advertising/acxiom-audience-connection.md)
* [Adobe Campaign Managed Cloud](../catalog/email-marketing/adobe-campaign-managed-services.md)
* [Advertising Cloud DSP](../catalog/advertising/adobe-advertising-cloud-connection.md)
* [龐博拉](../catalog/advertising/bombora.md)
* [條件](../catalog/advertising/criteo.md)
* [Demandbase](../catalog/advertising/demandbase.md)
* [Demandbase人員](../catalog/advertising/demandbase-people.md)
* [Experience Cloud 客群](../catalog/adobe/experience-cloud-audiences.md)
* [Facebook自訂對象](../catalog/social/facebook.md)
* [Gainsight PX](../catalog/analytics/gainsight-px.md)
* [LINE](../catalog/mobile-engagement/line.md)
* [（公司） LinkedIn相符受眾](../catalog/social/linkedin-b2b.md)
* [LinkedIn相符對象](../catalog/social/linkedin.md)
* [（舊版） (V2) Marketo Engage](../catalog/adobe/marketo-engage.md)
* [PubMatic Connect](../catalog/advertising/pubmatic.md)
* [傳送格線](../catalog/email-marketing/sendgrid.md)
* [Snap Inc](../catalog/advertising/snap-inc.md)
* [TikTok](../catalog/social/tiktok.md)
* [Twitter自訂對象](../catalog/social/twitter.md)
* [Yahoo DataX](../catalog/advertising/datax.md)

### 不支援對象名稱更新的目的地 {#name-update-not-supported}

對於前述未列出的目的地，對象名稱在初始啟用後會維持靜態。 如果您需要更新這些目的地的對象名稱，您必須：

1. 在Experience Platform中以所需的名稱建立新對象
2. 對目的地啟用新對象

>[!TIP]
>
>為避免混淆，請在首次啟用時使用描述性對象名稱，尤其是在啟用至不支援對象名稱更新的目的地時。

## 支援對象移除的目的地 {#support-removal}

當您從串流目的地移除（取消對應）對象時，Experience Platform會嘗試從目的地平台移除對應的對象。 不過，並非所有目的地都支援此功能。

當您從目的地取消對應對象時，下列串流目的地支援自動對象移除：

* [(API) Oracle Eloqua](../catalog/email-marketing/oracle-eloqua-api.md)
* [（公司） LinkedIn相符受眾](../catalog/social/linkedin-b2b.md)
* [（舊版） (V2) Marketo Engage](../catalog/adobe/marketo-engage.md)
* [Adobe Advertising Cloud DSP](../catalog/advertising/adobe-advertising-cloud-connection.md)
* [Bombra帳戶對象](../catalog/advertising/bombora.md)
* [條件](../catalog/advertising/criteo.md)
* [Experience Cloud 客群](../catalog/adobe/experience-cloud-audiences.md)
* [Facebook](../catalog/social/facebook.md)
* [Gainsight PX](../catalog/analytics/gainsight-px.md)
* [HubSpot](../catalog/crm/hubspot.md)
* [LINE](../catalog/mobile-engagement/line.md)
* [LinkedIn相符對象](../catalog/social/linkedin.md)
* [LiveRamp — 分佈](../catalog/advertising/liveramp-distribution.md)
* [Mailchimp興趣類別](../catalog/email-marketing/mailchimp-interest-categories.md)
* [PubMatic Connect](../catalog/advertising/pubmatic.md)
* [Salesforce Marketing Cloud帳戶參與度](../catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md)
* [傳送格線](../catalog/email-marketing/sendgrid.md)
* [Snap Inc](../catalog/advertising/snap-inc.md)
* [TikTok](../catalog/social/tiktok.md)
* [Twitter自訂對象](../catalog/social/twitter.md)
* [Yahoo DataX](../catalog/advertising/datax.md)

### 不支援對象移除的目的地

對於前述未列出的目的地，當您從目的地取消對應對象時，Experience Platform只會移除對應。 目的地平台中的對象會維持作用中，直到您在合作夥伴平台中手動將其刪除為止。
