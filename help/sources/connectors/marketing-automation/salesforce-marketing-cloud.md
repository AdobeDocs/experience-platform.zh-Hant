---
keywords: Experience Platform；首頁；熱門主題；salesforce marketing cloud;SalesforceMarketing Cloud；行銷自動化
solution: Experience Platform
title: SalesforceMarketing Cloud源概述
description: 了解如何使用API或使用者介面將SalesforceMarketing Cloud連線至Adobe Experience Platform。
exl-id: 2177d68c-0cef-4031-a0e7-8bf22ee2e70b
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---

# （測試版） [!DNL Salesforce Marketing Cloud]

>[!NOTE]
>
>此 [!DNL Salesforce Marketing Cloud] 來源為測試版。 請參閱 [來源概觀](../../home.md#terms-and-conditions) 以取得使用測試版標籤來源的詳細資訊。

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源(如Adobe應用程式、雲儲存、資料庫等)內嵌資料。

[!DNL Experience Platform] 提供從協力廠商行銷自動化系統擷取資料的支援。 對行銷自動化提供者的支援包括 [!DNL Salesforce Marketing Cloud].

## 先決條件

連接之前 [!DNL Salesforce Marketing Cloud] 來源，您必須確保 **權限範圍** 布建至 [!DNL Salesforce Marketing Cloud] 用戶端ID和用戶端密碼組合：

* `campaign_read`
* `list_and_subscribers_read`

您可以呼叫 `v2/userinfo` 資源 [!DNL Salesforce Marketing Cloud] API。 請參閱 [[!DNL Salesforce Marketing Cloud] API整合權限範圍檔案](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/data-access-permissions.html) 以了解如何請求和比較範圍。

有關範圍的詳細資訊，包括其相關權限和行為的清單，請參見此 [[!DNL Salesforce Marketing Cloud] REST API檔案](https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rest-permissions-and-scopes.html).

## IP位址允許清單

使用來源連接器前，必須將IP位址清單新增至允許清單。 若未將您地區專屬的IP位址新增至允許清單，在使用來源時可能會導致錯誤或效能不佳。 請參閱 [IP位址允許清單](../../ip-address-allow-list.md) 頁面以取得詳細資訊。

## Connect [!DNL Salesforce Marketing Cloud] 使用API到平台

以下檔案提供如何連線的資訊 [!DNL Salesforce Marketing Cloud] 使用API的平台：

* [使用流量服務API建立SalesforceMarketing Cloud基礎連接](../../tutorials/api/create/marketing-automation/salesforce-marketing-cloud.md)
* [使用流量服務API探索資料表](../../tutorials/api/explore/tabular.md)
* [使用流服務API為行銷自動化來源建立資料流](../../tutorials/api/collect/marketing-automation.md)

## Connect [!DNL Salesforce Marketing Cloud] 使用UI設為Platform

以下檔案提供如何連線的資訊 [!DNL Salesforce Marketing Cloud] 若要使用使用者介面來建立平台：

* [在UI中建立SalesforceMarketing Cloud來源連線](../../tutorials/ui/create/marketing-automation/salesforce-marketing-cloud.md)
* [在UI中建立行銷自動化來源連線的資料流](../../tutorials/ui/dataflow/marketing-automation.md)
