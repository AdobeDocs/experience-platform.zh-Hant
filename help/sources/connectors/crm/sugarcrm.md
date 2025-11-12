---
title: SugarCRM Source概述
description: 瞭解如何使用API或使用者介面將SugarCRM連結至Adobe Experience Platform。
last-substantial-update: 2023-08-23T00:00:00Z
exl-id: 03fbc4e9-974d-494e-8463-756c96665fd5
source-git-commit: 06b2108715ce368ff4ecf5c6c7dd3a327d9f61b1
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 8%

---

# [!DNL SugarCRM]

Adobe Experience Platform 讓您可以從外部來源擷取資料，同時可以使用 Experience Platform 服務來建立、加標籤，同時強化傳入資料。 您可以從多種來源(例如Adobe應用程式、雲端儲存、資料庫和許多其他來源)內嵌資料。

Experience Platform支援從協力廠商CRM應用程式擷取資料。 CRM提供者的支援包括[!DNL SugarCRM]。

[[!DNL SugarCRM]](https://www.sugarcrm.com/)是客戶關係管理(CRM)系統。 [!DNL SugarCRM]的功能包括銷售人員自動化、行銷活動、客戶支援、共同作業、Mobile CRM、Social CRM和報表。

[!DNL SugarCRM]來源可讓您從下列API端點擷取帳戶、連絡人和事件資料：

* [帳戶](https://market.apidocs.sugarcrm.com/#b0aeb0cd-80ea-4688-8474-54e4873f32f3)
* [連絡人](https://market.apidocs.sugarcrm.com/#308c5025-9478-4de3-8a41-1fc3cff1d8d1)
* [活動](https://market.apidocs.sugarcrm.com/#516ec3b1-8e70-43d4-8bf2-38a2ae74c0a5)

[!DNL SugarCRM]使用持有人權杖作為驗證機制，以與[!DNL SugarCRM]帳戶和連絡人API以及[!DNL SugarCRM]事件API通訊。

## IP位址允許清單

將來源連線至Experience Platform之前，您必須先將區域特定的IP位址新增至允許清單。 如需詳細資訊，請參閱[允許清單IP位址以連線至Experience Platform](../../ip-address-allow-list.md)的指南以瞭解詳細資訊。

## 先決條件

在建立[!DNL SugarCRM]來源連線之前，您必須先確定您有下列專案：

* [!DNL SugarMarket]帳戶。 如果您尚未擁有有效的[!DNL SugarCRM]帳戶，則必須連絡您的[!DNL SugarMarket]帳戶管理員，以取得此帳戶。

* 與行銷或銷售程式相關聯之任何使用者帳戶分開的唯一API使用者名稱和帳戶。 此唯一的使用者名稱和帳戶組合必須具有API存取許可權。 如需設定帳戶程式的詳細資訊，請瀏覽[[!DNL SugarMarket RESTFUL API]](https://market.apidocs.sugarcrm.com/#intro)檔案。

## 將[!DNL SugarCRM Accounts & Contacts]連線至Experience Platform

* [使用API建立來源連線，將 [!DNL SugarCRM Accounts & Contacts] 資料帶入Experience Platform](../../tutorials/api/create/crm/sugarcrm-accounts-contacts.md)。
* [使用使用者介面建立來源連線，將 [!DNL SugarCRM Accounts & Contacts] 資料帶入Experience Platform](../../tutorials/ui/create/crm/sugarcrm-accounts-contacts.md)。
* [使用流程服務API為CRM來源建立資料流](../../tutorials/api/collect/crm.md)


## 將[!DNL SugarCRM Events]連線至Experience Platform

* [使用API建立來源連線，將 [!DNL SugarCRM Events] 資料帶入Experience Platform](../../tutorials/ui/create/crm/sugarcrm-events.md)。
* [使用使用者介面建立來源連線，將 [!DNL SugarCRM Events] 資料帶入Experience Platform](../../tutorials/ui/create/crm/sugarcrm-events.md)。
* [在UI中為CRM來源連線建立資料流](../../tutorials/ui/dataflow/crm.md)
