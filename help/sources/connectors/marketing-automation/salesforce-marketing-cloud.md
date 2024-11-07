---
solution: Experience Platform
title: SalesforceMarketing CloudSource概觀
description: 瞭解如何使用API或使用者介面將SalesforceMarketing Cloud連結至Adobe Experience Platform。
exl-id: 2177d68c-0cef-4031-a0e7-8bf22ee2e70b
last-substantial-update: 2023-05-25T00:00:00Z
source-git-commit: a32d0d7ed7d18454099d2b55b3f6809cfbcd9b62
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 0%

---

# [!DNL Salesforce Marketing Cloud]

>[!IMPORTANT]
>
>[!DNL Salesforce Marketing Cloud]來源將於2025年5月底淘汰。

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源(例如Adobe應用程式、雲端儲存、資料庫和許多其他來源)內嵌資料。

Experience Platform提供從協力廠商行銷自動化系統擷取資料的支援。 對行銷自動化提供者的支援包括[!DNL Salesforce Marketing Cloud]。

## 先決條件

在將[!DNL Salesforce Marketing Cloud]來源連線到Platform之前，您必須確定已將下列&#x200B;**許可權範圍**&#x200B;布建到您的[!DNL Salesforce Marketing Cloud]使用者端ID和使用者端密碼組合：

* `campaign_read`
* `list_and_subscribers_read`

您可以呼叫[!DNL Salesforce Marketing Cloud] API的`v2/userinfo`資源來要求範圍。 如需如何要求與比較範圍的指引，請參閱[[!DNL Salesforce Marketing Cloud] API整合許可權範圍檔案](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/data-access-permissions.html>)。

如需有關範圍的詳細資訊，包括其相關許可權和行為清單，請參閱此[[!DNL Salesforce Marketing Cloud] REST API檔案](<https://developer.salesforce.com/docs/marketing/marketing-cloud/guide/rest-permissions-and-scopes.html>)。

>[!IMPORTANT]
>
>[!DNL Salesforce Marketing Cloud]來源整合目前不支援自訂物件擷取。

## IP位址允許清單

使用來源聯結器之前，必須將IP位址清單新增至允許清單。 未能將您區域特定的IP位址新增到允許清單可能會導致使用來源時的錯誤或效能不佳。 如需詳細資訊，請參閱[IP位址允許清單](../../ip-address-allow-list.md)頁面。

## 使用API連線[!DNL Salesforce Marketing Cloud]至平台

以下檔案提供如何使用API將[!DNL Salesforce Marketing Cloud]連線到Platform的資訊：

* [使用流量服務API建立SalesforceMarketing Cloud基本連線](../../tutorials/api/create/marketing-automation/salesforce-marketing-cloud.md)
* [使用流量服務API探索資料表](../../tutorials/api/explore/tabular.md)
* [使用流量服務API為行銷自動化來源建立資料流](../../tutorials/api/collect/marketing-automation.md)

## 使用UI連線[!DNL Salesforce Marketing Cloud]至平台

以下檔案提供如何使用使用者介面將[!DNL Salesforce Marketing Cloud]連線到Platform的資訊：

* [在UI中建立SalesforceMarketing Cloud來源連線](../../tutorials/ui/create/marketing-automation/salesforce-marketing-cloud.md)
* [在UI中建立行銷自動化來源連線的資料流](../../tutorials/ui/dataflow/marketing-automation.md)
